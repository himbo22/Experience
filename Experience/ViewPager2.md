# ViewPager2 - A Jetpack Library

## To use ``ViewPager2``, add the following AndroidX dependency to your project's ``build.gradle`` file:

``Groovy``
```
dependencies {
    implementation "androidx.viewpager2:viewpager2:1.0.0"
}
```

``Kotlin``
```
dependencies {
    implementation("androidx.viewpager2:viewpager2:1.0.0")
}
```

## ViewPager Adapter with Fragments

>public ``abstract class FragmentStateAdapter`` extends ``RecyclerView.Adapter`` implements ``StatefulAdapter``

```kotlin
class ExampleAdapter(fragment: Fragment) : FragmentStateAdapter(fragment) {
    override fun getItemCount(): Int {
        return 3 // return the size of fragments implement in viewpager
    }

    override fun createFragment(position: Int): Fragment {
        return when (position) {
            0 -> FragmentOne()
            1 -> FragmentTwo()
            else -> FragmentThree()
        }
    }
}
```
**Note**
``FragmentStateAdapter`` has 3 constructors, they are ``Fragment``,``FragmentActivity`` and ``FragmentManager`` + ``Lifecycle``.
Depend on your project to change the constructor in ``FragmentStateAdapter`` to reasonable.

**Using**
```kotlin
myViewPager2.adapter = ExampleAdapter(this) // if you are in fragment
```


## Disable swiping in ViewPager2

```kotlin
myViewPager2.isUserInputEnabled = false
```