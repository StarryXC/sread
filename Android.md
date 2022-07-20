# Android 发展史

```
行为变更
版本api对应关系
```

# Android 环境搭建

```
环境搭建
环境变量
项目结构

Android Studio 工具 # Logcat | -Dfile.encoding=UTF-8 | 快捷键

BlueStacks Genymotion https://cloud.genymotion.com/
```

## Android 命令行

```
adb install
adb uninstall
adb devices
adb tcpip
adb connect
adb shell
adb reboot

aapt
dex
getprop
pm
prop
ro.product.cpu.abi

pm list instrumentation 运行测试后，执行adb指令
```

## Android 项目结构

```
project
    module
        src
            main
                assets
                java
                jni
                AndroidManifest.xml
        build.gradle
        proguard-rules.pro
```

## AOSP

```
Android 源码目录结构

https://source.android.google.cn/
AndroidXRef就是其中一款备受青睐的源码在线阅读网站【网址：http://androidxref.com/】
需要VPN，即需要FQ
Android SDK Search 使用方法】

sudo apt-get install git git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev libc6-dev 
sudo apt-get install lib32ncurses5-dev x11proto-core-dev libx11-dev 
sudo apt-get install lib32z-dev libgl1-mesa-dev g++-multilib mingw32 tofrodos python-markdown 
sudo apt-get install libxml2-utils xsltproc gcc-multilib lib32readline5-dev
sudo apt-get install git

编译
source build/envsetup.sh
编译安卓源码
make (也可以使用 make -j4 四线程编译)
运行模拟器
lunch sdk-eng
emulator
emulator -kernel ./kernel/goldfish-android-goldfish-3.4/arch/arm/boot/zImage 指定内核启动模拟器
编译SDK
make -j4 sdk

命令查看内核版本
adb shell
cd proc
cat version

source build/envsetup.sh
mmm development/tools/idegen/ 编译idegen模块 mmm命令会把system.img等文件删除
out/host/linux-x86/frameworks/目录下生成了idegen.jar文件

development/tools/idegen/idegen.sh 根目录下生成
android.iml和android.ipr这两个文件，这两个文件是Android Studio的工程配置文件
make snod 重新生成镜像

源码地址 Android社区
https://www.androidos.net.cn/sourcecode
https://www.androidos.net.cn/android/9.0.0_r8/tree
```

# Android 框架原理

## Android 系统架构

```
系统架构
    应用程序层
    应用程序框架层
    运行时库层
    Linux内核层

架构原理
    系统启动过程
    Activity 启动过程
    Service 启动过程

HAL Hardware Abstract Layer 硬件抽象层
```

## Android 系统启动过程

```
BootLoader
内核空间 idle kthreadd
用户空间 进程 init

java 进程 zygote 孵化器 受精卵  fork 进程
 app_main.cpp main()  初始化 AndroidRuntime 环境 AppRuntime start
  AndroidTuntime.cpp start
    startVm 启动虚拟机
    注册jni
    jni调用 zygoteinit main
 zygoteInit 创建虚拟机 main方法 进入java的入口函数
 	preload 预加载信息 一部分framework资源 和 常用 java类  加快应用进程的启动
 	ZygoteServer 创建zygoteserver服务 Socket 进程通讯机制  binder 还没有初始化完成
 	forkSystemServer创建  反射启动system_server进程 执行main方法
 	  RuntimeInit .applicationInit
 	zygoterunselectloop zygote进入无线循环 ams发消息创建进程
 	
fork 写时拷贝 思索 binder多进程 容易死锁

SystemServer 系统服务 ams wms pkms
 lemanager 生命周期管理类
publishBinderService ServiceManager.addService 添加到ServiceManager
ams
初始化 clientlifecyclemanager
创建activity task 管理类

setSystemProvices 
meminfo 
dumpsys meminfo
gfxinfo binder
dbinfo
cpuinfo
permissinfo
processinfo
cacheinfo
dumpsys activity


 sublimetext

Activty
9。0 ams startactivyt
atm startactivity
servicemanager getService 代理模式

进程存在 realstartactivityLocked
进程不存在 service.startProcessAsync socket 通知 syogate fork 进程
如果创建应用进程 发射执行 Activity Thread main

ams  如何管理信的进程生命周期
句柄 activitry给 ams
attachapplication applicationthread

启动不用注册的Activitu 插件化 保管里 资源加载 类加载




binder 内存拷贝





Apps.loop

xygote fork 原因
ps 命令查看
init 
虚拟机再gogate 创建
systemserver 创建系统服务 所有应用进程共用服务 进程间通讯



进程 虚拟机
一个进程一个虚拟机
一个虚拟机一个进程
隔离 
进程 操作系统分配资源的最小单位 内存私有 进程隔离
虚拟机管理内存 符合沙河机制 进程挂点不会影响其他进程
线程 cpu执行调度的最小单位

```



# Android 框架搭建

## MVX

```
架构模式
    MVC
    MVP
    MVVM
pojo dao

Base 类设计


:MVC
BaseApplication # Application appContext = this getAppContext
BaseActivity # getLayoutId abstract

:MVP
BaseActivity<V, P> # V BaseView P BasePresenterImpl<V> BaseView LayoutInterface
	mPresenter # P Unbinder unbinder
	onCreate # attachView getLayoutId bind initViews(初始化recyclerview)
	onDestroy # detachView unbind

BaseFragment<V, P> # <V extends BaseView, P extends BasePresenterImpl<V>> BaseView, LayoutInterface
	mPresenter # P
	unbinder # Unbinder
	onCreateView # getLayoutId bind getInstance attachView initViews
	onDestroyView # detachView unbind

:base
BaseView # interface
BasePresenter # interface <V extends BaseView> attachView detachView isViewAttached
	BasePresenterImpl # mView
LayoutInterface # interface getLayoutId initViews

public class BaseHelper {
    public static <T> T getInstance(Object o, int i) {
        try {
            return ((Class<T>) ((ParameterizedType) (o.getClass()
                    .getGenericSuperclass())).getActualTypeArguments()[i])
                    .newInstance();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }
}

:business
BusinessContract # interface
BusinessContract.View # BaseView BusinessMethod
BusinessContract.Presenter # BasePresenter<BusinessContract.View> BusinessMethod
BusinessActivity
BusinessFragment

MainContract
MainContract.View # newFragment(tabId) MainActivity TabClickListener
MainActivity # initViews setFragmentManager TabClickListener
MainContract.Presenter # setFragmentManager showFragment(tabId)
MainPresenter # detachView mFragmentManager fragments.clear
	fragments # SparseArray<Fragment>
	mCurTabId # 
	mFragmentManager # 

public void showFragment(int tabId) {
        FragmentTransaction transaction = mFragmentManager.beginTransaction();
        if(mCurTabId != 0) {
            transaction.hide(fragments.get(mCurTabId));
        }
        Fragment newFragment = fragments.get(tabId);
        if(newFragment == null) {
            newFragment = mView.newFragment(tabId);
            fragments.put(tabId, newFragment);
            transaction.add(R.id.container, newFragment);
        } else {
            transaction.show(newFragment);
        }
        transaction.commitAllowingStateLoss();
        mCurTabId = tabId;
    }


ActivityItemConverter.newInstance()
                                .addHintItem("endedActivitiesList")
                                .addActivityItem(activitiesList.getEndedActivitiesList())
                                .addHintItem("onGoingActivitiesList")
                                .addActivityItem(activitiesList.getOnGoingActivitiesList())
                                .convert();

public static class ActivityItemConverter {
        public static ActivityItemConverter newInstance() {
            return new ActivityItemConverter();
        }
        private List<ItemData<?>> itemDataList = new ArrayList<>()
        public ActivityItemConverter addHintItem(String hint) {
            ItemData<String> itemData = new ItemData<>();
            itemData.setType(ItemData.ACTIVITY_HINT);
            itemData.setData(hint);
            itemDataList.add(itemData);
            return this;
        }
        public ActivityItemConverter addActivityItem(List<Activity> activities) {
            for (int i=0; i<activities.size(); i++) {
                ItemData<Activity> itemData = new ItemData<>();
                itemData.setType(ItemData.ACTIVITY_DATA);
                itemData.setData(activities.get(i));
                itemDataList.add(itemData);
            }
            return this;
        }
        public List<ItemData<?>> convert(){
            return itemDataList;
        }
    }
getItemViewType
data getType
ItemData<T>
BaseMutilTypeHolder<T> # onCreateViewHolder
	HintViewHolder.create(viewGroup) # LayoutInflater.from(parent.getContext()).inflate(R.layout.item_home, parent, false);
		ButterKnife.bind(this, itemView);
	ActivityViewHolder.create(viewGroup)
onBindViewHolder
	viewHolder.bindItemData

:MVVM
```

## xUtils

```
compile 'com.jiechic.library:xUtils:2.6.14'

ViewUtils
ViewUtils

https://github.com/wyouflf/xUtils
com.jiechic.library:xUtils:2.6.14

ViewUtils # inject
@ViewInject
@OnClick

DbManager # 
Column

xUtils3 https://github.com/wyouflf/xUtils3

```

# Android 性能优化

```
性能监控
性能优化
    布局优化
    内存优化
    启动优化
```

```
Debug
Debug.MemoryInfo

StrictMode.setThreadPolicy(new StrictMode.ThreadPolicy.Builder()
        .detectDiskReads()
        .detectDiskWrites()
        .detectNetwork()
        .penaltyLog()
        .build()
);
StrictMode.setVmPolicy(new StrictMode.VmPolicy.Builder()
        .detectLeakedSqlLiteObjects()
        .detectLeakedClosableObjects()
        .penaltyLog()
        .penaltyDeath()
        .build()
);
```

## Bugly

```
implementation 'com.tencent.bugly:crashreport:latest.release'
```

## LeakCanary

```
https://github.com/square/leakcanary/
leakcanary-android debugImplementation

```

## RenderScript

```
RenderScript
Allocation
```

## scalpel

```
debugCompile 'com.amitshekhar.android:debug-db:1.0.0' //在网页上查看sp和数据库 adb forward tcp:8080 tcp:8080
implementation 'com.jakewharton.scalpel:scalpel:1.1.2' // 检查过渡绘制

```

# Android 应用组件

```

```

# Android 广播接收器

```
系统广播
Intent.ACTION_BOOT_COMPLETED
Intent.ACTION_SCREEN_ON
```

## 来/去电广播

```
TelephonyManager.ACTION_PHONE_STATE_CHANGED
Manifest.permission.READ_PHONE_STATE
通话状态
去电
Intent.ACTION_NEW_OUTGOING_CALL 去电
Manifest.permission.PROCESS_OUTGOING_CALLS
String phoneNumber = intent.getStringExtra(Intent.EXTRA_PHONE_NUMBER);

```

## 电量变化广播

```
Intent.ACTION_BATTERY_CHANGED
request
response
int level = intent.getIntExtra("level",0);//电池剩余容量
int scale = intent.getIntExtra("scale",100);//电池总量
int cap = level * 100 / scale;//电池电量

```

## 短信接收广播

```
action 接收短信
if (android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.DONUT) {
    Object[] pduses = (Object[])intent.getExtras().get("pdus");
    for(Object pdus : pduses){
        byte[] pdusmessage = (byte[]) pdus;
        SmsMessage sms = SmsMessage.createFromPdu(pdusmessage);
        String mobile = sms.getOriginatingAddress();
        String content = sms.getMessageBody();
        long timestampMillis = sms.getTimestampMillis();
    }
}
```

## 网络状态变化

```
网络
监听网络变化
获取网络状态

android.permission.INTERNET
android.intent.action.MAIN
android.intent.category.LAUNCHER
android.intent.action.USER_PRESENT
android.intent.action.BOOT_COMPLETED
android.intent.action.PACKAGE_REMOVED
android.net.conn.CONNECTIVITY_CHANGE
android.intent.action.PACKAGE_REMOVED
android.intent.action.BOOT_COMPLETED
```

# Android 内容提供者

```

系统提供者
CalendarContract

```

## CalendarContract

```
CalendarContract.Events
_ID
TITLE
CONTENT_URI
DESCRIPTION
EVENT_LOCATION
EXTRA_EVENT_BEGIN_TIME long
EXTRA_EVENT_ALL_DAY boolean

ContactsContract.Contacts
_ID
DISPLAY_NAME
CONTENT_URI
CONTENT_FILTER_URI

ContactsContract.Data
CONTACT_ID
MIMETYPE
DISPLAY_NAME
CONTENT_URI

ContactsContract.CommonDataKinds.Phone
CONTENT_ITEM_TYPE
NUMBER

ContactsContract.PhoneLookup
CONTENT_FILTER_URI

ContactsContract.Intents
SHOW_OR_CREATE_CONTACT

ContactsContract.Intents.Insert
COMPANY
POSTAL

ContactsContract.CommonDataKinds.Phone.CONTENT_URI # URI
ContactsContract.CommonDataKinds.Phone.NUMBER # String 手机号
ContactsContract.PhoneLookup.DISPLAY_NAME # String 姓名


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

```

## MediaStore

```
MediaStore.Images.Media.DATA,
                MediaStore.Images.Media.DISPLAY_NAME,
                MediaStore.Images.Media.DATE_ADDED,
                MediaStore.Images.Media._ID


MediaStore.Audio.AudioColumns
ALBUM string 缩略图
TITLE string 标题

MediaStore.Audio.Media
EXTERNAL_CONTENT_URI


ContentValues values = new ContentValues();
values.put(MediaStore.Images.Media.TITLE, "");
values.put(MediaStore.Images.Media.DISPLAY_NAME, "name.jpeg");
values.put(MediaStore.Images.Media.MIME_TYPE, "image/jpeg");
// 创建一条图片uri,用于保存拍照后的照片
Uri uri = context.getContentResolver().insert(MediaStore.Images.Media.EXTERNAL_CONTENT_URI, values);

// MediaStore.Images.Media.INTERNAL_CONTENT_URI
// MediaStore.Images.Thumbnails.EXTERNAL_CONTENT_URI
Uri imageUri = MediaStore.Images.Media.EXTERNAL_CONTENT_URI;
ContentResolver mContentResolver = context.getContentResolver();
Cursor cursor = mContentResolver.query(imageUri, null,MediaStore.Images.Media.MIME_TYPE + "=? or " + MediaStore.Images.Media.MIME_TYPE + "=?",new String[] { "image/jpeg", "image/png" }, MediaStore.Images.Media.DATE_MODIFIED);
String path = cursor.getString(cursor.getColumnIndex(MediaStore.Images.Media.DATA));

```

## Settings

```

```

## CallLog

```
Uri: CallLog.Calls.CONTENT_URI 通话记录 Manifest.permission.READ_CALL_LOG
CallLog.Calls.NUMBER
CallLog.Calls.DATE
CallLog.Calls.TYPE
CallLog.Calls.DURATION

CallLog.Calls.CONTENT_URI # 查询通话记录的URI
CallLog.Calls.CACHED_NAME # String 姓名：通话记录的联系人
CallLog.Calls.NUMBER # String 号码：通话记录的电话号码
CallLog.Calls.TYPE # Int 通话类型：1.呼入; 2.呼出; 3.未接
CallLog.Calls.DATE # Long 通话时间 拨打时间：通话记录的日期
CallLog.Calls.DURATION # Int 通话时长 值为多少秒
CallLog.Calls.DEFAULT_SORT_ORDER # 按照时间逆序排列，最近打的最先显示
```

## sms

```
content://sms/
	_id # Int
	thread_id # Int
	address # String
	person # String
	date # Long
	protocol # Int
	read # Int
	status # Int
	type # Int
	body # String
	service_center # String
ContentResolver
	query # selection "date > '" + uploadTime + "'" sortOrder date desc
```

## Browser

```
content://browser/bookmarks ndroid.provider.Browser.BOOKMARKS_URI:
title Browser.BookmarkColumns.TITLE
url Browser.BookmarkColumns.URL
Intent intent = new Intent();
    intent.addFlags(Intents.FLAG_NEW_DOC);
    intent.putExtra("title", titleURL[0]); // Browser.BookmarkColumns.TITLE
    intent.putExtra("url", titleURL[1]); // Browser.BookmarkColumns.URL
    setResult(RESULT_OK, intent);
```

## DocumentsContract

```
public static final String GOOGLE_PHOTOS_URI = "com.google.android.apps.photos.content";
public static final String MEDIA_DOCUMENT_URI = "com.android.providers.media.documents";
public static final String DOWNLOADS_DOCUMENT_URI = "com.android.providers.downloads.documents";
public static final String EXTERNALSTORAGE_DOCUMENT_URI = "com.android.externalstorage.documents";

// 根据Uri获取图片绝对路径，解决Android4.4以上版本Uri转换
@TargetApi(Build.VERSION_CODES.KITKAT)
public static String getImageAbsolutePath19(Context context, Uri imageUri) {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT && DocumentsContract.isDocumentUri(context, imageUri)) {
        if (EXTERNALSTORAGE_DOCUMENT_URI.equals(imageUri.getAuthority())) {
            String docId = DocumentsContract.getDocumentId(imageUri);
            String[] split = docId.split(":"); // 0 type 1 path
            String type = split[0];
            if ("primary".equalsIgnoreCase(type)) {
                return Environment.getExternalStorageDirectory() + "/" + split[1];
            }
        } else if (DOWNLOADS_DOCUMENT_URI.equals(imageUri.getAuthority())) {
            String id = DocumentsContract.getDocumentId(imageUri);
            Uri contentUri = ContentUris.withAppendedId(Uri.parse("content://downloads/public_downloads"), Long.valueOf(id));
            return getDataColumn(context, contentUri, null, null);
        } else if (MEDIA_DOCUMENT_URI.equals(imageUri.getAuthority())) {
            String docId = DocumentsContract.getDocumentId(imageUri);
            String[] split = docId.split(":");
            String type = split[0];
            Uri contentUri = null;
            if ("image".equals(type)) {
                contentUri = MediaStore.Images.Media.EXTERNAL_CONTENT_URI;
            } else if ("video".equals(type)) {
                contentUri = MediaStore.Video.Media.EXTERNAL_CONTENT_URI;
            } else if ("audio".equals(type)) {
                contentUri = MediaStore.Audio.Media.EXTERNAL_CONTENT_URI;
            }
            String selection = MediaStore.Images.Media._ID + "=?";
            String[] selectionArgs = new String[] { split[1] };
            return getDataColumn(context, contentUri, selection, selectionArgs);
        }
    }
    // MediaStore (and general)
    if ("content".equalsIgnoreCase(imageUri.getScheme())) {
        // Return the remote address
        if (GOOGLE_PHOTOS_URI.equals(imageUri.getAuthority()))
            return imageUri.getLastPathSegment();
        return getDataColumn(context, imageUri, null, null);
    }
    // File
    else if ("file".equalsIgnoreCase(imageUri.getScheme())) {
        return imageUri.getPath();
    }
    return null;
}

private static String getDataColumn(Context context, Uri uri, String selection, String[] selectionArgs) {
    Cursor cursor = null;
    String column = MediaStore.Images.Media.DATA;
    String[] projection = { column };
    try {
        cursor = context.getContentResolver().query(uri, projection, selection, selectionArgs, null);
        if (cursor != null && cursor.moveToFirst()) {
            int index = cursor.getColumnIndexOrThrow(column);
            return cursor.getString(index);
        }
    } finally {
        if (cursor != null)
            cursor.close();
    }
    return null;
}


public static String getPath(final Context context, final Uri uri) {

        final boolean isKitKat = Build.VERSION.SDK_INT >= Build.VERSION_CODES.;

        // DocumentProvider
        if (isKitKat && DocumentsContract.isDocumentUri(context, uri)) {
            // ExternalStorageProvider
            if (isExternalStorageDocument(uri)) {
                final String docId = DocumentsContract.getDocumentId(uri);
                final String[] split = docId.split(":");
                final String type = split[0];

                if ("primary".equalsIgnoreCase(type)) {
                    return Environment.getExternalStorageDirectory() + "/" + split[1];
                }

                // TODO handle non-primary volumes
            }
            // DownloadsProvider
            else if (isDownloadsDocument(uri)) {
                final String id = DocumentsContract.getDocumentId(uri);
                final Uri contentUri = ContentUris.withAppendedId(
                        Uri.parse("content://downloads/public_downloads"), Long.valueOf(id));

                return getDataColumn(context, contentUri, null, null);
            }
            // MediaProvider
            else if (isMediaDocument(uri)) {
                final String docId = DocumentsContract.getDocumentId(uri);
                final String[] split = docId.split(":");
                final String type = split[0];

                Uri contentUri = null;
                if ("image".equals(type)) {
                    contentUri = MediaStore.Images.Media.EXTERNAL_CONTENT_URI;
                } else if ("video".equals(type)) {
                    contentUri = MediaStore.Video.Media.EXTERNAL_CONTENT_URI;
                } else if ("audio".equals(type)) {
                    contentUri = MediaStore.Audio.Media.EXTERNAL_CONTENT_URI;
                }

                final String selection = "_id=?";
                final String[] selectionArgs = new String[]{
                        split[1]
                };

                return getDataColumn(context, contentUri, selection, selectionArgs);
            }
        }
        // MediaStore (and general)
        else if ("content".equalsIgnoreCase(uri.getScheme())) {
            return getDataColumn(context, uri, null, null);
        }
        // File
        else if ("file".equalsIgnoreCase(uri.getScheme())) {
            return uri.getPath();
        }

        return null;
    }

    /**
     * Get the value of the data column for this Uri. This is useful for
     * MediaStore Uris, and other file-based ContentProviders.
     *
     * @param context       The context.
     * @param uri           The Uri to query.
     * @param selection     (Optional) Filter used in the query.
     * @param selectionArgs (Optional) Selection arguments used in the query.
     * @return The value of the _data column, which is typically a file path.
     */
    public static String getDataColumn(Context context, Uri uri, String selection,
                                       String[] selectionArgs) {

        Cursor cursor = null;
        final String column = "_data";
        final String[] projection = {
                column
        };

        try {
            cursor = context.getContentResolver().query(uri, projection, selection, selectionArgs,
                    null);
            if (cursor != null && cursor.moveToFirst()) {
                final int column_index = cursor.getColumnIndexOrThrow(column);
                return cursor.getString(column_index);
            }
        } finally {
            if (cursor != null)
                cursor.close();
        }
        return null;
    }


    /**
     * @param uri The Uri to check.
     * @return Whether the Uri authority is ExternalStorageProvider.
     */
    public static boolean isExternalStorageDocument(Uri uri) {
        return "com.android.externalstorage.documents".equals(uri.getAuthority());
    }

    /**
     * @param uri The Uri to check.
     * @return Whether the Uri authority is DownloadsProvider.
     */
    public static boolean isDownloadsDocument(Uri uri) {
        return "com.android.providers.downloads.documents".equals(uri.getAuthority());
    }

    /**
     * @param uri The Uri to check.
     * @return Whether the Uri authority is MediaProvider.
     */
    public static boolean isMediaDocument(Uri uri) {
        return "com.android.providers.media.documents".equals(uri.getAuthority());
    }
```

