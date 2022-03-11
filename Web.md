# HTML

## 环境配置

```
浏览器 # IE Firefox Chrome

:Chrome
chrome://<function>/ # version settings extensions
```

## 语法

```
:标签类型
<tag /> # 单标签
<tag></tag> # 多标签

:注释 # <!-- -->
```

## HTML 标签

```
全局属性
id
class
style

表格标签
<table> # 表格
<tr> # 行
<th> # 表头
<td> # 单元格
<thead> # 页眉
<tbody> # 主体
<tfoot> # 页脚
<caption> # 标题
<col> # 列属性
<colgroup> # 列组

列表标签
<ol> # 有序列表
<ul> # 无序列表
<li> # 列表项
<dl> # 自定义列表
<dt> # 自定义列表项
<dd> # 自定义列表项描述

图像标签
<img> # 图像
<map> # 图像地图
<area> # 图像区域

框架标签
<frameset> # 框架集
<frame> # 框架
<noframes> # 不支持框架
<iframe> # 内联框架

结构标签
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

文本标签
<p> # 段落
<hn> # 标题
<br> # 换行
<hr> # 水平线

样式标签
<b> # 字体加粗
<big> # 大号字
<small> # 小号字
<sup> # 上标字
<sub> # 下标字
<strong> # 加重语气
<em> # 着重文字
<i> # 斜体字
<ins> # 插入字
<del> # 删除字
<center> # 居中
<font> # 字体
<basefont> # 基准字体
<s> # 删除线
<u> # 下划线

格式化标签
<i> # 斜体
<b> # 加粗
<em> # 强调
<u> # 下划线
<del> # 删除线
<sup> # 上标
<sub> # 下标
<kbd> # 键盘码

超链接标签
<a> # 超链接
<link> # 引入 CSS
<script> # 引入 JS 脚本
<noscript> # 不支持 script

布局标签
<div> # 块级标签
<span> # 行内标签
<header> # 页眉
<section> # 节
<article> # 文章
<aside> # 侧栏
<footer> # 页脚
<summary> # 细节标题
<details> # 细节
<nav> # 导航

表单标签
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

多媒体标签
<canvas> # 绘图
<object> # 对象
<param> # 对象参数
<embed> # 嵌入
<audio> # 音频
<video> # 视频
<source> # 媒体源
```

```
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
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">
<html>
    <head>
        <title>title</title>
        <meta http-equiv="keywords" content="keyword1,keyword2,keyword3" />
        <meta http-equiv="description" content="this is my page" />
        <meta http-equiv="content-type" content="text/html; charset=UTF-8" />
        <link type="text/css" rel="stylesheet" href="css.css"/>
        <style type="text/css">
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
        </style>
    </head>
    <body>
        <div id="divId" class="divClass">div</div>
        <span style="background-color: navy; color: orange;">span</span>
        <p>段落</p>
        <hr />
        <a href="html.html" target="_blank">a</a>
        <img src="html.html" alt="image" width="100" height="100" />
        <form action="action">
            <input type="text">
        </form>
        
        <font color="gray" size="7">字体</font>

        <!-- 框架标签 -->
        <frameset rows="160,*">
            <frame src="top.html" name="top">
            <frameset cols="180,*">
                <frame src="left.html" name="left">
                <frame src="right.html" name="right">
            </frameset>
        </frameset>

        <iframe src="html.html" width="500px" height="500px" />

    </body>

</html>
```

## H5 API

```
地理定位
数据存储
stroage
worker
```

```
<html>
    <head>
        <title>
            标题
        </title>
    </head>
    <body
        bgcolor="green"
        text="black"
        leftmargin="160"
        topmargin="200"
        background="logo.gif">
        <p>段落</p>
    </body>
</html>
```

```
align 文本对齐方式
bgcolor 背景颜色
color 文本颜色
<html bg="#ffffff" 
```

# CSS

## 语法

```
注释

选择器
<selector> {
	attr:value;
}

选择器类型
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

样式表类型
style="" # 内联样式
<style type="text/css"> # 内部样式表
<style> # 外部样式表 浏览器默认样式
```

```
@font-face { /*CSS 定义字体*/
    font-family: "JetBrains Mono";
    font-style: normal;
    font-weight: 400;
    src: url("4iCs6KVjbNBYlgoKfw7z.ttf");
}

@import url("input.css");
```

```
.div {
    background-color: fuchsia;
    color: lime;

    list-style-type: none;
    list-style-image: url("1.gif");

    border: none;
    border-bottom: black solid 1px;

    width: 200px;
    height: 200px;
    padding: 10px;
    margin: 10px;

    position: absolute;
    top: 80px;
    left: 80px;

    float: left;
}
```

## CSS 属性

```
表格属性
border-collapse # 合并表格边框
border-spacing # 单元格边框距离
caption-side # 表格标题位置
empty-cells # 空单元格显示
table-layout # 单元格布局方式

列表属性
list-style # 简写属性
list-style-image # 列表项图像标志
list-style-position # 列表项标志位置
list-style-type # 列表项标志类

链接四种状态
a:link # 正常状态
a:visited # 已访问状态
a:hover # 鼠标悬浮状态
a:active # 鼠标点击状态

背景属性
background # 简写属性
background-color # 背景颜色
background-image # 背景图像
background-position # 背景图像位置
background-repeat # 背景图像重复方式
background-attachment # 背景图像附加方

轮廓属性
outline # 简写属性
outline-color # 轮廓颜色
outline-style # 轮廓样式
outline-width # 轮廓宽度

字体属性
font # 简写属性
font-family # 字体系列
font-size # 字体尺寸
font-size-adjust # 字体尺寸
font-stretch # 字体水平拉伸
font-style # 字体风格
font-variant # 字体变体
font-weight # 字体粗细

文本属性
color # 文本颜色
direction # 文本方向
line-height # 行高
letter-spacing # 字符间距
text-align # 文本对齐
text-decoration # 文本修饰
text-indent # 文本缩进
text-shadow # 文本阴影
text-transform # 文本转换
unicode-bidi # 文本方向
white-space # 文本空白处理方式
word-spacing # 字间

尺寸属性
height # 元素高度
line-height # 行高
max-height # 最大高度
max-width # 最大宽度
min-height # 最小高度
min-width # 最小宽度
width # 元素宽度

定位属性
position # 定位方式
left # 左偏移
right # 右偏移
top # 上偏移
bottom # 下偏移
overflow # 
clip # 元素形状
vertical-align # 垂直对齐方式
z-index # 元素堆叠顺序
```

## 盒子模式

```
填充属性
padding # 简写属性
padding-bottom # 下边距
padding-left # 左边距
padding-right # 右边距
padding-top # 上边距

边距属性
margin # 简写属性
margin-bottom # 下边距
margin-left # 左边距
margin-right # 右边距
margin-top # 上边

边框属性
border # 简写属性
border-style # 边框样式
border-width # 边框宽度
border-color # 边框颜色
border-bottom # 下边框
border-bottom-color # 下边框颜色
border-bottom-style # 下边框样式
border-bottom-width # 下边框宽度
border-left # 左边框
border-left-color # 左边框颜色
border-left-style # 左边框样式
border-left-width # 左边框宽度
border-right # 右边框
border-right-color # 右边框颜色
border-right-style # 右边框样式
border-right-width # 右边框宽度
border-top # 上边框
border-top-color # 上边框颜色
border-top-style # 上边框样式
border-top-width # 上边框宽度
```

# Xml

## 语法

```

```

## 约束

### DTD

```

```

### Schema

```

```

## XPath

```

```

# JSON

```

```

# YAML

```

```

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

```

```

```

```

```

```

