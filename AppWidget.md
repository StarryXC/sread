> Thinking

```

```

> Memory

### Android

```

AppWidgetProvider
AppWidgetManager
class AskBrainAppWidgetProvider extends AppWidgetProvider {
    @Override // 当 App Widget 实例第一次被创建时
    public void onEnabled(Context context) { super.onEnabled(context); }
    @Override // 当最后一个App Widget 实例 被删除时
    public void onDisabled(Context context) { super.onDisabled(context); }
    @Override // 删除 App Widget 时
    public void onDeleted(Context context, int[] appWidgetIds) { super.onDeleted(context, appWidgetIds); }
    @Override // 达到制定时间更新 向桌面添加App Widget 每次更新都调用一次该方法，使用频繁
    public void onUpdate(Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds) { super.onUpdate(context, appWidgetManager, appWidgetIds); }
    @Override // 接收广播事件
    public void onReceive(Context context, Intent intent) { super.onReceive(context, intent); }
}

PendingIntent pendingIntent = PendingIntent.getActivity(context, 100, new Intent(), 0);
RemoteViews remoteViews = new RemoteViews(context.getPackageName(), android.R.layout.simple_list_item_1);
remoteViews.setTextViewText(android.R.id.text1,"");
remoteViews.setOnClickPendingIntent(android.R.id.button1, pendingIntent);
AppWidgetManager appWidgetManager = AppWidgetManager.getInstance(context);
appWidgetManager.updateAppWidget(new ComponentName(context, AppWidgetManager.class), remoteViews);

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

<appwidget-provider>
	android:minHeight android:minWidth
	android:updatePeriodMillis # 6000 毫秒
	android:initialLayout # layout

```

