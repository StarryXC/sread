> Thinking

```
native # 修饰方法 本地方法
System loadLibrary # 加载本地库

类型映射
方法签名
```

> Memory

```
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



```