# Android 系统服务

```
ClipboardManager | 剪切板
ClipData | Item

InputMethodManager | 输入法 INPUT_METHOD_SERVICE
showSoftInput # 显示软键盘 InputMethodManager.SHOW_FORCED View.requestFocus
hideSoftInputFromWindow # 隐藏键盘 (editText.getWindowToken(),0) InputMethodManager.HIDE_NOT_ALWAYS
自定义键盘

PowerManager | 电源管理
WakeLock

ConnectivityManager 连接管理 | NetworkCallback
NetworkInfo | Type

NetworkStatsManager | UsageCallback | NETWORK_STATS_SERVICE

Vibrator 振荡器 | VIBRATOR_SERVICE | 震动模式
android.permission.VIBRATE

AccountManager | 账户管理
Account

AlarmManager 闹钟管理 | ALARM_SERVICE | set RTC_WAKEUP RTC
```



## 包管理

```
PackageManager
    应用名称 getApplicationLabel
    LaunchIntent getLaunchIntentForPackage

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

String packageName = context.getPackageName();
PackageManager packageManager = context.getPackageManager();
List<PackageInfo> packageInfos = packageManager.getInstalledPackages(0);
packageInfos.get(0).packageName;
packageInfos.get(0).versionName;
packageInfos.get(0).versionCode;

// 未安装apk
PackageInfo packageInfo = packageManager.getPackageArchiveInfo("", PackageManager.GET_META_DATA);

FeatureInfo[] featureInfos = packageManager.getSystemAvailableFeatures();
switch (featureInfos[0].name) {
    case PackageManager.FEATURE_CAMERA_FLASH:
}

List<ResolveInfo> resInfoList = packageManager.queryIntentActivities(new Intent(), PackageManager.MATCH_DEFAULT_ONLY);
String packageName = resInfoList.get(0).activityInfo.packageName;
int gids[] = packageManager.getPackageGids("");

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
@android:style/Theme.Translucent.NoTitleBar.Fullscreen

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
<supports-screens
    android:anyDensity="true"
    android:largeScreens="true"
    android:normalScreens="true"
    android:resizeable="true"
    android:smallScreens="true" />
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
@android:style/Theme.Light.NoTitleBar.Fullscreen
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

<uses-feature
    android:name="android.hardware.camera"
    android:required="true"/>
<uses-feature
    android:name="android.hardware.camera.autofocus"
    android:required="true"/>
    <uses-permission android:name="android.permission.CAMERA"/>
    <uses-permission android:name="android.permission.FLASHLIGHT"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
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

## 清单文件

```

```

## WiFi

```
WifiManager
WifiConfiguration
WifiInfo
WifiManager wifiManager = (WifiManager) getSystemService(Context.WIFI_SERVICE);
wifiManager.setWifiEnabled(true); // 禁用启动网卡
wifiManager.removeNetwork(1);
WifiConfiguration wifiConfiguration = new WifiConfiguration();
int network = wifiManager.addNetwork(wifiConfiguration);
wifiManager.enableNetwork(1, true);
wifiManager.saveConfiguration();

switch (wifiManager.getWifiState()) { // 网卡状态
    case WifiManager.WIFI_STATE_DISABLED:
        break;
}

WifiInfo wifiInfo = wifiManager.getConnectionInfo();
int ipAddress = wifiInfo.getIpAddress();
String ip = String.format("%d.%d.%d.%d",
        (ipAddress & 0xff),
        (ipAddress >> 8 & 0xff),
        (ipAddress >> 16 & 0xff),
        (ipAddress >> 24 & 0xff));

Enumeration<NetworkInterface> en = NetworkInterface.getNetworkInterfaces();
while (en.hasMoreElements()) {
    NetworkInterface networkInterface = en.nextElement();
    Enumeration<InetAddress> inetAddressEnumeration = networkInterface.getInetAddresses();
    while (inetAddressEnumeration.hasMoreElements()) {
        InetAddress ip = inetAddressEnumeration.nextElement();
        if (!ip.isLoopbackAddress() && InetAddressUtils.isIPv4Address(ip.getHostAddress())) {
            String hostAddress = ip.getHostAddress();
        }
    }
}

```



## 下载

```
DownloadManager
DownloadManager Context.DOWNLOAD_SERVICE

DownloadManager downloadManager = (DownloadManager) getSystemService(Context.DOWNLOAD_SERVICE);
DownloadManager.Query query = new DownloadManager.Query();
Cursor cursor = downloadManager.query(query);
if (!cursor.moveToFirst()) {
    // "无下载内容"
}
do {
    int status = cursor.getInt(cursor.getColumnIndex(DownloadManager.COLUMN_STATUS));
    String title = cursor.getString(cursor.getColumnIndex(DownloadManager.COLUMN_TITLE));
    if (title.equals("title")) {
        switch (status) {
            case DownloadManager.STATUS_SUCCESSFUL:
                String uri = cursor.getString(cursor.getColumnIndex(DownloadManager.COLUMN_LOCAL_URI));
                // 下载完成
                break;
            case DownloadManager.STATUS_RUNNING:
            case DownloadManager.STATUS_PAUSED:
            case DownloadManager.STATUS_PENDING:
                // 正在下载
                break;
            default:
                // 失败也视为可以再次下载
        }
        break;
    }
} while (cursor.moveToNext());

long enqueueId = 0;
query.setFilterById(enqueueId);
cursor = downloadManager.query(query);
if (cursor.moveToFirst()) {
    int columnIndex = cursor.getColumnIndex(DownloadManager.COLUMN_STATUS);
    if (DownloadManager.STATUS_SUCCESSFUL == cursor.getInt(columnIndex)) {
        String uri = cursor.getString(cursor.getColumnIndex(DownloadManager.COLUMN_LOCAL_URI));
//                return Uri.parse(uri);根据下载队列id获取下载Uri
    }
}

DownloadManager.Request request = new DownloadManager.Request(Uri.parse("parse"));
request.setDestinationInExternalPublicDir(Environment.DIRECTORY_DOWNLOADS, "downloadName");
request.setNotificationVisibility(DownloadManager.Request.VISIBILITY_VISIBLE_NOTIFY_COMPLETED);
request.setMimeType("application/vnd.android.package-archive");
downloadManager.enqueue(request);

DownloadManager.ACTION_DOWNLOAD_COMPLETE action
long enqueueId = intent.getLongExtra(DownloadManager.EXTRA_DOWNLOAD_ID, 0);
Uri uri = DownloadHelperSys.getDownloadUriById(context, enqueueId);

```

## Sms

```
SmsManager
SmsMessage


TelephonyManager
PhoneStateListener
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.READ_CALL_LOG" />

requestPermissions(new String[] {Manifest.permission.READ_PHONE_STATE, Manifest.permission.READ_CALL_LOG}, 100);

// 成员变量
PhoneStateListener phoneStateListener = new PhoneStateListener() {
    @Override
    public void onCallStateChanged(int state, String phoneNumber) {
        switch (state) {
            case TelephonyManager.CALL_STATE_RINGING: // 响铃状态
            case TelephonyManager.CALL_STATE_OFFHOOK: // 接听或拨打状态
            case TelephonyManager.CALL_STATE_IDLE: // 挂断状态
        }
    }
};
TelephonyManager telephonyManager = (TelephonyManager) getSystemService(Context.TELEPHONY_SERVICE);
// 监听通话 LISTEN_CALL_STATE 取消监听 LISTEN_NONE
telephonyManager.listen(phoneStateListener, PhoneStateListener.LISTEN_CALL_STATE);
telephonyManager.getDeviceId(); // 获取手机IMEI(需要“android.permission.READ_PHONE_STATE”权限)

```

## 传感器

```
SensorManager
Sensor
SensorEvent
SensorEventListener

SensorManager
    getSensorList Sensor.TYPE_ALL TYPE_ACCELEROMETER 加速度 重力 陀螺仪 TYPE_LIGHT 光线传感器
    getDefaultSensor 类型默认传感器
    registerListener
    unregisterListener
// 传感器采样率 设置低采样率 省电
SensorManager.SENSOR_DELAY_NORMAL; // 200_000 微妙
SensorManager.SENSOR_DELAY_UI;// 60_000 微妙
SensorManager.SENSOR_DELAY_GAME;// 20_000 微妙
SensorManager.SENSOR_DELAY_FASTEST;// 0微妙

Sensor
    getName 名称
    getVendor 制造商
    getResolution
    getPower 功率
    getType 传感器种类 Sensor.
动作传感器
位置传感器 方向 磁力
环境传感器 温度 压力 亮度

SensorEventListener
    onSensorChanged
    onAccuracyChanged

SensorEvent
    values x y z
    sensor
    timestamp
    accuracy

```

## 蓝牙

```
BluetoothManager
监听蓝牙状态变化 获取蓝牙状态

BluetoothAdapter bluetoothAdapter = BluetoothAdapter.getDefaultAdapter(); // 无蓝牙 null
if (bluetoothAdapter != null) {
    bluetoothAdapter.isDiscovering(); bluetoothAdapter.startDiscovery(); bluetoothAdapter.cancelDiscovery();
    bluetoothAdapter.isEnabled(); bluetoothAdapter.enable(); bluetoothAdapter.disable();// 蓝牙启用
    Set<BluetoothDevice> bondedDevices = bluetoothAdapter.getBondedDevices(); // 已配对的蓝牙适配器
    bondedDevices.iterator().next().getAddress();
    bondedDevices.iterator().next().getAddress();
}

Intent intent = new Intent(BluetoothDevice.ACTION_FOUND);
BluetoothDevice bluetoothDevice = intent.getParcelableExtra(BluetoothDevice.EXTRA_DEVICE);

// 提示longue开启蓝牙 未开启时使用
Intent intent = new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);

// 修改蓝牙设备可见性
Intent intent = new Intent(BluetoothAdapter.ACTION_REQUEST_DISCOVERABLE);
intent.putExtra(BluetoothAdapter.EXTRA_DISCOVERABLE_DURATION, 500); // 可见状态持续时间
    
```

## 通知

```
Android 8.0 NotificationChannel
    NotificationChannel()
        NotificationManager.IMPORTANCE_DEFAULT
    setVibrationPattern

NotificationManager
    createNotificationChannel
    cancel

NotificationCompat.Builder
    setContentTitle
    setContentText
    setContentIntent
    setTicker
    setSmallIcon
    setWhen
    setAutoCancel
    build

PendingIntent
    getActivity
        PendingIntent.FLAG_UPDATE_CURRENT

 * 在Android 8.0之前的设备上:
 * 通知栏通知的声音和震动可以被demo设置中的'声音'和'震动'开关控制
 * 在Android 8.0设备上:
 * 通知栏通知的声音和震动不受demo设置中的'声音'和'震动'开关控制

NotificationManager
Notification
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
        
Context ctx = this;
NotificationManager manager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
Notification.Builder builder = null;
// 此处必须兼容android O设备，否则系统版本在O以上可能不展示通知栏
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
    String channelId = "NotifyDevice";
    String channelName = "NotifyDeviceChannelName";
    NotificationChannel notificationChannel = manager.getNotificationChannel(channelId);
    if (notificationChannel == null) {
		// IMPORTANCE_HIGH IMPORTANCE_DEFAULT
        notificationChannel = new NotificationChannel(channelId, channelName, NotificationManager.IMPORTANCE_DEFAULT);
        manager.createNotificationChannel(notificationChannel);
    }
    String channel = "NotifyDeviceChannel";
    builder = new Notification.Builder(this, channel)
            .setChannelId(channelId);
} else {
    builder = new Notification.Builder(this);
}
builder.setContentTitle("")
        .setContentText("")
        .setTicker("")
        .setWhen(System.currentTimeMillis())
        .setSmallIcon(R.mipmap.ic_launcher)
        .setAutoCancel(true);
Notification notification = builder.getNotification();
Notification notification = builder.build();

NotificationCompat.Builder builder = new NotificationCompat.Builder(ctx, "")
        .setContentTitle("")
        .setSmallIcon(R.mipmap.ic_launcher)
        .setContentText("")
        .setStyle(new NotificationCompat.BigTextStyle().bigText("").setBigContentTitle(""))
        .setContentIntent(PendingIntent.getActivity(ctx, 100, new Intent(), 0))
        .setDeleteIntent(PendingIntent.getActivity(ctx, 100, new Intent(), 0))
        .setWhen(System.currentTimeMillis())
        .setOngoing(false)
        .setChannelId("")
        .setSound(Uri.parse(""))
        .setLargeIcon(BitmapFactory.decodeFile(""))
        .setDefaults(NotificationCompat.DEFAULT_ALL)
        .setPriority(NotificationCompat.PRIORITY_MAX);
notificationManager.notify(1, builder.build())

```



# Android 常用类

```
SystemClock
Build
CountDownTimer 倒计时 | start | cancel
Log 日志 | StackTrace
TextUtils
BuildConfig
Pair
Bundle
Build | VERSION | VERSION_CODES | BOARD厂商 MODEL型号 MANUFACTURER | RELEASE系统版本号
Uri | EMPTY
FileProvider
Process | Pid | Uid | Tid | killProcess
```

# Android 数据存储

```
SharedPreferences | 

SQLiteOpenHelper
SQLiteDatabase | create
Cursor

缓存设计

LruCache

File
Context
Environment

Context
    getCacheDir
    getFilesDir
    getDataDir
    getDatabasePath
    getDir

long maxMemory = Runtime.getRuntime().maxMemory();
int cacheSize = (int) (maxMemory / 8)/1024;
LruCache<String, Bitmap> lruCache = new LruCache<String, Bitmap>(cacheSize) {
    @Override
    protected int sizeOf(String key, Bitmap bitmap) {
        // 重写此方法来衡量每张图片的大小，默认返回图片数量。
        return bitmap.getRowBytes() * bitmap.getHeight() / 1024;
    }
    @Override
    protected void entryRemoved(boolean evicted, String key, Bitmap oldValue, Bitmap newValue) {
        Log.v("tag", "hard cache is full , push to soft cache");
    }
};
Bitmap bitmap = lruCache.get("a");
lruCache.put("a", bitmap);

LruCache

