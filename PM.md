```
FloatingActionButton
	app:srcCompat="@android:drawable/ic_dialog_email"
AppBarLayout
	android:theme="@style/AppTheme.AppBarOverlay"

androidx.appcompat.widget.Toolbar
	app:popupTheme="@style/AppTheme.PopupOverlay"
TextView
	android:textAppearance="?android:attr/textAppearanceLarge"  

ImageView
	android:scaleType="centerInside"
	android:adjustViewBounds="true"
LinearLayout
	android:baselineAligned="false"
TextView
	android:autoLink="web"
	android:textColorLink="@color/result_text"
	android:textIsSelectable="true"
	android:selectAllOnFocus="true"
	android:textAppearance="?android:attr/textAppearanceSmall"
LinearLayout
	app:layout_behavior="@string/appbar_scrolling_view_behavior"
    tools:context=".MainActivity"
    tools:showIn="@layout/activity_main"
android:fillViewport="true"
menu
item
	android:id="@+id/menu_share"
    android:title="@string/menu_share"
    android:icon="@android:drawable/ic_menu_share"
    android:orderInCategory="1"
    android:showAsAction="withText|ifRoom"
    app:showAsAction="never"

  <style name="CaptureTheme" parent="android:Theme.Holo">
    <item name="android:windowFullscreen">true</item>
    <item name="android:windowContentOverlay">@null</item>
    <item name="android:windowActionBarOverlay">true</item>
    <item name="android:windowActionModeOverlay">true</item>
  </style>

<?xml version="1.0" encoding="utf-8"?>
<!--
 Copyright (C) 2008 ZXing authors

 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.
 -->
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">
  <PreferenceCategory android:title="@string/preferences_scanning_title">
    <CheckBoxPreference
        android:key="preferences_decode_PDF417"
        android:defaultValue="false"
        android:title="@string/preferences_decode_PDF417_title"/>
  </PreferenceCategory>
  <PreferenceCategory android:title="@string/preferences_actions_title">
    <CheckBoxPreference
        android:key="preferences_supplemental"
        android:defaultValue="true"
        android:title="@string/preferences_supplemental_title"
        android:summary="@string/preferences_supplemental_summary"/>
  </PreferenceCategory>
  <PreferenceCategory android:title="@string/preferences_general_title">
    <ListPreference
        android:entries="@array/preferences_front_light_options"
        android:entryValues="@array/preferences_front_light_values"
        android:key="preferences_front_light_mode"
        android:defaultValue="OFF"
        android:title="@string/preferences_front_light_title"
        android:summary="@string/preferences_front_light_summary"/>
  </PreferenceCategory>
  <PreferenceCategory android:title="@string/preferences_result_title">
    <EditTextPreference
        android:key="preferences_custom_product_search"
        android:title="@string/preferences_custom_product_search_title"
        android:summary="@string/preferences_custom_product_search_summary"/>
    <ListPreference
        android:key="preferences_search_country"
        android:defaultValue="-"
        android:entries="@array/country_codes"
        android:entryValues="@array/country_codes"
        android:title="@string/preferences_search_country"/>
  </PreferenceCategory>
  <PreferenceCategory android:title="@string/preferences_device_bug_workarounds_title">
    <CheckBoxPreference
        android:key="preferences_disable_continuous_focus"
        android:defaultValue="false"
        android:title="@string/preferences_disable_continuous_focus_title"
        android:summary="@string/preferences_disable_continuous_focus_summary"/>
    <CheckBoxPreference
        android:key="preferences_disable_exposure"
        android:defaultValue="true"
        android:title="@string/preferences_disable_exposure_title"/>
  </PreferenceCategory>
</PreferenceScreen>

fastjson
JSONObject
	parse
	getString
	getJSONObject

HashMap
containsKey put

Intent
	setAction setFlags putExtra

PendingIntent.getBroadcast(ctx, 0, contentIntent, PendingIntent.FLAG_UPDATE_CURRENT);

// 此处必须兼容android O设备，否则系统版本在O以上可能不展示通知栏
        String channelId = ctx.getPackageName();
        String channelName = ctx.getPackageName();
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            NotificationChannel channel = new NotificationChannel(channelId, channelName, NotificationManager.IMPORTANCE_DEFAULT);
            NotificationManager manager = (NotificationManager) ctx.getSystemService(NOTIFICATION_SERVICE);
            manager.createNotificationChannel(channel);
        }

        NotificationCompat.Builder builder = new NotificationCompat.Builder(ctx, channelId)
                .setContentTitle(data.title)
                .setSmallIcon(SmartCloudSdk.AppIcon)
                .setContentText(data.content)
                .setStyle(new NotificationCompat.BigTextStyle().bigText(data.content).setBigContentTitle(data.title))
                .setContentIntent(_createPendingIntent(ctx,SmartCloudAgooNotificationContentAction, data))
                .setDeleteIntent(_createPendingIntent(ctx,SmartCloudAgooNotificationDeleteAction, data))
                .setWhen(System.currentTimeMillis())
                .setOngoing(false)
                .setChannelId(channelId)
                ;

        if(data.sound != null){
            Uri uri = Uri.parse(data.sound);
            builder.setSound(uri);
        }else{
            builder.setDefaults(NotificationCompat.DEFAULT_ALL);
        }

        if(data.imageUrl != null){
            if(data.imageUrl.startsWith("/")) {
                Bitmap bitmap = BitmapFactory.decodeFile(data.imageUrl);
                if(bitmap != null) {
                    builder.setLargeIcon(bitmap);
                }
            }else {
                Bitmap bitmap = getBitmap(data.imageUrl);
                if(bitmap != null) {
                    builder.setLargeIcon(bitmap);
                }
            }
        }

        if(SmartCloudSdk.isDebug){
            builder.setPriority(NotificationCompat.PRIORITY_MAX);
        }

        NotificationManager manager = (NotificationManager) ctx.getSystemService(NOTIFICATION_SERVICE);
        manager.notify(counter++, builder.build());

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.GINGERBREAD) {
            StrictMode.setThreadPolicy(new StrictMode.ThreadPolicy.Builder().detectAll().penaltyLog().build());
            StrictMode.setVmPolicy(new StrictMode.VmPolicy.Builder().detectAll().penaltyLog().build());
        }
        
 LoginBroadcastHelper.registerLoginReceiver       

Context
	<packageName>
PackageManager
	<packageInfo>
PackageInfo
	<version>

LocalBroadcastManager
	getInstance
	sendBroadcast
	registerReceiver
	unregisterReceiver

AppCompatActivity
Toolbar toolbar = findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);

FloatingActionButton

Snackbar.make(view, "Replace with your own action", Snackbar.LENGTH_LONG)
                        .setAction("Action", null).show();


onCreateOptionsMenu
onOptionsItemSelected
MenuInflater
	inflate
MenuItem
getItemId

registerActivityLifecycleCallbacks
Handler 
	<obtain>

ClipboardManager clipboard = getManager(context);
    ClipData clip = clipboard.getPrimaryClip();
    return hasText(context) ? clip.getItemAt(0).coerceToText(context) : null;
    
    getManager(context).setPrimaryClip(ClipData.newPlainText(null, text));

    ClipboardManager clipboard = getManager(context);
    ClipData clip = clipboard.getPrimaryClip();
    return clip != null && clip.getItemCount() > 0;

URI JAVA.NET
Pattern
	compile
	matcher
Matcher
	find
	group
String.substring(0
Html.fromHtml(title)

WeakReference
	<get>

TextView
textView.append(content);
textView.setMovementMethod(LinkMovementMethod.getInstance());

StringBuilder
append
length

Spannable content = new SpannableString(newText + "\n\n");
content.setSpan(new URLSpan(linkURL), linkStart, linkEnd, Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);

context.getString(R.string.msg_g
URLEncoder.encode(produc

org.json
JSONObject topLevel = (JSONObject) new JSONTokener(contents.toString()).nextValue();
      JSONArray items = topLevel.optJSONArray("items");
authorsArray.isNull(0)

new SimpleDateFormat("yyyyMMdd'T'HHmmss", Locale.ENGLISH),
format.setLenient(false);

Spannable styled = new SpannableString(contents.toString());
      styled.setSpan(new StyleSpan(Typeface.BOLD), 0, namesLength, 0);


Intent intent = new Intent(Intent.ACTION_INSERT);
    intent.setType("vnd.android.cursor.item/event");
    intent.putExtra("beginTime", start);
    if (allDay) {
      intent.putExtra("allDay", true);
    }
    if (end < 0L) {
      if (allDay) {
        // + 1 day
        end = start + 24 * 60 * 60 * 1000;
      } else {
        end = start;
      }
    }
    intent.putExtra("endTime", end);
    intent.putExtra("title", summary);
    intent.putExtra("eventLocation", location);
    intent.putExtra("description", description);
    if (attendees != null) {
      intent.putExtra(Intent.EXTRA_EMAIL, attendees);
      // Documentation says this is either a String[] or comma-separated String, which is right?
    }

    try {
      // Do this manually at first
      rawLaunchIntent(intent);
    } catch (ActivityNotFoundException anfe) {
      Log.w(TAG, "No calendar app available that responds to " + Intent.ACTION_INSERT);
      // For calendar apps that don't like "INSERT":
      intent.setAction(Intent.ACTION_EDIT);
      launchIntent(intent); // Fail here for real if nothing can handle it
    }

DateFormat format = allDay
        ? DateFormat.getDateInstance(DateFormat.MEDIUM)
        : DateFormat.getDateTimeInstance(DateFormat.MEDIUM, DateFormat.MEDIUM);
return format.format(date);

AsyncTask.executeOnExecutor(AsyncTask.THREAD_POOL_EXECUTOR);
task.cancel(true);

protected void onListItemClick(ListView l, View view, int position, long id) {
    Adapter adapter = getListAdapter();
    if (position >= 0 && position < adapter.getCount()) {
      String packageName = ((AppInfo) adapter.getItem(position)).getPackageName();
      Intent intent = new Intent();
      intent.addFlags(Intents.FLAG_NEW_DOC);
      intent.putExtra("url", "market://details?id=" + packageName); // Browser.BookmarkColumns.URL
      setResult(RESULT_OK, intent);
    } else {
      setResult(RESULT_CANCELED);      
    }
    finish();
  }


BaseAdapter
	<count> <item> <view>
View
	<findView>
LayoutInflater
	<init> <inflate>
Object
	<equals> <hashCode>

content://browser/bookmarks ndroid.provider.Browser.BOOKMARKS_URI:
title Browser.BookmarkColumns.TITLE
url Browser.BookmarkColumns.URL
Intent intent = new Intent();
    intent.addFlags(Intents.FLAG_NEW_DOC);
    intent.putExtra("title", titleURL[0]); // Browser.BookmarkColumns.TITLE
    intent.putExtra("url", titleURL[1]); // Browser.BookmarkColumns.URL
    setResult(RESULT_OK, intent);

ContentResolver
	query
Cursor
	moveToNext
	getString

PackageManager
	getInstalledApplications
ApplicationInfo
PackageItemInfo
	packageName
	appInfo.loadLabel(packageManager);
	appInfo.loadIcon(packageManager);

Collections.sort(labelsP
Name.startsWith(pre

ImageView setImageDrawable

Intent intent = new Intent(Intent.ACTION_PICK, ContactsContract.Contacts.CONTENT_URI);
      intent.addFlags(Intents.FLAG_NEW_DOC);
      startActivityForResult(intent, PICK_CONTACT);
      Intent intent = new Intent(Intent.ACTION_PICK);
      intent.addFlags(Intents.FLAG_NEW_DOC);
      intent.setClassName(ShareActivity.this, BookmarkPickerActivity.class.getName());
      startActivityForResult(intent, PICK_BOOKMARK);

KeyEvent
keyCode == KeyEvent.KEYCODE_ENTER && event.getAction() == KeyEvent.ACTION_DOWN
cursor
getColumnIndex
getInt
moveToNext

ContactsContract.Contacts.DISPLAY_NAME
ContactsContract.Contacts.HAS_PHONE_NUMBER

ContactsContract.CommonDataKinds.Phone.CONTENT_URI
ContactsContract.CommonDataKinds.Phone.CONTACT_ID
ContactsContract.CommonDataKinds.Phone.NUMBER getString
ContactsContract.CommonDataKinds.Phone.TYPE getInt

ContactsContract.CommonDataKinds.StructuredPostal.CONTENT_URI
ContactsContract.CommonDataKinds.StructuredPostal.CONTACT_ID
ContactsContract.CommonDataKinds.StructuredPostal.FORMATTED_ADDRESS
ContactsContract.Intents.Insert.POSTAL putString

ContactsContract.CommonDataKinds.Email.CONTENT_URI
ContactsContract.CommonDataKinds.Email.CONTACT_ID
ContactsContract.CommonDataKinds.Email.DATA

WifiConfiguration
wifiManager.isWifiEnabled()
wifiManager.removeNetwork(foundNetworkID);
      wifiManager.saveConfiguration();
wifiManager.addNetwork(config);
wifiManager.enableNetwork(networkId
wifiManager.saveConfiguration();

junit
@Test
assertEquals

HashMap
	<put> <isEmpty> <get> <size>
	<contains>
	<keySet> <clear>
Activity
	<finish> finish isFinishing
SQLiteOpenHelper
<lifecycle>
SQLiteDatabase
<execSQL>
Activity
configurationChanged configChanges

application
	<icon> <label> <name> <theme>

PackageManager packageManager = context.getPackageManager();
			PackageInfo packageInfo = packageManager.getPackageInfo(
					context.getPackageName(), 0);
			int labelRes = packageInfo.applicationInfo.labelRes;
			return context.getResources().getString(labelRes);
			
packageInfo.versionName;
packageInfo.versionCode;
			
WifiManager wifiManager = (WifiManager) context
				.getSystemService(context.WIFI_SERVICE);
		WifiInfo wifiInfo = wifiManager.getConnectionInfo();
		int ipAddress = wifiInfo.getIpAddress();
		String ip = String.format("%d.%d.%d.%d", (ipAddress & 0xff),
				(ipAddress >> 8 & 0xff), (ipAddress >> 16 & 0xff),
				(ipAddress >> 24 & 0xff));
		return ip;			
	InetAddress.getLocalHost().toString();		
			
Enumeration<NetworkInterface> en = NetworkInterface.getNetworkInterfaces();
while (en.hasMoreElements())
{
	NetworkInterface nif = en.nextElement();//
	Enumeration<InetAddress> inet = nif.getInetAddresses();
	while (inet.hasMoreElements())
	{
		InetAddress ip = inet.nextElement();
		if (!ip.isLoopbackAddress()
				&& InetAddressUtils.isIPv4Address(ip
				.getHostAddress()))
		{
			return ipaddress = ip.getHostAddress();
		}
	}
}			
			
			
```





