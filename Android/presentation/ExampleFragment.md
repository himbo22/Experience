```kotlin
@AndroidEntryPoint
class RegisterOrSignInFragment :
    BaseFragment<FragmentRegisterOrSignUpBinding, RegisterOrSignUpViewModel>() {
    override val bindingInflater: (LayoutInflater, ViewGroup?, Boolean) -> FragmentRegisterOrSignUpBinding
        get() = FragmentRegisterOrSignUpBinding::inflate
    override val viewModel: RegisterOrSignUpViewModel by viewModels()

    override fun bindEvent() {
        addItemClick(
            binding.btnBack,
            binding.btnSignIn,
            binding.btnRegister,
            listener = this
        )
    }

    override fun onSingleViewClick(view: View) {
        when (view) {
            binding.btnBack -> {
                findNavController().navigateUp()
            }

            binding.btnSignIn -> {
                val action =
                    RegisterOrSignInFragmentDirections.actionRegisterOrSignInFragmentToSignInFragment()
                findNavController().navigate(action)
            }

            binding.btnRegister -> {}
        }
    }

}
```