new LruCache<String, Bitmap>((int) (Runtime.getRuntime().() / 8)) {
              @Override
              protected int (String key, Bitmap value) {
            return value.getRowBytes() * value.getHeight();
        }

VERSION_CODES.N
FileProvider.getUriForFile(context, context.getPackageName() + ".fileProvider", file);
```

## StorageManager

```
StorageManager
StorageManager storageManager = (StorageManager) getSystemService(Context.STORAGE_SERVICE);
// getVolumeList
// getVolumePaths
// getVolumeState

// android.os.storage.StorageVolume
// getPathFile
// getDescriptionId
// isPrimary
// isRemovable
// isEmulated
// getStorageId
// allowMassStorage
// getMaxFileSize
// getMtpReserveSpace

```

## ASimpleCache

```
https://github.com/yangfuhai/ASimpleCache
```

## Realm

```
realm-gradle-plugin realm-android
```

## GreenDAO

```
https://github.com/greenrobot/greenDAO

classpath 'org.greenrobot:greendao-gradle-plugin:3.3.0'
plugins {
    id 'org.greenrobot.greendao'
}
implementation 'org.greenrobot:greendao:3.2.2'
implementation 'org.greenrobot:greendao-generator:3.2.2'
greendao {
    schemaVersion 1
    daoPackage 'yes.ican.android.db.greendao.gen'
    targetGenDir 'src/main/java'
    //targetGenDirTest：设置生成单元测试目录
    //generateTests：设置自动生成单元测试用例
//     OrmLite、SugarORM、Active Android、Realm 与 GreenDAO
}

```

## Room

```
androidx.room:room-common:
androidx.room:room-compiler:
androidx.room:room-guava:
androidx.room:room-migration:
androidx.room:room-runtime:
androidx.room:room-rxjava2:
androidx.room:room-testing:
android.arch.persistence.room:common:
android.arch.persistence.room:compiler:
android.arch.persistence.room:guava:
android.arch.persistence.room:migration:
android.arch.persistence.room:runtime:
android.arch.persistence.room:rxjava2:
android.arch.persistence.room:testing:
kapt 'androidx.room:room-compiler:2.2.1'

```

## MMKV

```
https://github.com/Tencent/MMKV

implementation 'com.tencent:mmkv:1.2.11' // 静态链接
implementation 'com.tencent:mmkv-shared:1.2.11' // 动态链接
```

# Android 异步处理

```
异步处理/线程通信

Handler

AsyncTask

HandlerThread

IntentService

JobService

JobParameters
JobInfo.Builder # (jobId, jobService) ComponentName(context.getPackageName(), JobService.class.getName())
	setPeriodic # 执行间隔时间
	setRequiredNetworkType # 执行网络类型 JobInfo.NETWORK_TYPE_NONE
	setMinimumLatency # 任务运行最少延迟时间
	setRequiresCharging # 是否充电时执行
	build # JobInfo 获取服务
JobScheduler # getSystemService Context.JOB_SCHEDULER_SERVICE
	schedule # JobInfo
JobService
	permission="android.permission.BIND_JOB_SERVICE"
	exported="true"

LoaderManager
LoaderManager
    initLoader LoaderCallbacks
        onCreateLoader
        onLoadFinished

if (id == LOADER_ALL) {
                CursorLoader cursorLoader = new CursorLoader(getActivity(),
                        MediaStore.Images.Media.EXTERNAL_CONTENT_URI, IMAGE_PROJECTION,
                        null, null, IMAGE_PROJECTION[2] + " DESC");
                return cursorLoader;
            } else if (id == LOADER_CATEGORY) {
                CursorLoader cursorLoader = new CursorLoader(getActivity(),
                        MediaStore.Images.Media.EXTERNAL_CONTENT_URI, IMAGE_PROJECTION,
                        IMAGE_PROJECTION[0] + " like '%" + args.getString("path") + "%'", null, IMAGE_PROJECTION[2] + " DESC");
                return cursorLoader;
            }

WorkManager
```

# Android IPC

```
Messenger Handler

Binder | Aidl

管道 copy 2 次 一对一
Socket 一对多 不安全 性能低
共享内存 copy 0 n对n 不安全 不能控制访问
File

性能
安全
设计模式

Binder copy 1 cs架构 1对多

内核空间 用户空间
物理地址 虚拟地址
copy_from_user copy_to_user4
程序地址是虚拟地址

alloc_page
MMU 内存管理单元 维护页表 虚拟地址 物理地址映射表
活跃代码  不活跃代码

zygote

app_process
app_main.cpp onZygoteInit
ProcessState self() open_driver mmap 内存映射
/dev/binder

mmap sys/mman.h
开辟物理内存空间
关联文件 读磁盘 4k 8k
在物理内存中对齐 4k整数倍
返回物理地址 mmu转为虚拟地址
activiy传参 mmap 开辟大小限制 1M - 8k

llinux 进程隔离

内核空间 虚拟地址
bid隔离
```

# Android 共享内存

```
MemoryFile | 内存文件
SharedMemory | 共享内存
```

# Android 国际化

```
Locale <-- Cloneable Serializable
    getAvailableLocales // 获取当前系统上的语言列表(Locale列表)
    getDefault
    getLanguage 当前手机系统语言 例如：当前设置的是“中文-中国”，则返回“zh-CN”

```

# Android 类加载

```
ClassLoader
    BaseDexClassLoader
        DexClassLoader
        PathClassLoader
```

# Android 集合

```
ArraySet | ArrayMap
SparseArray | SparseIntArray | SparseLongArray | SparseBooleanArray
```

# Android 注解

```
androidx.annotation:annotation:
com.android.support:support-annotations:23.4.0

Nullness注解
    @Nullable 参数可null
    @NonNull 参数不可null
Resource Type 注解
    @LayoutRes
    @AnimatorRes
    @AnimRes
    @AnyRes 任意资源类型
    @ArrayRes
    @AttrRes
    @BoolRes
    @ColorRes
    @DimenRes
    @DrawableRes
    @FractionRes
    @IdRes
    @IntegerRes
    @InterpolatorRes
    @IntDef
    @LongDef
    @Dimension
    @MenuRes
    @PluralsRes
    @RawRes
    @StringRes
    @StyleableRes
    @StyleRes
    @TransitionRes
    @XmlRes
    @ColorInt
    @ColorLong
Threading 注解
    @UiThread UI线程
    @MainThread 主线程
    @WorkerThread 子线程
    @BinderThread 绑定线程
Typedef 注解
    @IntDef
    @StringDef
Value Constraints注解
    @IntRange
    @FloatRange
    @Size

    集合不能为空: @Size(min=1)
    字符串最大只能有23个字符: @Size(max=23)
    数组只能有2个元素: @Size(2)
    数组的大小必须是2的倍数 (例如图形API中获取位置的x/y坐标数组: @Size(multiple=2)
Permissions 注解
    @RequiresPermission
    @RequiresPermission(Manifest.permission.SET_WALLPAPER)
    @RequiresPermission(anyOf = {
    Manifest.permission.ACCESS_COARSE_LOCATION,
    Manifest.permission.ACCESS_FINE_LOCATION}) // 至少需要权限集合中的一个
    @RequiresPermission(allOf = {
    Manifest.permission.READ_HISTORY_BOOKMARKS,
    Manifest.permission.WRITE_HISTORY_BOOKMARKS}) // 如果你同时需要多个权限

    对于intents的权限 直接在定义的intent常量字符串字段上标注权限需求
    @RequiresPermission(android.Manifest.permission.BLUETOOTH)
public static final String ACTION_REQUEST_DISCOVERABLE =
            "android.bluetooth.adapter.action.REQUEST_DISCOVERABLE";

            对于content providers的权限，你可能需要单独的标注读和写的权限访问，所以可以用@Read或者@Write标注每一个权限需求
            @RequiresPermission.Read(@RequiresPermission(READ_HISTORY_BOOKMARKS))
@RequiresPermission.Write(@RequiresPermission(WRITE_HISTORY_BOOKMARKS))
public static final Uri BOOKMARKS_URI = Uri.parse("content://browser/bookmarks");

Overriding Methods 注解
    @CallSuper
Return Values注解
    @CheckResult
    如果你的方法返回一个值，你期望调用者用这个值做些事情，那么你可以使用@CheckResult注解标注这个方法。
 这个在具体使用中用的比较少，除非特殊情况，比如在项目中对一个数据进行处理，这个处理比较耗时，我们希望调用该函数的调用者在不需要处理结果的时候，提示没有使用，酌情删除调用。
Keep：指出一个方法在被混淆的时候应该被保留。
   VisibleForTesting：可注解一个类，方法，或变量，表示有更宽松的可见性，这样它能够有更宽泛的可见性，使代码可以被测试。
Support Annotations中的注解的生命周期全部是RetentionPolicy.CLASS

IntelliJ注解

    IntelliJ，Android Studio就是基于它开发的，IntelliJ有一套它自己的注解；IntDef分析其实重用的是MagicConstant分析的代码，IntelliJ null分析其实用的是一组配置好的null注解。如果你执行Analyze > Infer Nullity…，它会试图找出所有的null约束并添加他们。这个检查有时会插入IntelliJ注解。你可以通过搜索,替换为Android注解库的注解，或者你也可以直接用IntelliJ注解。在build.gradle里或者通过Project Structure对话框的Dependencies面板都可以添加如下依赖
compile 'com.intellij:annotations:12.0'

经过查阅资料，系统了学习了Support Annotations注解，学以致用，通过这个Support Annotations可以提高代码可读性，同时可以在类加载时就可以检查一些错误，同时不会对性能有任何影响，因为Support Annotations中的注解的生命周期全部是RetentionPolicy.CLASS。接下来准备在项目中大量推广使用。
```

# Android 网络

```
Proxy
    getDefaultHost
    getDefaultPort

HttpClient
implementation 'commons-httpclient:commons-httpclient:3.1'
implementation 'org.apache.httpcomponents:httpcore:4.3.3'
implementation 'org.apache.httpcomponents:httpmime:4.3.6'

// formFile.getInputStream();
NameValuePair nameValuePair = new BasicNameValuePair("", "");
HttpEntity entity = new UrlEncodedFormEntity(new ArrayList<NameValuePair>() {{
    add(nameValuePair);
}});
HttpGet httpGet = new HttpGet();
HttpPost httpPost = new HttpPost();
httpPost.setEntity(entity);
HttpClient httpClient = new DefaultHttpClient();
HttpResponse httpResponse = httpClient.execute(httpGet);
HttpEntity httpEntity = httpResponse.getEntity();
InputStream inputStream = httpEntity.getContent();
httpEntity.getContentType();
httpEntity.getContentLength();
httpEntity.getContentEncoding();


AbstractHttpClient
    DefaultHttpClient

HttpClient
    AbstractHttpClient

HttpClient
    execute

AbstractHttpMessage
    BasicHttpRequest
        BasicHttpEntityEnclosingRequest
    BasicHttpResponse
    RequestWrapper
        EntityEnclosingRequestWrapper
    HttpRequestBase
        HttpDelete
        HttpEntityEnclosingRequestBase
            HttpPost
            HttpPut
        HttpGet
        HttpHead
        HttpOptions
        HttpTrace

HttpMessage
    HttpRequest
        HttpEntityEnclosingRequest
        HttpUriRequest
    HttpResponse

HttpRequest
    BasicHttpRequest

HttpEntityEnclosingRequest
    BasicHttpEntityEnclosingRequest
    EntityEnclosingRequestWrapper
    HttpEntityEnclosingRequestBase

HttpUriRequest
    RequestWrapper

HttpResponse
    BasicHttpResponse

HttpUriRequest
AbortableHttpRequest
Cloneable
    HttpRequestBase

HttpResponse
    setStatusLine
    getStatusLine
    setEntity
    getEntity

HttpEntityWrapper
    BufferedHttpEntity
    BasicManagedEntity
AbstractHttpEntity
    BasicHttpEntity
    ByteArrayEntity
    EntityTemplate
    FileEntity
    InputStreamEntity
    MultipartEntity
    SerializableEntity
    StringEntity
        UrlEncodedFormEntity

HttpEntity
    AbstractHttpEntity
    HttpEntityWrapper

ConnectionReleaseTrigger
EofSensorWatcher
    BasicManagedEntity

Cloneable
    ByteArrayEntity
    FileEntity
    StringEntity

HttpEntityEnclosingRequestBase
    setEntity
    getEntity

HttpMessage
    addHeader
    setHeader

HttpEntity
    getContent

BasicNameValuePair

Cloneable
NameValuePair
    BasicNameValuePair

BasicNameValuePair
    getName
    getValue

```

## AsyncHttpClient

```
https://github.com/AsyncHttpClient/async-http-client

RequestParams
    addBodyParameter
HttpRequest.HttpMethod.POST

RequestCallBack
    onSuccess
    onFailure

```

# Android LBS

```
LocationManager
Geocoder
Geocoder geocoder = new Geocoder(context);
List<Address> addressList = geocoder.getFromLocation(40.714, -73.961, 1);

LocationManager locationManager = (LocationManager) context.getSystemService(Context.LOCATION_SERVICE);
if (ActivityCompat.checkSelfPermission(context, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED
        && ActivityCompat.checkSelfPermission(context, Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
}
locationManager.getAllProviders();

Criteria criteria = new Criteria(); // 设置查询条件 查询Location Provider
criteria.setAccuracy(Criteria.ACCURACY_FINE);
criteria.setPowerRequirement(Criteria.POWER_LOW);
criteria.setAltitudeRequired(false);
criteria.setSpeedRequired(false);
criteria.setCostAllowed(false);
locationManager.getBestProvider(criteria, false);

locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, 5000, 5000, new LocationListener() {
    @Override
    public void onLocationChanged(Location location) { }
    @Override
    public void onStatusChanged(String provider, int status, Bundle extras) { }
    @Override
    public void onProviderEnabled(String provider) { }
    @Override
    public void onProviderDisabled(String provider) { }
});

http://maps.googleapis.com/maps/api/geocode/json?
    address=sdd
    bounds=34.34,-118|34.23,-118.23
    sensor=false
    latlng=40.12,-73.we
    region=es

```

## 高德地图

```

```

## 百度地图

```

```

# Android 即时通讯

## 环信

```
https://raw.githubusercontent.com/HyphenateInc/Hyphenate-SDK-Android/master/repository | com.hyphenate:hyphenate-sdk:3.3.0

```

```

```

# Android 推送

## 个推

```
implementation 'cn.jiguang.sdk:jpush:3.3.2'
implementation 'cn.jiguang.sdk:jcore:2.0.1'
```



# Android Json

```
JsonReader
JsonWriter
```



# Android 路由

## ARouter

```
ARouter

源码解析
    初始化流程
    navigation 流程

https://github.com/alibaba/ARouter

android {
    defaultConfig {
        javaCompileOptions {
            annotationProcessorOptions {
                arguments = [AROUTER_MODULE_NAME: project.getName()]
            }
        }
    }
}
implementation 'com.alibaba:arouter-api:1.5.2'
annotationProcessor 'com.alibaba:arouter-compiler:1.5.2'

api compiler | AROUTER_MODULE_NAME javaCompile annotationProcessor arguments kapt arguments arg

ARouter # init inject | build withString navigation
RouteType # id className | ACTIVITY SERVICE BOARDCAST CONTENT_PROVIDER FRAGMENT PROVIDER METHOD UNKNOWN
RouteMeta
	Postcard # withObject navigation
IProvider # init
	InterceptorService # doInterceptions
@Route # RoutePath
@Autowired # 自动装配


<activity android:name="action.heart.arouter.ARouterActivity">
            <intent-filter>
                <data
                    android:host="m.aliyun.com"
                    android:scheme="arouter"/>
                <action android:name="android.intent.action.VIEW" />

                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />

            </intent-filter>
        </activity>




```

## DeepLinkDispatch

```
https://github.com/airbnb/DeepLinkDispatch
```

# Android 分享

## 友盟

```
Umeng # https://dl.bintray.com/umsdk/release | common analytics utdid push analytics | latest.integration
implementation 'com.umeng.sdk:common:1.5.0'
implementation 'com.umeng.sdk:analytics:7.5.0'
implementation 'com.umeng.sdk:share-core:latest.integration'
implementation 'com.umeng.sdk:share-qq:latest.integration'
implementation 'com.umeng.sdk:share-sina:latest.integration'
implementation 'com.umeng.sdk:share-wechat:latest.integration'

public static final String APP_KEY = "621ccb2e317aa877606c0c38";
public static final String CHANNEL = "NotifyApp";
public static final String MESSAGE_SECRET = "92296cb1234f0c0ce685383b5408f696";

UMConfigure.setLogEnabled(true); // 日志开关

PushAgent.setup(this, APP_KEY, MESSAGE_SECRET); // 预初始化
UMConfigure.preInit(this, APP_KEY, CHANNEL);
UMConfigure.init(this, APP_KEY, CHANNEL, UMConfigure.DEVICE_TYPE_PHONE, MESSAGE_SECRET);

boolean isMainProcess = UMUtils.isMainProgress(this);
if (isMainProcess) {
    //启动优化：建议在子线程中执行初始化
    new Thread(new Runnable() {
        @Override
        public void run() {
            initUmengSDK();
        }
    }).start();
} else {
    //若不是主进程（":channel"结尾的进程），直接初始化sdk，不可在子线程中执行
    initUmengSDK();
}

private void initUmengSDK() { // 初始化友盟SDK
    //获取推送实例
    PushAgent pushAgent = PushAgent.getInstance(this);
    pushAgent.setNotificationOnForeground(true);
    pushAgent.setNotificationPlaySound(MsgConstant.NOTIFICATION_PLAY_SDK_ENABLE);
    pushAgent.setNotificationPlayLights(MsgConstant.NOTIFICATION_PLAY_SDK_ENABLE);
    pushAgent.setNotificationPlayVibrate(MsgConstant.NOTIFICATION_PLAY_SDK_ENABLE);
    //TODO:需修改为您app/src/main/AndroidManifest.xml中package值
    pushAgent.setResourcePackageName("notify.app");
    //设置通知栏显示通知的最大个数（0～10），0：不限制个数
    pushAgent.setDisplayNotificationNumber(3);
    pushAgent.setMessageHandler(new UmengMessageHandler() {
        @Override
        public void dealWithNotificationMessage(Context context, UMessage uMessage) {
            Vibrator vibrator = (Vibrator) getSystemService(VIBRATOR_SERVICE);
            AudioAttributes audioAttributes = new AudioAttributes.Builder()
                    .setUsage(AudioAttributes.USAGE_NOTIFICATION)
                    .build();
            vibrator.vibrate(500, audioAttributes);
            super.dealWithNotificationMessage(context, uMessage);
        }
    });
    //注册推送服务，每次调用register方法都会回调该接口
    pushAgent.register(new UPushRegisterCallback() {
        @Override
        public void onSuccess(String deviceToken) {
            //注册成功会返回deviceToken deviceToken是推送消息的唯一标志
            Log.i(TAG, "deviceToken --> " + deviceToken);
            String alias = "123456";
            String type = "aa";
            PushAgent.getInstance(MainApp.this).setAlias(alias, type, new UPushAliasCallback() {
                @Override
                public void onMessage(boolean success, String message) {
                    Log.i(TAG, "setAlias " + success + " msg:" + message);
                }
            });
        }
        @Override
        public void onFailure(String errCode, String errDesc) {
            Log.e(TAG, "register failure：--> " + "code:" + errCode + ",desc:" + errDesc);
        }
    });
}
```

## ShareSDK

```

```

# Android 数据总线

## EventBus

```
https://github.com/greenrobot/EventBus
implementation 'org.greenrobot:eventbus:3.3.1'

EventBus
EventBus # default register post
Subscribe # threadMode priority

LiveEventBus.get(Event.BIBI_REFRESH)
        .observe(this, androidx.lifecycle.Observer { refresh() })
    LiveEventBus.get(Event.BIBI_REFRESH).post(1)
```

# Android 依赖注入

## ButterKnife

```
ButterKnife
Unbinder

@BindView # Int Float Bool String Color Dimen Anim Font Bitmap Array Drawable
@OnClick # LongClick Touch CheckedChanged FocusChange PageChange TextChanged ItemClick ItemLongClick ItemSelected

https://github.com/JakeWharton/butterknife
// 10.2.3 7.0.1 8.8.1
implementation 'com.jakewharton:butterknife:10.2.3'
annotationProcessor 'com.jakewharton:butterknife-compiler:10.2.3'

Unbinder unbinder = ButterKnife.bind(this, new View(this));
unbinder.unbind();

```

## Dagger

```
https://github.com/square/dagger
```

# 

# Android 扫码

```
https://github.com/zxing/zxing
https://github.com/yipianfengye/android-zxingLibrary
https://github.com/devilsen/CZXing
api 'com.google.zxing:android-core:3.3.0'
api 'com.google.zxing:core:3.4.0'
```

# Android 单元测试

```

```

# Android 代码混淆

```
-optimizationpasses 5 #指定代码的压缩级别
-dontusemixedcaseclassnames #包明不混合大小写
-dontskipnonpubliclibraryclasses #不去忽略非公共的库类
-dontoptimize #优化 不优化输入的类文件
-dontpreverify #预校验
-verbose #混淆时是否记录日志
-optimizations !code/simplification/arithmetic,!field/*,!class/merging/* #混淆时所采用的算法
-keepattributes *Annotation* #保护注解
-ignorewarning #忽略警告

#-keepattributes SourceFile,LineNumberTable
#-renamesourcefileattribute SourceFile

-keep class **$$ViewInjector { *; }

-keepclasseswithmembernames class * {
    @butterknife.* <fields>;
}
-keepclasseswithmembernames class * {
    @butterknife.* <methods>;
}

#EventBus不被混淆

-keepclassmembers class ** {
    public void onEvent*(**);
}

-keep public class * implements com.bumptech.glide.module.GlideModule
-keep public enum com.bumptech.glide.load.resource.bitmap.ImageHeaderParser$** {
  **[] $VALUES;
  public *;
}

 #友盟相关混淆
-dontshrink
-dontwarn com.google.android.maps.**
-dontwarn android.webkit.WebView
-keep enum com.facebook.**
-keepattributes Exceptions,InnerClasses,Signature
-keepattributes SourceFile,LineNumberTable

-keep public interface com.facebook.**

-keep class com.umeng.** {*;}
-keepclassmembers class * {
   public <init> (org.json.JSONObject);
}
-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}
-keep public class com.lattu.zhonghuei.R$*{
public static final int *;
}

-keep class com.tencent.mm.sdk.modelmsg.** implements   com.tencent.mm.sdk.modelmsg.WXMediaMessage$IMediaObject {*;}
-keep class im.yixin.sdk.api.** implements im.yixin.sdk.api.YXMessage$YXMessageData{*;}
-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
    }

-keepnames class * implements android.os.Parcelable {
    public static final ** CREATOR;
    }
-keepattributes Signature
-keep public class * extends android.app.Activity
-keep public class * extends android.support.v4.**
-keep interface android.support.v4.app.** { *; }
-dontwarn android.support.**

-keep class * extends java.lang.annotation.Annotation {*;}
-keepnames class * implements java.io.Serializable
-keepclassmembers class * implements java.io.Serializable {
     static final long serialVersionUID;
     private static final java.io.ObjectStreamField[] serialPersistentFields;
     private void writeObject(java.io.ObjectOutputStream);
     private void readObject(java.io.ObjectInputStream);
     java.lang.Object writeReplace();
     java.lang.Object readResolve();
}

-keepclassmembers enum * {
   public static **[] values();
   public static ** valueOf(java.lang.String);
}

 #自定义组件不被混淆
-keep public class * extends android.view.View {
     public <init>(android.content.Context);
     public void set*(...);
}

#不混淆资源类
-keepclassmembers class **.R$* {
     public static <fields>;
}

#ButterKnife 混淆配置
-keep class butterknife.** { *; }
-dontwarn butterknife.internal.**
-keep class **$$ViewBindViewer { *; }

-keepclasseswithmembernames class * {
    @butterknife.* <fields>;
}

-keepclasseswithmembernames class * {
    @butterknife.* <methods>;
}

-keep public class **.R$*{
   public static final int *;
}

#（可选）避免Log打印输出
-assumenosideeffects class android.util.Log {
   public static *** v(...);
   public static *** d(...);
   public static *** i(...);
   public static *** w(...);
 }

-dontwarn dalvik.**
-dontwarn com.tencent.smtt.**
#-overloadaggressively
# ------------------ Keep LineNumbers and properties ---------------- #
-keepattributes Exceptions,InnerClasses,Signature,Deprecated,SourceFile,LineNumberTable,*Annotation*,EnclosingMethod
-renamesourcefileattribute TbsSdkJava
-keepattributes SourceFile,LineNumberTable


-keepattributes InnerClasses
-keepattributes *Annotation*

类的全限定名称 内部类 $

-keep <type> <name> { <member>; }
 # type enum class [public class]
 # name className <name*...> package.** className$**
 # member *; <fields>; <methods>; public protected *; public <fields>; public <methods>; public *;
	public <type> <name>(); public static final <fields>;


-keepclassmembers <type> <name> <link> <superType> {
	<member>;
}
 # type class
 # name *[继承或实现] **[不继承] className *<namepart>*<namepart>*
 # link extends
 # superType className
 # member <init>(type...); @Annotation <methods>; <type> <name>;
	@Annotation public *;
	public void *(***);


#-keepclassmembers class fqcn.of.javascript.interface.for.webview {
#   public *;
#}

# Uncomment this to preserve the line number information for
# debugging stack traces.
#-keepattributes SourceFile,LineNumberTable

# If you keep the line number information, uncomment this to
# hide the original source file name.
#-renamesourcefileattribute SourceFile

#-optimizationpasses 7
#-optimizations !code/simplification/arithmetic,!field/*,!class/merging/*
-dontoptimize
-dontusemixedcaseclassnames
-verbose
-dontskipnonpubliclibraryclasses
-dontskipnonpubliclibraryclassmembers 
-dontwarn dalvik.**
-dontwarn com.tencent.smtt.**
#-overloadaggressively

#@proguard_debug_start
# ------------------ Keep LineNumbers and properties ---------------- #
-keepattributes Exceptions,InnerClasses,Signature,Deprecated,SourceFile,LineNumberTable,*Annotation*,EnclosingMethod
-renamesourcefileattribute TbsSdkJava
-keepattributes SourceFile,LineNumberTable
#@proguard_debug_end

-keep class com.tencent.smtt.export.external.**{
    *;
}

-keep class com.tencent.tbs.video.interfaces.IUserStateChangedListener {
	*;
}

-keep public class com.tencent.smtt.sdk.WebView {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.WebView$HitTestResult {
	public static final <fields>;
	public java.lang.String getExtra();
	public int getType();
}

-keep public class com.tencent.smtt.sdk.WebView$WebViewTransport {
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.WebView$PictureListener {
	public <fields>;
	public <methods>;
}


-keepattributes InnerClasses

-keep public enum com.tencent.smtt.sdk.WebSettings$** {
    *;
}

-keep public enum com.tencent.smtt.sdk.QbSdk$** {
    *;
}

-keep public class com.tencent.smtt.sdk.WebSettings {
    public *;
}


-keepattributes Signature
-keep public class com.tencent.smtt.sdk.ValueCallback {
	public <fields>;
	public <methods>;
}

-keep class com.tencent.smtt.sdk.SystemWebChromeClient{
	public *;
}
# 1. extension interfaces should be apparent
-keep public class com.tencent.smtt.export.external.extension.interfaces.* {
	public protected *;
}

# 2. interfaces should be apparent
-keep public class com.tencent.smtt.export.external.interfaces.* {
	public protected *;
}

-keep public class com.tencent.smtt.sdk.WebViewCallbackClient {
	public protected *;
}

-keep public class com.tencent.smtt.sdk.WebStorage$QuotaUpdater {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.TBSGamePlayerService* {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.utils.Apn {
	public <fields>;
	public <methods>;
}
-keep class com.tencent.smtt.** {
	*;
}
# end


-keep public class com.tencent.smtt.export.external.extension.proxy.ProxyWebViewClientExtension {
	public <fields>;
	public <methods>;
}

-keep class MTT.ThirdAppInfoNew {
	*;
}

-keep public class com.tencent.smtt.gamesdk.* {
	public protected *;
}

-keep public class com.tencent.smtt.sdk.TBSGameBooter {
        public <fields>;
        public <methods>;
}

-keep public class com.tencent.smtt.sdk.TBSGameBaseActivity {
	public protected *;
}

-keep public class com.tencent.smtt.gamesdk.internal.TBSGameServiceClient {
	public *;
}

-keep public class * extends android.app.Activity{
	public <fields>;
	public <methods>;
}

-keep public class * extends android.app.Service

-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}

-keepclasseswithmembers class * {
	public <init>(android.content.Context, android.util.AttributeSet);
}

-keepattributes *Annotation*

-keepclasseswithmembernames class *{
	native <methods>;
}

-keep class * implements android.os.Parcelable {
  public static final android.os.Parcelable$Creator *;
}

#------------------  下方是共性的排除项目         ----------------
# 方法名中含有“JNI”字符的，认定是Java Native Interface方法，自动排除
# 方法名中含有“JRI”字符的，认定是Java Reflection Interface方法，自动排除

-keepclasseswithmembers class * {
    ... *JNI*(...);
}

-keepclasseswithmembernames class * {
	... *JRI*(...);
}

-keep class **JNI* {*;}

-dontwarn **
-optimizationpasses 5
-dontusemixedcaseclassnames
-dontskipnonpubliclibraryclasses
-dontpreverify
-verbose
-optimizations !code/simplification/arithmetic,!field/*,!class/merging/*

-keep public class * extends android.app.Activity
-keep public class com.android.vending.licensing.ILicensingService
-keep class sun.misc.Unsafe { *; }
-keep class **$$ViewBinder { *; }
-dontwarn butterknife.internal.**
-keepclasseswithmembernames class * {
    @butterknife.* <fields>;
}

-keepclasseswithmembernames class * {
    @butterknife.* <methods>;
}
-keepnames class * { @butterknife.Bind *;}
-keepclasseswithmembernames class * {
    native <methods>;
}
-keepclasseswithmembernames class * {
    public <init>(android.content.Context, android.util.AttributeSet);
}
-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}

-keepclassmembers class * extends android.app.Activity {
	public void *(android.view.View);
}

-keep class * implements android.os.Parcelable {
  public static final android.os.Parcelable$Creator *;
}
-keepclassmembers class fqcn.of.javascript.interface.for.webview {
   public *;
}

-keepattributes SourceFile,LineNumberTable
-renamesourcefileattribute SourceFile

-keepattributes Signature

-dontusemixedcaseclassnames
-dontskipnonpubliclibraryclasses
-verbose
-dontwarn

-dontoptimize
-dontpreverify

-keepattributes *Annotation*
-keep public class com.google.vending.licensing.ILicensingService

-keepclasseswithmembernames class * {
    native <methods>;
}

-keepclassmembers public class * extends android.view.View {
   void set*(***);
   *** get*();
}

# We want to keep methods in Activity that could be used in the XML attribute onClick
-keepclassmembers class * extends android.app.Activity {
   public void *(android.view.View);
}

# For enumeration classes, see http://proguard.sourceforge.net/manual/examples.html#enumerations
-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}

-keep class * implements android.os.Parcelable {
  public static final android.os.Parcelable$Creator *;
}

-keepclassmembers class **.R$* {
    public static <fields>;
}

-keep public class * extends com.umeng.**

# bugly
-dontwarn com.tencent.bugly.**
-keep public class com.tencent.bugly.**{*;}

-keep class com.hyphenate.** {*;}
#另外，demo中发送表情的时候使用到反射，需要keep SmileUtils,注意前面的包名，
#不要SmileUtils复制到自己的项目下keep的时候还是写的demo里的包名
-keep class com.lattu.zhonghuei.im.utils.SmileUtils {*;}

#2.0.9后加入语音通话功能，如需使用此功能的api，加入以下keep
-keep class net.java.sip.** {*;}
```



# Android 布局管理

```
ViewGroup <-- ViewParent ViewManager
    FrameLayout
    LinearLayout
        TableLayout
        TableRow
    GridLayout
    AbsoluteLayout
    RelativeLayout

ViewGroup.LayoutParams
    AbsoluteLayout.LayoutParams
    ViewGroup.MarginLayoutParams
        FrameLayout.LayoutParams
        LinearLayout.LayoutParams
            TableLayout.LayoutParams
            TableRow.LayoutParams
        GridLayout.LayoutParams
        RelativeLayout.LayoutParams

ViewGroup
    setClipToPadding android:clipToPadding
    setClipChildren
```

# Android View

```
View <-- Drawable.Callback KeyEvent.Callback AccessibilityEventSource
    AnalogClock
    ViewGroup
        FrameLayout
            TabHost
                FragmentTabHost
        LinearLayout
            RadioGroup
            SearchView
            TabWidget
            ZoomControls
        GridLayout
        AbsoluteLayout
        RelativeLayout
            DialerFilter
            TwoLineListItem
        AdapterView
    TextView
    ImageView
    ProgressBar
    SurfaceView

View
    setId android:id
    getId
    
    getTop
    
    setBackgroundResource
    
    setPadding
    setPaddingRelative
    getPaddingLeft android:paddingLeft
    getPaddingRight android:paddingRight
    getPaddingTop
    getPaddingBottom
    getPaddingStart
    getPaddingEnd
    
    callOnClick
    performClick
    setOnClickListener OnClickListener
        onClick
    performLongClick
    setOnLongClickListener OnLongClickListener
        onLongClick
    setOnKeyListener OnKeyListener
        onKey
    setOnTouchListener OnTouchListener
        onTouch

    requestLayout
    invalidate
    postInvalidate
    
    post
    
    setSelected
    isSelected
    
    requestFocus
    
    measure
    onMeasure
    setMeasuredDimension
    getMeasuredWidth
    getMeasuredHeight
    layout
    onLayout
    getWidth
    getHeight
    
    findViewById
    
    onKeyDown
    
    getSystemUiVisibility
    setSystemUiVisibility
        systemuivisibility |= View.SYSTEM_UI_FLAG
        View.SYSTEM_UI_FLAG_LAYOUT_STABLE
                | View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION
                | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN
                | View.SYSTEM_UI_FLAG_HIDE_NAVIGATION // hide nav bar
                | View.SYSTEM_UI_FLAG_FULLSCREEN // hide status bar
                | View.SYSTEM_UI_FLAG_IMMERSIVE
    setVisibility
        INVISIBLE
        VISIBLE
    getViewTreeObserver
    
    setBackgroundColor
    setLayerType
        View.LAYER_TYPE_SOFTWARE
    getParent
    
View.MeasureSpec
    makeMeasureSpec
        EXACTLY
    getMode
    getSize

ViewCompat
    setOverScrollMode
        OVER_SCROLL_ALWAYS
    getOverScrollMode

ViewGroup
    getChildAt
    removeView

ViewTreeObserver
    addOnPreDrawListener OnPreDrawListener
        onPreDraw
    removeOnPreDrawListener

自定义View: 宽度 高度 相同 SquareView
        setMeasuredDimension(getDefaultSize(0, widthMeasureSpec),
                getDefaultSize(0, heightMeasureSpec));

        int childWidthSize = getMeasuredWidth();
        // 高度和宽度一样
        heightMeasureSpec = widthMeasureSpec = MeasureSpec.makeMeasureSpec(
                childWidthSize, MeasureSpec.EXACTLY);
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);

自定义View
tools:text="Taro"
```



# TextView

```
TextView						<-- OnPreDrawListener
    Chronometer
    TextClock
    DigitalClock
    EditText
        AutoCompleteTextView	<-- FilterListener
            MultiAutoCompleteTextView
    Button
        CompoundButton			<-- Checkable
            CheckBox
            RadioButton
            ToggleButton
            Switch

BaseMovementMethod			<-- MovementMethod
    ScrollingMovementMethod	<-- MovementMethod
        LinkMovementMethod
    ArrowKeyMovementMethod	<-- MovementMethod

TextView
    setText
    getText
    append
    setHint android:hint
    getHint
    setTextSize
    getTextSize
    setTextColor
    getTextColors
    setHintTextColor
    getHintTextColors
    setLinkTextColor android:textColorLink
    getLinkTextColors
    setSingleLine
    isSingleLine
    setTextAppearance android:textAppearance
        ?android:attr/textAppearanceSmall
        ?android:attr/textAppearanceLarge
    setAllCaps
    isAllCaps
    setSelectAllOnFocus android:selectAllOnFocus
    setShowSoftInputOnFocus
    getShowSoftInputOnFocus
    isTextSelectable
    setTextIsSelectable android:textIsSelectable
    setMovementMethod
    addTextChangedListener TextWatcher
        beforeTextChanged
        onTextChanged
        afterTextChanged
    setFilters new InputFilter.LengthFilter(20)
    setInputType
        InputType.TYPE_TEXT_VARIATION_VISIBLE_PASSWORD
        InputType.TYPE_TEXT_VARIATION_PASSWORD | InputType.TYPE_CLASS_TEXT
    setCompoundDrawablesWithIntrinsicBounds android:drawableStart
    setCompoundDrawablesRelativeWithIntrinsicBounds
    setCompoundDrawablePadding android:drawablePadding
    getCompoundDrawablePadding
    setAutoLinkMask android:autoLink
        Linkify.ALL all
        Linkify.WEB_URLS web
        Linkify.EMAIL_ADDRESSES
        Linkify.PHONE_NUMBERS
        Linkify.MAP_ADDRESSES
    getAutoLinkMask
    setGravity android:gravity
        center_vertical
    getGravity

CompoundButton
    setButtonTintList android:buttonTint

AutoCompleteTextView
    自动完成输入个数 setThreshold
    getThreshold
    关闭自动提示 dismissDropDown
    输入文本之后过滤 performFiltering
    用户选择后调用 replaceText

LinkMovementMethod
    getInstance

RadioGroup
    android:checkedButton
    getCheckedRadioButtonId
    setOnCheckedChangeListener OnCheckedChangeListener
        onCheckedChanged

```

## Span

```
Layout
    StaticLayout
    DynamicLayout
    BoringLayout <-- TextUtils.EllipsizeCallback

SpannableStringInternal <-- CharSequence GetChars Spannable
    SpannableString
SpannableStringBuilder <-- CharSequence GetChars Spannable Editable Appendable GraphicsOperations

CharSequence
    GetChars
    Spanned
        Spannable
    Editable <-- GetChars Spannable Appendable

Parcelable
    ParcelableSpan
UpdateAppearance
    UpdateLayout

CharacterStyle
    前景色 ForegroundColorSpan <-- UpdateAppearance ParcelableSpan
    ClickableSpan <-- UpdateAppearance
        URLSpan <-- ParcelableSpan
    MetricAffectingSpan <-- UpdateLayout
        样式 StyleSpan <-- ParcelableSpan
            StyleSpan(Typeface.BOLD)
        AbsoluteSizeSpan <-- ParcelableSpan
        ReplacementSpan
            DynamicDrawableSpan
                ImageSpan
        LocaleSpan <-- ParcelableSpan
        RelativeSizeSpan <-- ParcelableSpan
        ScaleXSpan <-- ParcelableSpan
        SubscriptSpan <-- ParcelableSpan
        SuperscriptSpan <-- ParcelableSpan
        TextAppearanceSpan <-- ParcelableSpan
        TypefaceSpan <-- ParcelableSpan

Layout
    getWidth
    getHeight
    getPaint
    getLineCount
    getLineWidth
Layout.Alignment
    ALIGN_NORMAL

ImageSpan
    ImageSpan(bitmap, DynamicDrawableSpan.ALIGN_BOTTOM)

Spanned
    SPAN_EXCLUSIVE_INCLUSIVE
    getSpans
    getSpanStart
    getSpanEnd
    getSpanFlags
    nextSpanTransition
Spannable
    setSpan
Spannable.Factory
    getInstance
    newSpannable

Html
    fromHtml
        FROM_HTML_MODE_COMPACT
Html.ImageGetter
    getDrawable

Editable
    insert
    delete
    append
    clearSpans
    replace
    setFilters
    getFilters
```

## SuperTextView

```
https://github.com/chenBingX/SuperTextView
https://github.com/lygttpod/SuperTextView
implementation 'com.github.lygttpod:SuperTextView:2.1.7'

```

## EditText

```

```

# ImageView

```
ImageView
    ImageButton
        ZoomButton <-- OnLongClickListener

ImageView
    setScaleType ImageView.ScaleType android:scaleType
        CENTER_CROP
        centerInside
    setImageResource
    setImageDrawable
    setAdjustViewBounds android:adjustViewBounds

```

## CircleImageView

```
https://github.com/hdodenhof/CircleImageView

```

## Universal Image Loader

```
https://github.com/nostra13/Android-Universal-Image-Loader

```

## Glide

```
GlideModule

https://github.com/bumptech/glide
// 4.7.1 4.12.0 3.7.0
implementation 'com.github.bumptech.glide:glide:4.12.0'
annotationProcessor 'com.github.bumptech.glide:compiler:4.12.0'

RequestOptions requestOptions = new RequestOptions()
        .placeholder(R.mipmap.ic_launcher)
        .error(R.mipmap.ic_launcher)
        .override(100, 100)
        .dontAnimate();
Glide.with(context)
        .load("url")
        .apply(requestOptions)
        .into(new ImageView(context));

Glide.with(this)
                .load(Consts.IMAGEURI_1)
                .into(imageView);

Glide.with(this)
                .load(R.drawable.aboutus)
                .into(imageView);

Glide.with(this)
                .load("file:///android_asset/load.jpg")
                .into(imageView);

Glide.with(this)
                .load(Consts.IMAGEURI_1)
                .placeholder(R.drawable.aboutmeicon)//支持resid和Drawable
                .error(R.drawable.aboutus)//支持resid和Drawable
                .crossFade()
                .into(imageView);

Glide.with(this).load(Consts.IMAGEURI_1).into(new GlideDrawableImageViewTarget(imageView){
            @Override
            public void onResourceReady(GlideDrawable resource, GlideAnimation<? super GlideDrawable> animation) {
                super.onResourceReady(resource, animation);
                log();
            }
        });
```

## Picasso

```
https://github.com/square/picasso
implementation 'com.squareup.picasso:picasso:2.71828'
debugImplementation 'com.squareup.leakcanary:leakcanary-android:2.8.1'

Picasso.with(this).load(Consts.IMAGEURI_1).fit().into(imageView);





```

## Fresco

```
ImageView
    DraweeView
        GenericDraweeView
            SimpleDraweeView

https://github.com/facebook/fresco
https://www.fresco-cn.org/
implementation 'com.facebook.fresco:fresco:2.6.0'
implementation 'com.facebook.fresco:imagepipeline-okhttp3:2.6.0'

DiskCacheConfig diskCacheConfig = DiskCacheConfig.newBuilder(context)
        .setBaseDirectoryPath(new File(""))
        .build();
ImagePipelineConfig imagePipelineConfig = OkHttpImagePipelineConfigFactory.newBuilder(context, new OkHttpClient())
        .setDownsampleEnabled(true)
        .setMainDiskCacheConfig(diskCacheConfig)
        .build();
Fresco.initialize(context, imagePipelineConfig);

DraweeView draweeView = new DraweeView(context);
ImageRequestBuilder imageRequestBuilder = ImageRequestBuilder.newBuilderWithSource(Uri.parse("uri"));
imageRequestBuilder.setResizeOptions(new ResizeOptions(100, 100));
ImageRequest imageRequest = imageRequestBuilder.build();
DraweeController draweeController = Fresco.newDraweeControllerBuilder()
        .setOldController(draweeView.getController())
        .setImageRequest(imageRequest).build();
draweeView.setController(draweeController);
draweeView.getHierarchy();

new SimpleDraweeView(context)
        .getHierarchy()
        .setActualImageScaleType(ScalingUtils.ScaleType.CENTER_CROP);
```

# ProgressBar

```
进度条
ProgressBar
<SeekBar
            android:layout_gravity="center"
            android:layout_weight="1"
            android:indeterminateDrawable="@drawable/uvv_star_play_progress_seek"
            android:maxHeight="2dp"
            android:minHeight="2dp"
            android:progressDrawable="@drawable/uvv_star_play_progress_seek"
            android:thumb="@drawable/uvv_seek_dot"
            android:thumbOffset="10dip" />
```

# WebView

```
WebView
WebViewClient
WebChromeClient

AbsoluteLayout
    

WebView
    getSettings
    setScrollBarStyle
    setWebViewClient 
        onPageStarted
        onPageFinished
        onReceivedError
        shouldOverrideUrlLoading
        shouldInterceptRequest
    setWebChromeClient 
        onConsoleMessage
        onJsPrompt
        onJsAlert
            runOnUiThread
            JsResult confirm
        onProgressChanged
        onShowCustomView
        onHideCustomView
        onReceivedTitle
        openFileChooser Android5之前回调
            单个方法都要重写
            intent
            action Intent.ACTION_GET_CONTENT
            Category(Intent.CATEGORY_OPENABLE
            Type("image/*"
            Intent.createChooser(i, "File Chooser")
            startActivityForResult
            ValueCallback<Uri>
                onReceiveValue getdata
        onShowFileChooser return true Android5回调
            Intent.ACTION_GET_CONTENT
            Intent.CATEGORY_OPENABLE
            Type("image/*")
            
            Intent.ACTION_CHOOSER
            Intent.EXTRA_INTENT, contentSelectionIntent
            Intent.EXTRA_TITLE, "Image Chooser"
            startActivityForResult
            ValueCallback<Uri[]>
                onReceiveValue new Uri[]{getdata}
                    new Uri[]{}
    loadUrl
    destroy
    onResume
    onPause
    canGoBack
    goBack
    canGoForward
    goForward

WebSettings
    load
        file:///android_asset/
    setCacheMode
    getCacheMode
    setAllowFileAccess
    getAllowFileAccess
    setDefaultFontSize
    getDefaultFontSize
    setDatabaseEnabled
    getDatabaseEnabled
    setUseWideViewPort
    getUseWideViewPort
    setDomStorageEnabled
    getDomStorageEnabled
    setJavaScriptEnabled
    getJavaScriptEnabled
    setUserAgentString
    getUserAgentString
    setLoadWithOverviewMode
    setSupportZoom
    setBuiltInZoomControls
    setDisplayZoomControls
    setLayoutAlgorithm
        LayoutAlgorithm.SINGLE_COLUMN
    addJavascriptInterface
        @JavascriptInterface

```

# TabHost

```
FrameLayout tabContentView = tabHost.getTabContentView();
LayoutInflater.from(tabActivity).inflate(R.layout.activity_main, tabContentView, true);
TabHost.TabSpec tabSpec = tabHost.newTabSpec("tag")
        .setIndicator("label")
        .setContent(R.id.layout);
tabHost.addTab(tabSpec);
tabHost.setOnTabChangedListener(new TabHost.OnTabChangeListener() {
    @Override
    public void onTabChanged(String tabId) {
        if (tabId.equals("tag")) {
        }
    }
});
```



# ViewAnimator

```
FrameLayout
    ViewAnimator
        ViewFlipper
        ViewSwitcher
            TextSwitcher
            ImageSwitcher

```

# SurfaceView

```
View
    SurfaceView
    TextureView

SurfaceView
    getHolder

SurfaceHolder
    setType
        SURFACE_TYPE_PUSH_BUFFERS
    setFixedSize
    addCallback Callback
        surfaceCreated
        surfaceChanged
        surfaceDestroyed
    setKeepScreenOn
    lockCanvas
    lockHardwareCanvas
    unlockCanvasAndPost

TextureView
    getSurfaceTexture









```

# GLSurfaceView

```
SurfaceView
    GLSurfaceView <-- SurfaceHolder.Callback2

```

# VideoView

```
SurfaceView
    VideoView <-- MediaController.MediaPlayerControl SubtitleController.Anchor
FrameLayout
    MediaController
```

# CardView

```
implementation 'androidx.cardview:cardview:1.0.0'
implementation 'com.android.support:cardview-v7:'

FrameLayout
    CardView

CardView
    setRadius app:cardCornerRadius
    getRadius
    app:cardUseCompatPadding
    app:contentPadding
    app:cardBackgroundColor

```

# Toast

# Material Design

```
implementation 'com.google.android.material:material:1.3.0'
implementation 'com.android.support:design:28.0.0'
implementation 'androidx.coordinatorlayout:coordinatorlayout:1.1.0'
implementation 'com.android.support:coordinatorlayout:'

ExpandableWidget
    ExpandableTransformationWidget

ViewGroup
    CoordinatorLayout <-- NestedScrollingParent2 NestedScrollingParent3
    LinearLayout
        AppBarLayout <-- CoordinatorLayout.AttachedBehavior
    FrameLayout
        CollapsingToolbarLayout
        ScrimInsetsFrameLayout
            NavigationView
        BottomNavigationView
    ImageView
        ImageButton
            VisibilityAwareImageButton
                FloatingActionButton <-- TintableBackgroundView TintableImageSourceView ExpandableTransformationWidget Shapeable CoordinatorLayout.AttachedBehavior

CoordinatorLayout.Behavior
    ViewOffsetBehavior
        HeaderBehavior
            AppBarLayout.BaseBehavior
                AppBarLayout.Behavior

ViewGroup.MarginLayoutParams
    CoordinatorLayout.LayoutParams
    LinearLayout.LayoutParams
        AppBarLayout.LayoutParams
    FrameLayout.LayoutParams
        CollapsingToolbarLayout.LayoutParams

CoordinatorLayout.LayoutParams
    setAnchorId
    getAnchorId
    setBehavior app:layout_behavior
        @string/appbar_scrolling_view_behavior
	getBehavior

CoordinatorLayout.Behavior
	getTag setTag
	onAttachedToLayoutParams onDetachedFromLayoutParams
	onInterceptTouchEvent onTouchEvent
	getScrimColor getScrimOpacity
	onSaveInstanceState onRestoreInstanceState
	onMeasureChild onLayoutChild
	layoutDependsOn
	onDependentViewChanged onDependentViewRemoved
	onNestedScrollAccepted
	onNestedScroll onNestedPreScroll
	onNestedFling onNestedPreFling
	onStartNestedScroll onStopNestedScroll

AppBarLayout
	getTotalScrollRange
	android:theme="@style/AppTheme.AppBarOverlay"

AppBarLayout.LayoutParams
	setScrollFlags
	getScrollFlags
	setScrollInterpolator
	getScrollInterpolator

AppBarLayout.Behavior
	setTopAndBottomOffset

FloatingActionButton
    setOnClickListener
    app:srcCompat="@android:drawable/ic_dialog_email"

NavigationView
    setNavigationItemSelectedListener OnNavigationItemSelectedListener
        onNavigationItemSelected
    getMenu
    inflateMenu

BottomNavigationView
    setOnNavigationItemSelectedListener OnNavigationItemSelectedListener
        onNavigationItemSelected
    setOnNavigationItemReselectedListener OnNavigationItemReselectedListener
        onNavigationItemReselected
    getMenu
    inflateMenu app:menu menu 资源

BaseTransientBottomBar
    Snackbar

Snackbar
    make
        LENGTH_LONG
    setAction
    show

Toolbar
    android:elevation
    android:minHeight
        ?android:attr/actionBarSize
    android:popupTheme
        @android:style/ThemeOverlay.Material.Light
        @style/AppTheme.PopupOverlay
    android:theme
        @android:style/ThemeOverlay.Material.Dark.ActionBar

```



# ViewPager

```
ViewPager
PagerAdapter

自定义View: 禁止滑动切换
```

## UltraViewPager

```
https://github.com/alibaba/UltraViewPager
```

## PagerBottomTabStrip

```
https://github.com/tyzlmjj/PagerBottomTabStrip
implementation 'me.majiajie:pager-bottom-tab-strip:2.4.0'

```

## ViewPagerIndicator

```
https://github.com/JakeWharton/ViewPagerIndicator
```

# ViewPager2

```
ViewPager2

implementation 'androidx.viewpager2:viewpager2:1.0.0'

androidx.viewpager:viewpager:1.0.0
com.android.support:viewpager:

ViewPager
	setPageTransformer # ViewPager.PageTransformer transformPage
	addOnAdapterChangeListener removeOnAdapterChangeListener # ViewPager.OnAdapterChangeListener onAdapterChanged
		
	addOnPageChangeListener removeOnPageChangeListener # ViewPager.OnPageChangeListener
		# onPageScrolled onPageSelected onPageScrollStateChanged
		# ViewPager.SimpleOnPageChangeListener
	getAdapter setAdapter
	getCurrentItem setCurrentItem
	getOffscreenPageLimit setOffscreenPageLimit
	getPageMargin setPageMargin
	setPageMarginDrawable
	onInterceptTouchEvent # false 禁止滑动

class AskBrainPagerAdapter extends PagerAdapter {
    @Override
    public int getCount() { return 0; }
    @Override
    public boolean isViewFromObject(@NonNull View view, @NonNull Object object) { return false; }
    @NonNull
    @Override
    public Object instantiateItem(@NonNull ViewGroup container, int position) { return super.instantiateItem(container, position); }
    @Override
    public void destroyItem(@NonNull ViewGroup container, int position, @NonNull Object object) { super.destroyItem(container, position, object); }
}
class AskBrainFragmentPagerAdapter extends FragmentPagerAdapter {
    public AskBrainFragmentPagerAdapter(@NonNull FragmentManager fm, int behavior) { super(fm, behavior); }
    @NonNull
    @Override
    public Fragment getItem(int position) { return null; }
    @Override
    public int getCount() { return 0; }
    @Nullable
    @Override
    public CharSequence getPageTitle(int position) { return super.getPageTitle(position); }
}
class AskBrainFragmentStatePagerAdapter extends FragmentStatePagerAdapter {
    public AskBrainFragmentStatePagerAdapter(@NonNull FragmentManager fm, int behavior) { super(fm, behavior); }
    @NonNull
    @Override
    public Fragment getItem(int position) { return null; }
    @Override
    public int getCount() { return 0; }
}
ViewPager viewPager = new ViewPager(context);
viewPager.getAdapter(); viewPager.setAdapter(new AskBrainPagerAdapter());
viewPager.getCurrentItem(); viewPager.setCurrentItem(0);
viewPager.getOffscreenPageLimit(); viewPager.setOffscreenPageLimit(1);
viewPager.addOnPageChangeListener(new ViewPager.OnPageChangeListener() {
    @Override
    public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) { }
    @Override
    public void onPageSelected(int position) { }
    @Override
    public void onPageScrollStateChanged(int state) { }
});
viewPager.addOnAdapterChangeListener(new ViewPager.OnAdapterChangeListener() {
    @Override
    public void onAdapterChanged(@NonNull ViewPager viewPager, @Nullable PagerAdapter oldAdapter, @Nullable PagerAdapter newAdapter) { }
});

```



# DrawerLayout

```
implementation 'androidx.drawerlayout:drawerlayout:'
implementation 'com.android.support:drawerlayout:'

DrawerLayout | DrawerListener | SimpleDrawerListener | closeDrawer GravityCompat.START
```



# FlexboxLayout

```
https://github.com/google/flexbox-layout
implementation 'com.google.android.flexbox:flexbox:3.0.0'

```

# 列表

```
AdapterView
    AbsSpinner
        Spinner <-- OnClickListener
        Gallery <-- GestureDetector.OnGestureListener
    AbsListView <-- TextWatcher Filter.FilterListener ViewTreeObserver.OnGlobalLayoutListener ViewTreeObserver.OnTouchModeChangeListener RemoteViewsAdapter.RemoteAdapterConnectionCallback
        ListView
            ExpandableListView
        GridView

Adapter
    ListAdapter
    SpinnerAdapter
        ThemedSpinnerAdapter

BaseAdapter <-- ListAdapter SpinnerAdapter
    ArrayAdapter <-- Filterable ThemedSpinnerAdapter
    SimpleAdapter <-- Filterable ThemedSpinnerAdapter
    CursorAdapter <-- Filterable ThemedSpinnerAdapter CursorFilter.CursorFilterClient
        ResourceCursorAdapter
            SimpleCursorAdapter

AdapterView
    setAdapter
    setOnItemClickListener
    getFirstVisiblePosition
    getLastVisiblePosition

Adapter
    registerDataSetObserver
    unregisterDataSetObserver
    getCount
    getItem
    getItemId
    hasStableIds
    getView
    getItemViewType
    getViewTypeCount
    isEmpty
    getAutofillOptions


AbsListView
    smoothScrollToPosition
    smoothScrollBy
    setSelector android:listSelector
    getSelector
    onMeasure
        int expandSpec = MeasureSpec.makeMeasureSpec(Integer.MAX_VALUE >> 2, MeasureSpec.AT_MOST);
        super.onMeasure(widthMeasureSpec, expandSpec);
    setOnScrollListener OnScrollListener
        onScrollStateChanged
        onScroll
Spinner
    setPrompt

ListView
    setDivider android:divider
        @null
    setDividerHeight
    setSelectionFromTop
    addFooterView

GridView
    setColumnWidth
    getColumnWidth
    setNumColumns android:numColumns
    getNumColumns
    setVerticalSpacing android:verticalSpacing
    getVerticalSpacing
    setHorizontalSpacing
    getHorizontalSpacing
    setGravity android:gravity
    getGravity

View
    setScrollBarStyle android:scrollbars
        none
    getScrollBarStyle
    android:fadingEdge
        none

ArrayAdapter
    createFromResource
    setDropDownViewResource

BaseExpandableListAdapter <-- ExpandableListAdapter HeterogeneousExpandableList
    SimpleExpandableListAdapter 
    CursorTreeAdapter <-- Filterable CursorFilter.CursorFilterClient
        ResourceCursorTreeAdapter
            SimpleCursorTreeAdapter

ExpandableListAdapter
    registerDataSetObserver
    unregisterDataSetObserver
    getGroupCount
    getChildrenCount
    getGroup
    getChild
    getGroupId
    getChildId
    hasStableIds
    getGroupView
    getChildView
    isChildSelectable
    areAllItemsEnabled
    isEmpty
    onGroupExpanded
    onGroupCollapsed
    getCombinedChildId
    getCombinedGroupId

Intents.FLAG_NEW_DOC
market://details?id=packageName
Browser.BookmarkColumns.URL

```

## RecyclerView

```
implementation 'androidx.recyclerview:recyclerview:1.1.0'
implementation 'androidx.recyclerview:recyclerview-selection:1.1.0'

ViewGroup
    RecyclerView <-- ScrollingView NestedScrollingChild2 NestedScrollingChild3

RecyclerView.LayoutManager
	LinearLayoutManager <-- ItemTouchHelper.ViewDropHandler RecyclerView.SmoothScroller.ScrollVectorProvider
		GridLayoutManager
	StaggeredGridLayoutManager <-- RecyclerView.SmoothScroller.ScrollVectorProvider

RecyclerView.ItemAnimator
    SimpleItemAnimator
        DefaultItemAnimator

RecyclerView
    setAdapter
    getAdapter
    setLayoutManager
    getLayoutManager
    addItemDecoration
    setHasFixedSize
    addOnScrollListener
    setOnScrollListener
    setItemAnimator
    addOnItemTouchListener
    tools:itemCount
    tools:listitem layout

RecyclerView.Adapter
    onCreateViewHolder LayoutInflater.from(viewGroup.getContext()).inflate(R.layout.item_chat, viewGroup, false);
    onBindViewHolder
    createViewHolder
    bindViewHolder
    getItemViewType
    setHasStableIds
    getItemId
    getItemCount
    hasStableIds
    onViewRecycled
    onFailedToRecycleView
    onViewAttachedToWindow
    onViewDetachedFromWindow
    hasObservers
    registerAdapterDataObserver
    unregisterAdapterDataObserver
    onAttachedToRecyclerView
    onDetachedFromRecyclerView
    notifyDataSetChanged
    notifyItemChanged
    notifyItemRangeChanged
    notifyItemInserted
    notifyItemMoved
    notifyItemRangeInserted
    notifyItemRemoved
    notifyItemRangeRemoved
    -- OnItemClickListener

RecyclerView.ViewHolder
    getPosition
    getLayoutPosition
    getAdapterPosition
    getItemId
    getOldPosition
    getItemViewType
    isBound
    isRemoved
    isInvalid
    isUpdated
    setFlags
    addFlags
    addChangePayload
    clearPayload

RecyclerView.ItemDecoration
    onDraw
    onDrawOver
    getItemOffsets

RecyclerView.OnItemTouchListener
    RecyclerView.SimpleOnItemTouchListener

RecyclerView.OnItemTouchListener
    onInterceptTouchEvent
    onTouchEvent
    onRequestDisallowInterceptTouchEvent

RecyclerView.OnScrollListener
    onScrolled
    onScrollStateChanged

RecyclerView.ItemAnimator
    getMoveDuration
    setMoveDuration
    getAddDuration
    setAddDuration
    getRemoveDuration
    setRemoveDuration
    getChangeDuration
    setChangeDuration
    setListener
    recordPreLayoutInformation

GridLayoutManager
    setSpanSizeLookup GridLayoutManager.SpanSizeLookup
        getSpanSize
    getSpanSizeLookup
    getSpanCount
    setSpanCount

LinearLayoutManager
    setOrientation
        VERTICAL

RecyclerView.ItemDecoration
    ItemTouchHelper <-- RecyclerView.OnChildAttachStateChangeListener

ItemTouchHelper
    ItemTouchHelper(Callback) ItemTouchHelper.Callback
        getMovementFlags
        onMove
        onSwiped

```

## Paging

```
androidx.paging:paging-common:
androidx.paging:paging-runtime:
androidx.paging:paging-rxjava2:
android.arch.paging:common:
android.arch.paging:runtime:
android.arch.paging:rxjava2:
```

# 下拉刷新

## Ultra Pull To Refresh

```
https://github.com/liaohuqiu/android-Ultra-Pull-To-Refresh
compile 'in.srain.cube:ultra-ptr:1.0.11'
```

## SmartRefreshLayout

```
https://github.com/scwang90/SmartRefreshLayout
implementation 'com.scwang.smartrefresh:SmartRefreshLayout:1.1.0-alpha-11'
implementation 'com.scwang.smartrefresh:SmartRefreshHeader:1.1.0-alpha-11'

 smartRefresh.setOnRefreshListener {
smartRefresh.finishRefresh()
smartRefresh.setOnLoadMoreListener {
 smartRefresh.finishLoadMore()
 
 //static 代码段可以防止内存泄露
    static {
        //设置全局的Header构建器
        SmartRefreshLayout.setDefaultRefreshHeaderCreator(new DefaultRefreshHeaderCreator() {
            @Override
            public RefreshHeader createRefreshHeader(Context context, RefreshLayout layout) {
                layout.setPrimaryColorsId(R.color.main_color, R.color.main_color);//全局设置主题颜色

                MaterialHeader materialHeader = new MaterialHeader(context);

                materialHeader.setColorSchemeResources(R.color.main_color_two,R.color.main_color,R.color.main_color_two);
                return materialHeader;//.setTimeFormat(new DynamicTimeFormat("更新于 %s"));//指定为经典Header，默认是 贝塞尔雷达Header
            }
        });
        //设置全局的Footer构建器
      /*  SmartRefreshLayout.setDefaultRefreshFooterCreator(new DefaultRefreshFooterCreator() {
            @Override
            public RefreshFooter createRefreshFooter(Context context, RefreshLayout layout) {
                //指定为经典Footer，默认是 BallPulseFooter
                return new ClassicsFooter(context).setDrawableSize(20);
            }
        });*/

        Router.initialize(new Configuration.Builder()
                // 调试模式，开启后会打印log
                .setDebuggable(BuildConfig.DEBUG)
                // 模块名(即project.name)，每个使用Router的module都要在这里注册
                .registerModules("app")
                .build());


       // PlatformConfig.setW

    }
```

## MarkMjw PullToRefresh

```
https://github.com/MarkMjw/PullToRefresh
```

## TwinklingRefreshLayout

```
https://github.com/lcodecorex/TwinklingRefreshLayout
```

## Pull To Refresh

```
https://github.com/chrisbanes/Android-PullToRefresh
https://github.com/chrisbanes/Android-PullToRefresh
https://github.com/johannilsson/android-pulltorefresh
https://github.com/baoyongzhang/android-PullRefreshLayout
https://github.com/HomHomLin/Android-PullToRefreshRecyclerView
```

## BeautifulRefreshLayout

```
https://github.com/android-cjj/BeautifulRefreshLayout
```

## BGARefreshLayout

```
https://github.com/bingoogolapple/BGARefreshLayout-Android
```

## XListView

```
https://github.com/Maxwin-z/XListView-Android
```

## BaseRecyclerViewAdapterHelper

```
https://github.com/CymChad/BaseRecyclerViewAdapterHelper
com.github.CymChad:BaseRecyclerViewAdapterHelper:2.9.30'
implementation 'com.github.CymChad:BaseRecyclerViewAdapterHelper:2.9.44'
```

## MultiTypeAdapter

```
https://github.com/LidongWen/MultiTypeAdapter


```



# SwipeRefreshLayout

```
implementation 'androidx.swiperefreshlayout:swiperefreshlayout:1.1.0'

SwipeRefreshLayout
	setOnRefreshListener # SwipeRefreshLayout.OnRefreshListener onRefresh
	isRefreshing setRefreshing
	setOnChildScrollUpCallback # SwipeRefreshLayout.OnChildScrollUpCallback canChildScrollUp
	canChildScrollUp
```

# ConstraintLayout

```
implementation 'androidx.constraintlayout:constraintlayout:2.0.4'
implementation 'androidx.constraintlayout:constraintlayout-solver:2.0.4'
implementation 'com.android.support.constraint:constraint-layout:'
implementation 'com.android.support.constraint:constraint-layout-solver:'

ConstraintLayout
Guideline
Placeholder
Barrier
ConstraintSet
```



# ObservableScrollView

```
https://github.com/ksoichiro/Android-ObservableScrollView
```



# QMUI

```
Android UI 框架
https://qmuiteam.com/android
implementation 'com.qmuiteam:qmui:1.2.0'
implementation 'com.qmuiteam:arch:0.3.1'

QMUIRadiusImageView
```

# WheelView

```
https://github.com/wangjiegulu/WheelView
```

## Android Window

```
WindowManager
Window
Display
DisplayMetrics

WindowManager WINDOW_SERVICE
    getDefaultDisplay

Window getWindow()
    setSoftInputMode WindowManager.LayoutParams.SOFT_INPUT_ADJUST_PAN
    setFlags
        LayoutParams.FLAG_NOT_TOUCH_MODAL window外可以点击,不拦截窗口外的事件
        LayoutParams.FLAG_FULLSCREEN
        LayoutParams.FLAG_TRANSLUCENT_NAVIGATION
    addFlags
    clearFlags
    setGravity Gravity.CENTER
    getAttributes WindowManager.LayoutParams
    setAttributes
    setContentView
    findViewById
    getDecorView

WindowManager.LayoutParams
    width
    height
    alpha

Display
    getWidth
    getWidth

Window # activity.getWindow() dialog.getWindow()
	setFormat # PixelFormat.RGBA_8888
	setSoftInputMode # 
		# WindowManager.LayoutParams.SOFT_INPUT_STATE_HIDDEN
	setStatusBarColor setNavigationBarColor
	getCurrentFocus getDecorView findViewById
	setBackgroundDrawable setBackgroundDrawableResource
	hasFeature requestFeature
	setFeatureDrawable setFeatureDrawableAlpha setFeatureDrawableResource setFeatureDrawableUri
	setFeatureInt
	clearFlags addFlags setFlags
		# WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON 高亮
	setType # 
	FEATURE_NO_TITLE
	FEATURE_ACTION_BAR
	FEATURE_PROGRESS
WindowManager.LayoutParams
	FLAG_FULLSCREEN
	FLAG_DIM_BEHIND
	alpha dimAmount width height packageName
	gravity format flags type token
	buttonBrightness screenBrightness screenOrientation
	horizontalMargin verticalMargin
	horizontalWeight verticalWeight
	systemUiVisibility
	getTitle setTitle
	getColorMode setColorMode
		TYPE_APPLICATION_OVERLAY # O WindowType
		TYPE_SYSTEM_ALERT # WindowType

getSupportedWindowType
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            return WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY;
        } else {
            return WindowManager.LayoutParams.TYPE_SYSTEM_ALERT;
        }
```



# Android 对话框

## Dialog

```
Dialog						<-- DialogInterface Window.Callback KeyEvent.Callback View.OnCreateContextMenuListener
    AlertDialog				<-- DialogInterface
        ProgressDialog
        DatePickerDialog	<-- DialogInterface.OnClickListener DatePicker.OnDateChangedListener
        TimePickerDialog	<-- DialogInterface.OnClickListener TimePicker.OnTimeChangedListener

Dialog
    cancel
    setOnCancelListener DialogInterface.OnCancelListener
        onCancel
    dismiss
    setOnDismissListener DialogInterface.OnDismissListener
        onDismiss
    show
    isShowing
    setOnShowListener DialogInterface.OnShowListener
        onShow
    setOnKeyListener DialogInterface.OnKeyListener
        onKey
    setCancelable
    setCanceledOnTouchOutside
    hide

ProgressDialog
    setTitle
    setMessage
    setIndeterminate
    setCancelable
    setOnCancelListener DialogInterface.OnCancelListener
        onCancel
    show

AlertDialog.Builder
    setIcon
    setTitle
    setMessage
    setPositiveButton DialogInterface.OnClickListener
        onClick
    setNegativeButton
    setNeutralButton
    setCancelable
    create
    show
AlertDialog
    show
    getWindow
```

## Picker

```
FrameLayout
    DatePicker
    TimePicker
LinearLayout
    NumberPicker
```

## Popup

```
弹框

PopupWindow
    setAnimationStyle
    setFocusable
    setContentView
    setBackgroundDrawable
    setOutsideTouchable
    showAsDropDown
    setContentView
    setWidth
    setHeight
    setChangeLight
    isChangeLight
    lightScreen
    setLocation
        Gravity.BOTTOM
    setOnDismissListener OnDismissListener
        onDismiss
    showAtLocation
```

## Material Dialogs

```
https://github.com/afollestad/material-dialogs
https://github.com/afollestad/material-dialogs
compile 'com.afollestad.material-dialogs:core:0.8.5.9'
implementation 'com.afollestad.material-dialogs:core:0.9.6.0'
implementation 'com.afollestad.material-dialogs:commons:0.9.6.0'

com.afollestad.materialdialogs.MaterialDialog;
MaterialDialog dialog = new MaterialDialog.Builder(context)
                .customView(R.layout.bibi_dialog_trade_info_tip, false)
                .autoDismiss(false)
                .cancelable(false)
                .show();
```

## ImagePicker

```
https://github.com/jeasonlzy/ImagePicker
implementation 'com.lzy.widget:imagepicker:0.6.1'

ImagePicker imagePicker = ImagePicker.getInstance();
imagePicker.setImageLoader(new ImageLoader() {
    @Override
    public void displayImage(Activity activity, String path, ImageView imageView, int width, int height) { }
    @Override
    public void displayImagePreview(Activity activity, String path, ImageView imageView, int width, int height) { }
    @Override
    public void clearMemoryCache() { }
});
imagePicker.setImageLoader(null); // 设置图片加载器
imagePicker.setShowCamera(true); // 显示拍照按钮
imagePicker.setCrop(false); // 允许裁剪（单选才有效）
imagePicker.setSaveRectangle(true); // 是否按矩形区域保存
imagePicker.setSelectLimit(70); // 选中数量限制
imagePicker.setStyle(CropImageView.Style.RECTANGLE); // 裁剪框的形状
imagePicker.setFocusWidth(800); // 裁剪框的宽度。单位像素（圆形自动取宽高最小值）
imagePicker.setFocusHeight(800); // 裁剪框的高度。单位像素（圆形自动取宽高最小值）
imagePicker.setOutPutX(1000); // 保存文件的宽度。单位像素
imagePicker.setOutPutY(1000); // 保存文件的高度。单位像素

Intent intent = new Intent(context, ImageGridActivity.class);
intent.putExtra(ImageGridActivity.EXTRAS_TAKE_PICKERS, true); // 是否是直接打开相机
intent.putExtra(ImageGridActivity.EXTRAS_IMAGES,new ArrayList<ImageItem>());
context.startActivityForResult(intent, 100);

Intent intentPreview = new Intent(context, ImagePreviewDelActivity.class);
intentPreview.putExtra(ImagePicker.EXTRA_IMAGE_ITEMS, new ArrayList<ImageItem>());
intentPreview.putExtra(ImagePicker.EXTRA_SELECTED_IMAGE_POSITION, 8);
intentPreview.putExtra(ImagePicker.EXTRA_FROM_ITEMS, true);
activity.startActivityForResult(intentPreview, 200);

```

# Android 菜单

```
Menu

xmlns:app="http://schemas.android.com/apk/res-auto"
<menu>
<item>
	android:id
	android:title
	android:titleCondensed
	android:icon
	android:onClick
	android:actionLayout
	app:showAsAction # always
	app:actionViewClass # android.widget.FrameLayout
	app:actionProviderClass # android.app.MediaRouteActionProvider
	android:alphabeticShortcut # alphabeticShortcut
	android:numericShortcut # numericShortcut
	android:checkable android:checked
	android:visible
	android:enabled
	android:menuCategory # system
	android:orderInCategory # int 100
<group>
	android:id
	android:checkableBehavior # single
	android:visible
	android:enabled
	android:menuCategory # system
	android:orderInCategory # int 100

onCreateOptionsMenu
onOptionsItemSelected
MenuInflater
	inflate
MenuItem
getItemId
```

# Android 动画

```
补间动画 Animation					<-- Cloneable
    AnimationSet
    渐变(透明度) AlphaAnimation
    旋转(角度) RotateAnimation
    缩放(大小) ScaleAnimation
    平移(位置) TranslateAnimation

Animation
    时长 getDuration
    setDuration
    执行完成保持执行完成状态 getFillAfter
    setFillAfter
    执行完成保持执行之前状态 getFillBefore
    setFillBefore
    执行延迟时间 getStartOffset
    setStartOffset
    重复执行次数 getRepeatCount
    setRepeatCount
    setAnimationListener Animation.AnimationListener
        onAnimationStart
        onAnimationEnd
        onAnimationRepeat

AnimationSet
    addAnimation


anim.xml
<set>
    android:shareInterpolator
    时长(秒) android:duration
        200 毫秒
    插值器 android:interpolator

<translate>
    android:fromXDelta
        100%p -100%p
    android:toXDelta
    android:fromYDelta
    android:toYDelta
    android:duration

<alpha>
    android:fromAlpha
    android:toAlpha
        0.0~1.0
    android:duration

<scale>
    android:fromXScale
        0.9 1
    android:toXScale
    android:fromYScale
    android:toYScale
    android:pivotX
    android:pivotY
        50 绝对定位 50% 相对位置本身 50%p 相对位置父空间
    android:duration

<rotate>
    android:fromDegrees
        45~90
    android:toDegrees
    android:pivotX
        0.5
    android:pivotY

Integer IntEvaluator		<-- TypeEvaluator<Integer>
int[] IntArrayEvaluator		<-- TypeEvaluator<int[]>
Number FloatEvaluator		<-- TypeEvaluator<Number>
float[] FloatArrayEvaluator	<-- TypeEvaluator<float[]>
Object ArgbEvaluator		<-- TypeEvaluator<Object>
Rect RectEvaluator			<-- TypeEvaluator<Rect>
PointF PointFEvaluator		<-- TypeEvaluator<PointF>

TypeEvaluator
    evaluate

TypeEvaluator<Integer> evaluator = new ArgbEvaluator();
evaluator.evaluate(0, Color.WHITE, Color.BLACK);

插值器

BaseInterpolator		<-- Interpolator
    AccelerateInterpolator
    减速 DecelerateInterpolator
    先加速后减速 AccelerateDecelerateInterpolator
    AnticipateInterpolator
    OvershootInterpolator
    AnticipateOvershootInterpolator
    BounceInterpolator
    速率正弦曲线变化 CycleInterpolator
    匀速线性 LinearInterpolator
    PathInterpolator

TimeInterpolator
    定义动画变化速率 Interpolator

TimeInterpolator
    getInterpolation

@android:anim/linear_interpolator
@android:anim/accelerate_decelerate_interpolator
@android:anim/bounce_interpolator
@android:anim/accelerate_interpolator AccelerateInterpolator
加速 <accelerateInterpolator>
    android:factor
        1.5
@android:anim/anticipate_interpolator AnticipateInterpolator
<anticipateInterpolator>
    android:tension
        1.5
@android:anim/anticipate_overshoot_interpolator AnticipateOvershootInterpolator
<anticipateOvershootInterpolator>
    android:tension
        1.5
    android:extraTension
        1.5
@android:anim/cycle_interpolator CycleInterpolator
<cycleInterpolator>
    android:cycles
        5
@android:anim/decelerate_interpolator DecelerateInterpolator
<decelerateInterpolator>
    android:factor
        1.5
@android:anim/overshoot_interpolator OvershootInterpolator
<overshootInterpolator>
    android:tension
        1.5

帧动画 AnimationDrawable
    帧列表 <animation-list>
        展示一次 android:oneshot
        android:visible
    帧 <item>
        图片 android:drawable
        时长 android:duration

LayoutAnimationController
    GridLayoutAnimationController

<layoutAnimation>
    延迟 android:delay
        0.5
    android:animationOrder
        random
    动画资源 android:animation

LayoutAnimationController
    空间显示顺序 setOrder
        LayoutAnimationController.ORDER_NORMAL
viewGroup.setLayoutAnimation(layoutAnimationController)





PropertyValuesHolder  <-- Cloneable
    ofFloat

<propertyValuesHolder>
    android:valueFrom
    android:valueTo
    android:valueType
    android:propertyName

AnimationUtils
    loadAnimation
    loadLayoutAnimation
    loadInterpolator

ViewPropertyAnimator view.animate()
    相对父控件 x
	相对自己 translationX
	时长 setDuration
	start

属性动画 Animator
    AnimatorSet
    ValueAnimator
        ObjectAnimator
        TimeAnimator

Animator
    addListener Animator.AnimatorListener
        onAnimationStart
        onAnimationEnd
        onAnimationCancel
        onAnimationRepeat
    addPauseListener Animator.AnimatorPauseListener
        onAnimationPause
        onAnimationResume
    getDuration
    setDuration
    getStartDelay
    setStartDelay
    getTotalDuration
    getInterpolator
    setInterpolator
    start
    isStarted
    pause
    isPaused
    cancel
    end
    resume
    isRunning

ValueAnimator
    ofInt
    ofFloat
    ofPropertyValuesHolder
    addUpdateListener ValueAnimator.AnimatorUpdateListener
        onAnimationUpdate
    getAnimatedValue
    setRepeatMode
        ValueAnimator.RESTART
    setRepeatCount
        ValueAnimator.INFINITE

AnimatorSet
    playTogether
    playSequentially
    play

<set>
    android:ordering
        sequentially
<animator> # ValueAnimator
    android:duration
    android:interpolator
        @android:interpolator/linear
    android:repeatCount
        infinite
    android:repeatMode
        restart
    android:startOffset
        0
    android:valueFrom
    android:valueTo
    android:valueType
        colorType
<objectAnimator>
    android:propertyName
    android:duration
    android:valueFrom
    android:valueTo
    android:valueType
        intType
    android:startOffset
    android:repeatMode
        restart
    android:repeatCount
        infinite
    android:interpolator
        @android:interpolator/linear
    android:pathData
        1,2,2,3,5
    android:propertyXName
    android:propertyYName

AnimatorInflater
    loadAnimator

Keyframe
```

## NineOldAndroids

```
https://github.com/JakeWharton/NineOldAndroids
```

# Android 事件处理

```
Activity
View
ViewGroup | requestDisallowInterceptTouchEvent

MotionEvent | ACTION
KeyEvent | ACTION | KEYCODE
```

# Android 手势

```
GestureDetector | OnGestureListener | OnDoubleTapListener | OnContextClickListener | SimpleOnGestureListener

ScaleGestureDetector | OnScaleGestureListener | SimpleOnScaleGestureListener
```

## AppWidget

```
AppWidgetProvider
AppWidgetManager
class AskBrainAppWidgetProvider extends AppWidgetProvider {
    @Override // 当 App Widget 实例第一次被创建时
    public void onEnabled(Context context) { super.onEnabled(context); }
    @Override // 当最后一个App Widget 实例 被删除时
    public void onDisabled(Context context) { super.onDisabled(context); }
    @Override // 删除 App Widget 时
    public void onDeleted(Context context, int[] appWidgetIds) { super.onDeleted(context, appWidgetIds); }
    @Override // 达到制定时间更新 向桌面添加App Widget 每次更新都调用一次该方法，使用频繁
    public void onUpdate(Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds) { super.onUpdate(context, appWidgetManager, appWidgetIds); }
    @Override // 接收广播事件
    public void onReceive(Context context, Intent intent) { super.onReceive(context, intent); }
}

PendingIntent pendingIntent = PendingIntent.getActivity(context, 100, new Intent(), 0);
RemoteViews remoteViews = new RemoteViews(context.getPackageName(), android.R.layout.simple_list_item_1);
remoteViews.setTextViewText(android.R.id.text1,"");
remoteViews.setOnClickPendingIntent(android.R.id.button1, pendingIntent);
AppWidgetManager appWidgetManager = AppWidgetManager.getInstance(context);
appWidgetManager.updateAppWidget(new ComponentName(context, AppWidgetManager.class), remoteViews);

<receiver android:name=".appwidget.YicAppWidgetProvider">
    <intent-filter>
        <action android:name="android.appwidget.action.APPWIDGET_UPDATE" />
    </intent-filter>
    <intent-filter>
        <action android:name="org.lxh.action.MYAPPWIDGET_UPDATE"/>
    </intent-filter>
    <meta-data
        android:name="android.appwidget.provider"
        android:resource="@xml/roach_appwidget"/>
</receiver>

<appwidget-provider>
	android:minHeight android:minWidth
	android:updatePeriodMillis # 6000 毫秒
	android:initialLayout # layout

```

# Android 滚动

```
滚动
内嵌滚动

Scroller
OverScroller
ViewConfiguration
ViewConfigurationCompat
VelocityTracker

Scroller
    startScroll
    getCurrX
    getCurrY
    computeScrollOffset
    abortAnimation
    forceFinished

OverScroller
    startScroll

VelocityTracker
    obtain
    addMovement
    getXVelocity
    getYVelocity
    computeCurrentVelocity
    recycle

ViewConfiguration
    get
    getTouchSlop
    getMinimumFlingVelocity

FrameLayout
    HorizontalScrollView
    ScrollView
    NestedScrollView

NestedScrollingParentHelper

NestedScrollingParent
    NestedScrollingParent2
        NestedScrollingParent3
NestedScrollingChild
    NestedScrollingChild2
        NestedScrollingChild3
ScrollingView

NestedScrollingParent3
NestedScrollingChild3
ScrollingView
    NestedScrollView

View
    onScrollChanged
    scrollTo
    scrollBy

ScrollView
    setFillViewport android:fillViewport
    android:scrollbars none

NestedScrollingChild # 内嵌滚动 setNestedScrollingEnabled(true)
	setNestedScrollingEnabled isNestedScrollingEnabled
	startNestedScroll
	stopNestedScroll
	hasNestedScrollingParent
	dispatchNestedScroll dispatchNestedPreScroll # consumed
	dispatchNestedFling dispatchNestedPreFling # consumed
NestedScrollingParent

NestedScrollingParentHelper
	onStartNestedScroll # nestedScrollAxes
	onNestedScrollAccepted
	onStopNestedScroll
	onNestedScroll
	onNestedPreScroll # consumed[1] = dy;
	onNestedFling onNestedPreFling # 
	getNestedScrollAxes
```



# Android 偏好设置

```
PreferenceManager
    getDefaultSharedPreferences


Preference
<?xml version="1.0" encoding="utf-8"?>
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

```



# Android 轮波图

## Banner

```
https://github.com/youth5201314/banner
https://github.com/youth5201314/banner
implementation 'com.youth.banner:banner:1.4.10'
```

## ConvenientBanner

```
https://github.com/saiwu-bigkoo/Android-ConvenientBanner
```

## ViewFlow

```
https://github.com/pakerfeldt/android-viewflow
```

# Android 图表

## MPAndroidChart

```
https://github.com/PhilJay/MPAndroidChart
implementation 'com.github.PhilJay:MPAndroidChart:v3.0.3'
```

## KChartView

```
https://github.com/tifezh/KChartView
```

## Android-Charts

```
https://github.com/limccn/Android-Charts

```

# Android 多媒体

## 绘图

```
Canvas | draw | 








Canvas
    getWidth
    getHeight
    矩形 drawRect
    圆角矩形 drawRoundRect
    drawBitmap
    drawText
    drawPosText
    圆形 drawCircle
    drawBitmapMesh
    drawPath
    drawTextOnPath
    点 drawPoint
    多个点 drawPoints
    直线 drawLine
    多条直线 drawLines
    椭圆 drawOval
        椭圆是根据矩形生成的，以矩形的长为椭圆的X轴，矩形的宽为椭圆的Y轴，建立的椭圆图形
    弧 drawArc
        弧是椭圆的一部分，而椭圆是根据矩形来生成的，所以弧当然也是根据矩形来生成的
    drawRegion
    clipPath
        Region.Op.DIFFERENCE
    concat
    画布平移 translate
        画布坐标 屏幕左上角 x向左 y向下
    画布旋转 rotate
        围绕坐标原点旋转
    缩放 scale
    扭曲 skew
        倾斜角度的tan值
        (1.732f,0);//X轴倾斜60度，Y轴不变
    save
    restore
    setDrawFilter
        PaintFlagsDrawFilter(0, Paint.ANTI_ALIAS_FLAG | Paint.FILTER_BITMAP_FLAG)
    getDrawFilter

Paint
    ANTI_ALIAS_FLAG
    画笔颜色 setColor
    getColor
    文字大小 setTextSize
    getTextSize
    setTypeface
        Typeface.create("System", Typeface.BOLD)
    getTypeface
    setStyle
        填充 Style.FILL
        描边 Style.STROKE
        填充且描边 Style.FILL_AND_STROKE
    getStyle
    setAlpha
    getAlpha
    setShader
        Shader.TileMode.CLAMP
    getShader
    字体 setTypeface
    measureText
    getTextBounds
    getTextWidths
    setXfermode
        PorterDuffXfermode(PorterDuff.Mode.SRC_IN)
    喵边宽度 setStrokeWidth
    getStrokeWidth
    抗锯齿 影响绘制速度 setAntiAlias
    isAntiAlias
    文字对齐方式 setTextAlign
        Align.CENTER
        Align.LEFT
        Align.RIGHT
    文字加粗 setFakeBoldText
    下划线 setUnderlineText
    字体水平倾斜度，普通斜体字是-0.25 setTextSkewX
        字体水平倾斜度，普通斜体字是-0.25，可见往右斜
        水平倾斜度设置为：0.25，往左斜
    删除线效果 setStrikeThruText
    只会将水平方向拉伸，高度不会变 setTextScaleX
    getFontMetrics Paint.FontMetrics
        五线普 基线 baseLineY
        ascent = baseLineY + fm.ascent
        descent = baseLineY + fm.descent
        top = baseLineY + fm.top
        bottom = baseLineY + fm.bottom
    画text所占的区域 getFontMetricsInt Paint.FontMetricsInt
        top = baseLineY + fm.top;
        bottom = baseLineY + fm.bottom;
        width = (int)paint.measureText(text);
        Rect(baseLineX,top,baseLineX+width,bottom);
    最小矩形 getTextBounds
        top = baseLineY + minRect.top
        bottom = baseLineY + minRect.bottom
        drawRect(minRect,paint);
    画文字
        drawText(text, baseLineX, baseLineY, paint);
    阴影 setShadowLayer

Matrix
    MSCALE_X
    setRotate
    preRotate
    postRotate
    setTranslate
    preTranslate
    postTranslate
    setScale
    preScale
    postScale
    setSkew
    preSkew
    postSkew
    setConcat
    preConcat
    postConcat
    setPolyToPoly

Drawable
    DrawableContainer <-- Drawable.Callback
        AnimationDrawable <-- Runnable Animatable
        StateListDrawable
            AnimatedStateListDrawable
        LevelListDrawable
    BitmapDrawable
    NinePatchDrawable
    ColorDrawable
    DrawableWrapper <-- Drawable.Callback
        ClipDrawable
        InsetDrawable
        RotateDrawable
        ScaleDrawable
    GradientDrawable
    LayerDrawable <-- Drawable.Callback
        RippleDrawable
        TransitionDrawable <-- Drawable.Callback
    ShapeDrawable
        PaintDrawable
    PictureDrawable
    VectorDrawable

Drawable
    setColorFilter
    getColorFilter
    setBounds
    getBounds
    getIntrinsicWidth
    getIntrinsicHeight
    draw

Shader
    BitmapShader
    LinearGradient
    SweepGradient
    RadialGradient
    ComposeShader

DrawFilter
    毛边过滤 PaintFlagsDrawFilter

Xfermode
	PorterDuffXfermode

Typeface
    create
    createFromAsset
    createFromFile
    defaultFromStyle


ColorMatrix

ColorFilter
    PorterDuffColorFilter
        PorterDuff.Mode.SRC_IN
    BlendModeColorFilter
    ColorMatrixColorFilter
    LightingColorFilter

Icon <-- Parcelable
    createWithResource

Gravity

Point
Rect
RectF

区域 Region
    setPath
    op
        Region.Op.XOR 交集

RegionIterator
    RegionIterator(Region)
    next(Rect)


Path
    moveTo
    lineTo
    close
    addCircle
        逆向绘制 Path.Direction.CCW
    addOval

Color
    WHITE
    BLACK
    TRANSPARENT
    parse
    valueOf
    rgb
    parseColor

Bitmap
    createBitmap
    compress
        CompressFormat.PNG
        CompressFormat.JPEG

BitmapFactory
    decodeByteArray
    decodeFile

BitmapFactory.Options
    inJustDecodeBounds
    inSampleSize
    outMimeType
    outWidth
    outHeight
    outConfig
        Bitmap.Config.ALPHA_8

BitmapRegionDecoder
    newInstance
    decodeRegion

```

## 相机

```
Manifest.permission.CAMERA
Camera
    open
    release
    getParameters
    setParameters
    预览 setPreviewDisplay
    setOneShotPreviewCallback
    setPreviewCallback PreviewCallback
        onPreviewFrame
    开启预览 startPreview
    停止预览 stopPreview
    autoFocus AutoFocusCallback
        onAutoFocus
    cancelAutoFocus
    setAutoFocusMoveCallback AutoFocusMoveCallback
        onAutoFocusMoving
    照相 takePicture
        ShutterCallback onShutter
        PictureCallback onPictureTaken
    setDisplayOrientation
        90 竖直
    lock
    unlock
    摄像头数目 getNumberOfCameras
    getCameraInfo

Camera.Parameters
    预览尺寸 预览像素 getSupportedPreviewSizes Camera.Size
        width
        height
    getSupportedPictureSizes
    照片的大小 setPictureSize
    getPictureSize
    预览帧率 getSupportedPreviewFpsRange
    getSupportedPreviewFpsRange
    颜色格式 getSupportedPreviewFormats
    setPreviewFpsRange
    getPreviewFpsRange
    预览照片的大小 setPreviewSize
    getPreviewSize
    帧率 每秒几帧 setPreviewFrameRate
    getPreviewFrameRate
    照片的输出格式 setPictureFormat
        PixelFormat.JPEG
    getPictureFormat
    setPreviewFormat
        ImageFormat.NV21
        ImageFormat.YV12
    getPreviewFormat
    聚焦 setFocusMode
        Parameters.FOCUS_MODE_CONTINUOUS_VIDEO
    setFlashMode
        Parameters.FLASH_MODE_AUTO
        打开 Parameters.FLASH_MODE_TORCH
        关闭 Parameters.FLASH_MODE_OFF
    getFlashMode
    白平衡 setWhiteBalance
        Parameters.WHITE_BALANCE_AUTO
    getWhiteBalance
    闪光灯 setSceneMode
        Parameters.SCENE_MODE_AUTO
    getSceneMode
    set
        照片质量 ("jpeg-quality", 85)
    reset
    flatten
    unflatten
    setRotation

Camera.CameraInfo
    CAMERA_FACING_FRONT
    CAMERA_FACING_BACK
    facing
    orientation

判断手机是否存在摄像头
PackageManager
    hasSystemFeature
        PackageManager.FEATURE_CAMERA

Camera2 LOLLIPOP
CameraManager Context.CAMERA_SERVICE
    getCameraIdList
    getConcurrentCameraIds
    getCameraCharacteristics
    getCameraExtensionCharacteristics
    openCamera CameraDevice.StateCallback
        onOpened
        onDisconnected
        onError

CameraCharacteristics
    get
        CameraCharacteristics.LENS_FACING
        CameraMetadata.LENS_FACING_BACK
        CameraMetadata.LENS_FACING_FRONT
        CameraMetadata.LENS_FACING_EXTERNAL

CameraDevice
    close

```

## 音视频

```
MediaPlayer
    setDataSource
        uri
    setAudioStreamType
        AudioManager.STREAM_MUSIC
        AudioManager.STREAM_ALARM
    setOnCompletionListener OnCompletionListener
        onCompletion
    setOnErrorListener OnErrorListener
        onError
            MediaPlayer.MEDIA_ERROR_SERVER_DIED
    setOnPreparedListener OnPreparedListener
        onPrepared
    setOnInfoListener OnInfoListener
        onInfo
    setOnBufferingUpdateListener OnBufferingUpdateListener
        onBufferingUpdate
    seekTo
    setOnSeekCompleteListener OnSeekCompleteListener
        onSeekComplete
    setOnVideoSizeChangedListener OnVideoSizeChangedListener
        onVideoSizeChanged
    setVolume
    setDisplay
    setSurface
    prepare
    prepareAsync
    start
    stop
    release
    reset
    isPlaying
    setLooping
    isLooping
    mediaPlayer.setDataSource(file.getFileDescriptor(),
						file.getStartOffset(), file.getLength());
    setVolume(BEEP_VOLUME, BEEP_VOLUME);

AudioRecord
    getMinBufferSize
        (44100,
        AudioFormat.CHANNEL_IN_MONO,
        AudioFormat.ENCODING_PCM_16BIT);
    AudioRecord(
        MediaRecorder.AudioSource.MIC,
        44100,
        AudioFormat.CHANNEL_IN_MONO, //单声道
        AudioFormat.ENCODING_PCM_16BIT,
        minBufferSize);
    getState
        STATE_INITIALIZED
        STATE_UNINITIALIZED
    getRecordingState
        RECORDSTATE_RECORDING
    startRecording
    stop
    read
        ERROR_INVALID_OPERATION
        ERROR_BAD_VALUE
    release

AudioTrack
    getMinBufferSize(
        44100,
        AudioFormat.CHANNEL_IN_MONO,
        AudioFormat.ENCODING_PCM_16BIT);
    AudioTrack(
        AudioManager.STREAM_MUSIC,
        44100,
        AudioFormat.CHANNEL_OUT_MONO, //单声道
        AudioFormat.ENCODING_PCM_16BIT,
        minBufferSize,
        AudioTrack.MODE_STREAM);
    play
    getState
        STATE_INITIALIZED
    release
    getPlayState
        PLAYSTATE_PLAYING
        PLAYSTATE_PAUSED
    stop
    pause
    write

AudioManager Context.AUDIO_SERVICE
    铃声模式 getRingerMode
        RINGER_MODE_NORMAL
        静音 RINGER_MODE_SILENT
    getStreamVolume
        STREAM_ALARM
    setStreamVolume
        STREAM_MUSIC
        STREAM_ALARM
        STREAM_RING
        STREAM_NOTIFICATION
        STREAM_SYSTEM
        STREAM_VOICE_CALL
        STREAM_DTMF
        mode NORMAL speakerphoneOn
    getStreamVolume
    getStreamMinVolume
    getStreamMaxVolume

Activity
    设置activity音量控制键控制的音频流 setVolumeControlStream
        AudioManager.STREAM_MUSIC

MediaRecorder
    getMaxAmplitude
    setCamera
    setPreviewDisplay
    setVideoSource
        VideoSource.CAMERA
    setVideoEncoder
        VideoEncoder.H264
    setVideoFrameRate
        25
    setVideoSize
    setAudioSource
        AudioSource.DEFAULT
        麦克风 AudioSource.MIC
    setAudioEncoder
        AudioEncoder.AAC
        AudioEncoder.AMR_NB
    setAudioChannels
        1 MONO
    setAudioSamplingRate
        8000 8000Hz
    setAudioEncodingBitRate
        64
    setOutputFile
    setOutputFormat
        OutputFormat.MPEG_4
        OutputFormat.AMR_NB
    setMaxDuration
        30000
    setMaxFileSize
    setOrientationHint
        90
    reset
    prepare
    release
    start
    stop
    setOnErrorListener OnErrorListener
        onError
    setOnInfoListener OnInfoListener
        onInfo

SoundPool
    setOnLoadCompleteListener OnLoadCompleteListener
        onLoadComplete
    load
    unload
    play
    pause
    resume
    stop
    release

SoundPool.Builder
    build

RingtoneManager
    getDefaultUri
        闹钟 TYPE_ALARM
        通知 TYPE_NOTIFICATION
    铃声 getRingtone(uri)

铃声 Ringtone
    播放 play
    停止 stop
    isPlaying

MediaMetadataRetriever
    setDataSource
    getFrameAtTime


======
RemoteViews <-- Parcelable Filter

自定义 View
 绘制流程 onFinishInflate systemUI

View
    View 滚动
    View 内嵌滚动
    View 事件分发

ViewTreeObserver

Dialog # 自定义 ondestroy
PopupWindow # 自定义
Menu
Toast
通知 NotificationCompat.Builder
动画
InputEvent # DPAD_CENTER 确认键

View
    位置 状态 深色模式 执行动画

事件分发 touch

```

## 录屏

```
MediaProjectionManager
MediaProjectionManager mediaProjectionManager = (MediaProjectionManager) getSystemService(Context.MEDIA_PROJECTION_SERVICE);
Intent intent = mediaProjectionManager.createScreenCaptureIntent();
startActivityForResult(intent, 100);

MediaProjection mediaProjection = mediaProjectionManager.getMediaProjection(resultCode, data);
MediaCodec mediaCodec = MediaCodec.createEncoderByType("video/avc");
MediaFormat mediaFormat = MediaFormat.createVideoFormat("video/avc", 720, 1280);
mediaFormat.setInteger(MediaFormat.KEY_COLOR_FORMAT, MediaCodecInfo.CodecCapabilities.COLOR_FormatSurface);
mediaFormat.setInteger(MediaFormat.KEY_BIT_RATE, 400_000);
mediaFormat.setInteger(MediaFormat.KEY_FRAME_RATE, 15);
mediaFormat.setInteger(MediaFormat.KEY_I_FRAME_INTERVAL, 2);
mediaCodec.configure(mediaFormat, null, null, MediaCodec.CONFIGURE_FLAG_ENCODE);
Surface surface = mediaCodec.createInputSurface();
VirtualDisplay virtualDisplay = mediaProjection.createVirtualDisplay(
        "screen-codec",
        720, 1280, 1,
        DisplayManager.VIRTUAL_DISPLAY_FLAG_PUBLIC,surface, null, null);

mediaCodec.start();
MediaCodec.BufferInfo bufferInfo = new MediaCodec.BufferInfo();
long time = System.currentTimeMillis();

long startTime = bufferInfo.presentationTimeUs / 1000;
OutputStream outputStream = new FileOutputStream("");
int index = mediaCodec.dequeueOutputBuffer(bufferInfo, 100_000);// 微妙
if (index >= 0) {
    if (System.currentTimeMillis() - time >= 2000) { // 2s 关键帧
        Bundle bundle = new Bundle();
        bundle.putInt(MediaCodec.PARAMETER_KEY_REQUEST_SYNC_FRAME, 0);
        mediaCodec.setParameters(bundle);
        time = System.currentTimeMillis();
    }
    ByteBuffer byteBuffer = mediaCodec.getOutputBuffer(index);
    byte[] outData = new byte[bufferInfo.size];
    byteBuffer.get(outData);
    long duration = bufferInfo.presentationTimeUs / 1000 - startTime;
    outputStream.write(outData);
    outputStream.write('\n');
    mediaCodec.releaseOutputBuffer(index, false);
}

```

## GiraffePlayer

```
https://github.com/tcking/GiraffePlayer
```

## Vitamio

```
https://github.com/yixia/VitamioBundle
https://github.com/yixia/VitamioBundleStudio
http://www.vitamio.org/
```

## UniversalVideoView

```
https://github.com/linsea/UniversalVideoView
```

## ijkplayer

```
https://github.com/bilibili/ijkplayer
```

## DanmakuFlameMaster

```
https://github.com/bilibili/DanmakuFlameMaster
```

## PLDroidPlayer

```
https://github.com/pili-engineering/PLDroidPlayer
```

## PLDroidShortVideo

```
https://github.com/pili-engineering/PLDroidShortVideo
```

## PLDroidCameraStreaming

```
https://github.com/pili-engineering/PLDroidMediaStreaming
```

## ExoPlayer

```
https://github.com/google/ExoPlayer

implementation 'com.google.android.exoplayer:exoplayer:2.13.3'

exoplayer core dash ui

Timeline.Window window = new Timeline.Window();
SimpleExoPlayerView simpleExoPlayerView = null;

BandwidthMeter bandwidthMeter = new DefaultBandwidthMeter();
TrackSelection.Factory videoTrackSelectionFactory =
        new AdaptiveVideoTrackSelection.Factory(bandwidthMeter);
TrackSelector trackSelector =
        new DefaultTrackSelector(videoTrackSelectionFactory);
LoadControl loadControl = new DefaultLoadControl();
SimpleExoPlayer player =
        ExoPlayerFactory.newSimpleInstance(this, trackSelector, loadControl);
simpleExoPlayerView.setPlayer(player);
player.setPlayWhenReady(true);

DefaultBandwidthMeter bandwidthMeter = new DefaultBandwidthMeter();
DataSource.Factory dataSourceFactory = new DefaultDataSourceFactory(this, bandwidthMeter
        , new DefaultHttpDataSourceFactory(Util.getUserAgent(this, "yourApplicationName"), bandwidthMeter));
ExtractorsFactory extractorsFactory = new DefaultExtractorsFactory();
MediaSource videoSource = new ExtractorMediaSource(Uri.parse(VIDEO_URL),
        dataSourceFactory, extractorsFactory, mainHandler, null);
MediaSource videoSource2 = new ExtractorMediaSource(Uri.parse(VIDEO_URL_DEFAULT),
        dataSourceFactory, extractorsFactory, mainHandler, null);
//组合几个视频
ConcatenatingMediaSource concatenatingMediaSource = new ConcatenatingMediaSource(videoSource,videoSource2);
//不停循环
LoopingMediaSource loopingSource = new LoopingMediaSource(concatenatingMediaSource);
player.prepare(loopingSource);

//
DefaultBandwidthMeter bandwidthMeter = new DefaultBandwidthMeter();
// Produces DataSource instances through which media data is loaded.
DataSource.Factory dataSourceFactory = new DefaultDataSourceFactory(this, bandwidthMeter
        , new DefaultHttpDataSourceFactory(Util.getUserAgent(this, "yourApplicationName"), bandwidthMeter));
// Produces Extractor instances for parsing the media data.
ExtractorsFactory extractorsFactory = new DefaultExtractorsFactory();
// This is the MediaSource representing the media to be played.
MediaSource videoSource = new ExtractorMediaSource(Uri.parse(url),
        dataSourceFactory, extractorsFactory, mainHandler, null);

//不停循环
LoopingMediaSource loopingSource = new LoopingMediaSource(videoSource);
SurfaceView sv = (SurfaceView) findViewById(R.id.sv);
player.setVideoSurfaceView(sv);
player.setPlayWhenReady(true);
player.prepare(loopingSource);

//
int playerWindow = player.getCurrentWindowIndex();
playerPosition = C.TIME_UNSET;
Timeline timeline = player.getCurrentTimeline();
if (!timeline.isEmpty() && timeline.getWindow(playerWindow, window).isSeekable) {
    playerPosition = player.getCurrentPosition();
}
player.release();
player = null;
```

# Android NDK

```
NDK 编程 jni
    Android.mk
    Application.mk

Android.mk
Application.mk

ifndef USE_FREETYPE
USE_FREETYPE := 2.4.2
endif

ifeq ($(USE_FREETYPE),2.4.2)
LOCAL_PATH:= $(call my-dir)
include $(CLEAR_VARS)

LOCAL_ARM_MODE := arm

LOCAL_SRC_FILES:= \
	src/base/ftbbox.c \
	src/psnames/psnames.c \
	src/pshinter/pshinter.c

LOCAL_C_INCLUDES += \
	$(LOCAL_PATH)/builds \
	$(LOCAL_PATH)/include

LOCAL_CFLAGS += -W -Wall
LOCAL_CFLAGS += -fPIC -DPIC
LOCAL_CFLAGS += "-DDARWIN_NO_CARBON"
LOCAL_CFLAGS += "-DFT2_BUILD_LIBRARY"
LOCAL_CFLAGS += "-DTT_CONFIG_OPTION_BYTECODE_INTERPRETER"
LOCAL_CFLAGS += -O2

LOCAL_MODULE:= libft2

include $(BUILD_STATIC_LIBRARY)
endif

include $(CLEAR_VARS)
LOCAL_C_INCLUDES += \
	$(LOCAL_PATH)/builds \
	$(LOCAL_PATH)/include
LOCAL_LDLIBS := -L$(SYSROOT)/usr/lib -llog
LOCAL_MODULE := dxtx
LOCAL_STATIC_LIBRARIES := libft2
# for logging
LOCAL_LDLIBS    += -llog
# for native windows
LOCAL_LDLIBS    += -landroid

LOCAL_CFLAGS    += -UNDEBUG
include $(BUILD_SHARED_LIBRARY)



task ndkBuild(type: Exec) {
	def ndkDir = project.plugins.findPlugin('com.android.library').sdkHandler.getNdkFolder()
	commandLine "$ndkDir/ndk-build.cmd", '-C', 'src/main/jni',
			"NDK_OUT=$buildDir/ndk/obj",
			"NDK_APP_DST_DIR=$buildDir/ndk/libs/\$(TARGET_ARCH_ABI)"
}

task copyExeFile(type: Copy) {
	from fileTree(dir: file(buildDir.absolutePath + '/ndk/libs'), include: '**/*')
	into file('src/main/assets/')
}


```

## Android.mk

```
APP_ABI := all
LOCAL_PATH := $(call my-dir)
include $(CLEAR_VARS)

LOCAL_SRC_FILES:= VideoConvert.cpp

LOCAL_MODULE:= asdf

#LOCAL_CFLAGS += -std=c99
#LOCAL_C_INCLUDES :=
#LOCAL_STATIC_LIBRARIES :=
#LOCAL_SHARED_LIBRARIES :=

include $(BUILD_SHARED_LIBRARY)

LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)
LOCAL_MODULE := freetype2-prebuilt
LOCAL_SRC_FILES := ../obj/local/$(TARGET_ARCH_ABI)/libfreetype2-static.a
include $(PREBUILT_STATIC_LIBRARY)

