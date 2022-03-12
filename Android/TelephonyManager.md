> Thinking

```
TelephonyManager
PhoneStateListener
```

> Memory

```
TelephonyManager # Context.TELEPHONY_SERVICE
	getDeviceId
	listen

PhoneStateListener
	onCallStateChanged # state
		# TelephonyManager.CALL_STATE_IDLE 挂断状态
		# TelephonyManager.CALL_STATE_OFFHOOK 接听或拨打状态
		# TelephonyManager.CALL_STATE_RINGING 响铃状态
	LISTEN_CALL_STATE # 监听通话
	LISTEN_NONE # 取消监听
```

