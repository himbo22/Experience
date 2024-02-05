#BaseFragment

```kotlin
abstract class BaseFragment<VB : ViewBinding, vm : ViewModel> : Fragment(),
    SingleViewClickListener {
    private var _binding: VB? = null
    abstract val bindingInflater: ((LayoutInflater, ViewGroup?, Boolean) -> VB)?
    abstract val viewModel: vm
    protected val binding get() = _binding!!

    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        _binding = bindingInflater?.invoke(inflater, container, false)
        return _binding?.root
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        initData()
        bindComponent()
        bindEvent()
        bindData()
        observeData()
    }

    override fun onDestroy() {
        super.onDestroy()
        _binding = null
    }

    protected open fun initData() {}
    protected open fun bindData() {}
    protected open fun bindComponent() {}
    protected open fun bindEvent() {}
    protected open fun observeData() {}

    fun addViewClickEvents(vararg views: View) {
        requireContext().registerSingleViewClick(*views) { view ->
            onSingleViewClick(view)
        }
    }
}
```

