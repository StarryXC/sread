[TOC]

# Java 发展史

```
平台分支
JDK 5.0 特性
```

# Java 环境搭建

```

```

## Java 命令行

```
javac
java
jar
javap
javah
javadoc
```

# Java 基础语法

## Java 变量定义

```

```



## Java 流程控制

```
swith
int, byte, char, short
枚举 字符串
```

## Java 方法

```

```



# Java 面向对象语法

## Java 类

```
类的成员
    类的属性
    类的方法
    构造方法
    访问类成员

    类定义
        类的声明
        类的成员
        类成员默认初始化值:零值
    对象创建 创建对象 类的实例化
        类初始化
            代码块种类
        匿名对象 只使用一次的对象
        instanceof
        new
    属性访问器
    构造方法:调用 重载 默认 返回值
    类的封装
        访问修饰符
        构造方法私有化 单例模式
        外部不能直接操作类的属性
        访问控制权限
    abstract
    strictfp
    static
    final 编译器优化属性内联
        不可变类
    内部类
        静态内部类
        匿名内部类
    继承
        this
        super
        方法覆写
    多态
    代码块
```

## Java 接口

```
默认函数
```

## Java 包

```
静态导入
导包
```



## Java 枚举

```
枚举类的声明

构造方法 属性 抽象方法
Enum # values ordinal name valueOf


属性 字段
方法
构造函数 私有的
抽象方法

实现接口
继承抽象类

每一个枚举值代表枚举类的一个实例对象。

若枚举类只有一个枚举值，则可以当作单态设计模式使用。
```

```

```



# ---

## Java 泛型

```
类 变量 方法 | ? extends

```

## Java 对象操作

```
    对象比较
    对象拷贝 对象克隆
    对象哈希值 哈希函数
    字符串表示
```

## Java 多态

```
    方法多态性
    继承多态 对象多态性
```

## Java 4种代码块

```
普通代码块 写在一个方法之中的语句块
构造块 写在类中的一个语句块
	优先于构造方法执行，执行多次
静态块 写在类中使用static声明的语句块
	优先于构造块与构造方法执行，用于初始化静态属性，只执行一次
同步代码块 多线程
```

## Java 对象克隆

```
被克隆的类需实现Cloneable接口并覆盖Object的clone()方法
```



# Java 异常处理

```
异常处理语句
try catch finally
try with resources

Throwable
Error
Exception
RuntimeException

自定义异常
```

# Java 数据加密

```
加密原理
MessageDigest

byte b = 1; // 异或文件加密
b ^= 0x99;

MessageDigestSpi
    MessageDigest
FilterInputStream
    DigestInputStream
FilterOutputStream
    DigestOutputStream

MessageDigest
    getInstance
        MD5
        SHA-1
    digest

byte bytes[] = new byte[1];
StringBuilder stringBuilder = new StringBuilder();
for (int i=0;i<bytes.length;i++) {
    String is = Integer.toString(bytes[i]&0xff, 16);
    if (is.length() < 2) {
        stringBuilder.append("0");
    }
    stringBuilder.append(is);
}

StringBuffer stringBuilder = new StringBuffer("");
for (int offset = 0; offset < bytes.length; offset++) {
    int i = bytes[offset];
    if (i < 0)
        i += 256;
    if (i < 16)
        stringBuilder.append("0");
    stringBuilder.append(Integer.toHexString(i));
}

public static final String SIGN_ALGORITHMS = "MD5WithRSA";
public static String sign(String content, String privateKeyString) throws Exception {
    PKCS8EncodedKeySpec encodedKeySpec = new PKCS8EncodedKeySpec(Base64.decode(privateKeyString, 0));
    KeyFactory keyFactory = KeyFactory.getInstance("RSA");
    PrivateKey privateKey = keyFactory.generatePrivate(encodedKeySpec);
    Signature signature = Signature.getInstance(SIGN_ALGORITHMS);
    signature.initSign(privateKey);
    signature.update(content.getBytes());
    byte[] signed = signature.sign();
    return Base64.encodeToString(signed, 0);
}
public static boolean doCheck(String content, String sign, String publicKeyString) throws Exception {
    KeyFactory keyFactory = KeyFactory.getInstance("RSA");
    byte[] encodedKey = Base64.decode(publicKeyString, Base64.DEFAULT);
    PublicKey publicKey = keyFactory.generatePublic(new X509EncodedKeySpec(encodedKey));
    Signature signature = Signature.getInstance(SIGN_ALGORITHMS);
    signature.initVerify(publicKey);
    signature.update(content.getBytes());
    return signature.verify(Base64.decode(sign, 0));
}


Base64
    encodeToString
        DEFAULT

```

# Java 定时器

```

```



# Java 反射机制

```
Class 代表字节码

AnnotatedElement
    GenericDeclaration

类 Class <-- Serializable GenericDeclaration Type AnnotatedElement

AccessibleObject <-- AnnotatedElement
    Executable <-- Member GenericDeclaration
        构造方法 Constructor
        方法 Method
    属性 Field <-- Member

Class
    forName
    loadClass
    方法 getMethod
    getDeclaredMethod
    getMethods
    getDeclaredMethods
    属性 getField
    getDeclaredField
    getFields
    getDeclaredFields
    构造方法 getConstructor
    注解 getAnnotation
    getDeclaredAnnotation
    getAnnotations
    getDeclaredAnnotations
    名称 getName
    getSimpleName
    getCanonicalName
    是否枚举 isEnum
    是否实例 isInstance
    URL getResource
    流 getResourceAsStream
    getClassLoader
    newInstance

AccessibleObject
    setAccessible

Executable
    getName

Constructor

Method
    invoke
    getReturnType
    getParameterTypes
无参、有参、多参(带数组和基本数据类型)、静态、私有
类的 无参、有参、私有 构造函数

Field
    set
私有变量、静态变量、公共变量

Member
    getName
    getModifiers
    isSynthetic
    getType

AnnotatedElement
    getAnnotations

Array
    getLength
    get
    set
```

## Java 内省机制

```
内省 Introspector
java.beans 操作Java属性的Api

通过 PropertyDescriptor 类操作Bean的属性
通过Introspector类获得Bean对象的 BeanInfo
通过 BeanInfo 来获取属性的描述器（ PropertyDescriptor ）
通过属性描述器就可以获取某个属性对应的 getter/setter 方法
通过反射机制来调用这些方法

PropertyDescriptor
Introspector
BeanInfo

```

## Java beanutils

