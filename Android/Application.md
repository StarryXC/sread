> Thinking

```

```

> Memory

```
ActivityLifecycleCallbacks activityLifecycleCallbacks = new ActivityLifecycleCallbacks() {
    @Override
    public void onActivityCreated(@NonNull Activity activity, @Nullable Bundle bundle) { }
    @Override
    public void onActivityStarted(@NonNull Activity activity) { }
    @Override
    public void onActivityResumed(@NonNull Activity activity) { }
    @Override
    public void onActivityPaused(@NonNull Activity activity) { }
    @Override
    public void onActivityStopped(@NonNull Activity activity) { }
    @Override
    public void onActivitySaveInstanceState(@NonNull Activity activity, @NonNull Bundle bundle) { }
    @Override
    public void onActivityDestroyed(@NonNull Activity activity) { }
};
application.registerActivityLifecycleCallbacks(activityLifecycleCallbacks);
application.unregisterActivityLifecycleCallbacks(activityLifecycleCallbacks);

public class AskBrainApplication extends Application {
    @Override
    public void onCreate() { }
    @Override
    public void onConfigurationChanged(@NonNull Configuration newConfig) { }
    @Override
    public void onLowMemory() { }
    @Override
    public void onTrimMemory(int level) { }
}

<application
    android:allowBackup="true"
    android:hardwareAccelerated="false"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:roundIcon="@mipmap/ic_launcher_round"
    android:supportsRtl="true"
    android:theme="@style/Theme.AppCompat.Light.NoActionBar"
    />
```

