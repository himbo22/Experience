```kotlin
private fun Exception.toResponseBody(): BaseResponse<BaseError>? {
    return if (this is HttpException) {
        try {
            val body = response()?.errorBody()
            val errorResponse = Gson().fromJson<BaseResponse<BaseError>>(
                body?.string(),
                object : TypeToken<BaseResponse<BaseError>>() {}.type
            )
            if (errorResponse.data?.message == null || errorResponse.statusCode == null) {
                null
            } else {
                errorResponse
            }
        } catch (e: Exception) {
            e.printStackTrace()
            null
        }
    } else null
}

fun <T> Exception.toResourceError() = toResponseBody()?.let {
    Resource.Error<T>(message = it.data?.message ?: "", statusCode = it.statusCode.orZero())
} ?: run {
    Resource.Error(message = message)
}
```