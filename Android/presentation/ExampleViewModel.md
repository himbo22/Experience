```kotlin
@HiltViewModel
class MainViewModel @Inject constructor(
    private val isSignedIn: CheckSignInStateUseCase,
    private val saveDeviceInfoUseCase: SaveDeviceInfoUseCase,
    tokenTimeOut: ExpiredTokenTimeOutUseCase
) : BaseViewModel<MainEvent>() {
    private val _isShowingSplashScreen = MutableStateFlow(true)
    val isShowingSplashScreen = _isShowingSplashScreen.asStateFlow()
    val isExpiredToken = tokenTimeOut.navigateBackToSignInScreen

    init {
        viewModelScope.launch(Dispatchers.IO) {
            saveDeviceInfoUseCase()
            if (isSignedIn()) {
                sendEvent(MainEvent.NavigateToHomeScreen)
            } else {
                sendEvent(MainEvent.NavigateToWelcomeScreen)
            }
            _isShowingSplashScreen.update { false }
        }
    }
}

sealed class MainEvent : BaseEvent() {
    data object NavigateToWelcomeScreen : MainEvent()
    data object NavigateToHomeScreen : MainEvent()
}

```