```
beanutils工具包

内省
commons-beanutils.jar,commons-logging.jar
BeanUtils
	setProperty
	getProperty
```

# Java 大数值

```
精确计算/浮点计算
Number          <-- Serializable
    BigDecimal  <-- Comparable
    BigInteger  <-- Comparable

```

# Java 数学计算

```
数学计算
浮点操作
Math
    min
    ceil
    sqrt
    acos
    toDegrees
    abs
    toRadians
    sin
    cos
    pow

```

# Java 格式化

```
格式化 Format <-- Serializable Cloneable
    数字 NumberFormat
        DecimalFormat
        ChoiceFormat
    日期 DateFormat
        SimpleDateFormat
    消息 MessageFormat

Format
    格式化 format
    解析 parseObject

DecimalFormat
    DecimalFormat("0.00")

DateFormat
    getDateInstance
    getDateTimeInstance
    setLenient

```

# Java 日期时间

```
Date
Calendar

Serializable
    Date
    Calendar

Comparable
    Date
    Calendar

Cloneable
    Date
    Calendar


Calendar
    getInstance
    setTime
    getTime

Date
    getTime

Time
    Time()
    setToNow

```

# Java 正则表达式

```
正则语法
Pattern
<正则表达式> # 数字 字母 [] {} w
    ^\\w+([-+.]\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$ # 匹配email
    [\u0391-\uFFE5]+$ # 汉字

Pattern <-- Serializable
Matcher <-- MatchResult

Pattern
    compile
    matcher

Matcher
    find
    start
    end
    group


```

# Java 国际化

```
ResourceBundle
```

# Java 运行原理

```
内存管理/内存模型/垃圾回收机制

运行机制
跨平台原理

垃圾回收机制

对象引用类型
    Reference

垃圾回收 GC
不再有任何指向的空间为垃圾空间

JMM 内存模型
数组定义
数组名称 栈内存
数组对象 堆内存 一组连续内存
对象 对象名称栈内存 对象属性堆内存
全局代码区 所有的方法
全局数据区 存放static类型属性

WeakReference
	<get>

Reference
```

## Java 类加载

```
类加载器
类加载器
类加载机制
类加载器类型
类加载机制

ClassLoader
    getSystemClassLoader
    getParent
```



# Java 常用类

```
Object
包装类 | 自动装箱 | 自动拆箱
字符串 | 可变 | 不可变 | StringTokenizer | 大小写转换
System | gc | exit | time | stdio | property | arraycopy | load
    sun.boot.class.path
Runtime | exec | memory
Scanner
UUID
Random
```

# Java 集合框架

```
Iterable
    Collection
        List
        Set
            SortedSet
                NavigableSet
        Queue
            Deque

AbstractCollection			<-- Collection
    AbstractList			<-- List
        ArrayList			<-- Cloneable Serializable List RandomAccess
        AbstractSequentialList
            LinkedList		<-- Cloneable Serializable List Deque
        Vector				<-- Cloneable Serializable List RandomAccess
            Stack
    AbstractSet				<-- Set
        TreeSet				<-- Cloneable Serializable NavigableSet
        HashSet				<-- Cloneable Serializable Set
            LinkedHashSet	<-- Cloneable Serializable Set
        EnumSet				<-- Cloneable Serializable

Collection



BlockingQueue		<-- Queue
    BlockingDeque	<-- Deque
    TransferQueue

Map
    SortedMap
        NavigableMap

AbstractMap				<-- Map
    EnumMap				<-- Cloneable Serializable
    HashMap				<-- Cloneable Serializable Map
        LinkedHashMap	<-- Map
    TreeMap				<-- Cloneable Serializable NavigableMap
    WeakHashMap			<-- Map

Dictionary
    Hashtable		<-- Cloneable Serializable Map
        Properties

Map
    values

Collection
    stream
    findFirst

List
    add

Comparator
Iterator

BitSet

Collections
Arrays
Objects

Observable
Observer

ArrayList 数据结构底层
LinkedList 数据结构底层
HashMap 数据结构底层
    put
    size
    get
    isEmpty
    containsKey
    clear
    entrySet
    keySet
Map.Entry
    getKey
    getValue
    setValue

List<String> list = new ArrayList<>();
list.size();
list.get(1);

Vector<String> vector = new Vector<>();
vector.elements();
vector.addElement("");
vector.lastElement(); vector.firstElement(); vector.elementAt(0);
vector.removeElement(""); vector.removeElementAt(1);
vector.removeAllElements();

Stack<String> strings = new Stack<>();
boolean empty = strings.empty();

BitSet bitSet = new BitSet();
bitSet.and(bitSet);
bitSet.or(bitSet);
bitSet.xor(bitSet);

Collections.sort(list);
Collections.addAll(new ArrayList<>());

Object[] objects = new Object[2];
Arrays.toString(objects);
Arrays.sort(objects);
Arrays.copyOf(objects, 3);
Arrays.binarySearch(objects, new Object());
Arrays.stream(objects);
Arrays.equals(new byte[2], new byte[2]);

Objects.equals("", "");

Observable observable = new Observable();
observable.addObserver(new Observer() {
    @Override
    public void update(Observable o, Object arg) { }
});


```

# Java GUI

```

```

# Java 网络

```
TCP
UDP
HTTP

WebSockets
https://github.com/TooTallNate/Java-WebSocket
'org.java-websocket:Java-WebSocket:1.3.6'

TCP Socket <-- Closeable
    getOutputStream
    getInputStream
UDP ServerSocket <-- Closeable
DatagramSocket <-- Closeable

SocketAddress <-- Serializable
    InetSocketAddress

InetAddress <-- Serializable
    Inet4Address
    Inet6Address

InetAddress
    getLocalHost
    getByName

InetSocketAddress
    InetSocketAddress

Http URLConnection
    Http HttpURLConnection
        Https HttpsURLConnection

URI
    create
    getAuthority
    getHost
    getPort
    getQuery
    getPath
    getScheme
    getUserInfo

Http URL <-- Serializable
    getHost
    getPort
    getPath
    getAuthority
    getProtocol
    getDefaultPort
    getQuery
    getUserInfo
    getFile
    openConnection

URLConnection
    getConnectTimeout
    setConnectTimeout
    getReadTimeout
    setReadTimeout
    getDoOutput
    setDoOutput
    getDoInput
    setDoInput
    addRequestProperty
    connect
    getInputStream
    getErrorStream
    getOutputStream
    getHeaderFields
    getHeaderField

HttpURLConnection
    getResponseCode
    getRequestMethod
    setRequestMethod
    getResponseMessage
    getInstanceFollowRedirects
    setInstanceFollowRedirects
    disconnect
    getHeaderFieldDate
    getHeaderFieldKey
    getHeaderField

HttpsURLConnection
    setDefaultHostnameVerifier HostnameVerifier
        verify

URLDecoder
    decode
URLEncoder
    encode

Proxy

Proxy.Type
    HTTP

Socket 进行 Http 请求

```

