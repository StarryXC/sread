> Thinking

```
注释
选择器
    选择器类型
样式表类型
```

> Memory

```
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

样式表类型
style="" # 内联样式
<style type="text/css"> # 内部样式表
<style> # 外部样式表 浏览器默认样式
```

