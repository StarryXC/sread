> Thinking

```

```

> Memory

```
public class AskBrainBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) { }
}

IntentFilter intentFilter = new IntentFilter();
LocalBroadcastManager localBroadcastManager = LocalBroadcastManager.getInstance(context);
localBroadcastManager.registerReceiver(broadcastReceiver, intentFilter);
localBroadcastManager.unregisterReceiver(broadcastReceiver);

Intent intent = new Intent();
localBroadcastManager.sendBroadcast(intent);
```

