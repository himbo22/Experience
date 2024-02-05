#BaseActivity

##Example:

```kotlin
abstract class BaseActivity<VB : ViewBinding, VM : ViewModel> : AppCompatActivity(), SingleViewClickListener {
    private var startClickTime: Long = 0
    private var isKeyboardShown = false
    protected lateinit var binding: VB
    abstract val bindingInflater: ((LayoutInflater) -> VB)
    abstract val viewModel: VM
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        initSplashScreen()
        binding = bindingInflater(layoutInflater)
        setContentView(binding.root)
        setUpNavigation()
        initData()
        bindComponent()
        bindEvent()
        bindData()
        observeData()
        }
    }

    protected open fun initSplashScreen(){}

    protected open fun initData(){}

    protected open fun bindData(){}

    protected open fun bindComponent(){}

    protected open fun bindEvent(){}

    protected open fun observeData(){}

    protected open fun setUpNavigation(){}


    override fun dispatchTouchEvent(ev: MotionEvent): Boolean {
        when (ev.action) {
            MotionEvent.ACTION_DOWN -> startClickTime = System.currentTimeMillis()
            MotionEvent.ACTION_UP -> {
                if (System.currentTimeMillis() - startClickTime < ViewConfiguration.getTapTimeout()) {
                    val view = currentFocus as? EditText ?: return super.dispatchTouchEvent(ev)
                    val outRect = Rect()
                    view.getGlobalVisibleRect(outRect)
                    if (!outRect.contains(ev.x.toInt(), ev.y.toInt())) {
                        KeyboardUtils.hideKeyboard(view)
                        view.clearFocus()
                    }
                }
            }
        }
        return super.dispatchTouchEvent(ev)
    }

    fun addViewClickEvents(vararg views: View) {
        registerSingleViewClick(*views) {
            onSingleViewClick(it)
        }
    }

```

## Explain

In Base, we use ```protected open fun``` instead of ```abstract fun``` for decrease override functions from Base.

```kotlin
protected open fun initSplashScreen(){}
```
This function necessary for initialize Splash Screen, it must run before setContentView() run.

```kotlin
protected open fun initData(){}
```

```kotlin
protected open fun bindComponent(){}
```

```kotlin
protected open fun bindEvent(){}
```

```kotlin
protected open fun observeData(){}
```

```kotlin
protected open fun setUpNavigation(){}
```

```kotlin
protected open fun bindData(){}
```