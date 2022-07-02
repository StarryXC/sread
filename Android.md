[TOC]



# Android

## Json

```
JsonReader
JsonWriter
```

## FlexboxLayout

```
https://github.com/google/flexbox-layout
implementation 'com.google.android.flexbox:flexbox:3.0.0'

```

## ViewPager

```
ViewPager
PagerAdapter

自定义View: 禁止滑动切换
```

## ProgressBar

```
进度条
ProgressBar
<SeekBar
            android:id="@+id/seekbar"
            android:layout_width="match_parent"
            android:layout_height="40dp"
            android:paddingTop="15dp"
            android:paddingBottom="15dp"
            android:layout_marginLeft="15dp"
            android:layout_marginRight="15dp"
            android:layout_gravity="center"
            android:layout_weight="1"
            android:indeterminateDrawable="@drawable/uvv_star_play_progress_seek"
            android:maxHeight="2dp"
            android:minHeight="2dp"
            android:progressDrawable="@drawable/uvv_star_play_progress_seek"
            android:thumb="@drawable/uvv_seek_dot"
            android:thumbOffset="10dip" />
```

## 异步处理

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

## IPC

```
Messenger
Binder
Handler
Aidl
```

## ClipboardManager

```
剪切板
ClipboardManager
ClipData
ClipData.Item
```

## WebView

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

## DrawerLayout

```
implementation 'androidx.drawerlayout:drawerlayout:'
implementation 'com.android.support:drawerlayout:'


ViewGroup
    DrawerLayout

DrawerLayout.SimpleDrawerListener <-- DrawerLayout.DrawerListener

DrawerLayout
    addDrawerListener DrawerLayout.DrawerListener
        onDrawerSlide
        onDrawerOpened
        onDrawerClosed
        onDrawerStateChanged
    removeDrawerListener
    closeDrawer
        GravityCompat.START
    closeDrawers



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

## 数据加密

```
Base64
    encode
    decode
```

## 布局管理

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

## PowerManager

```
电源管理

PowerManager
WakeLock
```



## 菜单

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

## 倒计时

```
倒计时 CountDownTimer
    滴答 onTick
    完成 onFinish
    启动 start
    取消 cancel
```

## 集合

```
    Collection
        ArraySet # 
    Map
        ArrayMap
    SparseArray
    SparseIntArray
    SparseLongArray
    SparseBooleanArray
```

## 事件处理

```
MotionEvent
KeyEvent

class AskBrainActivity extends Activity {
    @Override
    public boolean dispatchTouchEvent(MotionEvent event) { return super.dispatchTouchEvent(event); }
    @Override
    public boolean onTouchEvent(MotionEvent event) { return super.onTouchEvent(event); }
    @Override
    public boolean onKeyDown(int keyCode, KeyEvent event) { return super.onKeyDown(keyCode, event); }
}
class AskBrainView extends View {
    public AskBrainView(Context context) { super(context); }
    @Override
    public boolean dispatchTouchEvent(MotionEvent event) { return super.dispatchTouchEvent(event); }
    @Override
    public boolean onTouchEvent(MotionEvent event) { return super.onTouchEvent(event); }
}
class AskBrainView extends ViewGroup {
    public AskBrainView(Context context) { super(context); }
    @Override
    protected void onLayout(boolean changed, int l, int t, int r, int b) { }
    @Override
    public boolean dispatchTouchEvent(MotionEvent ev) { return super.dispatchTouchEvent(ev); }
    @Override
    public boolean onInterceptTouchEvent(MotionEvent ev) { return super.onInterceptTouchEvent(ev); }
    @Override
    public boolean onTouchEvent(MotionEvent event) {
        requestDisallowInterceptTouchEvent(true);
        return super.onTouchEvent(event);
    }
}

switch (motionEvent.getAction()) {
    case MotionEvent.ACTION_DOWN:
    case MotionEvent.ACTION_UP:
    case MotionEvent.ACTION_CANCEL:
}
motionEvent.getX();
motionEvent.getY();
motionEvent.getRawX();
motionEvent.getRawY();

MotionEvent
	<coords>
	<action> <pointer> <point: id count coords>

