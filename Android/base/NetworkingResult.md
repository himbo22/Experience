#NetworkingResult

```kotlin
sealed class NetworkingResult<T> {
    class Success<T>(val data: T) : NetworkingResult<T>()
    class Error<T>(val errorCode: Int? = null, val message: String? = null) : NetworkingResult<T>()
}
```