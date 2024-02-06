# dependencies.gradle

```
ext {
    room_version = "2.6.1"
    lifecycle_version = "2.7.0"
    nav_version = "2.7.6"
    coroutines_version = "1.7.3"
    retrofit_version = "2.9.0"
    fragment_version = "1.6.2"
    gson_version = "2.9.0"
    glide_version = "4.16.0"
    hilt_version = "2.48.1"
    swipe_version = "1.1.0"
    datastore_version = "1.0.0"
    splashscreen_version = "1.0.1"
    core_ktx_version = "1.12.0"
    appcompat_version = "1.6.1"
    material_version = "1.11.0"
    constraintLayout_version = "2.1.4"
    junit_version = "4.13.2"
    ext_junit_version = "1.1.5"
    expresso_version = "3.5.1"
    hilt_compiler_version = "1.1.0"
    glide_compiler_version = "4.14.2"
    okhttp3_logging_interceptor = "4.10.0"
    scalable_size_version = "1.1.0"
}
```

How to create this ```file``` and link it into ```build.gradle```

Go to ```Project``` -> ```app``` and create new file name it : ```dependencies.gradle```

Now switch to ```build.gradle``` (Module :app) and use this line to link the file we just created : ```apply from: 'dependencies.gradle'```