## HttpClient

```

```

## OkHttp

```
implementation 'com.squareup.okhttp3:okhttp:3.12.1'

RequestBody
    FormBody
    MultipartBody

OkHttpClient
Request
Response
Call
WebSocket

http 断点下载

HttpLoggingInterceptor # level | Level.BODY

https://square.github.io/okhttp/
implementation 'com.squareup.okhttp3:okhttp:3.12.0'

FormBody formBody = new FormBody.Builder(Charset.defaultCharset())
        .add("", "")
        .build();

MultipartBody multipartBody = new MultipartBody.Builder()
        .setType(MultipartBody.FORM)
        .addFormDataPart("", "")
        .addFormDataPart("", "", formBody)
        .build();

// mime "application/json" "application/json;charset=utf-8"
RequestBody requestBody = RequestBody.create(MediaType.parse("image/png"), new File(""));
Request request = new Request.Builder()
        .url("")
        .header("", "")
        .addHeader("", "")
        .get()
        .post(requestBody)
        .build();
Request.Builder builder = request.newBuilder();

OkHttpClient okHttpClient = new OkHttpClient();
okHttpClient = new OkHttpClient.Builder()
        .addInterceptor(new Interceptor() {
            @NonNull
            @Override
            public Response intercept(@NonNull Chain chain) throws IOException {
                Call call = chain.call();
                Connection connection = chain.connection();
                int timeoutMillis = chain.connectTimeoutMillis();
                chain.readTimeoutMillis();
                chain.writeTimeoutMillis();
                chain.proceed(chain.request());
                return null;
            }
        })
        .retryOnConnectionFailure(true)
        .hostnameVerifier(new HostnameVerifier() {
            @Override
            public boolean verify(String hostname, SSLSession session) { return false; }
        })
        .sslSocketFactory(new SSLCertificateSocketFactory(1))
        .connectTimeout(1, TimeUnit.SECONDS)
        .readTimeout(1, TimeUnit.SECONDS)
        .writeTimeout(1, TimeUnit.SECONDS)
        .callTimeout(1, TimeUnit.SECONDS)
        .build();
OkHttpClient.Builder builder = okHttpClient.newBuilder();

Call call = okHttpClient.newCall(request);
call.cancel(); call.isCanceled()
call.timeout();
call.isExecuted();
call.clone();
call.enqueue(new Callback() {
    @Override
    public void onFailure(@NonNull Call call, @NonNull IOException e) { }
    @Override
    public void onResponse(@NonNull Call call, @NonNull Response response) throws IOException { }
});

Response response = call.execute();
response.header("", "");
ResponseBody responseBody = response.body();
BufferedSource source = responseBody.source();
String string = responseBody.string();
byte bytes[] = responseBody.bytes();
InputStream inputStream = responseBody.byteStream();
ByteString byteString = responseBody.byteString();
Reader reader = responseBody.charStream();
long length = responseBody.contentLength();
MediaType mediaType = responseBody.contentType();
responseBody.close();
Response.Builder builder = response.newBuilder();

WebSocket webSocket = okHttpClient.newWebSocket(request, new WebSocketListener() {
    @Override
    public void onClosed(@NonNull WebSocket webSocket, int code, @NonNull String reason) { super.onClosed(webSocket, code, reason); }
    @Override
    public void onClosing(@NonNull WebSocket webSocket, int code, @NonNull String reason) { super.onClosing(webSocket, code, reason); }
    @Override
    public void onFailure(@NonNull WebSocket webSocket, @NonNull Throwable t, @Nullable Response response) { super.onFailure(webSocket, t, response); }
    @Override
    public void onMessage(@NonNull WebSocket webSocket, @NonNull String text) { super.onMessage(webSocket, text); }
    @Override
    public void onMessage(@NonNull WebSocket webSocket, @NonNull ByteString bytes) { super.onMessage(webSocket, bytes); }
    @Override
    public void onOpen(@NonNull WebSocket webSocket, @NonNull Response response) { super.onOpen(webSocket, response); }
});
webSocket.send("");
webSocket.cancel();

class AskBrainInterceptor implements Interceptor {
    @Override
    public Response intercept(Chain chain) throws IOException {
        Request.Builder builder = chain.request().newBuilder();
        builder.header("Content-Type", "application/json;charset=utf-8")
                .header("Network-CU","");
        return chain.proceed(builder.build());
    }
}
```

## Retrofit

```
https://square.github.io/retrofit/

// 2.4.0 2.9.0
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:adapter-rxjava2:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0'

Retrofit retrofit = new Retrofit.Builder()
        .baseUrl("")
        .addConverterFactory(GsonConverterFactory.create())
        .client(new OkHttpClient())
        .build();
```

# Java JDBC

```
数据库

Url
    mysql com.mysql.jdbc.Driver
    jdbc:mysql://localhost:3306/jdbc root

DriverManager
    注册驱动 registerDriver
驱动 Driver
Wrapper
    Connection <-- AutoCloseable
    ResultSet <-- AutoCloseable
    ResultSetMetaData
        RowSetMetaData
Clob
Blob
Types




```

# Java IO

## BIO

```
字节流 InputStream <-- Closeable
    文件流 FileInputStream
    过滤流 FilterInputStream
        缓存流 BufferedInputStream
        数据流 DataInputStream <-- DataInput
        PushbackInputStream
    内存流 ByteArrayInputStream
    合并流 SequenceInputStream
    对象流 ObjectInputStream <-- ObjectInput ObjectStreamConstants

字节流 OutputStream <-- Closeable Flushable
    文件流 FileOutputStream
    过滤流 FilterOutputStream
        缓存流 BufferedOutputStream
        数据流 DataOutputStream <-- DataOutput
        打印流 PrintStream <-- Appendable Closeable
    内存流 ByteArrayOutputStream
    对象流 ObjectOutputStream <-- ObjectOutput ObjectStreamConstants

Closeable
Flushable

Reader <-- Readable Closeable
    BufferedReader
        LineNumberReader
    CharArrayReader
    InputStreamReader
        FileReader
    FilterReader
        PushbackReader
    PipedReader
    StringReader

Writer <-- Appendable Closeable Flushable
    BufferedWriter
    CharArrayWriter
    OutputStreamWriter
        FileWriter
    FilterWriter
    PipedWriter
    PrintWriter
    StringWriter

```