# Gradle

## 环境配置

```
gradle

GRADLE_USER_HOME
PATH

:项目结构
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

:settings.gradle
include # ":<name>"
include ':sample', ':bottom-navigation-bar'
rootProject
	name
	buildDir
project(':hyphenatechatsdk').projectDir = new File('../emclient-android/hyphenatechatsdk')

:build.gradle
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

:build.gradle
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

:gradle-wrapper.properties
distributionBase # GRADLE_USER_HOME
distributionPath # wrapper/dists
distributionUrl # https\://services.gradle.org/distributions/gradle-6.7.1-bin.zip
	# gradle-6.5-bin.zip gradle-5.4.1-all.zip
zipStorePath # wrapper/dists
zipStoreBase # GRADLE_USER_HOME

:local.properties
ndk.dir=D\:\\Programs\\android-sdk-windows\\ndk-bundle
sdk.dir=D\:\\Programs\\android-sdk-windows
target=android-19
android.library.reference.1=..

:gradle.properties
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

## 命令行

```
gradle
```

## 依赖管理

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

## 插件

### Android

```
com.android.tools.build # classpath gradle-3.3-all.zip
	gradle:2.3.3 gradle-4.10.1-all.zip

<version> <buildType>

api 'com.google.zxing:android-core:3.3.0'
    api 'com.google.zxing:core:3.4.0'

