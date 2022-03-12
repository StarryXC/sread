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
Xposed # compileOnly api 53:sources 82 | assets/xposed_init

IXposedHookLoadPackage # handleLoadPackage
XC_LoadPackage.LoadPackageParam classLoader
XposedHelpers # findAndHookMethod
XC_MethodHook # beforeHookedMethod afterHookedMethod
MethodHookParam # args setResult
XposedBridge # log
```

