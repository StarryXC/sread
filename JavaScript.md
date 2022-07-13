# SVG

```

```

# ProtoBuf

```

```

# Makdown

```
#n # 标题
```

# YAML

```

```

# JSON

```

```

# XML

```
<elements>
    <intElement></intElement>
    <booleanElement></booleanElement>
    <stringElement></stringElement>
    <doubleElement></doubleElement>
    <longElement></longElement>
    <arrayElement>
        <item></item>
        <item></item>
        <item></item>
    </arrayElement>
</elements>

约束
    DTD
    Schema
```

## DTD

```

```

## Schema

```

```

## XPath

```

```

```

```



# HTML

## 浏览器

```
浏览器 <script>

浏览器
IE Firefox Chrome

Chrome
chrome://version/
chrome://settings/
chrome://extensions/
```

## 标签类型

```
<tag /> # 单标签
<tag></tag> # 多标签
```

## 注释

```
<!-- -->
```

```
HTML
　　全局属性
　　表格标签
　　列表标签
　　图像标签
　　框架标签
　　结构标签
　　文本标签
　　样式标签
　　格式化标签
　　超链接标签
　　布局标签
　　表单标签
　　多媒体标签
```

## 结构标签

```

<html> # 文档根标签
<head> # 头部
<title> # 文档标题
<body> # 
<base> # 默认超链接设置
<meta> # 元数据
description 文档描述
keywords 页面关键词
author 作者

content-type 文档类型
expires 过期时间
refresh 刷新
set-cookie Cookie 设置

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">

<meta>
    http-equiv="keywords" content="keyword1,keyword2,keyword3"
    http-equiv="description" content="this is my page"
    http-equiv="content-type" content="text/html; charset=UTF-8"
    http-equiv="pragma" content="no-cache"
    http-equiv="cache-control" content="no-cache"
    http-equiv="expires" content="0"

body
    align 文本对齐方式
    bgcolor 背景颜色
    color 文本颜色
    bg="#ffffff"
    text="black"
    leftmargin="160"
    topmargin="200"
    background="logo.gif"

```

## 全局属性

```
id
class
style

<span>
    id="divId"
    class="divClass"
    style="background-color: navy; color: orange;"
```

## 文本标签

```

    段落 <p>
    标题 <hn>
    换行 <br>
    水平线 <hr>
```

## 样式标签

```

    字体加粗 <b>
    大号字 <big>
    小号字 <small>
    上标字 <sup>
    下标字 <sub>
    加重语气 <strong>
    着重文字 <em>
    斜体字 <i>
    插入字 <ins>
    删除字 <del>
    居中 <center>
    字体 <font>
        color
        size
    基准字体 <basefont>
    删除线 <s>
    下划线 <u>
```

## 格式化标签

```

    斜体 <i>
    加粗 <b>
    强调 <em>
    下划线 <u>
    删除线 <del>
    上标 <sup>
    下标 <sub>
    键盘码 <kbd>
```

## 图像标签

```
图像标签
    图像 <img>
        src
        alt
        width
        height
    图像地图 <map>
    图像区域 <area>
```

## 表单标签

```
<form> # 表单
<fieldset> # 
<legend> # 
<select> # 下拉列表
<option> # 下拉列表项
<textarea> # 多行文本域
<button> # 按钮
<datalist> # 选项列表
<option> # 选项列表项
<keygen> # 
<output> # 
<input> # 输入 type
text 文本
password 密码
submit 提交按钮
radio 单选按钮
checkbox 复选框
button 普通按钮
number 数值
date 日期
color 颜色
range 范围
month 月份
week 周
time 时间
datetime 日期时间
datetime-local 日期时间
email 邮件地址
search 搜索字段
tel 电话号码
url URL 地址

form
    action="action"
input
    type="text"
```

## 路由

```
超链接标签
<a> # 超链接
<style>
<link> # 引入 CSS
<script> # 引入 JS 脚本
<noscript> # 不支持 script

<a>
    href="html.html"
    target="_blank"
<style>
    type="text/css"
<link>
    type="text/css"
    rel="stylesheet"
    href="css.css"

链接四种状态
a:link # 正常状态
a:visited # 已访问状态
a:hover # 鼠标悬浮状态
a:active # 鼠标点击状态
```

## 列表

