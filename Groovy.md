

## gradle 插件配置

```
apply plugin: 'groovy'

dependencies {
    implementation gradleApi()
    implementation localGroovy()
}
repositories {
    mavenCentral()
}

```

```
字符串
字串传模板： "${path}"
File
file.text
file.write(fileText,"UTF-8")

def
fileText = (fileText =~ /${regex}/).replaceAll("<string name=\"${name}\">${value}</string>")
https://github.com/yangfuhai/ASimpleCache

implementation 'com.umeng.sdk:common:1.5.0'
implementation 'com.umeng.sdk:analytics:7.5.0'
implementation 'com.umeng.sdk:share-core:latest.integration'
implementation 'com.umeng.sdk:share-qq:latest.integration'
implementation 'com.umeng.sdk:share-sina:latest.integration'
implementation 'com.umeng.sdk:share-wechat:latest.integration'
cardview
implementation 'com.facebook.fresco:fresco:0.10.0+'
implementation 'com.facebook.fresco:imagepipeline-okhttp3:0.10.0+'
    
implementation 'com.android.support:multidex:1.0.2'
implementation 'com.github.PhilJay:MPAndroidChart:v3.0.3'
'org.java-websocket:Java-WebSocket:1.3.6'
        implementation 'com.scwang.smartrefresh:SmartRefreshLayout:1.1.0-alpha-11'
    implementation 'com.scwang.smartrefresh:SmartRefreshHeader:1.1.0-alpha-11'
    com.github.lygttpod:SuperTextView:2.1.7
    com.github.CymChad:BaseRecyclerViewAdapterHelper:2.9.30'
        api 'com.jakewharton:butterknife:8.8.1'
    annotationProcessor 'com.jakewharton:butterknife-compiler:8.8.1'
        implementation 'com.tencent.bugly:crashreport:latest.release'
        implementation 'cn.jiguang.sdk:jpush:3.3.2'
    implementation 'cn.jiguang.sdk:jcore:2.0.1'
    recyclerview
constraint-layout
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jre7:$kotlin_version"
        implementation 'com.squareup.retrofit2:retrofit:2.4.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.4.0'
    implementation 'com.google.code.gson:gson:2.8.5'
    implementation 'com.youth.banner:banner:1.4.10'
    implementation 'com.github.bumptech.glide:glide:4.7.1'
    
ButterKnife.bind(this, view);
CircleImageView
MutableList
import com.google.gson.annotations.SerializedName

data class Order(
    @SerializedName("side") val side: String
):Serializable
```









