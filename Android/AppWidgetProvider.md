> Thinking

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

> Memory

```
<appwidget-provider>
	android:minHeight android:minWidth
	android:updatePeriodMillis # 6000 毫秒
	android:initialLayout # layout

appwidget
	meta-data {android.appwidget.provider: @xml/appwidget_info}
	action android.appwidget.action.APPWIDGET_UPDATE
```