```
<ol> # 有序列表
<ul> # 无序列表
<li> # 列表项
<dl> # 自定义列表
<dt> # 自定义列表项
<dd> # 自定义列表项描述

list-style # 简写属性
list-style-image # 列表项图像标志
list-style-position # 列表项标志位置
list-style-type # 列表项标志类
```

```

```

## 布局

```
盒子模式
    内边距 Padding
    外边距 Margin
    边框 Border
    内容 Content

填充属性
    上右下左 padding
    上边距 padding-top
    右边距 padding-right
    下边距 padding-bottom
    左边距 padding-left

边距属性
    上右下左 margin
    上边距 margin-top
    右边距 margin-right
    下边距 margin-bottom
    左边距 margin-left

边框属性
    总样式 border
        宽度
        样式
        颜色
    上边框 border-top
    右边框 border-right
    下边框 border-bottom
    左边框 border-left
    样式 border-style
    上边框 border-top-style
    右边框 border-right-style
    下边框 border-bottom-style
    左边框 border-left-style
    宽度 border-width
    上边框 border-top-width
    右边框 border-right-width
    下边框 border-bottom-width
    左边框 border-left-width
    颜色 border-color
    上边框 border-top-color
    右边框 border-right-color
    下边框 border-bottom-color
    左边框 border-left-color

表格标签
    表格 <table>
    行 <tr>
    表头 <th>
    单元格 <td>
    页眉 <thead>
    主体 <tbody>
    页脚 <tfoot>
    标题 <caption>
    列属性 <col>
    列组 <colgroup>

表格属性
    合并表格边框 border-collapse
    单元格边框距离 border-spacing
    表格标题位置 caption-side
    空单元格显示 empty-cells
    单元格布局方式 table-layout

尺寸属性
    高度 height
    最大高度 max-height
    最小高度 min-height
    宽度 width
    最大宽度 max-width
    最小宽度 min-width
    行高 line-height

定位属性
    定位方式 position
    上偏移 top
    右偏移 right
    下偏移 bottom
    左偏移 left
    溢出 overflow
    元素形状 clip
    垂直对齐方式 vertical-align
    元素堆叠顺序 z-index

布局标签
    块级标签 <div>
    行内标签 <span>
    页眉 <header>
    节 <section>
    文章 <article>
    侧栏 <aside>
    页脚 <footer>
    细节标题 <summary>
    细节 <details>
    导航 <nav>

框架标签
    框架集 <frameset>
        cols
        rows
    框架 <frame>
        src
        name
    不支持框架 <noframes>
    内联框架 <iframe>
        src
        width
        height

float 属性
```

```

```

## worker

```

```

## geo

```

```

## 数据存储

```
stroage
```

## 绘图

```
多媒体标签
<canvas> # 绘图
<object> # 对象
<param> # 对象参数
<embed> # 嵌入
<audio> # 音频
<video> # 视频
<source> # 媒体源

<canvas id="canvas" width="1000" height	="1000" style="background:#000">
	您的浏览器不支持canvas标签
</canvas>
<script>
	var canvas=document.getElementById('canvas'); //获取canvas元素
	var cxt=canvas.getContext('2d'); //设置2d绘图环境
	var time=0; //声明一个时间参数(1:1天)
	function draw(){
		cxt.clearRect(0,0,1000,1000); //清除画布(清除之前的内容 重新画)
		//画轨道
		cxt.strokeStyle="#fff"; //设置笔触颜色
		cxt.beginPath();
		cxt.arc(500,500,100,0,360,false);
		cxt.closePath();
		cxt.stroke();
		//画太阳
		cxt.beginPath();
		cxt.arc(500,500,20,0,360,false);
		cxt.closePath();
		//太阳需要填充颜色
		//设置填充颜色(渐变色)
		//cxt.createRadialGradient(内圆心x,内圆形y,内半径,外圆心x,外圆心y,外半径);
		var sunColor=cxt.createRadialGradient(500,500,0,500,500,20);
		sunColor.addColorStop(0,"#f00");
		sunColor.addColorStop(1,"#f90");
		cxt.fillStyle=sunColor;
		cxt.fill();
		//画地球
		cxt.save();
		
		cxt.translate(500,500); //设置一下异次元空间的0，0点
		//设置旋转角度
		//cxt.rotate(90*Math.PI/190);
		//地球公转一周需要365天，time=1天 一天转365/360度
		cxt.rotate(time*365/360*Math.PI/190);
		//画出地球
		cxt.beginPath();
		cxt.arc(0,-100,10,0,360,false);
		cxt.closePath();
		//设置一下地球的颜色
		var earthColor=cxt.createRadialGradient(0,-100,0,0,-100,10);
		earthColor.addColorStop(0,'#78B1E8');
		earthColor.addColorStop(1,'#050C12');
		cxt.fillStyle=earthColor;
		cxt.fill();
		cxt.restore();
		time+=1; //每画一次图像，时间参数加1
	}
	//使地球动起来
	setInterval(draw,10);
</script>
```