## 格式化输出

```
格式化说明符
%i %d int 有符号10进制整数
%4d %04d 指定位数输出

%ld %lld 长整型

%o unsigned int 无符号8进制整数

%u unsigned int 无符号10进制整型
%lu

%x unsigned int 无符号16进制 小写 不输出前缀
%X unsigned int 无符号16进制 大写
%#x 无符号16进制 小写 输出前缀
%#X 无符号16进制 大写

%c 字符 char

%8s 字符串 char * 数组 char[] 以'\0'结尾
%6.9s 不小于6 不大于9字符串 char *
%S wchar_t *p = "tongtong" 字符串 wchar_t *

%f 单精度浮点数 6位四舍五入 double
%5.4f 单精度浮点数 6位四舍五入

%lf 双进度浮点数 同 f

%e %E 科学计数法 double

%g %G 有效位数 默认位数 double

%.4g 有效位数 指定位数

%p &pi // float pi
十六进制输出指针 void *

转义字符
转义字符 转义序列码
转义序列	含义
\\			\
\'			'
\"			"
\?			?
\a			警报铃声
\b			退格键
\f			换页符
\n			换行符
\r			回车
\t			水平制表符
\v			垂直制表符
\ooo		一到三位的八进制数
\xhhhh		一个或多个数字的十六进制数





```

## 序列化

```
ObjectOutputStream
	writeObject

ObjectInputStream
	readObject
```

## 文件

```
File
	getFreeSpace
	getTotalSpace
	getUsableSpace
	createTempFile
FileDescriptor
```

## NIO

```
Buffer
    ByteBuffer <-- Comparable
        MappedByteBuffer
            DirectByteBuffer <-- DirectBuffer
        HeapByteBuffer
    ShortBuffer <-- Comparable
        HeapShortBuffer
    IntBuffer <-- Comparable
        HeapIntBuffer
    LongBuffer <-- Comparable
        HeapLongBuffer
    FloatBuffer <-- Comparable
        HeapFloatBuffer
    DoubleBuffer <-- Comparable
        HeapDoubleBuffer
    CharBuffer <-- Comparable Appendable CharSequence Readable
        HeapCharBuffer

Closeable
    Channel
        InterruptibleChannel
        ReadableByteChannel
            ScatteringByteChannel
        WritableByteChannel
            ByteChannel <-- ReadableByteChannel
                SeekableByteChannel
            GatheringByteChannel

AbstractInterruptibleChannel <-- Channel InterruptibleChannel
    FileChannel <-- SeekableByteChannel GatheringByteChannel ScatteringByteChannel
    DatagramChannel
    SocketChannel
```

## Commons IO

```
org.apache.commons:commons-io:1.3.2

```

## Okio

```
https://square.github.io/okio/

implementation 'com.squareup.okio:okio:2.1.0'
```

# Java 并发

```
synchronized # 线程同步 锁膨胀
synchronized
volatile # 共享变量内存可见性

线程池
锁

J.C.U
并发类
安全容器

Object
    wait
    notify
    notifyAll

Thread <-- Runnable
ThreadGroup <-- Thread.UncaughtExceptionHandler
StackTraceElement <-- Serializable

Thread
    getContextClassLoader

StackTraceElement
    getClassName
    getMethodName
    getLineNumber
    getFileName

Exchanger
CyclicBarrier
CountDownLatch
    countDown
    await
    getCount
Semaphore <-- Serializable
Condition
    await
    signal


AbstractQueue <-- Queue
    ArrayBlockingQueue <-- BlockingQueue Serializable
    LinkedBlockingDeque <-- BlockingDeque Serializable
    LinkedBlockingQueue <-- BlockingQueue Serializable
    LinkedTransferQueue <-- TransferQueue Serializable
    PriorityBlockingQueue <-- BlockingQueue Serializable
    SynchronousQueue <-- BlockingQueue Serializable

Queue
    BlockingQueue
        TransferQueue
        BlockingDeque
Deque
    BlockingDeque

BlockingQueue
    add
    put
    offer
    remove
    poll
    take
    peek



AbstractQueue
    ConcurrentLinkedQueue <-- Queue Serializable
AbstractCollection
    ConcurrentLinkedDeque <-- Deque Serializable
AbstractSet
    ConcurrentSkipListSet <-- NavigableSet Cloneable Serializable
    CopyOnWriteArraySet <-- Serializable
CopyOnWriteArrayList <-- List RandomAccess Cloneable Serializable

List
    iterator
    subList

CopyOnWriteArrayList
    底层实现 Object[] array
    迭代器 COWIterator
    子列表 COWSubList

CopyOnWriteArraySet
    底层实现 CopyOnWriteArrayList al

ArrayBlockingQueue
    底层实现 Object[] items
    迭代器 Itr

ConcurrentLinkedQueue
    底层实现 Node
        值 item
        下个节点 next
    迭代器 Itr

ConcurrentLinkedDeque
    底层实现 Node
        值 item
        上个节点 prev
        下个节点 next
    迭代器 AbstractItr
        Itr
        DescendingItr

AbstractMap
    ConcurrentHashMap <-- ConcurrentMap Serializable
    ConcurrentSkipListMap <-- ConcurrentNavigableMap Cloneable Serializable

Map
    ConcurrentMap
        ConcurrentNavigableMap(NavigableMap)

Map
    keySet
    entrySet

ConcurrentHashMap
    底层实现 Node[]
        hash
        key
        val
        next
    key集合 KeySetView
    entry 集合 EntrySetView
    值集合 ValuesView

线程控制
	创建
	休眠
线程池
线程交替执行
	
线程交换数据
	
线程串行执行

线程通讯

线程本地变量
原子操作
锁
读写锁
死锁

线程同步
共享数据

```

# Java Json

## org.json

```
JSONObject
JSONArray
JSONTokener
```

## Gson

```
https://github.com/google/gson
implementation 'com.google.code.gson:gson:2.8.9'

Gson
TypeToken
@SerializedName
```

## Fastjson

```
https://github.com/alibaba/fastjson
implementation 'com.alibaba:fastjson:1.2.12'

JSON
JSONObject
JSONArray
```

# Java XML

```
JAXP Java API for XML Processing
```

## DOM