boolean onKeyDown(int keyCode, KeyEvent keyEvent) {
    switch (keyCode) {
        case KeyEvent.KEYCODE_BACK:
        case KeyEvent.KEYCODE_ENTER:
    }
    switch (keyEvent.getAction()) {
        case KeyEvent.ACTION_DOWN:
    }
    return super.onKeyDown(keyCode, keyEvent);
}






```

## 手势

```
GestureDetector
GestureDetector.SimpleOnGestureListener <-- OnGestureListener OnDoubleTapListener OnContextClickListener

GestureDetector.OnGestureListener
    onLongPress

GestureDetector.OnDoubleTapListener

GestureDetector.OnContextClickListener

ScaleGestureDetector
ScaleGestureDetector.SimpleOnScaleGestureListener <-- OnScaleGestureListener

```

## InputMethodManager

```
输入法

InputMethodManager
InputMethodManager # Context.INPUT_METHOD_SERVICE
	showSoftInput # 显示软键盘 InputMethodManager.SHOW_FORCED View.requestFocus
	hideSoftInputFromWindow # 隐藏键盘 (editText.getWindowToken(),0) InputMethodManager.HIDE_NOT_ALWAYS

```

## 日志

```
Log
    d
    getStackTraceString
```

## 偏好设置

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

## 闹钟

```
AlarmManager
Context.ALARM_SERVICE 闹钟

	set # (AlarmManager.RTC_WAKEUP,calendar.getTimeInMillis(),pendingIntent)
		# RTC_WAKEUP RTC

```

## 振荡器

```
Vibrator
Vibrator Context.VIBRATOR_SERVICE
    震动 vibrator
        震动模式

Vibrator android.permission.VIBRATE

Vibrator
    vibrate
        Vibrator vibrator = (Vibrator) context.getSystemService(Context.VIBRATOR_SERVICE);
        //震动模式隔1秒震动1.4秒
        long[] pattern = { 1000, 1400 };
        //震动重复，从数组的0开始（-1表示不重复）
        vibrator.vibrate(pattern, 0);
```

## 账户

```
AccountManager
Account
```

## 共享内存

```
内存文件 MemoryFile
    writeBytes
    close

共享内存 SharedMemory <-- Parcelable Closeable
    mapReadWrite
    mapReadOnly
    unmap

```

## 国际化

```
Locale <-- Cloneable Serializable
    getAvailableLocales // 获取当前系统上的语言列表(Locale列表)
    getDefault
    getLanguage 当前手机系统语言 例如：当前设置的是“中文-中国”，则返回“zh-CN”

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

## 类加载

```
ClassLoader
    BaseDexClassLoader
        DexClassLoader
        PathClassLoader
```

## 网络

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



## 连接管理

```
ConnectivityManager
    getActiveNetworkInfo
    getAllNetworkInfo
    getActiveNetwork
    getAllNetworks
    registerDefaultNetworkCallback
    registerNetworkCallback ConnectivityManager.NetworkCallback
        onAvailable
        onUnavailable
        onLosing
        onLost
    unregisterNetworkCallback

NetworkInfo
    isAvailable
    isConnected
    isConnectedOrConnecting
    getType
        ConnectivityManager.TYPE_MOBILE
    getTypeName
    getSubtype
    getSubtypeName

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

## NetworkStatsManager

```
NetworkStatsManager
NetworkStatsManager networkStatsManager = (NetworkStatsManager) getSystemService(Context.NETWORK_STATS_SERVICE);
networkStatsManager.registerUsageCallback(0, "", 0L, new NetworkStatsManager.UsageCallback() {
    @Override
    public void onThresholdReached(int i, String s) { }
});
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

## 注解

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

## SystemClock

```
SystemClock
    sleep
```

## Build

```
Build
    MANUFACTURER

Build.VERSION
    SDK_INT

Build.VERSION_CODES
    KITKAT
    N
```

## Window

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

## SwipeRefreshLayout

```
implementation 'androidx.swiperefreshlayout:swiperefreshlayout:1.1.0'

SwipeRefreshLayout
	setOnRefreshListener # SwipeRefreshLayout.OnRefreshListener onRefresh
	isRefreshing setRefreshing
	setOnChildScrollUpCallback # SwipeRefreshLayout.OnChildScrollUpCallback canChildScrollUp
	canChildScrollUp
```

```

```



# 数据存储

```
缓存设计

SharedPreferences

SQLiteOpenHelper
Cursor
SQLiteDatabase
    create

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



# 轮波图

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

# 路由

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

```

