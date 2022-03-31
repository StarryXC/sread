> Thinking

```
Service
ServiceConnection
```

> Memory

```
class AskBrainService extends Service {
    @Nullable
    @Override
    public IBinder onBind(Intent intent) { return null; }
    @Override
    public boolean onUnbind(Intent intent) { return super.onUnbind(intent); }
    @Override
    public void onCreate() {
        super.onCreate();
        startForeground(1, new Notification());
    }
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) { return super.onStartCommand(intent, flags, startId); }
    @Override
    public void onDestroy() { super.onDestroy(); }
}

Object lock = new Object();
ServiceConnection serviceConnection = new ServiceConnection() {
    @Override
    public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
        iBinder.linkToDeath(new IBinder.DeathRecipient() {
            @Override
            public void binderDied() { }
        }, 0);
        synchronized (lock) {
            iBinder = iBinder;
            lock.notify();
        }
    }
    @Override
    public void onServiceDisconnected(ComponentName componentName) { }
};
context.bindService(new Intent(), serviceConnection, Context.BIND_AUTO_CREATE);
context.unbindService(serviceConnection);
new Thread(new Runnable() {
    @Override
    public void run() {
        synchronized (lock) {
            if (iBinder == null) {
                lock.wait();
            }
        }
    }
}).start();

<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
    context.startForegroundService(new Intent(this, AskBrainService.class));
} else {
    context.startService(new Intent(this, AskBrainService.class));
}
```