```
DocumentBuilderFactory
DocumentBuilder
NodeList

TransformerFactory
Transformer
DOMSource <-- Source
StreamResult <-- Result

Node
    Document
    Element
```

## SAX

```
SAXParserFactory
SAXParser

DefaultHandler <-- EntityResolver DTDHandler ContentHandler ErrorHandler
```

## XmlPull

```
占用内存资源少

XmlPullParserFactory
XmlPullParser
XmlSerializer
```

# Java JNI

```
本地方法 native
System
    加载本地库 loadLibrary

#include "jni.h"
extern "C"
JNIEXPORT jstring JNICALL
(JNIEnv *env){
	std::string cpp_str = "Hello from C++";
	const char* c_str = cpp_str.c_str();
	jstring j_str = env->NewStringUTF(c_str);
	cpp_str = env->GetStringUTFChars(j_str, NULL);
	std::string result = cpp_str + cpp_str ;
	env->NewStringUTF(result.c_str());
	env->ReleaseStringUTFChars(fullPath_, fullPath);
	const char* cinfo = env->GetStringUTFChars(info,NULL);
}

类型映射
jbyte jbyteArray # byte 有符号 8位
jshort jshortArray # short 有符号 16位
jint jintArray # int 有符号 32位
jlong jlongArray # long 有符号 64位
jfloat jfloatArray # float 32位
jdouble jdoubleArray # double 64位
jchar jcharArray # char 无符号 16位
jboolean jbooleanArray # boolean 无符号 8位
jobject jobjectArray
jclass # java.lang.Class
jstring # java.lang.String
jarray
void # void

方法签名
boolean   Z
byte      B
char      C
short     S
int       I
long      J
float     F
double    D
java.lang.Object  Ljava/lang/Object;
type[]    [type
method()  ()ret-type

jni.h
GetEnv
    GetVersion

    DefineClass
    FindClass

    FromReflectedMethod
    FromReflectedField
    ToReflectedMethod

    GetSuperclass
    IsAssignableFrom

    ToReflectedField

    Throw ThrowNew
    ExceptionOccurred ExceptionDescribe ExceptionClear FatalError
    ExceptionCheck

    PushLocalFrame PopLocalFrame

    NewGlobalRef DeleteGlobalRef
    NewLocalRef DeleteLocalRef
    NewWeakGlobalRef DeleteWeakGlobalRef
    IsSameObject
    EnsureLocalCapacity

    AllocObject
    NewObject NewObjectV NewObjectA

    GetObjectClass
    IsInstanceOf

    GetMethodID
    CallObjectMethod CallObjectMethodV CallObjectMethodA # Void Byte Short Int Long Float Double Char Boolean
    CallNonvirtualObjectMethod CallNonvirtualObjectMethodV CallNonvirtualObjectMethodA # Void Byte Short Int Long Float Double Char Boolean

    GetFieldID
    GetObjectField SetObjectField # Byte Short Int Long Float Double Char Boolean

    GetStaticMethodID
    CallStaticObjectMethod CallStaticObjectMethodV CallStaticObjectMethodA # Void Byte Short Int Long Float Double Char Boolean

    GetStaticFieldID
    GetStaticObjectField SetStaticObjectField # Byte Short Int Long Float Double Char Boolean

    NewString NewStringUTF
    GetStringLength GetStringUTFLength
    GetStringChars GetStringUTFChars
    GetStringRegion GetStringUTFRegion
    ReleaseStringChars ReleaseStringUTFChars

    GetArrayLength
    NewObjectArray # Byte Short Int Long Float Double Char Boolean
    GetObjectArrayElement
    SetObjectArrayElement

    GetIntArrayElements # Byte Short Int Long Float Double Char Boolean
    ReleaseIntArrayElements # Byte Short Int Long Float Double Char Boolean
    GetIntArrayRegion SetIntArrayRegion # Byte Short Int Long Float Double Char Boolean

    RegisterNatives UnregisterNatives

    MonitorEnter MonitorExit

    GetStringCritical ReleaseStringCritical
    GetPrimitiveArrayCritical ReleasePrimitiveArrayCritical

    NewDirectByteBuffer
    GetDirectBufferAddress
    GetDirectBufferCapacity

    GetObjectRefType
    DestroyJavaVM GetJavaVM

	AttachCurrentThread DetachCurrentThread
    AttachCurrentThreadAsDaemon
```



# Java JNDI

```

```

# Java RMI

```

```

# Java SPI

```
ServiceLoader

```

## AutoService

```
auto-common auto-service
```

# Java 多媒体

```
ImageIO
ImageReader
ImageWriter

ImageTranscoder
    ImageWriter



ImageIO
    read
    write
```



# Java 日志

```

```

# Java 单元测试

```
JUnit
UT 单元测试

junit
@Test
assertEquals

// 4.13.2
testImplementation 'junit:junit:4.12'

Assert.assertEquals(10, 10);
```

# Kotlin

## 环境搭建

```

```

## 命令行

```
kotlinc
```



## 基础语法

```

```

## 面向对象语法

```

```

## 高阶函数

```
forEach
forEachIndexed
filter
let
para?.let{}
```



## 常用类

```

```

## 集合框架

```
MutableList

filter
firstOrNull
filterNotNull
getOrNull
f.isNotEmpty()

rise.split("|").toList()
```



# 基础语法

## 变量定义

```
var val
类型转换
1.toBigDecimal()
string.toDouble()

空判断
.isNullOrEmpty()
.isEmpty()
```

## 数组

```
listOf
```

## 方法

```
fun
```

# 面向对象语法

## 类

```
data class
data class Order
继承
val side: String

对象创建 # object
    延迟初始化 # lateinit by lazy
    构造函数 # init
    访问控制 # 默认 private

半生对象 # companion
对象表达式
```

## 注解

```
@JvmField

注解
@Retention(AnnotationRetention.SOURCE)
annotation class <AnnotationName>

```

# 常用类

## String

```
字串传模板： "${path}"
```

# Groovy

## 环境搭建

```

```

## 命令行

```
groovyc
```

## 基础语法

```

```

## 面向对象语法

```

```

## 常用类

```

```

## IO

```

```



# 基础语法

## 变量定义

```
def
```

## 方法

```
默认参数
```

# 面向对象语法

## 类

```
访问控制
访问控制 默认 public
```

## 接口

```

```

## 包

```

```

# 常用类

## String

```
fileText = (fileText =~ /${regex}/).replaceAll("<string name=\"${name}\">${value}</string>")

```

## 包装类

