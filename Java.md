# Java

```
环境搭建
    发展史
        平台分支
        JDK 5.0 特性
    命令行
        javac
        java
        jar
        javap
        javah
        javadoc

语法
    基础语法
        预留保留字
        注释
        变量定义
            数据类型
            变量类型转换
            字面量默认类型
        运算符
        流程控制
        数组
        方法
            参数传递
            可变参数
            方法重载
            Lambda
            递归调用
    正则表达式
    	正则语法
    	Pattern
    异常处理机制
        异常处理语句
        Throwable
        自定义异常
常用类
    Object
    字符串
    Random
    Scanner
    日期
    Math
    包装类
    大数值
    格式化
    Runtime
    ResourceBundle
    UUID
    定时器
GUI 编程
IO 编程
    IO 流
    序列化
    文件
NIO
    Buffer
    Channel
JCU 并发编程
JDBC 编程
	mysql # 注册驱动 jdbc:mysql://localhost:3306/jdbc root com.mysql.jdbc.Driver
    DriverManager
    Type
网络编程
    TCP Socket
    UDP Socket
    Http URL
JSON 编程
    orgJson
    gson
    fastjson
XML 编程
    DOM
    SAX
    XmlPull
集合框架
    Collection
    	TreeSet Comparator
    Map
    Dictionary
    Iterator
    Collections
    Arrays
    Objects
反射机制
    Class
    AccessibleObject
    Array
数据加密
	加密原理 使用异或加密图片数据
	MessageDigest
JNDI
RMI
SPI
    ServiceLoader


  # JAXP Java API for XML Processing

DocumentBuilderFactory # newInstance newDocumentBuilder
DocumentBuilder # parse newDocument
Document # getElementsByTagName createElement
Element # attribute
NodeList # item getLength
Node

TransformerFactory # newInstance newTransformer
Transformer # transform | DOMSource StreamResult

SAX
SAXParserFactory
SAXParser
ContentHandler
DefaultHandler

 # 占用内存资源少
XmlPullParserFactory
XmlPullParser
XmlSerializer


运行原理
	内存模型
	类加载
	类加载机制
类加载器类型
ClassLoader
    <跨平台原理>
    <运行机制>
    <垃圾回收机制>


```

## 面向对象语法

```javascript
:<类>
    <类定义>
    	<类成员默认初始化值:零值>
    <对象创建>
        <类初始化>
            <代码块种类>
        <匿名对象>
    instanceof
    new
    <属性访问器>

<构造方法:调用 重载 默认 返回值>

<访问控制权限>

<abstract>

<strictfp>

<static>

<final: 编译器优化属性内联>
    <不可变类>

<内部类>
    <静态内部类>
    <匿名内部类>

<继承>
    
    <this>
    <super>
    <方法覆写>

<接口>
    <默认函数>

<包>
    <静态导入>
    <导包>

<多态>
    <方法多态性>
    <继承多态>

<泛型> # 类 变量 方法 | ? extends

<枚举> # 构造方法 属性 抽象方法
	Enum # values ordinal name valueOf

<注解>
    <元注解>
        @Target # ElementType FIELD METHOD CONSTRUCTOR PARAMETER LOCAL_VARIABLE ANNOTATION_TYPE PACKAGE
        @Retention # RetentionPolicy SOURCE CLASS RUNTIME
    <内置注解>

<正则表达式> # 数字 字母 [] {} w
    ^\\w+([-+.]\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$ # 匹配email
    [\u0391-\uFFE5]+$ # 汉字
```



```javascript
synchronized # 线程同步 锁膨胀
volatile # 共享变量内存可见性

Object # wait notify

Thread # 创建线程
ThreadGroup
Runnable
StackTraceElement

线程池
锁
Condition
	await
    signal
CountDownLatch
	countDown await getCount
Exchanger

Collection
	Queue
		BlockingQueue # 阻塞队列
CopyOnWriteArrayList
SynchronousQueue
AbstractCollection
	AbstractSet
		CopyOnWriteArraySet
        ConcurrentSkipListSet
	AbstractQueue
		ArrayBlockingQueue
		ConcurrentLinkedQueue
        LinkedBlockingDeque
        LinkedBlockingQueue
        PriorityBlockingQueue
	ConcurrentLinkedDeque

CopyOnWriteArrayList
	lock: ReentrantLock
	array: Object[]
CopyOnWriteArrayList.COWIterator
CopyOnWriteArrayList.COWSubList
CopyOnWriteArrayList.COWSubListIterator

CopyOnWriteArraySet
	al: CopyOnWriteArrayList<E>

ArrayBlockingQueue
	lock: ReentrantLock
	items: Object[]
	takeIndex: int
	putIndex: int
	count: int
ArrayBlockingQueue.Itr

ConcurrentLinkedQueue
	head: Node<E>
	tail: Node<E>
ConcurrentLinkedQueue.Itr
ConcurrentLinkedQueue.Node
	item: E
	next: Node<E>

ConcurrentLinkedDeque
	head: Node<E>
	tail: Node<E>
ConcurrentLinkedDeque.AbstractItr
	ConcurrentLinkedDeque.Itr
ConcurrentLinkedDeque.Node
	item: E
	prev: Node<E>
	next: Node<E>

Map
	ConcurrentMap
    ConcurrentNavigableMap
AbstractMap
	ConcurrentHashMap
    ConcurrentSkipListMap

ConcurrentHashMap
	table: Node<K,V>[]
	nextTable: Node<K,V>[]
ConcurrentHashMap.CollectionView
	ConcurrentHashMap.KeySetView
	ConcurrentHashMap.ValuesView
	ConcurrentHashMap.EntrySetView
ConcurrentHashMap.Node
	hash: int
	key: K
	val: V
	next: Node<K,V>
```

