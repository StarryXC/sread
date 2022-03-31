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

Window window = getWindow();
window.setSoftInputMode(WindowManager.LayoutParams.SOFT_INPUT_ADJUST_PAN);
// WindowManager.LayoutParams.FLAG_NOT_TOUCH_MODAL window外可以点击,不拦截窗口外的事件
window.setFlags(0, 0); window.addFlags(0); window.clearFlags(0);
window.setGravity(Gravity.CENTER);
WindowManager.LayoutParams attributes = window.getAttributes();
attributes.width = 1;
attributes.height = 1;
window.setAttributes(attributes);

WindowManager manager = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);
Display display = manager.getDefaultDisplay();
display.getWidth();
display.getWidth();
```

