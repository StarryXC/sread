# 框架搭建

```
架构模式
MVC
MVP
MVVM
```

```
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
Glide.with(bannerIV.getContext()).load(activity.getBanner()).into(bannerIV);

ButterKnife
	bind
Unbinder
	unbind

```

```
android.R.color.transparent
```

# AOSP

```
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

Android 源码目录结构

```
Android 系统架构

HAL层，即Hardware Abstract Layer 硬件抽象层

https://source.android.google.cn/
AndroidXRef就是其中一款备受青睐的源码在线阅读网站【网址：http://androidxref.com/】
需要VPN，即需要FQ
Android SDK Search 使用方法】

https://github.com/getlantern/lantern
```

Window # FEATURE_NO_TITLE FEATURE_ACTION_BAR FEATURE_PROGRESS

# 系统权限定义

```
Manifest.permission
	INTERNET

PackageManager
	PERMISSION_GRANTED
```



```
ClipData

Uri.EMPTY
Build.VERSION_CODES.O
Build.VERSION
	SDK_INT
```



```
Intent.ACTION_SCREEN_ON
Intent.ACTION_BOOT_COMPLETED 启动完成
TelephonyManager.ACTION_PHONE_STATE_CHANGED
Manifest.permission.READ_PHONE_STATE

通话状态
去电
Intent.ACTION_NEW_OUTGOING_CALL 去电
Manifest.permission.PROCESS_OUTGOING_CALLS
String phoneNumber = intent.getStringExtra(Intent.EXTRA_PHONE_NUMBER);

电量变化
Intent.ACTION_BATTERY_CHANGED
request
response
int level = intent.getIntExtra("level",0);//电池剩余容量
int scale = intent.getIntExtra("scale",100);//电池总量
int cap = level * 100 / scale;//电池电量

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

网络
监听网络变化
获取网络状态

```

### 预览录像

```
intent.setAction(Intent.ACTION_VIEW);
intent.setDataAndType(Uri.parse("file://path"), "video/mp4");
```

```
intent.addCategory(Intent.CATEGORY_APP_BROWSER);
intent.removeCategory(Intent.CATEGORY_APP_BROWSER);
Set<String> categories = intent.getCategories();

intent.putExtra("key", "value");
intent.getStringExtra("key");

intent.setAction(Intent.ACTION_DIAL);
intent.setData(Uri.parse(""));
intent.setType("video/mp4");
intent.setDataAndType(Uri.parse(""), "video/mp4");
```

# 异步处理/线程通讯

```
JobParameters
JobInfo.Builder # (jobId, jobService) ComponentName(context.getPackageName(), JobService.class.getName())
	setPeriodic # 执行间隔时间
	setRequiredNetworkType # 执行网络类型 JobInfo.NETWORK_TYPE_NONE
	setMinimumLatency # 任务运行最少延迟时间
	setRequiresCharging # 是否充电时执行
	build # JobInfo 获取服务
JobScheduler # getSystemService Context.JOB_SCHEDULER_SERVICE
	schedule # JobInfo
```

## AppWidgetProvider

```
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

public class YicAppWidgetProvider extends AppWidgetProvider {

    @Override
    public void onEnabled(Context context) {
        super.onEnabled(context);
    }

    @Override
    public void onDisabled(Context context) {
        super.onDisabled(context);
    }

    @Override
    public void onReceive(Context context, Intent intent) {
        super.onReceive(context, intent);
        if(intent.getAction().equals("adsfasdfasdf")){
            RemoteViews remoteViews = new RemoteViews(context.getPackageName(),R.layout.activity_attribute_set);
            remoteViews.setTextViewText(R.id.button,"武萧雨");
            AppWidgetManager appWidgetManager = AppWidgetManager.getInstance(context);
            appWidgetManager.updateAppWidget(new ComponentName(context, YicAppWidgetProvider.class),remoteViews);
        } else if("org.lxh.action.MYAPPWIDGET_UPDATE".equals(intent.getAction())){
            AppWidgetManager appWidgetManager = AppWidgetManager.getInstance(context);
            ComponentName componentName = new ComponentName(context,YicAppWidgetProvider.class);
            RemoteViews remoteViews = new RemoteViews(context.getPackageName(),R.layout.activity_main);
            remoteViews.setImageViewResource(android.R.id.home,android.R.id.home);
            remoteViews.setTextViewText(android.R.id.home,"text");
            appWidgetManager.updateAppWidget(componentName,remoteViews);
        }
    }

    //每次更新都调用一次该方法，使用频繁
    @Override
    public void onUpdate(Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds) {
        for(int i=0;i<appWidgetIds.length;i++){
            Log.d("news","aasd:"+appWidgetIds[i]);
            RemoteViews remoteViews = new RemoteViews(context.getPackageName(),R.layout.activity_attribute_set);
//            remoteViews.setOnClickPendingIntent(R.id.button, PendingIntent.getActivity(context,101,new Intent(context,MainActivity.class),0));
            remoteViews.setOnClickPendingIntent(R.id.button, PendingIntent.getBroadcast(context,101,new Intent("adsfasdfasdf"),0));
            appWidgetManager.updateAppWidget(appWidgetIds[i],remoteViews);
        }

        for(int i=0;i<appWidgetIds.length;i++){
            Intent intent = new Intent(context, YicMainActivity.class);
            PendingIntent pendingIntent = PendingIntent.getActivity(context,0,intent,PendingIntent.FLAG_UPDATE_CURRENT);
            pendingIntent = PendingIntent.getBroadcast(context,0,intent,PendingIntent.FLAG_UPDATE_CURRENT);
            RemoteViews remoteViews = new RemoteViews(context.getPackageName(), R.layout.activity_main);
            remoteViews.setOnClickPendingIntent(android.R.id.home,pendingIntent);
            appWidgetManager.updateAppWidget(appWidgetIds[i],remoteViews);

//            appWidgetManager.updateAppWidget(appWidgetIds,remoteViews);
        }

        super.onUpdate(context, appWidgetManager, appWidgetIds);
    }

    @Override
    public void onDeleted(Context context, int[] appWidgetIds) {
        super.onDeleted(context, appWidgetIds);
    }
}
```

## 手势

```
GestureDetector

GestureDetector.OnGestureListener
GestureDetector.OnDoubleTapListener
GestureDetector.SimpleOnGestureListener
GestureDetector.OnContextClickListener
ScaleGestureDetector
ScaleGestureDetector.OnScaleGestureListener
ScaleGestureDetector.SimpleOnScaleGestureListener

Scroller
OverScroller
ViewConfiguration
VelocityTracker
```

# 多媒体编程

```
Canvas
Matrix
Paint

Shader
    LinearGradient
    SweepGradient
    RadialGradient
    ComposeShader

Xfermode
	PorterDuffXfermode
	
Drawable # bounds draw

Point # x y set
Rect # left right top bottom width height offset
RectF
Color # parse valueOf WHITE BLACK TRANSPARENT
ColorMatrix
Matrix # translate rotate scale skew concat values setPolyToPoly

Bitmap # Config | create createScaled compress recycle config byteCount rowBytes density width height
BitmapFactory # resource byteArray file stream resourceStream fileDescriptor | Options justDecodeBounds out sampleSize
BitmapRegionDecoder # newInstance decodeRegion getWidth getHeight isRecycled recycle

Gravity # NO_GRAVITY CENTER FILL CLIP RELATIVE LEFT RIGHT TOP BOTTOM START END

```



```
Paint
    getTextBounds # 获取文字矩形，不包括两边空白 文本适合的最小范围 最小的有界矩形
    getTextWidths # 获取每个字符的宽度 两边增加高级值
    measureText # 测量文字宽度
    getShader setShader
    

StaticLayout # new StaticLayout(text, new TextView(getContext()).getPaint(), boundedWidth , Layout.Alignment.ALIGN_NORMAL, 1.0f, 0.0f, false);
	getHeight
	getLineCount
	getLineWidth
	getDesiredWidth
```

## 相机

### Camera

```
Manifest.permission.CAMERA
Camera
	getParameters setParameters
	setPreviewDisplay # Camera.PreviewCallback onPreviewFrame
	autoFocus # Camera.AutoFocusCallback onAutoFocus
	startPreview stopPreview # 开始停止预览
	takePicture # 照相
		# Camera.ShutterCallback onShutter
		# Camera.PictureCallback onPictureTaken (byte[] data, Camera camera)
	open
	release
	setDisplayOrientation # 90 Portrait mode
	lock unlock
	getNumberOfCameras # 摄像头数目 判断手机是否存在摄像头 context.getPackageManager().hasSystemFeature(PackageManager.FEATURE_CAMERA) ? 1 : 0;
	getCameraInfo # Camera.CameraInfo
	setOneShotPreviewCallback # Camera.PreviewCallback onPreviewFrame
Camera.CameraInfo
	CAMERA_FACING_FRONT CAMERA_FACING_BACK
	facing
	orientation
