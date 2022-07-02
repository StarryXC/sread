# Java

## 变量定义

```

```

## 异常处理

```
Throwable <-- Serializable
    Exception
        RuntimeException
    Error

异常处理语句
    try { } catch () { } finally { }

自定义异常
```

## 方法

```

```

## String

```
StringBuilder
StringBuffer
String
StringTokenizer

大小写转换
```



## Object

```

```

## Json

```
org.json
JSONObject
JSONArray
JSONTokener

Gson
https://github.com/google/gson
implementation 'com.google.code.gson:gson:2.8.9'
import com.google.gson.annotations.SerializedName
// 2.8.0
implementation 'com.google.code.gson:gson:2.8.5'

Gson
TypeToken
@SerializedName

Fastjson
https://github.com/alibaba/fastjson
implementation 'com.alibaba:fastjson:1.2.12'
JSON
JSONObject
JSONArray
```

## SPI

```
ServiceLoader

```

## AutoService

```
auto-common auto-service
```

## JAXP

```
JAXP Java API for XML Processing
DOM
SAX

Node
    Document
    Element

DocumentBuilderFactory
DocumentBuilder
NodeList

TransformerFactory
Transformer
DOMSource <-- Source
StreamResult <-- Result

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

## 数据加密

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

## JDBC

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

## 包装类

```
数字 Number		<-- Serializable
    字节型 Byte	<-- Comparable
    短整型 Short	<-- Comparable
    整型 Integer	<-- Comparable
    长整型 Long	<-- Comparable
    单精度 Float	<-- Comparable
    双精度 Double	<-- Comparable
字符型 Character	<-- Comparable Serializable
布尔型 Boolean		<-- Comparable Serializable

```

## 大数值

```
精确计算/浮点计算
Number          <-- Serializable
    BigDecimal  <-- Comparable
    BigInteger  <-- Comparable

```

## 数学计算

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



## JUnit

```
UT 单元测试

junit
@Test
assertEquals

// 4.13.2
testImplementation 'junit:junit:4.12'

Assert.assertEquals(10, 10);
```

## 定时器

```

```

## 反射机制

```
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

Field
    set

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

## 并发编程

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

## 格式化

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

## 集合框架

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

## JNDI

```

```

## RMI

```

```

## 日志

```

```

## 日期时间

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

## Random

```
Random
```

## 正则表达式

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

## 国际化

```
ResourceBundle
```

## 类加载

```

```

## 运行原理

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

## 类加载器

```
类加载器
类加载机制
类加载器类型
类加载机制

ClassLoader
    getSystemClassLoader
    getParent
```

## System

```
System
    currentTimeMillis
    nanoTime
    exit
    gc
    arraycopy
    load
    loadLibrary
    mapLibraryName
    setErr
    setIn
    setOut
    lineSeparator
    clearProperty
    getProperties
    setProperties
    getProperty
        sun.boot.class.path
    setProperty
Runtime
```



# 网络

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

```

```

```

```

```

```



# Java Web

## 环境搭建

```
Java 容器
Web 项目目录结构
Java 容器
    Tomcat

Web 项目目录结构
```

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

## Servlet

```
javax.servlet
Servlet
ServletConfig
ServletContext
RequestDispatcher
GenericServlet
ServletRequest
ServletResponse
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

## web.xml

```
web.xml
    web-app
    servlet
    welcome-file-list
```

## JSP 内置对象

```
request
    getContextPath()
    String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";

```

## EL 语法

```

```

## EL 内置对象

```

```

## JSTL

```

```

```

```

```

```



# Kotlin

## 类

```
data class
继承
val side: String

```

## String

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

```

```

```

```

# Groovy

## String

```

```

## 包装类

```
BigInteger = 30g
BigDecimal = 3.5g
```

```

```

```

```

# Hibernate

```
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

# 注解处理

## 注解

```
public class YicAnnotation {
    private final static int GET=0;
    private final static int POST=1;
    private final static int DELETE=2;
    private final static int PUT=3;
    @IntDef({GET, POST, DELETE,PUT})
    @Retention(RetentionPolicy.SOURCE)
    public @interface ReqType{}
}
```

## JavaPoet

```
https://github.com/square/javapoet
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

```

```

```

```

```

```

```

