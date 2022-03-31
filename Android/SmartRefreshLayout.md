> Thinking

```

```

> Memory

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

