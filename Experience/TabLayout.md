# TabLayout 

## Using

You can do this:
```xml
<com.google.android.material.tabs.TabLayout
            android:id="@+id/tab_layout"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

            <com.google.android.material.tabs.TabItem
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/news" />

            <com.google.android.material.tabs.TabItem
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/videos" />

            <com.google.android.material.tabs.TabItem
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/artists" />

            <com.google.android.material.tabs.TabItem
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/podcast" />

        </com.google.android.material.tabs.TabLayout>
```
Or this:

```xml
<com.google.android.material.tabs.TabLayout
            android:id="@+id/tab_layout"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">
```

```kotlin
TabLayoutMediator(tabLayout, viewPager) { tab, pos ->
            when (pos) {
                0 -> tab.setText(R.string.news)
                1 -> tab.setText(R.string.video)
                2 -> tab.setText(R.string.artist)
                else -> tab.setText(R.string.podcast)
            }
        }.attach()
```

You can replace ``setText`` by ``setIcon``.