android.net.conn.CONNECTIVITY_CHANGE
android.intent.action.PACKAGE_REMOVED
android.intent.action.BOOT_COMPLETED

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

### Kotlin-Android

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


implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
implementation "org.jetbrains.kotlin:kotlin-stdlib-jre7:$kotlin_version"
androidx.core:core-ktx:1.0.2
```

### Kotlin

```

```

### Maven

```
:maven # gradle upload 执行方式 gradlew uploadArchives

uploadArchives
	repositories.mavenDeployer
		repository(url: uri('E:/env/repo')) # 配置本地仓库路径，项目根目录下的repository目录中
			# repository(url: uri('libs'))
			# repository(url: uri("${rootProject.projectDir}/"))
			# repository(url:  'maven.repo.local' )
		pom.groupId = "yes.ican.logmap-android" # 唯一标识（通常为模块包名，也可以任意）
        pom.artifactId = "LogMap" # 项目名称（通常为类库模块名称，也可以任意）
        pom.version = "1.0.0" # 版本号
        pom.packaging = "aar" # 
        pom.project {
			name  'viewlibrary'
			groupId  'secondriver'
			artifactId  'viewlibrary'
			version  '1.2.0'
			packaging  'aar'

			licenses {
				license {
					name  'The Apache Software License, Version 2.0'
					url  'http://www.apache.org/licenses/LICENSE-2.0.txt'
					distribution  'repo'
				}
			}

			developers {
				developer {
					id  'secondriver'
					name  'secondriver'
				}
			}
		}

