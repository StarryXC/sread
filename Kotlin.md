

```
@Retention(AnnotationRetention.SOURCE)
annotation class <AnnotationName>
```

# 集合

```
var arra = listOf<String>("123", "234", "345")
var arra2 = listOf<String>("123", "234", "345")

arra.forEach {
	println(it)
}

arra = arra.filter {
	it.contains("5")
}

arra.indexOf("123")
println(arra.firstOrNull())
println(arra.filterNotNull())
arra.getOrNull(12)
    arra.size
```

```
@JvmField
para?.let{}

1.toBigDecimal()
.isNullOrEmpty()
.isEmpty()
string.toDouble()
.forEachIndexed
ContextCompat.getColor(

subscribe = Flowable.interval(0, 5, TimeUnit.SECONDS)
.onBackpressureDrop()
.subscribe {
 smartRefresh.setOnRefreshListener {
smartRefresh.finishRefresh()
smartRefresh.setOnLoadMoreListener {
 smartRefresh.finishLoadMore()
 <style name="AppTheme.NoActionBar">
<item name="windowActionBar">false</item>
<item name="windowNoTitle">true</item>
</style>

<style name="AppTheme.AppBarOverlay" parent="ThemeOverlay.AppCompat.Dark.ActionBar" />
<style name="AppTheme.PopupOverlay" parent="ThemeOverlay.AppCompat.Light" />
<style name="AppTheme.NoActionBar">
<item name="windowActionBar">false</item>
<item name="windowNoTitle">true</item>
<item name="android:windowDrawsSystemBarBackgrounds">true</item>
<item name="android:statusBarColor">@android:color/transparent</item>
</style>
disposable = Flowable.fromIterable(coinTypeBeans)
    .map { coinTypeBean -> coinTypeBean.mark.replace("_", "/").toUpperCase() }
    .distinct()
    .toList()
    .subscribe { strings, _ ->
    }
val data = JSONObject.parseObject(message) alibaba
        String.format(
        code.replace(
        ContextCompat.getDrawable(
radioGroup.setOnCheckedChangeListener { _, i ->
        childFragmentManager.beginTransaction()
                .replace(R.id.depth_fragment, BibiDepthFragment.newInstance(code))
        .commit()
LiveEventBus.get(Event.BIBI_REFRESH)
        .observe(this, androidx.lifecycle.Observer { refresh() })
    LiveEventBus.get(Event.BIBI_REFRESH).post(1)
com.afollestad.materialdialogs.MaterialDialog;
MaterialDialog dialog = new MaterialDialog.Builder(context)
                .customView(R.layout.bibi_dialog_trade_info_tip, false)
                .autoDismiss(false)
                .cancelable(false)
                .show();

<?xml version="1.0" encoding="utf-8" standalone="no"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">

    <item android:id="@android:id/background">

        <shape></shape>

    </item>
    <item android:id="@android:id/progress">
        <clip>
            <shape>
                <gradient
                    android:centerColor="#601ED189"
                    android:endColor="#601ED189"
                    android:startColor="#601ED189" />
            </shape>
        </clip>
    </item>
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recycler_list"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:paddingStart="10dp"
        android:paddingEnd="10dp"
        tools:itemCount="10"
        tools:listitem="@layout/machine_item_income" />
</layer-list>
    <CheckBox
        android:id="@+id/check_no_tip"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:buttonTint="@color/common_hint"
        android:text="不再提示"
        android:textColor="@color/common_hint" />
    <RadioGroup
        android:id="@+id/trade_type_group"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:checkedButton="@id/check_buy"
        android:orientation="horizontal"
        android:paddingLeft="@dimen/common_margin"
        android:paddingRight="@dimen/common_margin">
<androidx.cardview.widget.CardView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    app:cardBackgroundColor="@color/common_tab"
    app:cardCornerRadius="5dp"
    app:cardUseCompatPadding="true"
    app:contentPadding="@dimen/common_margin">


Glide.with(holder.itemView.context).load(item.image)
                        .into(holder.getView(R.id.img_icon) as ImageView)
                        left_drawerLayout.closeDrawer(GravityCompat.START)
mView.iv_close.setOnClickListener { dismiss() }
 it.rise.split("|").toList().filter { f -> f.isNotEmpty() }
 
 ## hello world JNI
// extern "C" 标识后面的用C编译 ,这里的意思是这个函数用C编译,C++为了函数重载会把参数带上,而c没有函数重载
// JNICALL表示调用约定，相当于C++的stdcall，说明调用的是本地方法
// JNIEXPORT表示函数的链接方式，当程序执行的时候从本地库文件中找函数
// 中间的jstring就是返回类型,是c++中对应java中String的类型
// JNIEnv 是对java环境的引用,并且提供了一些类型转换方法
// jobject 是调用这个函数的java对象.没发现如何使用
extern "C" JNIEXPORT jstring JNICALL Java_com_happy_fei_helloworldjni_MainActivity_stringFromJNI(
        JNIEnv *env,
        jobject /* this */) {
    std::string hello = "Hello from C++";
    return env->NewStringUTF(hello.c_str());
}

​```

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<meta http-equiv="content-type" content="text/html; charset=UTF-8">
<link rel="stylesheet" type="text/css" href="./styles.css">
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">    
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
	
extern "C" 告诉编译器后面的按照C的风格编译.我测试下如果函数前不加extern "C"会报错
​```
java.lang.UnsatisfiedLinkError: No implementation found for java.lang.String com.happy.fei.helloworldjni.MainActivity.helloWorld(java.lang.String, java.lang.String) (tried Java_com_happy_fei_helloworldjni_MainActivity_helloWorld and Java_com_happy_fei_helloworldjni_MainActivity_helloWorld__Ljava_lang_String_2Ljava_lang_String_2)
​```
错误的信息是没有找到helloWorld函数也没有找到helloWorld(String,String)函数.
问题:什么时候可以不使用extern "C". 我这个文件是CPP啊,不过留待以后熟练了发现吧.现在还不太溜

###### 稍微难一点
```
