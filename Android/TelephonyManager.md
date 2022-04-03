> Thinking

```
TelephonyManager
PhoneStateListener
```

> Memory

```
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.READ_CALL_LOG" />

requestPermissions(new String[] {Manifest.permission.READ_PHONE_STATE, Manifest.permission.READ_CALL_LOG}, 100);

// 成员变量
PhoneStateListener phoneStateListener = new PhoneStateListener() {
    @Override
    public void onCallStateChanged(int state, String phoneNumber) {
        switch (state) {
            case TelephonyManager.CALL_STATE_RINGING: // 响铃状态
            case TelephonyManager.CALL_STATE_OFFHOOK: // 接听或拨打状态
            case TelephonyManager.CALL_STATE_IDLE: // 挂断状态
        }
    }
};
TelephonyManager telephonyManager = (TelephonyManager) getSystemService(Context.TELEPHONY_SERVICE);
// 监听通话 LISTEN_CALL_STATE 取消监听 LISTEN_NONE
telephonyManager.listen(phoneStateListener, PhoneStateListener.LISTEN_CALL_STATE);
telephonyManager.getDeviceId(); // 获取手机IMEI(需要“android.permission.READ_PHONE_STATE”权限)


```
