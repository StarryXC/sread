> Thinking

```
org.jetbrains.kotlin # classpath ext.kotlin_version = '1.3.50'
	kotlin-gradle-plugin:$kotlin_version

kotlin-android kotlin-android-extensions kotlin-kapt
android
	kotlinOptions # jvmTarget = '1.8'

org.jetbrains.kotlin
	kotlin-stdlib
	kotlin-stdlib-jdk7 kotlin-stdlib-jdk8
androidx.core:core-ktx:1.2.0

implementation "org.jetbrains.kotlin:kotlin-stdlib-jre7:$kotlin_version"
implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
implementation "org.jetbrains.kotlin:kotlin-stdlib-jre7:$kotlin_version"
androidx.core:core-ktx:1.0.2
```

> Memory

```
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-android-extensions'
    id 'kotlin-kapt'
}

android {
    kotlinOptions {
        jvmTarget = '1.8'
    }
}
classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.6'
        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.4.1'
        classpath 'me.xx2bab.gradle:seal-manifest-precheck-plugin:1.1.0'
```

