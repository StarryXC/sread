> Thinking

```
XposedHelpers
IXposedHookLoadPackage
XposedBridge
meta-data kv
xposedmodule true
xposeddescription @string/gps_hack_desc
xposedminversion 54
```

> Memory

```
// 53 82 | assets/xposed_init
compileOnly 'de.robv.android.xposed:api:82'
compileOnly 'de.robv.android.xposed:api:82:sources'

IXposedHookLoadPackage # handleLoadPackage
XC_LoadPackage.LoadPackageParam classLoader
XposedHelpers # findAndHookMethod
XC_MethodHook # beforeHookedMethod afterHookedMethod
MethodHookParam # args setResult
XposedBridge # log
```

