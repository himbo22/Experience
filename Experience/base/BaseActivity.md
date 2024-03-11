#BaseActivity

###Example:

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

#Apply it on Activity

```kotlin
@AndroidEntryPoint
class MainActivity : BaseActivity<ActivityMainBinding, MainViewModel>() {
    private var navController: NavController? = null
    private var graph: NavGraph? = null

    override val bindingInflater: (LayoutInflater) -> ActivityMainBinding
        get() = ActivityMainBinding::inflate
    override val viewModel: MainViewModel by viewModels()
    override fun initSplashScreen() {
        installSplashScreen().setKeepOnScreenCondition { viewModel.isShowingSplashScreen.value }
    }

    override fun observeData() {
        lifecycleScope.launch {
            repeatOnLifecycle(Lifecycle.State.STARTED) {
                viewModel.event.collect { mainEvent ->
                    when (mainEvent) {
                        MainEvent.NavigateToHomeScreen -> {
                            graph?.setStartDestination(R.id.homeFragment)
                            graph?.let { graph -> navController?.setGraph(graph, null) }
                        }

                        MainEvent.NavigateToWelcomeScreen -> {
                            graph?.setStartDestination(R.id.welcomeFragment)
                            graph?.let { graph -> navController?.setGraph(graph, null) }
                        }
                    }
                }
            }
        }
    }

    override fun setUpNavigation() {
        val navHostFragment =
            supportFragmentManager.findFragmentById(R.id.nav_host_fragment) as NavHostFragment
        navController = navHostFragment.findNavController()
        val inflater = navController?.navInflater
        graph = inflater?.inflate(R.navigation.nav_graph)
    }

    override fun onSupportNavigateUp(): Boolean {
        return navController?.navigateUp()!! || super.onSupportNavigateUp()
    }

    override fun onSingleViewClick(view: View) {}
}
```