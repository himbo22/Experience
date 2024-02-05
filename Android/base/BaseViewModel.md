#BaseViewModel

```kotlin
open class BaseViewModel<T : BaseEvent> @Inject constructor() : ViewModel() {
    private val _event = Channel<T>()
    val event get() = _event.receiveAsFlow()

    protected fun sendEvent(event: T) {
        viewModelScope.launch {
            _event.send(event)
        }
    }
}
open class BaseEvent
```