CLEAR_VARS
BUILD_EXECUTABLE
BUILD_SHARED_LIBRARY
BUILD_STATIC_LIBRARY
PREBUILT_SHARED_LIBRARY
PREBUILT_STATIC_LIBRARY

TARGET_ARCH
TARGET_PLATFORM
TARGET_ARCH_ABI
TARGET_ABI

LOCAL_PATH
LOCAL_MODULE
LOCAL_MODULE_FILENAME
LOCAL_SRC_FILES
LOCAL_CPP_EXTENSION
LOCAL_CPP_FEATURES
LOCAL_C_INCLUDES
LOCAL_CFLAGS
LOCAL_CPPFLAGS
LOCAL_STATIC_LIBRARIES
LOCAL_SHARED_LIBRARIES
LOCAL_WHOLE_STATIC_LIBRARIES
LOCAL_LDLIBS
LOCAL_LDFLAGS
LOCAL_ALLOW_UNDEFINED_SYMBOLS
LOCAL_ARM_MODE
LOCAL_ARM_NEON
LOCAL_DISABLE_FORMAT_STRING_CHECKS
LOCAL_EXPORT_CFLAGS
LOCAL_EXPORT_CPPFLAGS
LOCAL_EXPORT_C_INCLUDES
LOCAL_EXPORT_LDFLAGS
LOCAL_EXPORT_LDLIBS
LOCAL_SHORT_COMMANDS
LOCAL_THIN_ARCHIVE
LOCAL_FILTER_ASM
my-dir
all-subdir-makefiles
this-makefile
parent-makefile
grand-parent-makefile
import-module

