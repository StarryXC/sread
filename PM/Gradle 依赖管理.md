> Thinking

```
repositories
dependencies
	implementation compile
	api compile
	provided compileOnly
	annotationProcessor apt
	testImplementation testCompile
	androidTestImplementation androidTestCompile
```

> Memory

```
Maven Urls
https://jitpack.io
maven { url "https://maven.aliyun.com/repository/public" }
maven { url "https://maven.aliyun.com/repository/google" }
maven { url "https://maven.aliyun.com/repository/jcenter" }
maven { url "file://D:/adsf/hubtest" }
maven { url "http://maven.aliyun.com/nexus/content/groups/public/" }
maven { url 'https://maven.google.com/' name 'Google'}

repositories {
    maven { name "" url "" }
    google()
    jcenter()
    mavenCentral()
    mavenLocal()
}

dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    implementation project(':app')
    implementation (name: 'LogMap2-1.0.0', ext: 'aar') {
        exclude module:'LoopViewPager.class'
        exclude group: 'com.android.support', module: 'support-annotations'
    }
}
```

