> Thinking

```
WindowManager
Window
Display
DisplayMetrics
```

> Memory

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
```