```



# lbs

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

# 即时通讯

## 环信

```
https://raw.githubusercontent.com/HyphenateInc/Hyphenate-SDK-Android/master/repository | com.hyphenate:hyphenate-sdk:3.3.0

```

```

```

# 推送

## 个推

```
implementation 'cn.jiguang.sdk:jpush:3.3.2'
implementation 'cn.jiguang.sdk:jcore:2.0.1'
```

```

```

```

```

# 数据总线

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

```

```

```

```

```

```

```

```

# ViewPager

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



# 框架搭建

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
```

# WheelView

```
https://github.com/wangjiegulu/WheelView
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

# 图表

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

# 扫码

```
https://github.com/zxing/zxing
https://github.com/yipianfengye/android-zxingLibrary
https://github.com/devilsen/CZXing
api 'com.google.zxing:android-core:3.3.0'
api 'com.google.zxing:core:3.4.0'
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
implementation 'com.android.support:recyclerview-v7:'
implementation 'com.android.support:recyclerview-selection:'

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

```

```

```

```

```

```



# 代码混淆

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

# --------------------------------------------------------------------------
# Addidional for x5.sdk classes for apps

-keep class com.tencent.smtt.export.external.**{
    *;
}

-keep class com.tencent.tbs.video.interfaces.IUserStateChangedListener {
	*;
}

-keep class com.tencent.smtt.sdk.CacheManager {
	public *;
}

-keep class com.tencent.smtt.sdk.CookieManager {
	public *;
}

-keep class com.tencent.smtt.sdk.WebHistoryItem {
	public *;
}

-keep class com.tencent.smtt.sdk.WebViewDatabase {
	public *;
}