Application.mk
# Android OS 放弃GCC转向了 Clang 编译器,NDK 将移除GCC
#   APP_STL  := gnustl_static 改为 APP_STL := c++_static
#   删除NDK_TOOLCHAIN or NDK_TOOLCHAIN_VERSION
#对于cmake编译
#   删除 ANDROID_TOOLCHAIN
#对于独立的toolchains
#   用clang/clang++ binaries 代替 gcc/g++

APP_PLATFORM := android-16
APP_ALLOW_MISSING_DEPS=true

APP_ABI := all,armeabi,armeabi-v7a,arm64-v8a
#APP_ABI:=armeabi arm64-v8a x86_64 x86 armeabi-v7a
#NDK_TOOLCHAIN_VERSION:=clang3.5
#APP_STL:=gnustl_static
APP_STL:=c++_static
#APP_OPTIM：= debuge


APP_ABI

APP_ASFLAGS
APP_ASMFLAGS
APP_BUILD_SCRIPT
APP_CFLAGS
APP_CLANG_TIDY
APP_CLANG_TIDY_FLAGS
APP_CONLYFLAGS
APP_CPPFLAGS
APP_CXXFLAGS
APP_DEBUG
APP_LDFLAGS
APP_MANIFEST
APP_MODULES
APP_OPTIM
APP_PLATFORM
APP_PROJECT_PATH
APP_SHORT_COMMANDS
APP_STL
APP_STRIP_MODE
APP_THIN_ARCHIVE
APP_WRAP_SH

 ## hello world JNI
