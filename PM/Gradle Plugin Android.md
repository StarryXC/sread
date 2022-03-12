> Thinking

```
com.android.tools.build # classpath gradle-3.3-all.zip
	gradle:2.3.3 gradle-4.10.1-all.zip

<version> <buildType>
```

> Memory

```
:android # com.android.application 应用 com.android.library 库

compileSdkVersion # int 测试23 com.android.support:appcompat-v7:23.3.0 android.test.InstrumentationTestRunner
buildToolsVersion # string

useLibrary # org.apache.http.legacy
resourcePrefix 'machine_'

defaultConfig
	applicationId # library 不能设置
	minSdkVersion # int
	targetSdkVersion # int
	versionCode # int
	versionName # string
	testInstrumentationRunner # android.support.test.runner.AndroidJUnitRunner androidx.test.runner.AndroidJUnitRunner
		# android.test.InstrumentationTestRunner
	consumerProguardFiles 'consumer-rules.pro'
	manifestPlaceholders=[
                MAIN_AC:"visit.health.patient.main.MainActivity",
                APP_NAME:"@string/app_name_patient"
        ]
    multiDexEnabled true
	externalNativeBuild {
		cmake {
			cppFlags "-std=c++11"
			abiFilters 'armeabi'
			arguments "-DANDROID_STL=gnustl_static"
		}
	}
	ndk {
		abiFilters 'x86', 'x86_64', 'armeabi', 'armeabi-v7a', 'arm64-v8a'
	}
	flavorDimensions "default"

externalNativeBuild {
	cmake {
		path "CMakeLists.txt"
	}
}

signingConfigs # config
	storeFile # file("pangdan.keystore")
	storePassword
	keyAlias
	keyPassword
buildTypes # release debug
	minifyEnabled # runProguard false 混淆
	proguardFiles # getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
	buildConfigField # "boolean", "LEO_DEBUG", "true"
	versionNameSuffix # "-deb2ug"
	zipAlignEnabled # Zipalign优化
	shrinkResources # 移除无用的resource文件
	signingConfig # signingConfigs.config
	minifyEnabled

compileOptions
	sourceCompatibility # JavaVersion.VERSION_1_7 JavaVersion.VERSION_1_8
	targetCompatibility

lintOptions
	abortOnError # false 忽略lint错误
	disable "InvalidPackage" # 
	lintConfig file("lint.xml") # 
	checkReleaseBuilds # false

sourceSets # 源文件设置 main
	jniLibs.srcDirs = ['libs']//jnilib so文件目录
    java.srcDirs = ['src']
    resources.srcDirs = ['src']
    aidl.srcDirs = ['src']
    renderscript.srcDirs = ['src']
    res.srcDirs = ['res']
    assets.srcDirs = ['assets']
    jni.srcDirs = []
    jniLibs.srcDirs = ['libs']
    manifest.srcFile 'AndroidManifest.xml'
    androidTest.setRoot('tests')
    debug.setRoot('build-types/debug')
    release.setRoot('build-types/release')

packagingOptions {
	pickFirst "androidx/viewpager/widget/LoopViewPager.class"
}

dataBinding{
    enabled=true
}

flavorDimensions 'cover' # 
productFlavors # <name>
	dimension 'cover'
	applicationId
	manifestPlaceholders



:androidx
implementation fileTree(dir: 'libs', include: ['*.jar'])
implementation 'androidx.appcompat:appcompat:1.1.0'
implementation 'com.google.android.material:material:1.1.0'
implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
testImplementation 'junit:junit:4.12'
androidTestImplementation 'androidx.test.ext:junit:1.1.1'
androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'

:support
implementation fileTree(dir: 'libs', include: ['*.jar'])
implementation 'com.android.support:appcompat-v7:28.0.0' # appcompat-v7 design recyclerview-v7 percent cardview-v7 support-v4
implementation 'com.android.support:design:28.0.0'
implementation 'com.android.support.constraint:constraint-layout:1.1.3'
testImplementation 'junit:junit:4.12'
androidTestImplementation 'com.android.support.test:runner:1.0.2'
androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'

:old test api
implementation fileTree(dir: 'libs', include: ['*.jar'])
implementation 'com.android.support:appcompat-v7:23.3.0' # 23.4.0
testImplementation 'junit:junit:4.12'

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
```

