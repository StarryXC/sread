> Thinking

```
环境变量

project # 项目结构
	module
		build.gradle
	gradle
		wrapper
			gradle-wrapper.jar
			gradle-wrapper.properties
	build.gradle
	settings.gradle
	gradle.properties
	local.properties
	gradlew
	gradlew.bat
```

> Memory

```
GRADLE_USER_HOME PATH

settings.gradle
rootProject.name = ""
include ':app'
include ':app', ':app'
project(':app').projectDir(new File(""))
findProject(':app').name = "name"

gradle.properties
org.gradle.jvmargs=-Xmx2048m -Dfile.encoding=UTF-8
org.gradle.parallel=true
org.gradle.daemon=true
org.gradle.java.home=E:\\AndroidStudio\\jdk
kotlin.code.style=official
android.useAndroidX=true # 启用 AndroidX Refactor -> Migrate to AndroidX
android.enableJetifier=true # 依赖库使用 AndroidX
android.useDeprecatedNdk=true
android.buildCacheDir=./build-cache

build.gradle
buildscript {
    repositories {
        google()
        maven { url 'https://maven.aliyun.com/repository/public' }
        maven { url 'https://maven.aliyun.com/repository/jcenter' }
        maven { url 'https://maven.aliyun.com/repository/google' }
    }
    dependencies {
        classpath "com.android.tools.build:gradle:4.2.1"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:1.5.20"
    }
}
allprojects {
    repositories {
        maven { url 'https://maven.aliyun.com/repository/public' }
        maven { url 'https://maven.aliyun.com/repository/jcenter' }
        maven { url 'https://maven.aliyun.com/repository/google' }
    }
    flatDir { dirs 'libs' }
}
task clean(type: Delete) {
    delete rootProject.buildDir
}
this.getAllprojects()
this.getName()
String property = project.findProperty("android.useAndroidX")
project.setProperty("android.useAndroidX", true)
project.subprojects(new Action<Project>() {
    @Override
    void execute(Project project) {
        print(project.name)
    }
})

build.gradle
apply plugin:'com.android.application'
apply from:'config.gradle'

gradle-wrapper.properties
distributionBase=GRADLE_USER_HOME
# 6.5 5.4.1 4.10.1 3.3 2.3.3
distributionUrl=https\://services.gradle.org/distributions/gradle-6.7.1-bin.zip
distributionPath=wrapper/dists
zipStorePath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME

local.properties
ndk.dir=D\:\\Programs\\android-sdk-windows\\ndk-bundle
sdk.dir=D\:\\Programs\\android-sdk-windows
target=android-19
android.library.reference.1=..
```

