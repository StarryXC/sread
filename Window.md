> Thinking

```

```

> Memory

### Android

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

