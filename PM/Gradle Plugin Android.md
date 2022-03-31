> Thinking

```

```

> Memory

```
plugins {
    id 'com.android.application'
    id 'com.android.library'
}
android {
    compileSdk 28
    compileSdkVersion "29.0.2"
    defaultConfig {
        applicationId "env.app"
        minSdk 23
        targetSdk 28
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
}
android {
    useLibrary 'org.apache.http.legacy'
}
android {
    signingConfigs {
        signConfig {
            storeFile file("./bitong.keystore")
            storePassword "bitong2018"
            keyAlias "bitong"
            keyPassword "bitong2018"
        }
    }
    buildTypes {
        release {
            signingConfig signingConfigs.signConfig
            minifyEnabled false // 混淆
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
            buildConfigField "boolean", "LO", "true"
            shrinkResources true // 移除无用的resource文件
            zipAlignEnabled true // Zipalign 优化
            versionNameSuffix "-deb2ug"
        }
        debug {
            signingConfig signingConfigs.signConfig
        }
    }
    lintOptions {
        checkReleaseBuilds false
        abortOnError false // 忽略lint错误
        disable "InvalidPackage"
        // lintConfig file("lint.xml")
    }
    dexOptions {
        javaMaxHeapSize "4g"
    }
    packagingOptions {
        exclude 'META-INF/DEPENDENCIES'
        exclude 'META-INF/NOTICE'
        exclude 'META-INF/LICENSE'
        exclude 'META-INF/LICENSE.txt'
        exclude 'META-INF/NOTICE.txt'
        pickFirst "androidx/viewpager/widget/LoopViewPager.class"
    }
    sourceSets {
        main {
            jniLibs.srcDirs = ['libs'] // jnilib so文件目录
            java.srcDirs = ['src/main/java']
            resources.srcDirs = ['src/main/res']
            aidl.srcDirs = ['src/main/aidl']
            renderscript.srcDirs = ['src/main/rs']
            res.srcDirs = ['src/main/res']
            assets.srcDirs = ['src/main/assets']
            shaders.srcDirs = ['src/main/shaders']
            manifest.srcFile 'AndroidManifest.xml'
            androidTest.setRoot('androidTest')
            debug.setRoot('build-types/debug')
            release.setRoot('build-types/release')
            jni.srcDirs = []
        }
    }
}
android {
    defaultConfig {
        ndk {
            //选择要添加的对应cpu类型的.so库。
            abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a', 'x86', 'x86_64', 'mips', 'mips64'
        }
        externalNativeBuild {
            cmake {
                cppFlags "-std=c++11"
                abiFilters 'armeabi'
                arguments "-DANDROID_STL=gnustl_static"
            }
        }
    }
    externalNativeBuild {
        cmake {
            path "CMakeLists.txt"
        }
    }
}
android {
    defaultConfig {
        multiDexEnabled true
    }
}
android {
    defaultConfig {
        consumerProguardFiles 'consumer-rules.pro'
        manifestPlaceholders = [
                UMENG_APPKEY: "5b67faa3f43e48518600021a",
                UMENG_CHANNEL: "bitong"
        ]
    }
}
android {
    dataBinding{
        enabled=true
    }
}
dependencies { // androidx
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'androidx.appcompat:appcompat:1.1.0'
    implementation 'com.google.android.material:material:1.1.0'
    implementation 'androidx.constrainntlayout:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test.ext:junit:1.1.1'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
}
dependencies { // support
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.android.support:appcompat-v7:28.0.0' # appcompat-v7 design recyclerview-v7 percent cardview-v7 support-v4
    implementation 'com.android.support:design:28.0.0'
    implementation 'com.android.support.constraint:constraut:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.2'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
}
android {
    flavorDimensions 'default'
    productFlavors {
        ask {
            applicationId ''
            dimension 'cover'
            manifestPlaceholders = [
                    MAIN_AC:"visit.health.patient.main.MainActivity",
                    APP_NAME:"@string/app_name_patient"
            ]
        }
        brain {
            applicationId ''
            dimension 'cover'
            manifestPlaceholders = [
                    MAIN_AC:"visit.health.patient.main.MainActivity",
                    APP_NAME:"@string/app_name_patient"
            ]
        }
    }
}
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="org.note.myapplication">
    <application>
        <uses-library android:name="android.test.runner"/>
    </application>
    <instrumentation
        android:name="android.test.InstrumentationTestRunner"
        android:label="Tests"
        android:targetPackage="org.note.myapplication" />
</manifest>
android {
    compileSdkVersion 23
    buildToolsVersion "29.0.2"
    defaultConfig {
        applicationId ''
        testInstrumentationRunner "android.test.InstrumentationTestRunner"
    }
}
dependencies { // test
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.android.support:appcompat-v7:23.3.0' # 23.4.0
    testImplementation 'junit:junit:4.12'
}

project.compileSdkVersion as int
resourcePrefix 'machine_'
```

