> Thinking

```
:repositories
	maven { url ""}
		# https://maven.aliyun.com/repository/public
		# http://maven.aliyun.com/nexus/content/groups/public/
		# https://jitpack.io
		# file://D:/adsf/hubtest
	google() # https://maven.aliyun.com/repository/google
	jcenter() # https://maven.aliyun.com/repository/jcenter
	mavenCentral()
	mavenLocal()
	maven { url 'https://maven.aliyun.com/repository/public' }

:dependencies
	implementation compile
	api compile
	provided compileOnly
	annotationProcessor apt
	testImplementation testCompile
	androidTestImplementation androidTestCompile
	
	fileTree(include: ['*.jar'], dir: 'libs')
	project(':<project>')
	name: 'LogMap2-1.0.0', ext: 'aar'
	('', {}) ('') {
		exclude module:'LoopViewPager.class'
		exclude group: 'com.android.support', module: 'support-annotations'
	}
```

> Memory

```

```

