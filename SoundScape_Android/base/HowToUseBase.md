#How to use Base

Use,... 

```kotlin
abstract class BaseActivity<VB: ViewBinding, VM: ViewModel> : AppCompatActivity(){
    abstract val bindingInflater: ((LayoutInflater) -> VB)
    abstract val viewModel: VM
    ... code ...
}
```

MainActivity extend from BaseActivity

```kotlin
class MainActivity: BaseActivity<ActivityMainBinding, MainViewModel>(){
    override val bindingInflater: (LayoutInflater) -> ActivityMainBinding
        get() = ActivityMainBinding::inflate
    override val viewModel: MainViewModel by viewModels()
}
```