Camera.Parameters
	<flash mode>
	getSupportedPreviewSizes # 预览尺寸 预览像素 Camera.Size width height
	getSupportedPictureSizes # Camera.Size width height
	getPictureSize setPictureSize # 设置照片的大小
	getSupportedPreviewFpsRange # 预览帧率
	getSupportedPreviewFormats # 颜色格式
	getPreviewFpsRange setPreviewFpsRange
	getPreviewSize setPreviewSize # 设置预览照片的大小
	getPreviewFrameRate setPreviewFrameRate # 帧率 每秒几帧
	getPictureFormat setPictureFormat # 设置照片的输出格式 PixelFormat.JPEG
	getPreviewFormat setPreviewFormat # ImageFormat.NV21 YV12
	getFlashMode setFocusMode # 聚焦 Camera.Parameters.FOCUS_MODE_CONTINUOUS_VIDEO
	getFlashMode setFlashMode # Camera.Parameters.FLASH_MODE_AUTO
		# Camera.Parameters.FLASH_MODE_TORCH 打开
		# Camera.Parameters.FLASH_MODE_OFF 关闭
	getWhiteBalance setWhiteBalance # 白平衡 Camera.Parameters.WHITE_BALANCE_AUTO
	getSceneMode setSceneMode # 闪光灯 Camera.Parameters.SCENE_MODE_AUTO
	set # 照片质量 ("jpeg-quality", 85)
	flatten unflatten # reset
	setRotation
SurfaceView
	getHolder
```

### CameraManager

```
check Manifest.permission.CAMERA
api Build.VERSION_CODES.LOLLIPOP

CameraManager # Context.CAMERA_SERVICE
	getCameraIdList
	getCameraCharacteristics # cameraId
	openCamera # CameraDevice.StateCallback onOpened onDisconnected onError

CameraCharacteristics
	get # CameraCharacteristics.LENS_FACING
		# CameraMetadata.LENS_FACING_BACK LENS_FACING_FRONT LENS_FACING_EXTERNAL

CameraDevice
	close
```

## 音视频

```
MediaPlayer
SoundPool # Builder OnLoadCompleteListener | load unload play pause resume stop release
AudioManager # streamVolume MUSIC ALARM RING NOTIFICATION SYSTEM VOICE_CALL DTMF mode NORMAL speakerphoneOn
```

```
MediaRecorder
MediaRecorder.AudioSource
MediaRecorder.AudioEncoder
MediaRecorder.OutputFormat
MediaRecorder.OnErrorListener
MediaRecorder.OnInfoListener

MediaRecorder
	setCamera
	setVideoSource # MediaRecorder.VideoSource.CAMERA
	setVideoEncoder # MediaRecorder.VideoEncoder.H264
	setVideoFrameRate # 20
	setVideoSize
	setPreviewDisplay # surfaceHolder.getSurface()
	setAudioSource # MediaRecorder.AudioSource.DEFAULT MIC麦克风
	setAudioEncoder # MediaRecorder.AudioEncoder.AAC AMR_NB
	setAudioChannels # 1
	setAudioSamplingRate # 8000
	setAudioEncodingBitRate # 64
	setOutputFile # 
	setOutputFormat # MediaRecorder.OutputFormat.MPEG_4 AMR_NB
	setMaxDuration # 30000
	setOrientationHint # 90
	reset
	prepare release
	start stop
```

# Proguard 代码混淆

```
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
```

# [Jetpack](Jetpack)

```
compile 'com.afollestad.material-dialogs:core:0.8.5.9'
compile 'com.kyleduo.switchbutton:library:1.4.1'
compile 'com.google.android.gms:play-services-maps:8.4.0'
```



# Intent Call

```
            Intent localIntent = new Intent();
            localIntent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
            if (Build.VERSION.SDK_INT >= 9) {
                localIntent.setAction("android.settings.APPLICATION_DETAILS_SETTINGS");
                localIntent.setData(Uri.fromParts("package", context.getPackageName(), null));
            } else if (Build.VERSION.SDK_INT <= 8) {
                localIntent.setAction(Intent.ACTION_VIEW);
                localIntent.setClassName("com.android.settings", "com.android.settings.InstalledAppDetails");
                localIntent.putExtra("com.android.settings.ApplicationPkgName", context.getPackageName());
            }
            context.startActivity(localIntent);
