First we need to define ```InterceptorInfo```.

```kotlin
data class InterceptorInfo(
    val headerInfo: HeaderInfo,
    val deviceId: String
)
```

```HeaderInfo```
```kotlin
data class HeaderInfo(
    val accessToken: String = "",
    val refreshToken: String = "",
    val sessionId: String = ""
)
```

Now we create an Interceptor class, then we implement the ```intercept``` function.

```kotlin
class AuthInterceptor(
    private val preferencesManager: PreferencesManager,
    private val updateSessionInfoUseCase: UpdateSessionInfoUseCase
) : Interceptor {

    override fun intercept(chain: Interceptor.Chain): Response {

    }
}
```

Inside ```intercept``` function :
```kotlin
    override fun intercept(chain: Interceptor.Chain): Response {
        val request: Request = chain.request()
        val interceptorInfo: InterceptorInfo = runBlocking {
            val accessToken: String = preferencesManager.accessTokenFlow.first()
            val refreshToken: String = preferencesManager.refreshTokenFlow.first()
            val sessionInfo: String = preferencesManager.sessionIdFlow.first()
            val deviceId: String = preferencesManager.deviceId.first()
            InterceptorInfo(
                HeaderInfo(accessToken, refreshToken, sessionInfo),
                deviceId
            )
        }
        val headerInfo: HeaderInfo = interceptorInfo.headerInfo
        val response: Response = chain.proceed(
            request.newBuilder().setHeader(headerInfo.accessToken, headerInfo.sessionId).build()
        )
        return if (response.code != HttpCode.SUCCESS && response.code < HttpCode.SERVER_ERROR) {
            val clonedResponse: Response = cloneResponse(response)
            val errorResponse: BaseResponse<BaseError>? =
                NetworkingErrorMapper.convertToErrorResponse(clonedResponse.body?.string())
            errorResponse?.let { error ->
                if (error.statusCode == NetworkingStatusCode.ACCESS_TOKEN_EXPIRED) {
                    val refreshTokenRequest: Request.Builder = request.newBuilder().apply {
                        setHeader(headerInfo.refreshToken, headerInfo.sessionId)
                        url("${BuildConfig.BASE_URL}user/refresh_token?deviceId=${interceptorInfo.deviceId}")
                        method("POST", "".toRequestBody("text/plain".toMediaTypeOrNull()))
                    }
                    val refreshResponse: Response = chain.proceed(refreshTokenRequest.build())
                    if (refreshResponse.code == NetworkingStatusCode.REFRESH_TOKEN_EXPIRED) {
                        refreshResponse
                    } else {
                        try {
                            val signInInfo: SignInInfo? =
                                Gson().fromJson<BaseResponse<SignInInfo>>(
                                    refreshResponse.body?.string(),
                                    object : TypeToken<BaseResponse<SignInInfo>>() {}.type
                                )?.data
                            signInInfo?.let {
                                val sessionInfo: SessionInfo = signInInfo.sessionInfo
                                runBlocking {
                                    updateSessionInfoUseCase(
                                        HeaderInfo(
                                            accessToken = sessionInfo.accessToken,
                                            refreshToken = sessionInfo.refreshToken,
                                            sessionId = sessionInfo.id
                                        )
                                    )
                                }
                                chain.proceed(
                                    request.newBuilder()
                                        .setHeader(sessionInfo.accessToken, sessionInfo.id)
                                        .build()
                                )
                            } ?: run {
                                refreshResponse
                            }
                        } catch (e: Exception) {
                            refreshResponse
                        }
                    }
                } else {
                    addBodyToResponse(clonedResponse)
                }
            } ?: run {
                addBodyToResponse(clonedResponse)
            }
        } else {
            response
        }
    }

```






