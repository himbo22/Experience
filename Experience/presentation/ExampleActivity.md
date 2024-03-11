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