> Thinking

```
环境变量

项目结构
```

> Memory

```
GRADLE_USER_HOME
PATH

project
	subproject
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

settings.gradle
include # ":<name>"
include ':sample', ':bottom-navigation-bar'
rootProject
	name
	buildDir
project(':hyphenatechatsdk').projectDir = new File('../emclient-android/hyphenatechatsdk')

build.gradle
buildscript
	repositories # google()
	dependencies # classpath "com.android.tools.build:gradle:4.2.1"
allprojects
	repositories # flatDir { dirs 'libs' }
task clean(type: Delete) {
    delete rootProject.buildDir
}
getName() # module 名称
project.compileSdkVersion as int

build.gradle
apply plugin:'com.android.application'
apply from:'config.gradle'

// cccXXX=true
// enableAndroidX=false
println(project.findProperty("android.useAndroidX")) // 通过代码设置属性
project.setProperty("android.useAndroidX", enableAndroidX)
println(project.findProperty("android.useAndroidX"))
project.subprojects(new Action<Project>() {
    @Override
    void execute(Project project) {
        print(project.name)
    }
})
print(project)

gradle-wrapper.properties
distributionBase # GRADLE_USER_HOME
distributionPath # wrapper/dists
distributionUrl # https\://services.gradle.org/distributions/gradle-6.7.1-bin.zip
	# gradle-6.5-bin.zip gradle-5.4.1-all.zip
zipStorePath # wrapper/dists
zipStoreBase # GRADLE_USER_HOME

local.properties
ndk.dir=D\:\\Programs\\android-sdk-windows\\ndk-bundle
sdk.dir=D\:\\Programs\\android-sdk-windows
target=android-19
android.library.reference.1=..

gradle.properties
org.gradle.jvmargs=-Xmx2048m -Dfile.encoding=UTF-8
org.gradle.parallel=true
org.gradle.daemon=true
org.gradle.java.home=E:\\AndroidStudio\\jdk
android.useAndroidX=true #启用 AndroidX Refactor -> Migrate to AndroidX
android.enableJetifier=true #依赖库使用 AndroidX
android.useDeprecatedNdk=true

gradlew <task> # assembleRelease
	clean <task> # task -> build






```