```
BigInteger = 30g
BigDecimal = 3.5g
```

# IO

## File

```
file.text
file.write(fileText,"UTF-8")
```

# Scala

## 环境搭建

```

```

## 命令行

```

```

## 基础语法

```

```

## 面向对象语法

```

```

# 基础语法

## 变量定义

```
val var
```

# Java Web 环境搭建

```
Java 容器
Web 项目目录结构
Java 容器
    Tomcat

Web 项目目录结构
```

## web.xml

```
web.xml
    web-app
    servlet
    welcome-file-list
```

# Java JSP

## JSP 语法

```
指令
脚本
表达式

指令 <%@ %>
page
    language="java"
    import="java.util.*"
    pageEncoding="ISO-8859-1"
脚本 <% %>
表达式 <%= %>
```

## JSP 内置对象

```
request
    getContextPath()
    String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";

```

# Java Servlet

```
Servlet GenericServlet
ServletConfig
ServletRequest
ServletResponse
setContentType getContentType # text/html;charset=UTF-8

HttpServletResponse
setHeader # Location /day05/wxy.html 设置重定向 设置 302
sendRedirect 重定向

HttpSession
RequestDispatcher

javax.servlet
Servlet
ServletConfig
ServletContext
RequestDispatcher
GenericServlet


ServletInputStream
ServletOutputStream

javax.servlet.http
HttpServlet
HttpServletRequest
HttpServletResponse
HttpSession

javax.servlet.annotation
@WebServlet
@WebInitParam
@WebFilter
```

# Java EL

## EL 语法

```

```

## EL 内置对象

```

```

# Java JSTL

```

```

# Struts

```
Action
DispatchAction
ActionMapping
ActionForward
ActionForm
FormFile

<struts-config>
<form-beans>
<form-bean>
<action-mappings>
<action>
<forward>
```

```

```

# Struts 2

```
com.opensymphony.xwork2
Action
ActionSupport
ActionContext
ServletActionContext
RequestAware
SessionAware
ApplicationAware

<struts>
<package>
<action>
<result>
<constant>
<include>
```

```

```

# Spring

```
@SpringBootApplication
@Configuration
@Bean

SpringApplication

<beans>
<bean>
<property>
<value>
<ref>

ApplicationContext
ClassPathXmlApplicationContext
```

```

```

```

```



# Hibernate

```
implementation fileTree(dir: 'libs', include: ['*.jar'])
implementation 'org.hibernate:hibernate-core:5.4.11.Final'
// implementation 'org.hibernate:hibernate-annotations:3.5.6-Final'

implementation 'org.javassist:javassist:3.24.0-GA'
implementation 'org.slf4j:slf4j-log4j12:1.4.1'
implementation 'org.slf4j:slf4j-api:1.4.1'
implementation 'mysql:mysql-connector-java:5.1.10'
implementation 'log4j:log4j:1.2.13'

Configuration
AnnotationConfiguration
SessionFactory
Session
Transaction
SessionStatistics


// xml 元注解初始化
Configuration configuration = new Configuration().configure(); // 加载hibernate的配置文件
SessionFactory sessionFactory = configuration.buildSessionFactory();
Session session = sessionFactory.openSession(); // 打开session
Transaction transaction = session.beginTransaction(); // 开启事务

// insert id 不能相同
TableRecord tableRecord = new TableRecord();
Serializable serializable = session.save(tableRecord); // 把对象放入到了一级缓存中
System.out.println(serializable);
session.persist(tableRecord); // 取代save

// update
TableRecord tableRecord = session.get(TableRecord.class, 0L); // 查询 会把对象放入session缓存
System.out.println(tableRecord);
tableRecord.setName("tab0");

TableRecord tableRecord = new TableRecord();
tableRecord.setId(1);
session.update(tableRecord); // id存在，执行update语句 id不存在，报错 会把对象放入session缓存

// query
TableRecord tableRecord = session.get(TableRecord.class, 1L); //没有发出sql语句,说明数据来自于缓存
System.out.println(tableRecord);

Query query = session.createQuery("from TableRecord"); // 创建查询 org.hibernate.Query
List<TableRecord> tableRecords = query.list(); // 查询所有记录
for (TableRecord tableRecord : tableRecords) {
    System.out.println(tableRecord);
}

// delete
TableRecord tableRecord = session.get(TableRecord.class, 0L);
session.delete(tableRecord); // 删除

// refresh
TableRecord tableRecord = new TableRecord();
tableRecord.setId(1);
tableRecord.setName("tabName");
System.out.println(tableRecord);
session.refresh(tableRecord); // 把数据库中的数据同步到缓存中 发出sql语句了
System.out.println(tableRecord);

TableRecord tableRecord = session.get(TableRecord.class, 1L); //没有发出sql语句,说明数据来自于缓存
SessionStatistics sessionStatistics = session.getStatistics(); //SessionStatistics hibernate为一级缓存提供了一个统计机制
int entityCount = sessionStatistics.getEntityCount(); // session缓存中的实体个数
System.out.println(entityCount);
// session.clear(); // 清空session缓存中所有对象
session.evict(tableRecord); // 清除session缓存中单个对象
System.out.println(sessionStatistics.getEntityCount());


TableRecord tableRecord = new TableRecord();
TableRecord2 tableRecord2 = new TableRecord2(); // student是一个持久化状态的对象 要想让班级维护关系必须 inverse="false"
tableRecord2.setId(1);
Set<TableRecord2> tableRecord2Set = new HashSet<>();
tableRecord2Set.add(tableRecord2);
tableRecord.setTableRecord2Set(tableRecord2Set);
session.update(tableRecord);

/*
classes是一个持久化状态的对象,不需要对classes进行update显示操作
<set name="students" cascade="save-update"> 删除该班级的学生
 */
TableRecord tableRecord = session.get(TableRecord.class, 0L);
tableRecord.setTableRecord2Set(null); // 解除关联
for (TableRecord2 tableRecord2 : tableRecord.getTableRecord2Set()) {
    session.delete(tableRecord2);
}

/*
<set name="students" cascade="delete"> 在删除班级的同时删除学生
 */
TableRecord tableRecord = session.get(TableRecord.class, 0L);
session.delete(tableRecord);

Configuration configuration = new Configuration().configure(); // 加载hibernate的配置文件
SessionFactory sessionFactory = configuration.buildSessionFactory();
Session session = sessionFactory.openSession(); // 打开session

Transaction transaction = session.beginTransaction(); // 开启事务

// TODO: 22-1-3

/*
刷新session一级缓存中持久化对象到数据库中
    如果一个对象由ID值，则会去检查该对象的副本，如果和副本一致，则什么都不做，如果和副本不一致，则发出update语句
    如果一个对象没有ID值，则会发出insert语句
    在执行session.flush之前，所有的对持久化对象的属性的改变都在一级缓存中，和数据库没有关系
    在执行session.flush的时候，数据还停留在缓存中
 */
session.flush();
transaction.commit(); // 提交事务
session.close(); // 关闭session session生命周期结束，一级缓存生命周期也结束





Configuration configuration = new Configuration().configure(); // 加载hibernate的配置文件 org.hibernate.cfg.AnnotationConfiguration;
SessionFactory sessionFactory = configuration.buildSessionFactory();
Session session = sessionFactory.openSession(); // 打开session
// sessionFactory.getCurrentSession();

Transaction transaction = session.beginTransaction(); // 开启事务

// TODO: 22-1-3

/*
刷新session一级缓存中持久化对象到数据库中
    如果一个对象由ID值，则会去检查该对象的副本，如果和副本一致，则什么都不做，如果和副本不一致，则发出update语句
    如果一个对象没有ID值，则会发出insert语句
    在执行session.flush之前，所有的对持久化对象的属性的改变都在一级缓存中，和数据库没有关系
    在执行session.flush的时候，数据还停留在缓存中
 */
session.flush();
transaction.commit(); // 提交事务
session.close(); // 关闭session session生命周期结束，一级缓存生命周期也结束

```

