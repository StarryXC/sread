> Thinking

```
SurfaceView
	GLSurfaceView
TabHost
```

> Memory

```
SurfaceHolder surfaceHolder = surfaceView.getHolder();
surfaceHolder.setType(SurfaceHolder.SURFACE_TYPE_PUSH_BUFFERS);
surfaceHolder.setFixedSize(100, 100);
surfaceHolder.addCallback(new SurfaceHolder.Callback() {
    @Override
    public void surfaceCreated(@NonNull SurfaceHolder surfaceHolder) { }
    @Override
    public void surfaceChanged(@NonNull SurfaceHolder surfaceHolder, int i, int i1, int i2) { }
    @Override
    public void surfaceDestroyed(@NonNull SurfaceHolder surfaceHolder) { }
});
surfaceHolder.setKeepScreenOn(true);
Canvas canvas = surfaceHolder.lockCanvas();
canvas = surfaceHolder.lockHardwareCanvas();
surfaceHolder.unlockCanvasAndPost(canvas);

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