task uploadLocal(type: Upload) {
    // 需要把config设置成project的，要不然会报错
    configuration = project.configurations.findByName('archives')
    repositories {
        mavenDeployer {
            repository(url: uri('C:/Users/Developer/Desktop/StarryAndroidSupport/repo'))
            pom.groupId = "czw.starry"// 唯一标识（通常为模块包名，也可以任意）
            pom.artifactId = "starry-java" // 项目名称（通常为类库模块名称，也可以任意）
            pom.version = "1.0.0" // 版本号
        }
    }
}

uploadArchives.dependsOn uploadLocal # 
```

### android-maven

```
com.github.dcendents # classpath
	android-maven-gradle-plugin:1.5

com.github.dcendents.android-maven
group='com.ert.asdf'
```



### java

```
:java # 
sourceCompatibility # = JavaVersion.VERSION_1_7
targetCompatibility
dependencies # implementation fileTree(dir: 'libs', include: ['*.jar'])
```

### java-library

```
:java-library
java
	sourceCompatibility
	targetCompatibility
```

```

```



# Maven

## 环境配置

```

```

## 命令行

```
mvn
```

## Nexus

```
https://www.sonatype.com/nexus
```

## Bintray

```
https://bintray.com/signup/oss
```



# Ant

## 环境配置

```
Ant
ANT_HOME PATH
```

## 命令行

```
ant # 默认 build.xml
	-version # 版本