```

```

```

```

```

```

```

```

# MyBatis

```

```

```

```

```

```

```

```

```

```





# 响应式编程

## Java Stream API

```
AutoCloseable
    BaseStream
        Stream
        IntStream
        LongStream
        DoubleStream

Consumer
Supplier
Predicate
Collector

Function
ToIntFunction
ToLongFunction
ToDoubleFunction
IntFunction
BiFunction
    BinaryOperator

Spliterator
    Spliterator.OfPrimitive
    Spliterator.OfInt
    Spliterator.OfLong
    Spliterator.OfDouble

Optional

Collectors

BiFunction
    apply
    andThen
```

## RxJava

```
https://github.com/ReactiveX/RxJava
https://github.com/ReactiveX/RxAndroid
implementation 'io.reactivex.rxjava2:rxjava:2.1.3'
implementation 'io.reactivex.rxjava2:rxandroid:2.1.1'
    2.2.21
    1.3.8

ObservableSource
    Observable
Publisher
    Flowable
SingleSource
    Single

背压
subscribe = Flowable.interval(0, 5, TimeUnit.SECONDS)
.onBackpressureDrop()
.subscribe {

Disposable # dispose
ObservableSource
Observable # just iterable map flatMap filter zipWith toList subscribe materialize subscribeOn observeOn
Schedulers # io computation newThread from
AndroidSchedulers # mainThread
Function # apply
Consumer # accept
Predicate # test
Observer # next error complete subscribe
Subscriber # next error complete subscribe
ObservableOnSubscribe # subscribe
Emitter # next error complete
ObservableEmitter # disposed serialize cancellable
Cancellable # cancel
Action # run
Function # 3 4 5 6 7 8 9 | apply

disposable = Flowable.fromIterable(coinTypeBeans)

Flowable flowable = Flowable.fromIterable(new ArrayList<>());

Observable<String> observable = Observable.just("");
observable.map((Function<String, String>) s -> null); observable.map(new Function<String, String>() {
    @Override
    public String apply(@NonNull String s) throws Exception { return null; }
});
observable.distinct();
Single<List<String>> listSingle = observable.toList();
observable.observeOn(Schedulers.io());
observable.subscribe(s -> { }); observable.subscribe(new Consumer<String>() {
    @Override
    public void accept(String s) throws Exception { }
});




```

```

```

# Guava

```
Google 工具库

implementation 'com.google.guava:guava:24.1-jre'
```



# 爬虫

## Jsoup

```
https://jsoup.org/
http://www.open-open.com/jsoup/
compile 'org.jsoup:jsoup:1.10.3'


Document document = Jsoup.connect("http://baidu.com").get();
Elements elements = document.select("#wrapper_wrapper");

String html = "<html><head><title>First parse</title></head>"
        + "<body><p>Parsed HTML into a doc.</p></body></html>";
Document doc = Jsoup.parse(html,"");

String html = "<div><p>Lorem ipsum.</p>";
Document doc = Jsoup.parseBodyFragment(html);

Document doc = Jsoup.connect("http://baidu.com")//只支持Web URLs (http和https 协议)
        .data("query", "Java")
        .userAgent("Mozilla")
        .cookie("auth", "token")
        .timeout(3000)
        .post();

File file = new File("");
Document doc = Jsoup.parse(file,"gbk");

element = document.getElementById("id");
string = document.title();
element = document.body();

element = element.getElementById("id");
elements = element.getElementsByTag("tag");
elements = element.getElementsByClass("className");
elements = element.getElementsByAttribute("key");

elements = element.siblingElements();
element = element.firstElementSibling();
element = element.lastElementSibling();
element = element.nextElementSibling();
element = element.previousElementSibling();

element = element.parent();
elements = element.parents();
element = element.child(0);
elements = element.children();

string = element.attr("key");// <a> .attr("href") .attr("abs:href") .attr("src") .attr("abs:src")
element = element.attr("key","value");
string = elements.attr("key");
elements = elements.attr("key","value");
attributes = element.attributes();
string = element.id();
string = element.className();
Set<String> stringSet = element.classNames();
boolean has = element.hasClass("className");
element = element.addClass("className");
element = element.removeClass("className");
string = element.text();
element = element.text("value");
string = element.html();
element = element.html("html-value");
string = element.outerHtml();
string = element.data();
Tag tag = element.tag();
string = element.tagName();
element = element.tagName("tagName");

element = element.append("html");
element = element.prepend("html");
element = element.appendText("text");
element = element.prependText("text");
element = element.appendElement("tagName");
element = element.prependElement("tagName");

elements = document.select("");//elements对象支持类似于CSS (或jquery)的选择器语法
element = elements.first();
```

```

```

```

```

# 注解处理

## 注解

```
    元注解
    内置注解

public class YicAnnotation {
    private final static int GET=0;
    private final static int POST=1;
    private final static int DELETE=2;
    private final static int PUT=3;
    @IntDef({GET, POST, DELETE,PUT})
    @Retention(RetentionPolicy.SOURCE)
    public @interface ReqType{}
}

元注解
@Target # ElementType FIELD METHOD CONSTRUCTOR PARAMETER LOCAL_VARIABLE ANNOTATION_TYPE PACKAGE
@Retention # RetentionPolicy SOURCE CLASS RUNTIME

```

