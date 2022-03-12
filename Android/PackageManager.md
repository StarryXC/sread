> Thinking

```
PackageManager
PackageInfo
PackageItemInfo

AndroidManifest.xml

PackageManager
	getInstalledApplications
ApplicationInfo
PackageItemInfo
	packageName
	appInfo.loadLabel(packageManager);
	appInfo.loadIcon(packageManager);
```

> Memory

```
PackageManager
	PERMISSION_GRANTED

PackageManager
	PERMISSION_GRANTED

PackageManager packageManager = context.getPackageManager();
			PackageInfo packageInfo = packageManager.getPackageInfo(
					context.getPackageName(), 0);
			int labelRes = packageInfo.applicationInfo.labelRes;
			return context.getResources().getString(labelRes);
			
packageInfo.versionName;
packageInfo.versionCode;

android.permission.INTERNET 访问网络
android.permission.CAMERA # 访问相机
android.permission.ACCESS_FINE_LOCATION # GPS定位 网络定位
android.permission.ACCESS_COARSE_LOCATION # 网络定位 信号接收塔 WiFi接入点


android.permission.ACCESS_WIFI_STATE 访问wifi网络信息，可用于网络定位
android.permission.ACCESS_NETWORK_STATE 获取运营商信息
android.permission.CHANGE_WIFI_STATE 改变wifi状态权限
android.permission.READ_PHONE_STATE 读取手机当前状态
android.permission.WRITE_EXTERNAL_STORAGE 向扩展存储写入数据
android.permission.READ_EXTERNAL_STORAGE
android.permission.MOUNT_UNMOUNT_FILESYSTEMS SD卡读取权限
android.permission.INTERACT_ACROSS_USERS_FULL
android.permission.RECORD_AUDIO
android.permission.READ_LOGS
android.permission.GET_TASKS
android.permission.SET_DEBUG_APP
android.permission.SYSTEM_ALERT_WINDOW
android.permission.GET_ACCOUNTS
android.permission.MANAGE_ACCOUNTS
android.permission.USE_CREDENTIALS
android.permission.MANAGE_ACCOUNTS
android.permission.WRITE_APN_SETTINGS
android.permission.READ_CONTACTS
android.permission.FLASHLIGHT

android.permission.VIBRATE
android.permission.INTERNET
android.permission.RECORD_AUDIO
android.permission.CAMERA
android.permission.ACCESS_NETWORK_STATE
android.permission.ACCESS_MOCK_LOCATION
android.permission.WRITE_EXTERNAL_STORAGE
android.permission.MOUNT_UNMOUNT_FILESYSTEMS
android.permission.ACCESS_FINE_LOCATION
android.permission.GET_TASKS
android.permission.ACCESS_WIFI_STATE
android.permission.CHANGE_WIFI_STATE
android.permission.WAKE_LOCK
android.permission.MODIFY_AUDIO_SETTINGS
android.permission.READ_PHONE_STATE
android.permission.RECEIVE_BOOT_COMPLETED

android.permission.READ_PRIVILEGED_PHONE_STATE

SEND_SMS
CALL_PHONE
RECORD_AUDIO
READ_EXTERNAL_STORAGE WRITE_EXTERNAL_STORAGE
CAMERA
RECORD_AUDIO

AndroidManifest.xml
<application>
    android:usesCleartextTraffic="true" android 9.0 强制使用https的问题
    android:allowBackup
    	<icon> <label> <name> <theme>
<uses-library>
    android:name="org.apache.http.legacy" android:required="false" android 9.0 使用 httpclient
<provider>
    android:name="androidx.core.content.FileProvider" android 7.0 访问file
    android:authorities="${applicationId}.fileProvider"
    android:grantUriPermissions="true"
    android:exported="false"
<meta-data>
    android:name="android.support.FILE_PROVIDER_PATHS"
    android:resource="@xml/file_paths"
file_paths
<paths>
<external-path>
	path # . 目录
	name # external_storage_root

<intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <data>
        android:scheme="http"
        android:host="baidu.com"
        android:mimeType="image/jpeg"

Features
android.hardware.camera
android.hardware.camera.autofocus
android.hardware.camera.front
android.hardware.camera.front.autofocus

Categorys
Intent.CATEGORY_LAUNCHER android.intent.category.LAUNCHER
android.intent.category.DEFAULT
android.intent.category.OPENABLE
android.intent.category.BROWSABLE


Actions
Intent.ACTION_MAIN android.intent.action.MAIN
android.intent.action.VIEW
android.intent.action.GET_CONTENT

Intent.ACTION_BATTERY_CHANGED
boolean onBatteryNow = intent.getIntExtra(
						BatteryManager.EXTRA_PLUGGED, -1) <= 0;

Context
	<packageName>
PackageManager
	<packageInfo>
PackageInfo
	<version>
	
系统权限定义
Manifest.permission
	INTERNET
```

