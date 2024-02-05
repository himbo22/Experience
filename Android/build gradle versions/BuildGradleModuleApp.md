#build.gradle (Module :app)

```plugins {
    id 'com.android.application'
    id 'org.jetbrains.kotlin.android'
    id 'kotlin-kapt'
    id("com.google.dagger.hilt.android")
    id("com.google.devtools.ksp")
    id 'androidx.navigation.safeargs'
    id 'kotlin-parcelize'
}

apply from: 'dependencies.gradle'

android {
    compileSdk 34


    lintOptions {
        warning 'NewerVersionAvailable'
    }


    defaultConfig {
        applicationId "com.app.soundscape"
        minSdk 24
        targetSdk 34
        versionCode 1
        versionName "1.0"


        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }


    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
    kotlinOptions {
        jvmTarget = '1.8'
    }
    buildFeatures {
        viewBinding true
    }

}

dependencies {
    
    implementation "androidx.core:core-ktx:${core_ktx_version}"
    implementation "androidx.appcompat:appcompat:${appcompat_version}"
    implementation "com.google.android.material:material:${material_version}"
    implementation "androidx.constraintlayout:constraintlayout:${constraintLayout_version}"
    testImplementation "junit:junit:${junit_version}"
    androidTestImplementation "androidx.test.ext:junit:${ext_junit_version}"
    androidTestImplementation "androidx.test.espresso:espresso-core:${expresso_version}"

    //Fragment
    implementation "androidx.fragment:fragment-ktx:${fragment_version}"

    //Room
    implementation "androidx.room:room-runtime:${room_version}"
    implementation "androidx.room:room-ktx:${room_version}"
    ksp "androidx.room:room-compiler:${room_version}"

    //Gson
    implementation "com.google.code.gson:gson:${gson_version}"

    //Retrofit
    implementation "com.squareup.retrofit2:retrofit:${retrofit_version}"
    implementation "com.squareup.retrofit2:converter-gson:${retrofit_version}"
    implementation("com.squareup.okhttp3:logging-interceptor:${okhttp3_logging_interceptor}")

    //Coroutines
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core:${coroutines_version}")
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:${coroutines_version}")

    //Coroutine Lifecycle Scopes
    implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:${lifecycle_version}"
    implementation "androidx.lifecycle:lifecycle-runtime-ktx:$lifecycle_version"
    implementation("androidx.lifecycle:lifecycle-livedata-ktx:$lifecycle_version")

    //Navigation components
    implementation "androidx.navigation:navigation-fragment-ktx:$nav_version"
    implementation "androidx.navigation:navigation-ui-ktx:$nav_version"

    //Glide
    implementation "com.github.bumptech.glide:glide:${glide_version}"
    ksp "com.github.bumptech.glide:compiler:${glide_compiler_version}"

    //Hilt
    implementation "com.google.dagger:hilt-android:${hilt_version}"
    kapt "com.google.dagger:hilt-compiler:${hilt_version}"
    kapt "androidx.hilt:hilt-compiler:${hilt_compiler_version}"

    //Swipe refresh layout
    implementation "androidx.swiperefreshlayout:swiperefreshlayout:${swipe_version}"

    //DataStore
    implementation "androidx.datastore:datastore-preferences:${datastore_version}"

    //Splash screen
    implementation("androidx.core:core-splashscreen:${splashscreen_version}")

    //Scalable size unit
    implementation "com.intuit.sdp:sdp-android:${scalable_size_version}"
    implementation "com.intuit.ssp:ssp-android:${scalable_size_version}"
}
kapt {
    correctErrorTypes = true
}
```