#InputValidationResult

```kotlin
sealed class InputValidationResult {
    data object Success : InputValidationResult()
    data object InValidFormat : InputValidationResult()
    data object EmptyInput : InputValidationResult()
}
```