```

```

# CSS

## 注释

```

```

## 选择器

```
<selector> {
	attr:value;
}
```

## 选择器类型

```
<tag> # 元素选择器
#<id> # id 选择器
.<class> # 类选择器
<tag>.<class>
* # 通用选择器 通配符选择器
<tag>, <tag>, <tag> # 分组选择器
<tag>[<attr>]  # 属性选择器
	=
	$=
	|=
	~=
	^=
	*=
<tag> <tag> # 后代选择器 包含选择器
<tag> > <tag> # 子元素选择器
<tag> + <tag> # 相邻兄弟选择器
            div {
                background-color: green;
                color: red;
                font-size: 30px;
            }
            .divClass { }
            #divId { }
            span b {}
            div,span b {}
            a:LINK {}
            a:HOVER {}
            a:ACTIVE {}
            a:VISITED {}
            p:FIRST-LETTER {}
            input:FOCUS {}

```

## 样式表类型

```
内联样式 <element>
    style="key:value;key:value"
内部样式表 <style>
    type="text/css"
外部样式表 浏览器默认样式 <link>
    rel="stylesheet"
    type="text/css"
    href
```

## 背景属性

```
background # 简写属性
background-color # 背景颜色
background-image # 背景图像
background-position # 背景图像位置
background-repeat # 背景图像重复方式
background-attachment # 背景图像附加方
```

## 轮廓属性

```
outline # 简写属性
outline-color # 轮廓颜色
outline-style # 轮廓样式
outline-width # 轮廓宽度
```

```
　　表格属性
　　列表属性
　　链接四种状态
　　背景属性
　　轮廓属性
　　字体属性
　　文本属性
　　尺寸属性
　　定位属性
　　float
```

```

```



## Flex

```

```

## 文本属性

```
文本属性
    文本颜色 color
    文本方向 direction
    行高 line-height
    字符间距 letter-spacing
    文本对齐 text-align
    文本修饰 text-decoration
    文本缩进 text-indent
    文本阴影 text-shadow
    文本转换 text-transform
    文本方向 unicode-bidi
    文本空白处理方式 white-space
    字间 word-spacing
```

## 字体属性

```
字体属性
    字体 font
    字体系列 font-family
    字体尺寸 font-size
    字体尺寸 font-size-adjust
    字体水平拉伸 font-stretch
    字体风格 font-style
    字体变体 font-variant
    字体粗细 font-weight

@font-face { /*CSS 定义字体*/
    font-family: "JetBrains Mono";
    font-style: normal;
    font-weight: 400;
    src: url("4iCs6KVjbNBYlgoKfw7z.ttf");
}
// 导入字体
@import url("dir/input.css");

```

```

```

```

```



```

```

# JavaScript

```
在线压缩 http://tool.oschina.net/jscompress/
在线格式化 http://tool.oschina.net/codeformat/js/

```



## 变量定义

```
var
```

## 变量类型

```
本地变量
全局变量
```

## JS 对象

```
Number
String
Boolean
Array
Object
Date
Math
RegExp
```

## BOM 对象

```
Window
Screen
Location
History
Navigator
console
```

```

```

# ECMAScript

## 注释

```

```

## 变量定义

```
let const
```

```

```

```

```

```

```

```

```

# TypeScript

## 注释

```

```

## 变量定义

```
var <name>:<type>
```

## 数据类型

```
number string
```

## 运算符

```

```

## 流程控制

```

```

# jQuery

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

# Ionic

```

```

```

```

```

```

# TelerikUI

```

```

```

```

```

```

```

```



# Vue

```
vue
```



```
双向数据绑定
```

## 事件处理

```

```

## 路由

```

```

## 指令

```
自定义指令
```

## 修饰符

```

```

## 循环

```

```

## 条件判断

```

```

# React

## JSX

```
注释
元素数组
样式
表达式
class 属性
for 属性
```

## 环境搭建

```
create-react-app
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

