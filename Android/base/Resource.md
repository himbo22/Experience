#Resource

```kotlin
sealed class Resource<T> {
    class Success<T>(val data: T) : Resource<T>()
    class Error<T>(val data: T? = null, val message: String? = null) : Resource<T>()
}
```