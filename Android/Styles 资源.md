> Thinking

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

> Memory

```
  <style name="CaptureTheme" parent="android:Theme.Holo">
    <item name="android:windowFullscreen">true</item>
    <item name="android:windowContentOverlay">@null</item>
    <item name="android:windowActionBarOverlay">true</item>
    <item name="android:windowActionModeOverlay">true</item>
  </style>
  
   <style name="AppTheme.NoActionBar">
<item name="windowActionBar">false</item>
<item name="windowNoTitle">true</item>
</style>


<style name="AppTheme.AppBarOverlay" parent="ThemeOverlay.AppCompat.Dark.ActionBar" />
<style name="AppTheme.PopupOverlay" parent="ThemeOverlay.AppCompat.Light" />
<style name="AppTheme.NoActionBar">
<item name="windowActionBar">false</item>
<item name="windowNoTitle">true</item>
<item name="android:windowDrawsSystemBarBackgrounds">true</item>
<item name="android:statusBarColor">@android:color/transparent</item>
</style>

```

