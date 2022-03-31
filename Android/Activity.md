> Thinking

```
Activity
    ActivityGroup
        TabActivity

AppCompatActivity

ActionBar
```

> Memory

```
public class AskBrainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) { }
    @Override
    protected void onStart() { }
    @Override
    protected void onResume() { }
    @Override
    protected void onPause() { }
    @Override
    protected void onStop() { }
    @Override
    protected void onDestroy() { }
    @Override
    public void onAttachedToWindow() { }
    @Override
    public void onDetachedFromWindow() { }
    @Override // configChanges
    public void onConfigurationChanged(@NonNull Configuration newConfig) { }
    @Override
    public void onLowMemory() { }
    @Override
    public void onTrimMemory(int level) { }
}

activity.setContentView(R.layout.activity_main);
activity.findViewById(R.id.content);

activity.setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT);
activity.overridePendingTransition(R.anim.left_in, R.anim.reght_out);

public class AskBrainActivity extends AppCompatActivity {
    
    void startActivity() {
        Intent intent = new Intent();
        intent.putExtra("", "");
        startActivity(intent);
        overridePendingTransition(0, 0);
        
        startActivityForResult(intent, 100);
        finish();
        isFinishing();
        setResult(100, intent);
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
    }
}

class AskBrainActivity extends AppCompatActivity {

    public void chekcPermission() {
        switch (ActivityCompat.checkSelfPermission(this, Manifest.permission.WRITE_EXTERNAL_STORAGE)) {
            case PackageManager.PERMISSION_GRANTED:
            case PackageManager.PERMISSION_DENIED:
        }
    }
    
    void requestPermissions() {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            requestPermissions(new String[]{ }, 100);
        }
        ActivityCompat.requestPermissions(this, new String[]{ }, 100);
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (grantResults.length == permissions.length) {
        }
    }
}

Toolbar toolbar = findViewById(R.id.toolbar);
appCompatActivity.setSupportActionBar(toolbar);
ActionBar actionBar = appCompatActivity.getSupportActionBar();
if (actionBar != null) {
    actionBar.hide();
    actionBar.show();
}

TabHost tabHost = tabActivity.getTabHost();
TabHost.TabSpec tabSpec = tabHost.newTabSpec("");
tabSpec.setIndicator("", context.getDrawable(android.R.mipmap.sym_def_app_icon));
tabSpec.setContent(new Intent());
tabHost.addTab(tabSpec);

<activity android:name=".AskBrainActivity"
    android:exported="true"
    android:launchMode="singleInstance"
    android:screenOrientation="behind"
    android:windowSoftInputMode="adjustPan"
    android:configChanges="orientation|keyboardHidden|screenSize"
    android:noHistory="true"
    android:theme="@style/Theme.AppCompat.Light.NoActionBar"
    android:process=":process"
    />

<activity-alias
    android:name=".sd.Ask"
    android:targetActivity=".AskBrainActivity"
    android:exported="true"
    />

<intent-filter>
    <action android:name="android.intent.action.MAIN" />
    <category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
<intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <data android:scheme="tencent100424468" />
</intent-filter>
```