-keep class com.tencent.smtt.sdk.WebBackForwardList {
	public *;
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

-keep public class com.tencent.smtt.sdk.WebViewClient {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.DownloadListener {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.WebChromeClient {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.WebChromeClient$FileChooserParams {
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

-keep public class com.tencent.smtt.sdk.WebIconDatabase {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.WebStorage {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.DownloadListener {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.QbSdk {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.QbSdk$PreInitCallback {
	public <fields>;
	public <methods>;
}
-keep public class com.tencent.smtt.sdk.CookieSyncManager {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.Tbs* {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.utils.LogFileUtils {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.utils.TbsLog {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.utils.TbsLogClient {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.CookieSyncManager {
	public <fields>;
	public <methods>;
}

# Added for game demos
-keep public class com.tencent.smtt.sdk.TBSGamePlayer {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.TBSGamePlayerClient* {
	public <fields>;
	public <methods>;
}

-keep public class com.tencent.smtt.sdk.TBSGamePlayerClientExtension {
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

-keep class com.tencent.mtt.MttTraceEvent {
	*;
}

# Game related
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

-keep public class com.tencent.smtt.sdk.TBSGameBaseActivityProxy {
	public protected *;
}

-keep public class com.tencent.smtt.gamesdk.internal.TBSGameServiceClient {
	public *;
}
#---------------------------------------------------------------------------


#------------------  下方是android平台自带的排除项，这里不要动         ----------------

-keep public class * extends android.app.Activity{
	public <fields>;
	public <methods>;
}
-keep public class * extends android.app.Application
{
	public <fields>;
	public <methods>;
}
-keep public class * extends android.app.Service
-keep public class * extends android.content.BroadcastReceiver
-keep public class * extends android.content.ContentProvider
-keep public class * extends android.app.backup.BackupAgentHelper
-keep public class * extends android.preference.Preference

-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}

-keepclasseswithmembers class * {
	public <init>(android.content.Context, android.util.AttributeSet);
}

-keepclasseswithmembers class * {
	public <init>(android.content.Context, android.util.AttributeSet, int);
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
-keep class com.google.gson.stream.** { *; }
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
-keepclasseswithmembernames class * {
    public <init>(android.content.Context, android.util.AttributeSet, int);
}
-keepclassmembers enum * {
    public static **[] values();
    public static ** valueOf(java.lang.String);
}

-keepclassmembers class * extends android.app.Activity {
	public void *(android.view.View);
}

-keepclassmembers class fqcn.of.javascript.interface.for.webview {
   public *;
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


# This is a configuration file for ProGuard.
# http://proguard.sourceforge.net/index.html#manual/usage.html

-dontusemixedcaseclassnames
-dontskipnonpubliclibraryclasses
-verbose
-dontwarn

# Optimization is turned off by default. Dex does not like code run
# through the ProGuard optimize and preverify steps (and performs some
# of these optimizations on its own).
-dontoptimize
-dontpreverify
# Note that if you want to enable optimization, you cannot just
# include optimization flags in your own project configuration file;
# instead you will need to point to the
# "proguard-android-optimize.txt" file instead of this one from your
# project.properties file.

-keepattributes *Annotation*
-keep public class com.google.vending.licensing.ILicensingService
-keep public class com.android.vending.licensing.ILicensingService

# For native methods, see http://proguard.sourceforge.net/manual/examples.html#native
-keepclasseswithmembernames class * {
    native <methods>;
}

# keep setters in Views so that animations can still work.
# see http://proguard.sourceforge.net/manual/examples.html#beans
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

-keep class android.support.v4.** {*;}

-keep class org.xmlpull.** {*;}
-keep class com.baidu.** {*;}
-keep public class * extends com.umeng.**
-keep class com.umeng.** { *; }
-keep class com.squareup.picasso.* {*;}

# bugly
-dontwarn com.tencent.bugly.**
-keep public class com.tencent.bugly.**{*;}

-keep class com.hyphenate.** {*;}
-keep class com.hyphenate.chat.** {*;}
-keep class org.jivesoftware.** {*;}
-keep class org.apache.** {*;}
#另外，demo中发送表情的时候使用到反射，需要keep SmileUtils,注意前面的包名，
#不要SmileUtils复制到自己的项目下keep的时候还是写的demo里的包名
-keep class com.lattu.zhonghuei.im.utils.SmileUtils {*;}

#2.0.9后加入语音通话功能，如需使用此功能的api，加入以下keep
-keep class net.java.sip.** {*;}
-keep class org.webrtc.voiceengine.** {*;}
-keep class org.bitlet.** {*;}
-keep class org.slf4j.** {*;}
-keep class ch.imvs.** {*;}





```

# 单元测试

```

```

```

```

# Jetpack

```
【Foundation 基础组件】

　　【AppCompat】

　　【KTX】

　　【Multidex】

　　【Test】

【Architecture 架构组件】

　　【Lifecycles】

　　【LiveData】

　　【ViewModel】

　　【Room】

　　【DataBinding】

　　【Paging】

　　【Navigation】

　　【WorkManager】

【Behaviour 行为组件】

　　【DownloadManager】

　　【Media & Playback】

　　【Notifications】

　　【Permissions】

　　【Preferences】

　　【Sharing】

　　【Slices】

【UI 组件】

　　【Animation & transitions】

　　　　【Auto】

　　　　【Emoji】

　　　　【Fragment】

　　　　【Layout】

　　　　【Palette】

　　　　【TV】

　　　　【Wear OS by Google】

　　【Components】

　　　　【ViewPager2】

　　　　【LiveDataBus】

　　　　【PagedList】

　　　　【CameraX】

　　　　【RMI】

【Androidx】

　　【ConstraintLayout】

　　【SwipeRefreshLayout】

　　【RecyclerView】

　　【DrawerLayout】

　　【CardView】

　　【ViewPager】

　　【Material Design】

　　【Compats】
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

## ConstraintLayout

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

```
常用类
    Log
    TextUtils
    BuildConfig
    Pair    
    BaseBundle
        Bundle
    SystemClock
    Build # VERSION_CODES VERSION RELEASE系统版本号 | BOARD厂商 MODEL型号 MANUFACTURER
    Uri
        FileProvider

SystemClock.sleep(3000);
Uri.EMPTY
Build.VERSION_CODES.O
Build.VERSION
	SDK_INT
int myPid = Process.myPid();
int myUid = Process.myUid();
int myTid = Process.myTid();
Process.killProcess(Process.myPid());




```

```

```

# 分享

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

# 动画

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

# 对话框

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



# 性能优化

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

# Hook 框架

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

# 插件化

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

# 拼音 TinyPinyin

```
https://github.com/promeG/TinyPinyin
implementation 'com.github.promeg:tinypinyin:2.0.3'
implementation 'com.github.promeg:tinypinyin-lexicons-android-cncity:2.0.3'
```

# 依赖注入

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