// extern "C" 标识后面的用C编译 ,这里的意思是这个函数用C编译,C++为了函数重载会把参数带上,而c没有函数重载
// JNICALL表示调用约定，相当于C++的stdcall，说明调用的是本地方法
// JNIEXPORT表示函数的链接方式，当程序执行的时候从本地库文件中找函数
// 中间的jstring就是返回类型,是c++中对应java中String的类型
// JNIEnv 是对java环境的引用,并且提供了一些类型转换方法
// jobject 是调用这个函数的java对象.没发现如何使用
extern "C" JNIEXPORT jstring JNICALL Java_com_happy_fei_helloworldjni_MainActivity_stringFromJNI(
        JNIEnv *env,
        jobject /* this */) {
    std::string hello = "Hello from C++";
    return env->NewStringUTF(hello.c_str());
}
	
extern "C" 告诉编译器后面的按照C的风格编译.我测试下如果函数前不加extern "C"会报错
​```
java.lang.UnsatisfiedLinkError: No implementation found for java.lang.String com.happy.fei.helloworldjni.MainActivity.helloWorld(java.lang.String, java.lang.String) (tried Java_com_happy_fei_helloworldjni_MainActivity_helloWorld and Java_com_happy_fei_helloworldjni_MainActivity_helloWorld__Ljava_lang_String_2Ljava_lang_String_2)
​```
错误的信息是没有找到helloWorld函数也没有找到helloWorld(String,String)函数.
问题:什么时候可以不使用extern "C". 我这个文件是CPP啊,不过留待以后熟练了发现吧.现在还不太溜

