### Kotlin

```
字符串
字串传模板： "${path}"
File
file.text
file.write(fileText,"UTF-8")

def
fileText = (fileText =~ /${regex}/).replaceAll("<string name=\"${name}\">${value}</string>")

implementation 'com.github.PhilJay:MPAndroidChart:v3.0.3'
'org.java-websocket:Java-WebSocket:1.3.6'
        implementation 'com.scwang.smartrefresh:SmartRefreshLayout:1.1.0-alpha-11'
    implementation 'com.scwang.smartrefresh:SmartRefreshHeader:1.1.0-alpha-11'
    com.github.lygttpod:SuperTextView:2.1.7
    com.github.CymChad:BaseRecyclerViewAdapterHelper:2.9.30'

-
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jre7:$kotlin_version"

    implementation 'com.google.code.gson:gson:2.8.5'
    implementation 'com.youth.banner:banner:1.4.10'

CircleImageView
MutableList
import com.google.gson.annotations.SerializedName

data class Order(
    @SerializedName("side") val side: String
):Serializable
```



```

 smartRefresh.setOnRefreshListener {
smartRefresh.finishRefresh()
smartRefresh.setOnLoadMoreListener {
 smartRefresh.finishLoadMore()

val data = JSONObject.parseObject(message) alibaba
        String.format(
        code.replace(
com.afollestad.materialdialogs.MaterialDialog;
MaterialDialog dialog = new MaterialDialog.Builder(context)
                .customView(R.layout.bibi_dialog_trade_info_tip, false)
                .autoDismiss(false)
                .cancelable(false)
                .show();

mView.iv_close.setOnClickListener { dismiss() }
 it.rise.split("|").toList().filter { f -> f.isNotEmpty() }
 
```

# 并发编程 J.C.U

```java
Thread
    start
Thread thread = new Thread(){
    @Override
    public void run() {
        Thread currentThread = Thread.currentThread();
        try {
            boolean interrupted = currentThread.isInterrupted();
            System.out.println("Thread.interrupted() => " + interrupted);
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            // e.printStackTrace();
            boolean interrupted = currentThread.isInterrupted();
            System.out.println("Thread.interrupted() => " + interrupted);
        }
    }
};
thread.();.join()
Thread.sleep(1500);
thread.interrupt();
boolean interrupted = Thread.interrupted();
System.out.println("Thread.interrupted() => " + interrupted);
// Thread.yield();

synchronized
线程控制
	创建
	休眠
线程池
线程交替执行
	Condition
线程交换数据
	Exchanger
线程串行执行
	Object
线程通讯
	Exchanger
	CyclicBarrier
	CountDownLatch
	Semaphore
线程本地变量
原子操作
锁
读写锁
死锁

线程同步
共享数据
```



```
apply plugin: 'java'

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'org.hibernate:hibernate-core:5.4.11.Final'
//    implementation 'org.hibernate:hibernate-annotations:3.5.6-Final'
    
    implementation 'org.javassist:javassist:3.24.0-GA'
    implementation 'org.slf4j:slf4j-log4j12:1.4.1'
    implementation 'org.slf4j:slf4j-api:1.4.1'
    implementation 'mysql:mysql-connector-java:5.1.10'
    implementation 'log4j:log4j:1.2.13'
}

repositories {
    mavenLocal()
    mavenCentral()
    jcenter()
    maven { url 'https://maven.aliyun.com/repository/public' }
}

```


