First, we have to define some classes for next purpose.

```kotlin
class NetworkingError(
    val networkingErrorAction: NetworkingErrorAction
) : Exception()
```


```kotlin
sealed class NetworkingErrorAction {
    data class ShowDialog(
        val title: String = "",
        val description: String = "",
    ) : NetworkingErrorAction()

    data object LogOutWhenRefreshTokenExpired : NetworkingErrorAction()
    data object None : NetworkingErrorAction()
}
```


```kotlin
object NetworkingStatusCode {
    const val ACCESS_TOKEN_EXPIRED = 4001
    const val REFRESH_TOKEN_EXPIRED = 5000
    const val LOGIN_FAILED = 4005
}
```

```kotlin
object NetworkingErrorMapper {
    fun map(exception: Exception): NetworkingError {
        return when (exception) {
            is HttpException -> {
                if (exception.code() == NetworkingStatusCode.REFRESH_TOKEN_EXPIRED) {
                    NetworkingError(NetworkingErrorAction.LogOutWhenRefreshTokenExpired)
                } else {
                    convertToErrorResponse(
                        exception.response()?.errorBody()?.string()
                    )?.let { baseResponse ->
                        when (baseResponse.statusCode) {
                            NetworkingStatusCode.LOGIN_FAILED -> showErrorDialog(description = baseResponse.data.message)
                            else -> showErrorDialog()
                        }
                    } ?: run {
                        showErrorDialog()
                    }
                }
            }

            else -> {
                showErrorDialog(description = exception.message)
            }
        }
    }

    fun showErrorDialog(title: String? = "", description: String? = ""): NetworkingError =
        NetworkingError(NetworkingErrorAction.ShowDialog(title ?: "", description ?: ""))

    fun convertToErrorResponse(json: String?): BaseResponse<BaseError>? =
        Gson().fromJson<BaseResponse<BaseError>>(
            json, object : TypeToken<BaseResponse<BaseError>>() {}.type
        )
}
```