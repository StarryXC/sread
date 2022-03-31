> Thinking

```

```

> Memory

```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <attr name="title" format="string" />
    <attr name="bg" format="float|reference" />
    <attr name="sex">
        <enum name="man" value="0" />
        <enum name="woman" value="1" />
    </attr>
    <declare-styleable name="AskBrainView">
        <attr name="title" />
        <attr name="content" format="string" />
    </declare-styleable>
</resources>





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
android.R.color.transparent

<style name="Translucent_NoTitle">
        <item name="android:windowFrame">@null</item>
        <item name="android:windowBackground">@android:color/transparent</item>
        <item name="android:windowNoTitle">true</item>
        <item name="android:windowIsFloating">true</item>
        <item name="android:windowContentOverlay">@null</item>
    </style>
    <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
        <item name="android:windowIsTranslucent">true</item>
    </style>

    <style name="AppThemeNotTranslucent" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="android:windowIsTranslucent">false</item>
    </style>

    <style name="CustomSeekbarStyle" >
        <item name="android:maxHeight">10dp</item>
        <item name="android:indeterminateOnly">false</item>
        <item name="android:indeterminateDrawable">@color/colorAccent</item>
        <item name="android:progressDrawable">@drawable/seekbar_progress_drawable</item>
        <item name="android:minHeight">10dp</item>
        <item name="android:thumb">@mipmap/acc_huadong</item>
    </style>

    <style name="CustomDialog_two" parent="@style/DialogTheme">
        <item name="android:windowNoTitle">true</item>
        <!-- 设置title -->
        <item name="android:windowBackground">@android:color/transparent</item>
        <item name="android:windowFrame">@null</item>
        <!-- 设置边框 -->
        <item name="android:windowIsTranslucent">true</item>
        <!-- 设置半透明 -->
        <item name="android:windowFullscreen">true</item>
        <!-- 设置全屏 -->
        <!--  是否浮现在activity之上  -->
        <item name="android:windowIsFloating">true</item>
        <!-- 是否模糊  -->
        <item name="android:backgroundDimEnabled">true</item>
    </style>


    <style name="AppWelcome" parent="Theme.AppCompat.Light.NoActionBar">
        <!--<item name="android:windowBackground">@mipmap/splash</item>-->
        <item name="android:windowBackground">@color/transparent</item>
        <item name="android:windowFullscreen">true</item>
    </style>
    <style name="Appwelcome" parent="android:Theme.Translucent.NoTitleBar.Fullscreen"/>
```

