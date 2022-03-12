> Thinking

```
SurfaceView
	GLSurfaceView
TabHost
```

> Memory

```
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

TabHost
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