###### 稍微难一点

```

# Android Hook 框架

## Xposed

```
XposedHelpers
IXposedHookLoadPackage
XposedBridge
meta-data kv
xposedmodule true
xposeddescription @string/gps_hack_desc
xposedminversion 54

// 53 82 | assets/xposed_init
compileOnly 'de.robv.android.xposed:api:82'
compileOnly 'de.robv.android.xposed:api:82:sources'

IXposedHookLoadPackage # handleLoadPackage
XC_LoadPackage.LoadPackageParam classLoader
XposedHelpers # findAndHookMethod
XC_MethodHook # beforeHookedMethod afterHookedMethod
MethodHookParam # args setResult
XposedBridge # log
```

# Android 插件化

## Tinker

```
https://github.com/Tencent/tinker

// 低版本编译不通过
classpath "com.tencent.tinker:tinker-patch-gradle-plugin:1.9.14.19"
plugins {
    id 'com.tencent.tinker.patch'
}
tinkerPatch {
    buildConfig {
        tinkerId "1.0"
    }
}
compileOnly 'com.tencent.tinker:tinker-android-anno:1.9.14.19'
implementation 'com.tencent.tinker:tinker-android-lib:1.9.14.19'

gradle.properties
TINKER_ID=1.0
TINKER_ENABLE=true