```

# Views

## 

```
    ActionBar actionBar = getSupportActionBar();
            if (actionBar != null) {
                actionBar.show();
```

### MotionEvent

```
MotionEvent
	<coords>
	<action> <pointer> <point: id count coords>
```



### Scroller

```
Scroller # startScroll computeScrollOffset currX currY
	OverScroller
VelocityTracker
ViewConfiguration # get touchSlop minimumFlingVelocity
View.MeasureSpec # makeMeasureSpec size mode EXACTLY
```

### NestedScrolling

```
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

### Spans

```
SpannableString spannableString = new SpannableString("");
ForegroundColorSpan foregroundColorSpan = new ForegroundColorSpan(0x111111);
spannableString.setSpan(foregroundColorSpan, 1, 20, Spanned.SPAN_EXCLUSIVE_INCLUSIVE);;

SpannableStringBuilder spannableStringBuilder = new SpannableStringBuilder();
spannableStringBuilder.append("append");
```

### Editable

```
Editable
    append insert delete replace clear
    clearSpans
	getFilters setFilters
```

### GridView

```
<GridView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:listSelector="#00000000"
    android:numColumns="7"
    android:scrollbars="none"
    android:verticalSpacing="5dp"
    android:gravity="center"
    android:fadingEdge="none"
    />
GridView
    @Override
    public void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        int expandSpec = MeasureSpec.makeMeasureSpec(Integer.MAX_VALUE >> 2, MeasureSpec.AT_MOST);
        super.onMeasure(widthMeasureSpec, expandSpec);
    }
```

## 

```
FrameLayout
	
	
LinearLayout
	
```

## Scrolls

```
ScrollView
	# android:scrollbars none
	# android:fillViewport true
HorizontalScrollView
NestedScrollView
	onScrollChanged
	onNestedPreScroll
```

## 

```
SurfaceView
	GLSurfaceView

SurfaceView
	<holder>
	getHolder
	
	setFixedSize
	addCallback # SurfaceHolder.Callback surfaceChanged surfaceDestroyed

SurfaceHolder
	<callback>
	setType # SurfaceHolder.SURFACE_TYPE_PUSH_BUFFERS
	setKeepScreenOn
	lockCanvas
	unlockCanva
```

## TabHost

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



# Resources

```
:资源访问
<package>.R.<type>.<name> # 代码访问
@[package:]<type>/<name> # XML 访问
	layout res/layout layout.xml
	drawable res/drawable drawable.xml
	color res/color color.xml
	anim res/anim anim.xml
	animator res/animator animator.xml 动画资源
	interpolator res/anim interpolator.xml
	menu res/menu menu.xml 菜单资源
	raw
	xml
	font res/font font.xml 字体资源
	res/values integer bool dimen color string style id
		array # int[] string[] array
		Quantity Strings (Plurals)
:资源适配目录
mipmap drawable
	-mdpi -hdpi -xhdpi -xxhdpi -xxxhdpi
	-anydpi-v26
	-v24 -v26
raw
layout
	-sw550dp-large
values
	-large -xlarge
	-en -zh-rTW
	-w820dp -sw600dp -sw720dp-land
	-v21
	-night

Resources
	<configuration>
Configuration
	<orientation> 竖屏拍照时，需要设置旋转90度，否者看到的相机预览方向和界面方向不相同
AssetManager # Context.getAssets assets/
	open
TypedArray
TypedValue
AnimationUtils # Animation
AnimatorInflater
LayoutInflater
```

## Layout

```
:布局资源
<merge>
	xmlns:tools="http://schemas.android.com/tools"
	tools:context=".MainActivity"
    tools:showIn="@layout/activity_main"
    tools:parentTag="android.widget.FrameLayout"
<include>
	layout
<View> <requestFocus /> </View>

LayoutInflater # Activity.getLayoutInflater Context.LAYOUT_INFLATER_SERVICE
	from
	inflate
View
	inflate
```

## Drawable

```
ResourcesCompat.getDrawable


//This evaluator can be used to perform type interpolation between integer values that represent ARGB colors.
//这个求值器用来执行计算用整形表示的颜色的差值
ArgbEvaluator argbEvaluator = new ArgbEvaluator();
int   startColor = ActivityCompat.getColor(MainActivity.this,R.color.colorPrimary);
int   endColor   = Color.WHITE;

//根据fraction计算出开始和结束中间的色值
int calcColor = (int) argbEvaluator.evaluate(fraction, startColor, endColor);

ColorFilter colorFilter = new PorterDuffColorFilter(calcColor, PorterDuff.Mode.SRC_IN);

iv1Drawable.setColorFilter(colorFilter);


Drawable mutate
	ColorDrawable
	GradientDrawable # 渐变 线性渐变 发散渐变 平铺渐变
	DrawableContainer
		LevelListDrawable
		StateListDrawable
		AnimationDrawable
	LayerDrawable
		TransitionDrawable
	DrawableWrapper
		ScaleDrawable
		ClipDrawable
		InsetDrawable
	BitmapDrawable
	NinePatchDrawable

Drawable
	setBounds
	draw
```

### GradientDrawable

```
<shape> # GradientDrawable
	android:shape # rectangle ring
<corners>
	android:radius
	android:topLeftRadius android:topRightRadius
	android:bottomLeftRadius android:bottomRightRadius
<gradient> # 渐变效果
	android:angle # 0-360
	android:centerX android:centerY # 50%
	android:startColor android:centerColor android:endColor
	android:type # sweep radial
	android:useLevel # true
	android:gradientRadius
<padding> # 内边距 android:left android:right android:top android:bottom
<size> # 区域大小 android:width android:height
<solid> # 背景颜色 会覆盖gradient android:color
<stroke> # 边框效果
	android:width
	android:color
	android:dashGap android:dashWidth
```

### LevelListDrawable

```
<level-list> # LevelListDrawable
<item>
	android:drawable
	android:minLevel android:maxLevel # int
```

### StateListDrawable

```
<selector> # StateListDrawable
	android:constantSize
	android:dither
	android:variablePadding
	android:visible
<item>
	android:drawable
	android:state_pressed
```

### LayerDrawable

```
<layer-list> # LayerDrawable
<item>
	android:id
	android:drawable # >V< shape bitmap
	android:left android:right android:top android:bottom

<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android" >
    <item android:id="@android:id/progress">
        <clip>
            <shape> <solid android:color="#0071f8"/> </shape>
        </clip>
    </item>
    <item android:left="5dp" android:top="5dp">
        <shape> <solid android:color="#60000000"/> </shape>
    </item>
    <item android:bottom="5dp" android:right="5dp">
        <shape> <solid android:color="#000000"/> </shape>
    </item>
</layer-list>
```

### AnimationDrawable

```
<animation-list> # AnimationDrawable
	android:oneshot
<item>
	android:drawable
	android:duration
```

### ScaleDrawable

```
<scale> # ScaleDrawable
	android:drawable
	android:scaleGravity # center
	android:scaleWidth android:scaleHeight # 50%
```

### ClipDrawable

```
<clip> # ClipDrawable 裁剪
	android:drawable
	android:clipOrientation # vertical
	android:gravity # center
```

### InsetDrawable

```
<inset> # InsetDrawable 嵌入
	android:drawable # 
	android:inset
	android:insetLeft android:insetRight android:insetTop android:insetBottom

```

### TransitionDrawable

```
<transition> # TransitionDrawable
<item>
	android:drawable
	android:id
	android:left android:right android:top android:bottom

```

### BitmapDrawable

```
<bitmap> # BitmapDrawable Bitmap .png / .jpg / .gif
	android:src
	android:antialias
	android:dither
	android:filter
	android:gravity # center
	android:mipMap
	android:tileMode # clamp mirror 镜像平铺效果
```

### NinePatchDrawable

```
<nine-patch> # NinePatchDrawable .9.png
	android:src
	android:dither
```

### VectorDrawable

```
<vector>
	android:width android:height # dimen
	android:viewportWidth android:viewportHeight # int
<path>
	android:fillColor
	android:pathData
	android:strokeWidth
	android:strokeColor
	android:fillType # nonZero evenOdd
<aapt:attr> # xmlns:aapt="http://schemas.android.com/aapt"
	name # android:fillColor
<gradient>
	android:startX android:endX # 78.5885
	android:startY android:endY # 78.5885
	android:type # linear
<item>
	android:color
	android:offset # 0.0 1.0
```

### AdaptiveIconDrawable

```
<adaptive-icon> # AdaptiveIconDrawable mipmap
<background> # android:drawable
<foreground> # android:drawable
```

## ColorStateList

```
<selector> # ColorStateList 颜色状态列表
<item>
	android:color
    android:state_selected
    android:state_enabled
    android:state_window_focused
    android:state_pressed
    android:state_activated
    android:state_checkable
    android:state_checked
    android:state_active
    android:state_focused
    android:state_first
    android:state_middle
    android:state_last
    android:state_single
    android:state_hovered
    android:state_drag_hovered
    android:state_drag_can_accept
    android:state_accelerated
```

## Animation

### View

```
Animation 补间动画
	TranslateAnimation 平移
	RotateAnimation 旋转
	AlphaAnimation 渐变
	ScaleAnimation 缩放
	AnimationSet
AnimationDrawable 帧动画 res/drawable/
LayoutAnimationController
	GridLayoutAnimationController
PropertyValuesHolder
TypeEvaluator
	IntEvaluator IntArrayEvaluator
	FloatEvaluator FloatArrayEvaluator
	ArgbEvaluator
	PointFEvaluator RectEvaluator
TimeInterpolator
	Interpolator # 定义动画变化速率
BaseInterpolator
	LinearInterpolator # @android:anim/linear_interpolator 匀速
	DecelerateInterpolator
	AccelerateInterpolator
	AccelerateDecelerateInterpolator # @android:anim/accelerate_decelerate_interpolator 先加速后减速
	OvershootInterpolator AnticipateOvershootInterpolator
	BounceInterpolator @android:anim/bounce_interpolator

<set> # anim.xml
	android:shareInterpolator
	android:duration # 动画时长，单位秒
	android:interpolator # 插值器 @android:anim/linear_interpolator
<translate> # singleable
	android:fromXDelta android:toXDelta # 100%p -100%p
	android:fromYDelta android:toYDelta
	android:duration # 200 毫秒
<alpha> # singleable
	android:fromAlpha android:toAlpha # 0.0~1.0
	android:duration
<scale> # singleable
	android:fromXScale android:toXScale # 0.9 1
	android:fromYScale android:toYScale
	android:pivotX android:pivotY # 50%
	android:duration
<rotate> # singleable
	android:fromDegrees android:toDegrees # 45~90
	android:pivotX android:pivotY # 0.5

<layoutAnimation>
	android:delay # 0.5
	android:animationOrder # random
	android:animation # 动画资源

<accelerateInterpolator> # AccelerateInterpolator @android:anim/accelerate_interpolator
	android:factor # 1.5
	加速
<anticipateInterpolator> # AnticipateInterpolator @android:anim/anticipate_interpolator
	android:tension # 1.5
<anticipateOvershootInterpolator> # AnticipateOvershootInterpolator @android:anim/anticipate_overshoot_interpolator
	android:tension # 1.5
	android:extraTension # 1.5
<cycleInterpolator> # CycleInterpolator @android:anim/cycle_interpolator
	android:cycles # 5
	速率正弦曲线变化
<decelerateInterpolator> # DecelerateInterpolator @android:anim/decelerate_interpolator
	android:factor # 1.5
	减速
<overshootInterpolator> # OvershootInterpolator @android:anim/overshoot_interpolator
	android:tension="1.5

AnimationUtils
	loadAnimation
Animation
	setAnimationListener # Animation.AnimationListener onAnimationStart onAnimationEnd onAnimationRepeat
AnimationSet
	addAnimation
ViewPropertyAnimator # view.animate()
	x # x 是相对父控件
	translationX # translationX 是相对自己
	setDuration
	start
```

### Property

```
Animator # 属性动画
	AnimatorSet
	ValueAnimator
		ObjectAnimator
		TimeAnimator
Keyframe
PropertyValuesHolder

Animator.AnimatorListener
Animator.AnimatorPauseListener
ValueAnimator.AnimatorUpdateListener

<set>
	android:ordering # sequentially
<animator> # ValueAnimator
	android:duration
	android:interpolator # @android:interpolator/linear
	android:repeatCount # infinite
	android:repeatMode # restart
	android:startOffset # 0
	android:valueFrom android:valueTo
	android:valueType # colorType
<objectAnimator>
	android:propertyName
	android:duration
	android:valueFrom android:valueTo
	android:valueType # intType
	android:startOffset
	android:repeatMode # restart
	android:repeatCount # infinite
	android:interpolator # @android:interpolator/linear
	android:pathData # 1,2,2,3,5
	android:propertyXName android:propertyYName
<propertyValuesHolder>
	android:valueFrom android:valueTo
	android:valueType
	android:propertyName

AnimatorSet
	playTogether
AnimatorInflater
	loadAnimator
Animator
	addListener # Animator.AnimatorListener onAnimationStart onAnimationEnd onAnimationCancel onAnimationRepeat
	addPauseListener # Animator.AnimatorPauseListener onAnimationPause onAnimationResume
ValueAnimator
	ofInt
	ofPropertyValuesHolder
	addUpdateListener # ValueAnimator.AnimatorUpdateListener onAnimationUpdate
```

## Menu

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
```

## Xml

```
<appwidget-provider>
	android:minHeight android:minWidth
	android:updatePeriodMillis # 6000 毫秒
	android:initialLayout # layout

<paths>
<external-path>
	path # . 目录
	name # external_storage_root
```

## Font

```
<font-family>
<font>
```

## Values

```
<resources> # 值资源
<integer> # name integers.xml
<integer-array> # name <item>
<dimen> # name dimens.xml 尺寸资源 尺寸计量 dp sp px pt mm in
<color> # name colors.xml transparent white
<bool> # name bools.xml
<string> # name strings.xml
<string-array> # name <item>
<plurals> # name
	<item> # quantity zero one two few many other
<array> # name <item>
<item>
	name # 
	type # id
	format # reference
<declare-styleable> # name
<attr>
	name
	format
<enum>
	name
	value

Resources # Context.getResources	
	getResourceName
	getResourcePackageName getResourceTypeName getResourceEntryName
	getIdentifier # ("name", "id", context.getPackageName())
	getInteger getIntArray
	getDimension getDimensionPixelOffset getDimensionPixelSize
	getColor
	getBoolean
	getString getStringArray
	getText getTextArray
	getDisplayMetrics
	getDrawable
TypedValue
	COMPLEX_UNIT_DIP
	applyDimension
DisplayMetrics
	widthPixels heightPixels
Context
	obtainStyledAttributes # attrs styleable
TypedArray
	getString
	getBoolean
	getInt getInteger getFloat
	getDimension getDimensionPixelSize
	getFraction # string
	getColor
	recycle
```

### Styles

```
<appTheme>

<style> # name parent styles.xml 样式/主题资源
<item> # name
wrap_wrap # layout_width layout_height
	tv_15 # android:textSize 15sp
match_wrap # layout_width layout_height
	match_wrap_lrt_885 # layout_marginLeft layout_marginRight layout_marginTop
match_match # layout_width layout_height
weight_wrap # layout_width 0 layout_height wrap_content layout_weight 1

Theme.AppCompat.Light.NoActionBar
Theme.AppCompat.Light.DarkActionBar
android:Theme.Light
android:Theme.Holo.Light
android:Theme.Holo.Light.DarkActionBar
android:Theme.Translucent.NoTitleBar.Fullscreen
android:windowTranslucentStatus true
android:statusBarColor @color/white

    <!-- Base application theme. -->
    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>

windowActionBar
windowNoTitle

```

# Managers

## AlarmManager

```
AlarmManager # Context.ALARM_SERVICE 闹钟

ActivityManager # ACTIVITY_SERVICE
	set # (AlarmManager.RTC_WAKEUP,calendar.getTimeInMillis(),pendingIntent)
		# RTC_WAKEUP RTC


```

## TelephonyManager

```
TelephonyManager # Context.TELEPHONY_SERVICE
	getDeviceId
	listen # PhoneStateListener.LISTEN_CALL_STATE PhoneStateListener.LISTEN_NONE

PhoneStateListener
	onCallStateChanged # state
		# TelephonyManager.CALL_STATE_IDLE 挂断状态
		# TelephonyManager.CALL_STATE_OFFHOOK 接听或拨打状态
		# TelephonyManager.CALL_STATE_RINGING 响铃状态
	LISTEN_CALL_STATE # 监听通话
	LISTEN_NONE # 取消监听
```

## ActivityManager

```
ActivityManager
	getRunningAppProcesses
	clearApplicationUserData
	getMemoryInfo
    getProcessesInErrorState
    getRunningTasks # 获得系统里正在运行的所有进程
    getRunningServices
    getRecentTasks(20, 1) # RECENT_WITH_EXCLUDED=1,RECENT_IGNORE_UNAVAILABLE=2
    getProcessMemoryInfo(new int[]{Process.myPid()});
ActivityManager.RunningAppProcessInfo
	processName pid uid
    lastTrimLevel lru pkgList
    importance importanceReasonCode importanceReasonPid importanceReasonComponent
    IMPORTANCE_FOREGROUND
ActivityManager.MemoryInfo
	availMem # 可用内存
    lowMemory # 最低内存
    threshold # 临界值，达到这个值，进程就要被杀死
    totalMem # 总内存
ActivityManager.ProcessErrorStateInfo
	condition # 进程进入的条件
    crashData # crash数据
    longMsg # 对条件condition的描述
    processName
    pid
    shortMsg
    stackTrace # 堆栈追踪到的信息
    tag # activity名是否与错误有关联
    uid
    describeContents # 数据包裹的描述
ActivityManager.RunningTaskInfo
    baseActivity # 任务主activity名
    description # 任务的描述
    taskInfo.id # 任务的id号
    numActivities # 该任务的activity的数量
    numRunning # 当前活动的activity数量
    thumbnail
    topActivity # 当前活动activity中处于最顶端的activity
    describeContents # 描述文本
ActivityManager.RunningServiceInfo
	service # 服务组件名
    clientPackage
    process
    activeSince # 开始时间
    clientCount # 连接到服务的客户数量
    clientLabel # 标识特殊服务
    crashCount # 运行过程中奔溃的次数
    flags
    lastActivityTime # 最后服务结束的时间
    restarting # 如果非0,代表服务没启动,计划启动
    foreground # 是否处于处于最前面的服务状态
    started # 服务以后已经开启
    pid
    uid
ActivityManager.RecentTaskInfo
	baseIntent # 触发该任务的Intent
    description # 描述性文字
    id # 如果是运行中的TASK，唯一标识该任务，如果不是，为-1
    origActivity # 触发任务的第一个activity
    persistentId # 当前任务的唯一标识
```

## InputMethodManager

```
InputMethodManager # Context.INPUT_METHOD_SERVICE
	showSoftInput # 显示软键盘 InputMethodManager.SHOW_FORCED View.requestFocus
	hideSoftInputFromWindow # 隐藏键盘 (editText.getWindowToken(),0) InputMethodManager.HIDE_NOT_ALWAYS
```

## 

```
Window # activity.getWindow() dialog.getWindow()
	setFormat # PixelFormat.RGBA_8888
	setSoftInputMode # 
		# WindowManager.LayoutParams.SOFT_INPUT_STATE_HIDDEN
	setStatusBarColor setNavigationBarColor
	getCurrentFocus getDecorView findViewById
	getAttributes setAttributes
	setBackgroundDrawable setBackgroundDrawableResource
	hasFeature requestFeature
	setFeatureDrawable setFeatureDrawableAlpha setFeatureDrawableResource setFeatureDrawableUri
	setFeatureInt
	clearFlags addFlags setFlags
		# WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON 高亮
	setType # 
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
```

## DownloadManager

```
Context.DOWNLOAD_SERVICE

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

### AndroidManifest.xml

```
<application>
	android:usesCleartextTraffic # true <!-- android 9.0 强制使用https的问题 -->
	android:allowBackup
<uses-library>
	<!-- android 9.0 使用 httpclient -->
	android:name="org.apache.http.legacy" android:required="false"

	        <!-- android 7.0 访问file -->
        <provider
            android:name="android.support.v4.content.FileProvider"
            android:authorities="${applicationId}.fileProvider"
            android:grantUriPermissions="true"
            android:exported="false">
            <meta-data
                android:name="android.support.FILE_PROVIDER_PATHS"
                android:resource="@xml/file_paths" />
        </provider>



androidx.core.content.FileProvider provider
	meta-data {android.support.FILE_PROVIDER_PATHS: @xml/bdp_update_filepaths}
appwidget
	meta-data {android.appwidget.provider: @xml/appwidget_info}
	action android.appwidget.action.APPWIDGET_UPDATE

JobService
	permission="android.permission.BIND_JOB_SERVICE"
	exported="true"
android.permission.INTERNET
android.intent.action.MAIN
android.intent.category.LAUNCHER
android.intent.action.USER_PRESENT
android.intent.action.BOOT_COMPLETED
android.intent.action.PACKAGE_REMOVED

            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />

                <data android:scheme="http"
                    android:host="baidu.com"
                    android:mimeType="image/jpeg"/>
            </intent-filter>
```

### Permissions

```
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
```

### Actions

```
Intent.ACTION_MAIN android.intent.action.MAIN
android.intent.action.VIEW
android.intent.action.GET_CONTENT

Intent.ACTION_BATTERY_CHANGED
boolean onBatteryNow = intent.getIntExtra(
						BatteryManager.EXTRA_PLUGGED, -1) <= 0;
```

### Categorys

```
Intent.CATEGORY_LAUNCHER android.intent.category.LAUNCHER
android.intent.category.DEFAULT
android.intent.category.OPENABLE
android.intent.category.BROWSABLE
```

### Features

```
android.hardware.camera
android.hardware.camera.autofocus
android.hardware.camera.front
android.hardware.camera.front.autofocus
```

### MimeTypes

```
image/jpeg
```

### Schemes

```
http
```



# Providers

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
```

## MediaStore

```
MediaStore.Audio.AudioColumns
ALBUM string 缩略图
TITLE string 标题

MediaStore.Audio.Media
EXTERNAL_CONTENT_URI

```

## Settings

```
Uri: CallLog.Calls.CONTENT_URI 通话记录 Manifest.permission.READ_CALL_LOG
CallLog.Calls.NUMBER
CallLog.Calls.DATE
CallLog.Calls.TYPE
CallLog.Calls.DURATION
```

# CMakeLists.txt

```
ndk
	jni
		Android.mk
		Application.mk
```

```
cmake_minimum_required(VERSION 3.4.1)
#设置变量
set(OpenCV_DIR E:/opencv-3.4.2-android-sdk/OpenCV-android-sdk/sdk/native/jni)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11") #支持-std=gnu++11
find_package(OpenCV REQUIRED)

#判断编译器类型,如果是gcc编译器,则在编译选项中加入c++11支持
if(CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")
    message(STATUS "optional:-std=c++11")
endif(CMAKE_COMPILER_IS_GNUCXX)

target_include_directories(
                            dxtx
                            PRIVATE
                            E:/opencv-3.4.2-android-sdk/OpenCV-android-sdk/sdk/native/jni/include
                            src/main/jni/include
                            )

add_library( 
             native-lib # 名称
             
             SHARED # 类型
             
             src/main/cpp/JNIc.cpp # 原文件路径
             src/main/cpp/JNIc.h
              )

add_library(freetype STATIC IMPORTED)
set_target_properties(freetype  PROPERTIES IMPORTED_LOCATION
                       ${CMAKE_SOURCE_DIR}/src/main/obj/local/${ANDROID_ABI}/libft2.a)

find_library( # 名称
              log-lib
              # 库名称
              log )
include_directories(src/main/jniLibs/include)
target_link_libraries( # 目标库
                       native-lib
                       # 链接库
                       ${log-lib} )
target_link_libraries(
                        dxtx freetype
                       ${OpenCV_LIBS}
                       ${Log-lib} )
```

```
${CMAKE_SOURCE_DIR}


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

# Android.mk

```
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
```

```
Android.mk
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
```

```
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
```

# Application.mk

```
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
```

```
LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)
LOCAL_MODULE := freetype2-prebuilt
LOCAL_SRC_FILES := ../obj/local/$(TARGET_ARCH_ABI)/libfreetype2-static.a
include $(PREBUILT_STATIC_LIBRARY)
```

```
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
```

# Alibaba

```
ARouter # https://github.com/alibaba/ARouter | api compiler | AROUTER_MODULE_NAME javaCompile annotationProcessor arguments kapt arguments arg

ARouter # init inject | build withString navigation
RouteType # id className | ACTIVITY SERVICE BOARDCAST CONTENT_PROVIDER FRAGMENT PROVIDER METHOD UNKNOWN
RouteMeta
	Postcard # withObject navigation
IProvider # init
	InterceptorService # doInterceptions
@Route # RoutePath
@Autowired # 自动装配

Fastjson # fastjson https://github.com/alibaba/fastjson
JSON # parse
JSONObject
```



# Tencent

## QMUI

```
com.qmuiteam # https://qmuiteam.com/android
	qmui:1.2.0
	arch:0.3.1
```

## Tinker

```
com.tencent.tinker # https://github.com/Tencent/tinker
	tinker-patch-gradle-plugin:1.9.14.19 # classpath 低版本编译不通过
com.tencent.tinker.patch # plugin
com.tencent.tinker
	tinker-android-anno:1.9.14.19 # provided
	tinker-android-lib:1.9.14.19 # compile


```

## MMKV

```
com.tencent # https://github.com/Tencent/MMKV
	mmkv:1.2.11 # 静态链接
	mmkv-shared:1.2.11 # 动态链接
```

# Google

```
Gson # https://github.com/google/gson | gson
Gson # toJson fromJson
TypeToken # type rawType

FlexboxLayout # https://github.com/google/flexbox-layout | flexbox

ExoPlayer # https://github.com/google/ExoPlayer | exoplayer core dash ui

AutoService # | auto-common auto-service
```

```
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

# JakeWharton

```
ButterKnife # https://github.com/JakeWharton/butterknife | butterknife compiler 10.2.3 7.0.1

@BindView # Int Float Bool String Color Dimen Anim Font Bitmap Array Drawable
@OnClick # LongClick Touch CheckedChanged FocusChange PageChange TextChanged ItemClick ItemLongClick ItemSelected

ButterKnife
Unbinder
```

# Square

```
OkHttp # https://square.github.io/okhttp/ | okhttp

Interceptor.Chain
chain.connection(),
chain.proceed(request);

FormBody # Builder add build
Request # newBuilder | Builder url get post header build
RequestBody
Response # newBuilder | body
ResponseBody # source header contentLength contentType close string bytes byteStream charStream
OkHttpClient # newCall newBuilder | Builder timeout interceptor build
Call # cancel clone execute enqueue | Callback onFailure onResponse
Interceptor
WebSocket
WebSocketListener

File file = new File(URI.create(choosedUri.toString()));
MediaType MEDIA_TYPE_PNG = MediaType.parse("image/png");
RequestBody requestBody = new MultipartBody.Builder().setType(MultipartBody.FORM)
.addFormDataPart("avatar","avatar",RequestBody.create(MEDIA_TYPE_PNG,file)).build();


http 断点下载

HttpLoggingInterceptor # level | Level.BODY

Okio # https://square.github.io/okio/

Retrofit # https://square.github.io/retrofit/ | retrofit adapter converter

Picasso # https://github.com/square/picasso | picasso

LeakCanary # https://github.com/square/leakcanary/ | leakcanary-android debugImplementation

JavaPoet # https://github.com/square/javapoet | javapoet
```

# ReactiveX

```
RxJava # https://github.com/ReactiveX/RxJava | rxjava
RxAndroid # https://github.com/ReactiveX/RxAndroid | rxandroid

Disposable # dispose
ObservableSource
Observable # just iterable map flatMap filter zipWith toList subscribe materialize subscribeOn observeOn
Schedulers # io computation newThread from
AndroidSchedulers # mainThread
Function # apply
Consumer # accept
Predicate # test
Observer # next error complete subscribe
Subscriber # next error complete subscribe
ObservableOnSubscribe # subscribe
Emitter # next error complete
ObservableEmitter # disposed serialize cancellable
Cancellable # cancel
Action # run
Function # 3 4 5 6 7 8 9 | apply
```

# Hook

## 

```
Xposed # compileOnly api 53:sources 82 | assets/xposed_init

IXposedHookLoadPackage # handleLoadPackage
XC_LoadPackage.LoadPackageParam classLoader
XposedHelpers # findAndHookMethod
XC_MethodHook # beforeHookedMethod afterHookedMethod
MethodHookParam # args setResult
XposedBridge # log
```

```
Glide # https://github.com/bumptech/glide | glide compiler 4.12.0 4.7.1
GlideModule

Realm # realm-gradle-plugin realm-android

GreenDAO # https://github.com/greenrobot/greenDAO | greendao-gradle-plugin org.greenrobot.greendao | greendao schemaVersion daoPackage targetGenDir targetGenDirTest generateTests


EventBus # https://github.com/greenrobot/EventBus | eventbus
EventBus # default register post
Subscribe # threadMode priority

RecyclerView.ItemDecoration


```

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

CallLog.Calls.CONTENT_URI # 查询通话记录的URI
CallLog.Calls.CACHED_NAME # String 姓名：通话记录的联系人
CallLog.Calls.NUMBER # String 号码：通话记录的电话号码
CallLog.Calls.TYPE # Int 通话类型：1.呼入; 2.呼出; 3.未接
CallLog.Calls.DATE # Long 通话时间 拨打时间：通话记录的日期
CallLog.Calls.DURATION # Int 通话时长 值为多少秒
CallLog.Calls.DEFAULT_SORT_ORDER # 按照时间逆序排列，最近打的最先显示

ContactsContract.CommonDataKinds.Phone.CONTENT_URI # URI
ContactsContract.CommonDataKinds.Phone.NUMBER # String 手机号
ContactsContract.PhoneLookup.DISPLAY_NAME # String 姓名
```

# Chart

```
KChartView # https://github.com/tifezh/KChartView

Charts # https://github.com/limccn/Android-Charts

IndicatorSeekBar # https://github.com/warkiz/IndicatorSeekBar

PullToRefresh # https://github.com/chrisbanes/Android-PullToRefresh

RoundCorners # https://github.com/KuangGang/RoundCorners

PagerBottomTabStrip # https://github.com/tyzlmjj/PagerBottomTabStrip | pager-bottom-tab-strip

Banner # https://github.com/youth5201314/banner | banner

ConvenientBanner

apk-parser # net.dongliu:apk-parser:2.6.9

xUtils # https://github.com/wyouflf/xUtils | com.jiechic.library:xUtils:2.6.14

ViewUtils # inject
@ViewInject
@OnClick

DbManager # 
Column

xUtils3 # https://github.com/wyouflf/xUtils3

WheelView # https://github.com/wangjiegulu/WheelView

UniversalVideoView # https://github.com/linsea/UniversalVideoView

UltraViewPager # https://github.com/alibaba/UltraViewPager

TinyPinyin # https://github.com/promeG/TinyPinyin

ImagePicker # https://github.com/jeasonlzy/ImagePicker | com.lzy.widget:imagepicker:0.6.1

SwipeMenuListView # https://github.com/baoyongzhang/SwipeMenuListView

FlowLayout # https://github.com/huang7855196/FlowLayout

Umeng # https://dl.bintray.com/umsdk/release | common analytics utdid push analytics | latest.integration

个推
极光
ShareSDK
高德地图
百度地图

scrcpy

环信 # https://raw.githubusercontent.com/HyphenateInc/Hyphenate-SDK-Android/master/repository | com.hyphenate:hyphenate-sdk:3.3.0
https://github.com/liaohuqiu/android-Ultra-Pull-To-Refresh
https://github.com/nostra13/Android-Universal-Image-Loader
https://github.com/AsyncHttpClient/async-http-client

action：MediaStore.ACTION_IMAGE_CAPTURE
extra MediaStore.EXTRA_OUTPUT, imageUriFromCamera
result： imageUriFromCamera

action：Intent.ACTION_OPEN_DOCUMENT
Category：Intent.CATEGORY_OPENABLE
type："image/*"

Intent.ACTION_PICK
data MediaStore.Images.Media.EXTERNAL_CONTENT_URI
type "image/*"

result: intent.getData()

action com.android.camera.action.CROP
data uri
type image/*
Flags Intent.FLAG_GRANT_READ_URI_PERMISSION
Intent.FLAG_GRANT_WRITE_URI_PERMISSION
Extra
crop true string
宽高的比例
aspectX 1 int
aspectY 1 int
裁剪图片宽高
outputX 300 int
outputY 300 int
return-data false boolean
outputFormat Bitmap.CompressFormat.JPEG.toString() 输出格式，一般设为Bitmap格式及图片类型
intent.setClipData(ClipData.newRawUri(MediaStore.EXTRA_OUTPUT, uri));
MediaStore.EXTRA_OUTPUT, uriClipUri // 输出图片路径
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N){
            //将存储图片的uri读写权限授权给相机应用
            List<ResolveInfo> resInfoList = activity.getPackageManager().queryIntentActivities(intent, PackageManager.MATCH_DEFAULT_ONLY);
            for (ResolveInfo resolveInfo : resInfoList) {
                String packageName = resolveInfo.activityInfo.packageName;
                activity.grantUriPermission(packageName, uriClipUri , Intent.FLAG_GRANT_WRITE_URI_PERMISSION | Intent.FLAG_GRANT_READ_URI_PERMISSION);
            }
        }
result uriClipUri
6 api
result resultData.getExtras().getParcelable("data") bitmap

android n
FileProvider.getUriForFile(context,BuildConfig.APPLICATION_ID + ".fileprovider", file);


```



```
implementation 'com.github.CymChad:BaseRecyclerViewAdapterHelper:2.9.44'
https://github.com/zzhouj/Android-DraggableGridViewPager
https://github.com/lafosca/AndroidFaceCropper
https://github.com/openaphid/android-flip
https://github.com/koral--/android-gif-drawable
https://github.com/CyberAgent/android-gpuimage
https://github.com/liaohuqiu/android-GridViewWithHeaderAndFooter
https://github.com/passsy/android-HoloCircularProgressBar
https://github.com/JoanZapata/android-iconify
https://github.com/daimajia/AndroidImageSlider
https://github.com/BakerJQ/Android-InfiniteCards
https://github.com/googlemaps/android-maps-utils
https://github.com/guohuanwen/AndroidLoadingAnimation
https://github.com/android-cjj/Android-MaterialRefreshLayout
https://github.com/SimonVT/android-menudrawer
https://github.com/a750183047/ObservableScrollView
https://github.com/ksoichiro/Android-ObservableScrollView
https://github.com/Lichenwei-Dev/ObservableScrollView
https://github.com/hanks-zyh/ScrollViewOnTouch
https://github.com/amarjain07/StickyScrollView
https://github.com/markzhai/AndroidPerformanceMonitor
https://github.com/ademar111190/android-phased-seek-bar
https://github.com/addappcn/android-pickers
https://github.com/Bigkoo/Android-PickerView
https://github.com/rtyley/android-pinned-header-listviews
https://github.com/dmytrodanylyk/android-process-button
https://github.com/jaredrummler/AndroidProcesses
https://github.com/309624472/AndroidProcesses
https://github.com/baoyongzhang/android-PullRefreshLayout
https://github.com/chrisbanes/Android-PullToRefresh
https://github.com/johannilsson/android-pulltorefresh
https://github.com/HomHomLin/Android-PullToRefreshRecyclerView
https://github.com/androidquery/androidquery
https://github.com/saiwu-bigkoo/Android-QuickSideBar
https://github.com/YahooArchive/android-range-seek-bar
https://github.com/android-cjj/Android-RecyclerViewWithFooter
https://github.com/SpecialCyCi/AndroidResideMenu
https://github.com/karonl/InDoorSurfaceView
https://github.com/woozzu/IndexableListView
https://github.com/gyf-dev/ImmersionBar
https://github.com/frapontillo/ImageViewEx
https://github.com/kevinsawicki/http-request
https://github.com/akexorcist/Android-RoundCornerProgressBar
https://github.com/ragunathjawahar/android-saripaar/
https://github.com/siyamed/android-satellite-menu
https://github.com/rno/Android-ScrollBarPanel
https://github.com/Kaopiz/android-segmented-control
https://github.com/vinc3m1/android-segmentedradiobutton
https://github.com/siyamed/android-shape-imageview
https://github.com/ximsfei/Android-skin-support
https://github.com/tjerkw/Android-SlideExpandableListView
https://github.com/loopj/android-smart-image-view
https://github.com/saiwu-bigkoo/Android-SnappingStepper
https://github.com/mrwonderman/android-square-progressbar
https://github.com/kikoso/android-stackblur
https://github.com/Canner/android-stepsview
https://github.com/avast/android-styled-dialogs
https://github.com/saiwu-bigkoo/Android-SVProgressHUD
https://github.com/romannurik/Android-SwipeToDismiss
https://github.com/BoD/android-switch-backport
https://github.com/square/android-times-square
https://github.com/norbsoft/android-typeface-helper
https://github.com/thiagolocatelli/android-uitableview
https://github.com/jenzz/Android-UndoBar
https://github.com/jgilfelt/android-viewbadger
https://github.com/pakerfeldt/android-viewflow
https://github.com/felixpalmer/android-visualizer
https://github.com/alamkanak/Android-Week-View
https://github.com/maarek/android-wheel
https://github.com/anupcowkur/Android-Wheel-Menu
https://github.com/romannurik/android-wizardpager
https://github.com/yipianfengye/android-zxingLibrary
https://github.com/LyndonChin/AndroidScreenSlidePager
https://github.com/wutongke/AndroidSkinAnimator
https://github.com/jayschwa/AndroidSliderPreference
https://github.com/umano/AndroidSlidingUpPanel
https://github.com/etsy/AndroidStaggeredGrid
https://github.com/daimajia/AndroidSwipeLayout
https://github.com/RomanTruba/AndroidTouchGallery
https://github.com/daimajia/AndroidViewAnimations
https://github.com/daimajia/AnimationEasingFunctions
https://github.com/AntennaPod/AntennaPod
https://github.com/ogaclejapan/ArcLayout
https://github.com/daCapricorn/ArcMenu
https://github.com/felipecsl/AsymmetricGridView
https://github.com/Ericliu001/async-expandable-list
https://github.com/nakardo/ATableView
https://github.com/frankiesardo/auto-parcel
https://github.com/AndroidDeveloperLB/AutoFitTextView
https://github.com/LRH1993/AutoFlowLayout
https://github.com/nugongshou110/AutoHomeRefreshListView
https://github.com/hzsweers/barber
https://github.com/android-cjj/BeautifulRefreshLayout
https://github.com/recruit-lifestyle/BeerSwipeRefresh
https://github.com/bingoogolapple/BGARefreshLayout-Android
https://github.com/HotBitmapGG/bilibili-android-client
https://github.com/tvbarthel/BlurDialogFragment
https://github.com/PomepuyN/BlurEffectForAndroidDesign
https://github.com/Ashok-Varma/BottomNavigation
https://github.com/zhengxiaopeng/BounceProgressBar
https://github.com/cdflynn/bubble-scroll
https://github.com/dupengtao/BubbleTextView
https://github.com/JakeWharton/butterknife
https://github.com/traex/CalendarListview
https://github.com/chrisjenx/Calligraphy
https://github.com/wonderkiln/CameraKit-Android
https://github.com/canyinghao/CanDialog
https://github.com/canyinghao/CanPhotos
https://github.com/canyinghao/CanRefresh
https://github.com/gabrielemariotti/cardslib
https://github.com/Ramotion/cardslider-android
https://github.com/tvbarthel/ChaseWhisplyProject
https://github.com/stfalcon-studio/ChatKit
https://github.com/chrisbanes/cheesesquare
https://github.com/kpbird/chips-edittext-library
https://github.com/ashqal/ChromeLikeSwipeLayout
https://github.com/michael-rapp/ChromeLikeTabSwitcher
https://github.com/pwnall/chromeview
https://github.com/hdodenhof/CircleImageView
https://github.com/THEONE10211024/CircleIndicator
https://github.com/ImangazalievM/CircleMenu
https://github.com/tuesda/CircleRefreshLayout
https://github.com/feeeei/CircleSeekbar
https://github.com/dmytrodanylyk/circular-progress-button
https://github.com/chrisbanes/ActionBar-PullToRefresh
https://github.com/lopspower/CircularFillableLoaders
https://github.com/oguzbilgener/CircularFloatingActionMenu
https://github.com/Sefford/CircularProgressDrawable
https://github.com/pyricau/CleanAndroidCode
http://cnode-material-design/
https://github.com/Shinelw/ColorArcProgressBar
https://github.com/MichaelEvans/ColorArt
https://github.com/THEONE10211024/ColorPhrase
https://github.com/flavienlaurent/colorpicker
https://github.com/android-cjj/ComicReader
https://github.com/liulingfeng/Common
https://github.com/nanchen2251/CompressHelper
https://github.com/zetbaitsu/Compressor
https://github.com/Yalantis/Context-Menu.Android
https://github.com/iwgang/CountdownView
https://github.com/andremion/CounterFab
https://github.com/nolanlawson/CustomFastScrollViewDemo
https://github.com/MostafaGazar/CustomShapeImageView
https://github.com/square/dagger
https://github.com/iZeroer/Daily
https://github.com/Bilibili/DanmakuFlameMaster
https://github.com/flavienlaurent/datetimepicker
https://github.com/Raizlabs/DBFlow
https://github.com/facebook/device-year-class
https://github.com/dinocore1/DevsmartLib-Android
https://github.com/orhanobut/dialogplus
https://github.com/flavienlaurent/discrollview
https://github.com/andyken/DividedDraggableView
https://github.com/DreaminginCodeZH/Douya
https://github.com/bauerca/drag-sort-listview
https://github.com/thquinn/DraggableGridView
https://github.com/BlueMor/DragLayout
https://github.com/CrazyPumPkin/DragMoreScrollView
https://github.com/shehabic/Droppy
https://github.com/PSD-Company/duo-navigation-drawer
https://github.com/dodola/DynamicCardLayout
https://github.com/2359media/EasyAndroidAnimations
https://github.com/JmStefanAndroid/EasyBehavior
https://github.com/CaMnter/EasyRecyclerView
https://github.com/CaMnter/EasySlidingTabs
https://github.com/blackfizz/EazeGraph
https://github.com/AndroidAlliance/EdgeEffectOverride
https://github.com/Freelander/Elephant
https://github.com/sungerk/elestickheader
https://github.com/rockerhieu/emojicon
https://github.com/chiragjain/Emoticons-Keyboard
https://github.com/timroes/EnhancedListView
https://github.com/greenrobot/EventBus
https://github.com/ThinkKeep/EvilsLive

https://github.com/traex/ExpandableLayout
https://github.com/Manabu-GT/ExpandableTextView
https://github.com/florent37/ExpectAnim
https://github.com/jcodeing/ExtractWordView
https://github.com/ManuelPeinado/FadingActionBar
https://github.com/medyo/fancybuttons
https://github.com/davidschreiber/FancyCoverFlow
https://github.com/mvarnagiris/Financius
https://github.com/TheFinestArtist/FinestWebView-Android
https://github.com/uccmawei/FingerprintIdentify
https://github.com/eluleci/FlatUI

https://github.com/castorflex/FlipImageView
https://github.com/Yalantis/FlipViewPager.Draco
https://github.com/shamanland/floating-action-button
https://github.com/makovkastar/FloatingActionButton
https://github.com/toanvc/FloatingActionMenu-Animation
https://github.com/diegocarloslima/FloatingGroupExpandableListView
https://github.com/mxn21/FlowingDrawer
https://github.com/nex3z/FlowLayout
https://github.com/deano2390/FlowTextView
https://github.com/H07000223/FlycoSystemBar
https://github.com/race604/FlyRefresh
https://github.com/alexvasilkov/FoldableLayout
https://github.com/facebook/fresco
	https://www.fresco-cn.org/
https://github.com/HomHomLin/FrescoImageView
https://github.com/Hitomis/FunGameRefresh
https://github.com/guanchao/GHDownload
https://github.com/tcking/GiraffePlayer
https://github.com/ManuelPeinado/GlassActionBar

https://github.com/codinguser/gnucash-android
https://github.com/googlemaps/android-samples
https://github.com/Mirkoddd/GoogleDateTimePickers
https://github.com/jpardogo/GoogleProgressBar
https://github.com/googlesamples/android-ActionBarCompat-ListPopupMenu
https://github.com/googlesamples/android-BeamLargeFiles
https://github.com/googlesamples/android-Camera2Video
https://github.com/googlesamples/android-EmojiCompat
https://github.com/googlesamples/android-GridViewPager
https://github.com/googlesamples/android-LNotifications
https://github.com/woxingxiao/GracefulMovies
https://github.com/HujiangTechnology/gradle_plugin_android_aspectjx
https://github.com/appsthatmatter/GraphView
https://github.com/greenrobot/greenDAO
https://github.com/yuweiguocn/GreenDaoUpgradeHelper
https://github.com/EvilBT/HDImageView
https://github.com/zzz40500/HeadsUp
https://github.com/lecho/hellocharts-android
https://github.com/LarsWerkman/HoloColorPicker
https://github.com/Prototik/HoloEverywhere
https://bitbucket.org/danielnadeau/holographlibrary
https://github.com/sephiroth74/HorizontalVariableListView
https://github.com/PrivacyApps/html-textview
https://github.com/hsllany/HtmlNative
https://github.com/Bilibili/ijkplayer
https://github.com/sephiroth74/ImageViewZoom
https://github.com/qdxxxx/IndexBarLayout
https://github.com/MartinvanZ/Inscription
https://github.com/koush/ion
https://github.com/google/iosched
https://github.com/twotoasters/JazzyListView
https://github.com/jfeinstein10/JazzyViewPager
https://github.com/imallan/JellyRefreshLayout
https://github.com/chiemy/JellyViewPager
https://github.com/jonfhancock/JsonToJava
https://github.com/frakbot/JumpingBeans
https://github.com/lfkdsk/JustWeEngine
https://github.com/lfkdsk/JustWeTools
https://github.com/jcodeing/K-Sonic
https://github.com/flavioarfaria/KenBurnsView
https://github.com/jenly1314/KingTV
https://github.com/mthli/Knife
https://github.com/kot32go/KShareViewActivityManager
https://github.com/ksvc/KSYMediaPlayer_Android
https://github.com/Lauzy/LBehavior
https://github.com/linheimx/LChart
https://github.com/keklikhasan/LDrawer
https://github.com/julienr/libpng-android
https://github.com/frankiesardo/LinearListView
https://github.com/jianghejie/LinkedViewPager
https://github.com/jpardogo/ListBuddies
https://github.com/hefuyicoder/ListenerMusicPlayer
https://github.com/nhaarman/ListViewAnimations
https://github.com/facebook/litho
https://github.com/dinuscxj/LoadingDrawable
https://github.com/mikepenz/LollipopShowcase
https://github.com/imbryk/LoopingViewPager
https://github.com/GitLqr/LQRWeChat
https://github.com/jdsjlzx/LRecyclerView
https://github.com/hackware1993/MagicIndicator
https://github.com/afollestad/material-camera
https://github.com/afollestad/material-dialogs
https://github.com/vpaliyX/Material-Motion
https://github.com/oli107/material-range-bar
https://github.com/navasmdc/MaterialDesignLibrary
https://github.com/mikepenz/MaterialDrawer
https://github.com/rengwuxian/MaterialEditText
https://github.com/dexafree/MaterialList
https://github.com/lsjwzh/MaterialLoadingProgressBar
https://github.com/DreaminginCodeZH/MaterialProgressBar
https://github.com/DreaminginCodeZH/MaterialRatingBar
https://github.com/zhihu/Matisse
https://github.com/nugongshou110/MeiTuanRefreshListView
https://github.com/dodola/MetaballLoading
https://github.com/nntuyen/mkloader
https://github.com/javiersantos/MLManager
https://github.com/maning0303/MNProgressHUD
https://github.com/cangwang/ModuleBus
https://github.com/andyken/MoneyTextView
https://github.com/PhilJay/MPAndroidChart
https://github.com/ajaysahani/MultiActionTextView
https://github.com/lovetuzitong/MultiImageSelector
https://github.com/Jay-Goo/MultiSelectPopWindow
https://github.com/romannurik/muzei
https://github.com/LuckyJayce/MVCHelper
https://github.com/huopochuan/MyViewPager
https://github.com/mmBs/NavigationDrawerSI
https://github.com/anzewei/NestRefreshLayout
https://github.com/huburt-Hu/NewbieGuide
https://github.com/xiaoyanger0825/NiceVieoPlayer
https://github.com/sd6352051/NiftyDialogEffects
https://github.com/JakeWharton/NineOldAndroids
https://github.com/flavienlaurent/NotBoringActionBar
https://github.com/youxiachai/Notifications4EveryWhere
https://github.com/wenmingvs/NotifyUtil
https://github.com/daimajia/NumberProgressBar
https://github.com/akshay2211/Oblique
https://github.com/pengjianbo/OkHttpFinal
https://github.com/linsea/OpenDanmaku
https://github.com/j256/ormlite-android
https://github.com/square/otto
https://github.com/EverythingMe/OverScrollView
https://github.com/babylikebird/owspace
https://github.com/mrKlar/PagedDragDropGrid
https://github.com/JorgeCastilloPrz/PagedHeadListView
https://github.com/nicolasjafelle/PagingGridViewhttps://github.com/nicolasjafelle/PagingListView
https://github.com/nicolasjafelle/PagingListView
https://github.com/DingMouRen/PaletteImageView
https://github.com/anzewei/ParallaxBackLayouthttps://github.com/chrisjenx/ParallaxScrollView
https://github.com/chrisjenx/ParallaxScrollView
https://github.com/ybq/ParallaxViewPager
https://github.com/Yasic/ParticleTextView
https://github.com/DreaminginCodeZH/PatternLock
PathAnimation
https://github.com/guoxiaoxing/phoenix
https://github.com/lightbox/PhotoProcessing
https://github.com/bm-x/PhotoView
https://github.com/chrisbanes/PhotoView
https://github.com/chrisbanes/photup
https://github.com/square/phrase
https://github.com/wuseal/PieChartView
https://github.com/androidessence/PinchZoomTextViewhttps://github.com/beworker/pinned-section-listview
https://github.com/beworker/pinned-section-listview
https://github.com/JimiSmith/PinnedHeaderListView
https://github.com/GDG-Korea/PinterestLikeAdapterView
https://github.com/codingWang/PinWheel
https://github.com/handsomezhou/PinyinSearchLibrary
https://github.com/pili-engineering/PLDroidMediaStreaming
https://github.com/pili-engineering/PLDroidShortVideo
https://github.com/pockethub/PocketHub
https://github.com/wangchenyan/PonyMusic
https://github.com/Baobomb/PopupListView
https://github.com/r0adkll/PostOffice
https://github.com/skydoves/PowerMenu
https://github.com/f2prateek/progressbutton
https://github.com/Todd-Davies/ProgressWheel
https://github.com/MarkMjw/PullScrollView
https://github.com/chiemy/PullSeparateListView
https://github.com/MarkMjw/PullToRefresh
https://github.com/matrixxun/PullToZoomInListView
https://github.com/OCNYang/QBox
https://github.com/chentao0707/QrCodeScan
https://github.com/lawloretienne/QuickReturn
https://github.com/ManuelPeinado/QuickReturnHeader
https://github.com/edmodo/range-bar

https://github.com/lsjwzh/RecyclerViewPager
https://github.com/CodeFalling/RecyclerViewSwipeDismiss
https://github.com/ManuelPeinado/RefreshActionItem
https://github.com/tarek360/RichPath
https://github.com/desmond1121/RippleCompat
https://github.com/traex/RippleEffect
https://github.com/siriscac/RippleView
https://github.com/romainguy/road-trip
https://github.com/roboguice/roboguice
https://github.com/stephanenicolas/robospice
https://github.com/octo-online/RoboSpice-samples
https://github.com/zhengxiaopeng/Rocko-Android-Demos
https://github.com/Jude95/RollViewPager
https://github.com/vinc3m1/RoundedImageView

https://github.com/imuhao/RxPicker
https://github.com/vondear/RxTools
https://github.com/fengzhizi715/SAF
https://github.com/JakeWharton/salvage
https://github.com/JayFang1993/ScanBook
https://github.com/SimonVT/schematic
https://github.com/guanchao/ScrollerCalendarhttps://github.com/timqi/SectorProgressView
https://github.com/timqi/SectorProgressView
https://github.com/neild001/SeekArc
https://github.com/pungrue26/SelectableRoundedImageView
https://github.com/dmytrodanylyk/shadow-layout
https://github.com/yingLanNull/ShadowImageView
https://github.com/lijiankun24/ShadowLayout
https://github.com/tobykurien/SherlockNavigationDrawer
https://github.com/pyricau/shipfaster
https://github.com/amlcurran/ShowcaseView
https://github.com/fredericojssilva/ShowTipsView
https://github.com/timusus/Shuttle
https://github.com/Yalantis/Side-Menu.Android
https://github.com/SimpleMobileTools/Simple-Calendar
https://github.com/ksoichiro/SimpleAlertDialog-for-Android
https://github.com/ome450901/SimpleRatingBar
https://github.com/mpcjanssen/simpletask-android
https://github.com/SinaVDDeveloper
https://github.com/yydcdut/SlideAndDragListView
https://github.com/kingideayou/SlideBottomPanel
https://github.com/HomHomLin/SlidingLayout
https://github.com/jfeinstein10/SlidingMenu
https://github.com/MEiDIK/SlimAdapter
https://github.com/scwang90/SmartRefreshLayout
https://github.com/ogaclejapan/SmartTabLayout
https://github.com/castorflex/SmoothProgressBar
https://github.com/dkzwm/SmoothRefreshLayout
https://github.com/stfalcon-studio/SmsVerifyCatcher
https://github.com/MrEngineer13/SnackBar
https://github.com/matecode/Snacky
https://github.com/CarlLee/SnappingSwipingRecyclerView
https://github.com/nhachicha/SnappyDB
https://github.com/anastr/SpeedView
https://github.com/lilei644/SpringActionMenu
https://github.com/emilsjolander/sprinkles
https://github.com/maurycyw/StaggeredGridView
https://github.com/timehop/sticky-headers-recyclerview
https://github.com/Gavin-ZYX/StickyDecoration
https://github.com/TonicArtos/StickyGridHeaders
https://github.com/qdxxxx/StickyHeaderDecoration
https://github.com/emilsjolander/StickyListHeaders
https://github.com/nuptboyzhb/SuperSwipeRefreshLayout
https://github.com/chenBingX/SuperTextView
https://github.com/JohnPersano/SuperToasts
https://github.com/nhaarman/supertooltips
https://github.com/MegatronKing/SVG-Android
https://github.com/japgolly/svg-android
https://github.com/kikoso/Swipeable-Cards
https://github.com/ikew0ng/SwipeBackLayout
https://github.com/Diolor/Swipecards
https://github.com/android-notes/SwissArmyKnife
https://github.com/kyleduo/SwitchButton
https://github.com/jgilfelt/SystemBarTint
https://github.com/InQBarna/TableFixHeaders
https://github.com/kingideayou/TagCloudView
https://github.com/beartung/tclip-android
https://github.com/amulyakhare/TextDrawable
https://github.com/torryharris/TH-ProgressButton
https://github.com/moagrius/TileView
https://github.com/Sunzxyong/Tiny
https://github.com/RomainPiel/Titanic
https://github.com/todotxt/todo.txt-android
https://github.com/zcweng/ToggleButton
https://github.com/chaychan/TouTiao
https://github.com/Hitomis/transferee
https://github.com/andkulikov/transitions-everywherehttps://github.com/wuyexiong/transparent-over-animtabsview
https://github.com/wuyexiong/transparent-over-animtabsview
https://github.com/chrislacy/TweetLanes
https://github.com/jess-anders/two-way-gridview
https://github.com/lucasr/twoway-view
https://github.com/Yalantis/uCrop
https://github.com/cymcsg/UltimateAndroid
https://github.com/soarcn/UndoBar
https://github.com/czy1121/update
https://github.com/dmytrodanylyk/video-crop
https://github.com/danylovolokh/VideoPlayerManager
https://github.com/guohuanwen/ViewAniamtion
https://github.com/inovex/ViewPager3D
https://github.com/LuckyJayce/ViewPagerIndicator
https://github.com/JakeWharton/ViewPagerIndicator
http://www.vitamio.org/
https://github.com/yixia/VitamioBundle
https://github.com/yixia/VitamioBundleStudio
https://github.com/THEONE10211024/WaterDropListView
https://github.com/recruit-lifestyle/WaveSwipeRefreshLayout
https://github.com/john990/WaveView
https://github.com/Zhaoss/WeiXinRecordedDemo
https://github.com/diogobernardino/WilliamChart
https://github.com/timqi/WindRoseDiagramView/
https://github.com/Maxwin-z/XListView-Android
https://github.com/sendtion/XRichText
https://github.com/TheFinestArtist/YouTubePlayerActivity
https://github.com/youngkaaa/YViewPagerDemo
https://github.com/zxing/zxing
https://github.com/frakbot/CreditsRoll
https://github.com/edmodo/cropper
https://github.com/patrick-doyle/CrossBow
https://github.com/keyboardsurfer/Crouton
https://github.com/liaohuqiu/cube-sdk
https://github.com/xyczero/custom-swipelistview
jitsi
https://github.com/jitsi/jitsi
https://desktop.jitsi.org/
https://jitsi.org/
https://github.com/jitsi/jitsi-android
https://github.com/johnkil/Android-RobotoTextView
http://www.trinea.cn/android/android-http-cache/
https://github.com/Trinea/android-demo
https://github.com/Maxwin-z/XListView-Android
http://mirrors.neusoft.edu.cn/
http://mirror.neu.edu.cn/
http://search.maven.org/
https://fir.im/
https://github.com/tifezh/KChartView
https://github.com/crossbario/autobahn-java
```

