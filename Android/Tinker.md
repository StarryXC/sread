> Thinking

```

```

> Memory

```
https://github.com/Tencent/tinker

// 低版本编译不通过
classpath "com.tencent.tinker:tinker-patch-gradle-plugin:1.9.14.19"
plugins {
    id 'com.tencent.tinker.patch'
}
tinkerPatch {
    buildConfig {
        tinkerId "1.0"
    }
}
compileOnly 'com.tencent.tinker:tinker-android-anno:1.9.14.19'
implementation 'com.tencent.tinker:tinker-android-lib:1.9.14.19'

gradle.properties
TINKER_ID=1.0
TINKER_ENABLE=true





```