```

# Jetpack

```
Foundation 基础组件
    AppCompat
    KTX
    Multidex
    Test

Architecture 架构组件
    Lifecycles
    LiveData
    ViewModel
    Room
    DataBinding
    Paging
    Navigation
    WorkManager

Behaviour 行为组件
	DownloadManager
	Media & Playback
	Notifications
	Permissions
	Preferences
	Sharing
	Slices
UI 组件
    Animation & transitions
        Auto
        Emoji
        Fragment
        Layout
        Palette
        TV
        Wear OS by Google
    Components
        ViewPager2
        LiveDataBus
        PagedList
        CameraX
        RMI
    Androidx
        ConstraintLayout
        SwipeRefreshLayout
        RecyclerView
        DrawerLayout
        CardView
        ViewPager
        Material Design
        Compats
```

## AppCompat

```
Android
ContextCompat
ActivityCompat

ContextCompat
    ActivityCompat
implementation 'androidx.appcompat:appcompat:1.2.0'

ContextCompat
	getColor
	checkSelfPermission
ActivityCompat
	requestPermissions
ContextCompat.getColor(
ContextCompat.getDrawable(

```

## KTX

```
implementation 'androidx.core:core-ktx:1.0.2'

val mSharedPreferences = context.getSharedPreferences("", Context.MODE_PRIVATE)
        mSharedPreferences.edit() {
            putBoolean("boo",false)
        }

        val mView: View = View(context)
        mView.doOnLayout {
        }
        mView.setOnClickListener({v -> })
        mView.setOnClickListener {  }

        val string = "baidu.com"
//        string.javaClass.simpleName
        val uri = string.toUri()

        val mIntent = Intent(context, MyAppCompatActivity::class.java)
        context.startActivity(mIntent)


//        var stackTrace : Array<StackTraceElement>  = Thread.currentThread().stackTrace
//        var stackTraceElement : StackTraceElement = stackTrace[3]
```

## DataBinding

```
数据绑定
DataBinding
    DataBindingUtil
    ViewDataBinding
    BindingAdapter
    BaseObservable

@Bindable

ViewDataBinding
	setLifecycleOwner # 生命周期拥有者 使databinding可以感知到Activity的生命周期 保证数据在可见时才会更新 不可见时不会跟新
```



## Multidex

```
MultiDexApplication
MultiDex

// 1.0.3
implementation 'com.android.support:multidex:1.0.2'
```



# 拼音 TinyPinyin

```
https://github.com/promeG/TinyPinyin
implementation 'com.github.promeg:tinypinyin:2.0.3'
implementation 'com.github.promeg:tinypinyin-lexicons-android-cncity:2.0.3'
```

# Litho

```
Android UI 框架
https://github.com/facebook/litho
```



# 工件映射 Artifact Mappings

```
implementation 'com.android.support:support-vector-drawable:28.0.0'
AndroidX build artifact # Old build artifact
androidx.arch.core # android.arch.core
	core-common # common
	core # core
	core-testing # core-testing
	core-runtime # runtime
androidx.sqlite # android.arch.persistence
	sqlite # db
	sqlite-framework # db-framework
androidx.test.espresso.idling # com.android.support.test.espresso.idling
	idling-concurrent # idling-concurrent
	idling-net # idling-net
androidx.test.espresso # com.android.support.test.espresso
	espresso-core # espresso-core 3.2.0 3.0.2
	espresso-accessibility # espresso-accessibility
	espresso-contrib # espresso-contrib
	espresso-idling-resource # espresso-idling-resource
	espresso-intents # espresso-intents
	espresso-remote # espresso-remote
	espresso-web # espresso-web
androidx.test.jank # com.android.support.test.janktesthelper
	janktesthelper # janktesthelper
androidx.test # com.android.support.test.services
	test-services # test-services
androidx.test.uiautomator # com.android.support.test.uiautomator
	uiautomator # uiautomator
androidx.test # com.android.support.test
	monitor # monitor
	orchestrator # orchestrator
	rules # rules
	runner # runner
androidx.vectordrawable # com.android.support
	vectordrawable-animated # animated-vector-drawable
androidx.appcompat # com.android.support
	appcompat # appcompat-v7 28.0.0
androidx.asynclayoutinflater # com.android.support
	asynclayoutinflater # asynclayoutinflater
androidx.car # com.android.support
	car # car
androidx.collection # com.android.support
	collection # collections
androidx.cursoradapter # com.android.support
	cursoradapter # cursoradapter
androidx.browser # com.android.support
	browser # customtabs
androidx.customview # com.android.support
	customview # customview
androidx.documentfile # com.android.support
	documentfile # documentfile
androidx.exifinterface # com.android.support
	exifinterface # exifinterface
androidx.gridlayout # com.android.support
	gridlayout # gridlayout-v7
androidx.heifwriter # com.android.support
	heifwriter # heifwriter
androidx.interpolator # com.android.support
	interpolator # interpolator
androidx.leanback # com.android.support
	leanback # leanback-v17
androidx.loader # com.android.support
	loader # loader
androidx.localbroadcastmanager # com.android.support
	localbroadcastmanager # localbroadcastmanager
androidx.media2 # com.android.support
	media2 # media2
    media2-exoplayer # media2-exoplayer
androidx.mediarouter # com.android.support
	mediarouter # mediarouter-v7
androidx.multidex # com.android.support
	multidex # multidex
	multidex-instrumentation # multidex-instrumentation
androidx.palette # com.android.support
	palette # palette-v7
androidx.percentlayout # com.android.support
	percentlayout # percent
androidx.leanback # com.android.support
	leanback-preference # preference-leanback-v17
androidx.legacy # com.android.support
	legacy-preference-v14 # preference-v14
androidx.preference # com.android.support
	preference # preference-v7
androidx.print # com.android.support
	print # print
androidx.recommendation # com.android.support
	recommendation # recommendation
androidx.slice # com.android.support
	slice-builders # slices-builders
	slice-core # slices-core
	slice-view # slices-view
androidx.slidingpanelayout # com.android.support
	slidingpanelayout # slidingpanelayout
androidx.core # com.android.support
	core # support-compat
androidx.contentpager # com.android.support
	contentpager # support-content
androidx.legacy # com.android.support
	legacy-support-core-ui # support-core-ui
androidx.legacy # com.android.support
	legacy-support-core-utils # support-core-utils
androidx.dynamicanimation # com.android.support
	dynamicanimation # support-dynamic-animation
androidx.emoji # com.android.support
	emoji # support-emoji
	emoji-appcompat # support-emoji-appcompat
	emoji-bundled # support-emoji-bundled
androidx.fragment # com.android.support
	fragment # support-fragment
androidx.media # com.android.support
	media # support-media-compat
androidx.tvprovider # com.android.support
	tvprovider # support-tv-provider
androidx.legacy # com.android.support
	legacy-support-v13 # support-v13
	legacy-support-v4 # support-v4
androidx.vectordrawable # com.android.support
	vectordrawable # support-vector-drawable
androidx.textclassifier # com.android.support
	textclassifier # textclassifier
androidx.transition # com.android.support
	transition # transition
androidx.versionedparcelable # com.android.support
	versionedparcelable # versionedparcelable
androidx.wear # com.android.support
	wear # wear
androidx.webkit # com.android.support
	webkit # webkit
junit:junit:4.12/4.+ # junit:junit:4.12
```

```
compile 'com.kyleduo.switchbutton:library:1.4.1'
compile 'com.google.android.gms:play-services-maps:8.4.0'
IndicatorSeekBar # https://github.com/warkiz/IndicatorSeekBar
RoundCorners # https://github.com/KuangGang/RoundCorners
apk-parser # net.dongliu:apk-parser:2.6.9
TinyPinyin # https://github.com/promeG/TinyPinyin
SwipeMenuListView # https://github.com/baoyongzhang/SwipeMenuListView
FlowLayout # https://github.com/huang7855196/FlowLayout
scrcpy
https://github.com/rengwuxian/MaterialEditText
https://github.com/koral--/android-gif-drawable
https://github.com/CyberAgent/android-gpuimage
https://github.com/daimajia/AndroidImageSlider
https://github.com/markzhai/AndroidPerformanceMonitor

https://github.com/gyf-dev/ImmersionBar
https://github.com/ximsfei/Android-skin-support
https://github.com/square/android-times-square
https://github.com/umano/AndroidSlidingUpPanel
https://github.com/etsy/AndroidStaggeredGrid
https://github.com/daimajia/AndroidSwipeLayout
https://github.com/daimajia/AndroidViewAnimations
https://github.com/AntennaPod/AntennaPod
https://github.com/LRH1993/AutoFlowLayout
https://github.com/HotBitmapGG/bilibili-android-client
https://github.com/PomepuyN/BlurEffectForAndroidDesign
https://github.com/Ashok-Varma/BottomNavigation
https://github.com/chrisjenx/Calligraphy
https://github.com/wonderkiln/CameraKit-Android
https://github.com/gabrielemariotti/cardslib
https://github.com/chrisbanes/cheesesquare
https://github.com/ImangazalievM/CircleMenu
https://github.com/dmytrodanylyk/circular-progress-button
http://cnode-material-design/
https://github.com/zetbaitsu/Compressor
https://github.com/Yalantis/Context-Menu.Android
https://github.com/googlemaps/android-samples
https://github.com/googlesamples/android-ActionBarCompat-ListPopupMenu
https://github.com/googlesamples/android-BeamLargeFiles
https://github.com/googlesamples/android-Camera2Video
https://github.com/googlesamples/android-EmojiCompat
https://github.com/googlesamples/android-GridViewPager
https://github.com/googlesamples/android-LNotifications
https://github.com/HujiangTechnology/gradle_plugin_android_aspectjx
https://github.com/lecho/hellocharts-android
https://github.com/LarsWerkman/HoloColorPicker
https://bitbucket.org/danielnadeau/holographlibrary
https://github.com/PrivacyApps/html-textview
https://github.com/koush/ion
https://github.com/google/iosched
https://github.com/jfeinstein10/JazzyViewPager
https://github.com/flavioarfaria/KenBurnsView
https://github.com/ksvc/KSYMediaPlayer_Android
https://github.com/nhaarman/ListViewAnimations
https://github.com/dinuscxj/LoadingDrawable
https://github.com/hackware1993/MagicIndicator
https://github.com/navasmdc/MaterialDesignLibrary
https://github.com/mikepenz/MaterialDrawer
https://github.com/romannurik/muzei
https://github.com/daimajia/NumberProgressBar
https://github.com/square/otto
PathAnimation
https://github.com/guoxiaoxing/phoenix
https://github.com/square/phrase
https://github.com/pockethub/PocketHub
https://github.com/chentao0707/QrCodeScan
https://github.com/lsjwzh/RecyclerViewPager
https://github.com/traex/RippleEffect
https://github.com/roboguice/roboguice
https://github.com/vinc3m1/RoundedImageView
https://github.com/vondear/RxTools
https://github.com/dmytrodanylyk/shadow-layout
https://github.com/amlcurran/ShowcaseView
https://github.com/Yalantis/Side-Menu.Android
https://github.com/SinaVDDeveloper
https://github.com/jfeinstein10/SlidingMenu
https://github.com/ogaclejapan/SmartTabLayout
https://github.com/castorflex/SmoothProgressBar
https://github.com/dkzwm/SmoothRefreshLayout
https://github.com/lilei644/SpringActionMenu
https://github.com/timehop/sticky-headers-recyclerview
https://github.com/Gavin-ZYX/StickyDecoration
https://github.com/TonicArtos/StickyGridHeaders
https://github.com/qdxxxx/StickyHeaderDecoration
https://github.com/emilsjolander/StickyListHeaders
https://github.com/nuptboyzhb/SuperSwipeRefreshLayout
https://github.com/ikew0ng/SwipeBackLayout
https://github.com/kyleduo/SwitchButton
https://github.com/jgilfelt/SystemBarTint
https://github.com/andkulikov/transitions-everywhere
https://github.com/lucasr/twoway-view
https://github.com/Yalantis/uCrop
https://github.com/Zhaoss/WeiXinRecordedDemo
https://github.com/sendtion/XRichText
https://github.com/getlantern/lantern
jitsi
https://github.com/jitsi/jitsi
https://desktop.jitsi.org/
https://jitsi.org/
https://github.com/jitsi/jitsi-android
http://www.trinea.cn/android/android-http-cache/
https://github.com/Trinea/android-demo
http://mirrors.neusoft.edu.cn/
http://mirror.neu.edu.cn/
http://search.maven.org/
https://fir.im/
https://github.com/tifezh/KChartView
https://github.com/Bigkoo/Android-PickerView
https://github.com/crossbario/autobahn-java
https://github.com/Raizlabs/DBFlow
https://github.com/orhanobut/dialogplus
https://github.com/DreaminginCodeZH/Douya
https://github.com/blackfizz/EazeGraph
https://github.com/rockerhieu/emojicon
https://github.com/Manabu-GT/ExpandableTextView
https://github.com/deano2390/FlowTextView
https://github.com/H07000223/FlycoSystemBar
https://github.com/zhihu/Matisse
https://github.com/chrisbanes/PhotoView
```

