# App class

```kotlin
@HiltAndroidApp
class MyApplication : Application() {
    companion object {
        var instance: Application?=null
        var res: Resources?=null
    }
    override fun onCreate() {
        super.onCreate()
        instance = this
        res = resources
    }
}
```

# Declaration in the manifest

```xml
<application
        android:name=".MyApplication"
        ...>
</application>    
```

# Using

```kotlin
    val s : String = MyApplication.res?.getString(R.string.text)
```