```

## build.xml

```
<project> # name default
<target> # name depends
<property> # name value 内置属性 自定义属性
<task-name> # 内置任务 用户自定义任务

<copy> # 拷贝
<javac>


<zip> # 归档
<gzip>
```



# CMake

## 环境配置

```

```

## 命令行

```
cmake
```

## CMakeLists.txt

# GNUMake

## 环境配置

```

```

## 命令行

```
make # 执行编译
```

## 语法

```
target
```



# XMake

## 环境配置

```
:Mac # brew
xmake pkg-config # xmake是构建工具 pkg-config是用来提供编译指令 在xmake.lua中

```

# Git

## 环境配置

```
Git # GitHub
```

## 运行原理

```
工作区 本地仓库 远程仓库
```



## 命令行

```
git
	--help
	--version

git init # 初始化仓库

git branch # 查看本地分支
	-a

git clone <url> # scheme: http https ssh git
	-b <branch> # 指定分支拉取

git pull # 更新本地分支
	origin <branch> # 拉取指定分支

git push # 推送本地仓库到远程仓库
	-u origin master

git fetch

git status



git add 添加文件到代码库
git add origin 添加库源
git add origin <branch> 默认 master
git add origin url 远程url

git commit 提交文件到代码库
git commit -m "update" 提交日志
git commit -am 添加当前所有文件并提交

git config
git config --system http.sslcainfo D:\\Programs\\Git\\mingw32\\ssl\\certs\\ca-bundle.crt
git config --global user.email "czwxiaoliang@163.com"
git config --global user.name "czwxiaoliang"

.gitconfig
[user]
	email = czwxiaoliang@163.com
	name = chengzhiwei



git remote 关联远程库
git remote -v 显示远程库版本

git merge 合并分支
git merge origin/master --allow-unrelated-histories 解决冲突

ssh-keygen # 密钥生成器
```

## .gitignore

```
/build	目录
/name/
*.ext
/name/name.ext
/* 所有文件
name/ 根目录 子目录
# 注释

通配符
/ 斜杠 目录
* 星号 匹配多个字符
? 问号 匹配单个字符
[] 方括号 单字符匹配列表
! 不忽略文件 跟踪文件
```

```

```

## GitLab

```

```

## Gerrit

```

```

## Phabricator

```

```

### Arcanist

```

```



# SVN

## 环境配置

```

```

## 命令行

```
svn
```

# CVS

## 环境配置

```

```

## 命令行

```

```