## Spliterator

```javascript
Spliterator<String> spliterator = new Spliterator<String>() {};
Consumer

OfPrimitive
OfInt
OfLong
OfDouble
```

## Stream

```javascript
Stream
Optional
Collectors

Stream
Consumer
Supplier

Predicate

Function

ToIntFunction
ToLongFunction
ToDoubleFunction
IntFunction

BiFunction
apply
andThen
BinaryOperator

Collector
Collectors
```

# 内存管理

```javascript
垃圾回收 GC
不再有任何指向的空间为垃圾空间

数组定义
数组名称 栈内存
数组对象 堆内存 一组连续内存

对象 对象名称栈内存 对象属性堆内存

全局代码区 所有的方法
全局数据区 存放static类型属性

4种代码块
普通代码块 写在一个方法之中的语句块
构造块 写在类中的一个语句块
	优先于构造方法执行，执行多次
静态块 写在类中使用static声明的语句块
	优先于构造块与构造方法执行，用于初始化静态属性，只执行一次
同步代码块 多线程
JMM 内存模型

对象引用类型
Reference
```

# JNI 编程

```javascript
native # 修饰方法 本地方法
System loadLibrary # 加载本地库

:类型映射
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

:方法签名
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
```

```
GetEnv # jni.h
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

# 多媒体

```
ImageIO
	read
	write
```



```
对象多态性

创建对象
类的声明
类的实例化
类的成员
	类的属性
	类的方法
	构造方法
	访问类成员

对象操作
对象比较
对象拷贝 对象克隆
对象哈希值 哈希函数
字符串表示

匿名对象
只使用一次的对象

类的封装
访问修饰符
构造方法私有化 单例模式
外部不能直接操作类的属性
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

JNI
jstring
JNIEnv

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

public class MeJunit {

	@Test
	public void textMethod() {
		Assert.assertEquals(10, 10);
	}

}

```

# JUnit

# Java Web

```
环境搭建
    Web 项目目录结构
    Java 容器
        Tomcat
web.xml
    web-app
    servlet
    welcome-file-list
JSP
	JSP 语法
		指令
		脚本
		表达式
	内置对象
Servlet
EL
JSTL
```

# JSP

```
<%@ page language="java" import="java.util.*" pageEncoding="ISO-8859-1"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
```

# Servlet

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

# Apache

## Commons IO

```
org.apache.commons:commons-io:1.3.2
```

# Struts

```
<struts-config>
<form-beans>
<form-bean>
<action-mappings>
<action>
<forward>
```

```
Action
DispatchAction
ActionMapping
ActionForward
ActionForm
FormFile
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
```

```
<struts>
<package>
<action>
<result>
<constant>
<include>
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

# Hibernate

```
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




```

```
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

```

```

```

```

```

```

Configuration
AnnotationConfiguration
SessionFactory
Session
Transaction
SessionStatistics



# MyBatis

# Mina

# Netty

# Hadoop

# Hive

# Spark

# XNIO

# Kotlin

```
环境搭建
    命令行
        kotlinc
语法
    基本语法
        注释
        变量定义 # var val
            数据类型
        运算符
        流程控制
        方法 # fun
    面向对象语法
        类
        对象创建 # object
            延迟初始化 # lateinit by lazy
            构造函数 # init
            访问控制 # 默认 private
        半生对象 # companion
        对象表达式
        注解
集合
    
高阶函数
```



# Groovy

```
环境搭建
    命令行
        groovyc
语法
    基础语法
        注释
        变量定义 # def
            数据类型
        运算符
        流程控制
        方法 # 默认参数
    面向对象语法
        类
            访问控制 # 默认 public
        接口
        包
常用类
    字符串
    包装类 # BigInteger = 30g BigDecimal = 3.5g
```



# Scala

```
变量定义 # val var
    运算符
```