## JavaPoet

```
https://github.com/square/javapoet
```

# Mina

```

```

# Netty

```

```

# Hadoop

```

```

# Hive

```

```

# Spark

```

```

# XNIO

```

```

```

 
注释
标识符 关键字 保留字
变量
    常量 字面量
    变量类型 全局变量 局部变量
    数据类型 类型转换
        数值型 字符型 布尔型
        枚举 结构体 共用体 指针
    变量存储类型
运算符 操作数 优先级 结合性
    算术运算符 按位运算符 逻辑运算符
    比较/关系运算符 赋值运算符 条件运算符
    指针运算符 成员访问 取地址 类型判定 级联
    描述法：名称 作用 运算结果类型
表达式 语句
流程控制
    分支流程 循环流程 跳转流程
    描述法：书写形式种类 几种书写形式
数组
方法 函数
    可变参数函数 参数类型/参数传递方式
    匿名函数
    Lambda
    可选参数 必选参数
    命名参数 索引参数

注释
单行注释 可以嵌套
多行注释 不能嵌套
文档注释 生成开发者文档
对程序说明
调试程序

标识符
字母 区分大小写
数字
下划线 _
美元符号 $
不能以数字开头
长度无限制
自定义的名字

关键字
关键字 编程语言内定具备特殊含义的标识符

命名规范
见名知意 有意义的名字
关键字、保留字不能用于自定义的标识符
类名和接口名单词的首字母大写，其他单词小写
变量名与方法名首单词全部小写，其他单词首字母大写，其他小写
包名全部单词小写
常量全部单词大写，单词与单词之间使用下划线分隔

变量
变量声明 & 变量初始化
<type> <name>; # 定义变量
<type> <name> = <value>; # 定义变量并赋值
<type> <name1>, <name2>; # 同时定义多个变量
<type> <name1>, <name2> = <value2>; # 同时定义多个变量并赋值

数据类型
1字节8位
2字节16位
4字节32位
8字节64位
基本数据类型
引用数据类型

位数表示范围取值
存储空间 (位数) 取值范围 (有符号) 取值范围 (无符号)
1Byte = 8bit
	-128 ~ 127			0 ~ 255
2Byte = 16bit
	-32,768 ~ 32,767	0 ~ 65,535
4Byte = 32bit
	-2,147,483,648 ~ 2,147,483,647
	0 ~ 4,294,967,295
8Byte = 64bit

逻辑运算
与 同真为真
或 同假为假
异或 相同false 相异true

位操作 对数的二进制进行的操作
位运算是直接多操作数的二进制的每一个二进制位（bit）都进行布尔运算 更面向底层的操作

单目运算符 一元运算符
双目运算符 二元运算符
三目运算符 三元运算符

表达式
表达式 符合一定语法规则的运算符和操作数的序列
表达式的值 运算的结果
表达式的类型 运算结果的类型
表达式的运算顺序
1. 首先按运算符优先级从高到底进行运算
2. 优先级相同，按运算符约定的结合方向进行运算

循环语句 满足条件时反复执行特定代码
循环类型
	无限循环 死循环
	有限循环
循环语句四个组成部分
初始化部分
循环条件部分
循环体部分
循环部分

数组
:<数组：特性>
    <数组声明>
    <数组初始化>
    <数组访问>
    <数组操作>
        <遍历>
        <拷贝>
多个相同数据类型的组合，实现一组数据统一管理
一位数组 二维数组 多维数组
数组声明 数组定义

数组初始化
	静态初始化
	动态初始化

数组小标 从0开始
数组下标从0开始，最大值为 length -1
数组内存分析 栈内存 堆内存

数组的特点：
	1. 数组只能存储同一种 数据类型的数据。
	2. 数组是会给存储到数组中 的元素分配一个索引值的，索引值从0开始，最大的索引值是length-1；
	3. 数组一旦初始化，长度固定。
	4. 数组中的元素与元素之间的内存地址是连续的。

方法 函数
可重复调用的代码段
返回值类型
函数名
形式参数
实际参数
返回值

2、函数的重载存在的原因：为了增强方法的阅读性，优化了程序设计。
数组遍历 一位数组 二维数组
数组排序
	选择排序 内循环一次，最值出现在头角标位置
	冒泡排序 内循环一次，最值出现在尾角标位置
	二分法 折半查找 适合有序数组 
获取数组最大值 最小值
1、定义函数可以将功能代码进行封装
2、便于对该功能进行复用
3、函数只有被调用才会被执行
4、函数的出现提高了代码的复用性
5、对于函数没有具体返回值的情况，返回值类型用关键字void表示，那么该函数中的return语句如果在最后一行可以省略不写。

```



```
程序设计
面向对象三大特性

类：指代对象 功能 核心方法(重载方法 参数作用)

程序设计
结构化程序设计
	程序结构
		顺序结构 按顺序执行
		选择结构 按选择条件执行
		循环结构
			当型 判断是否符合条件执行
			直到型 先执行在判断是否符合条件再执行
面向对象程序设计
	一切皆对象，一切的操作都有对象
面向对象设计 类的设计
	类与对象的关系 # 类是对象的模版 对象是类的具体实现
	类 # 对一类事物的描述 共性描述
	对象/实例 # 该类事物的每个个体 个性体现
	特征 # 继承 封装 多态
面向过程程序设计


面向对象三大特性
封装性 类成员和方法对外部的可见性
	只能通过定制好的方法访问数据
	方便加入控制逻辑
	限制对属性的不合理操作
	便于修改，增强代码安全和可维护性
继承性 扩展类的功能
多态性 方法重载 对象多态性
2.3封装的好处
	1：隐藏了类的具体实现
	2：操作简单
	3：提高对象数据的安全性


3.4构造代码块
给所有的对象进行统一的初始化 
对象一建立就运行并且优先于构造函数
1：构造代码块和构造函数的区别，构造代码块是给所有对象进行统一初始化， 构造函数给对应的对象初始化。
    2：构造代码块的作用：它的作用就是将所有构造方法中公共的信息进行抽取

this只能在非静态中（没有static修饰的）函数使用
可以解决构造函数中对象属性和函数形参的同名问题
"==" 用于引用类型变量时，比较的是内存地址。判断两个 对象是否为同一个对象

```

