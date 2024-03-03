#build.gradle (Project)

```
plugins {
    id 'com.android.application' version '7.4.2' apply false
    id 'com.android.library' version '7.4.2' apply false
    id 'org.jetbrains.kotlin.android' version '1.9.10' apply false
    id("com.google.devtools.ksp") version "1.9.10-1.0.13" apply false
    id("com.google.dagger.hilt.android") version "2.48.1" apply false
    id 'androidx.navigation.safeargs' version '2.4.2' apply false
}

tasks.register('clean', Delete) {
    delete rootProject.buildDir
}

```