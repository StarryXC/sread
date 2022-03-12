> Thinking

```
Drawable mutate
	ColorDrawable
	GradientDrawable # 渐变 线性渐变 发散渐变 平铺渐变
	DrawableContainer
		LevelListDrawable
		StateListDrawable
		AnimationDrawable
	LayerDrawable
		TransitionDrawable
	DrawableWrapper
		ScaleDrawable
		ClipDrawable
		InsetDrawable
	BitmapDrawable
	NinePatchDrawable

Drawable
	setBounds
	draw
```

> Memory

```
GradientDrawable
<shape> # GradientDrawable
	android:shape # rectangle ring
<corners>
	android:radius
	android:topLeftRadius android:topRightRadius
	android:bottomLeftRadius android:bottomRightRadius
<gradient> # 渐变效果
	android:angle # 0-360
	android:centerX android:centerY # 50%
	android:startColor android:centerColor android:endColor
	android:type # sweep radial
	android:useLevel # true
	android:gradientRadius
<padding> # 内边距 android:left android:right android:top android:bottom
<size> # 区域大小 android:width android:height
<solid> # 背景颜色 会覆盖gradient android:color
<stroke> # 边框效果
	android:width
	android:color
	android:dashGap android:dashWidth


<level-list> # LevelListDrawable
<item>
	android:drawable
	android:minLevel android:maxLevel # int
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
</layer-list>

<selector> # StateListDrawable
	android:constantSize
	android:dither
	android:variablePadding
	android:visible
<item>
	android:drawable
	android:state_pressed


<layer-list> # LayerDrawable
<item>
	android:id
	android:drawable # >V< shape bitmap
	android:left android:right android:top android:bottom

<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android" >
    <item android:id="@android:id/progress">
        <clip>
            <shape> <solid android:color="#0071f8"/> </shape>
        </clip>
    </item>
    <item android:left="5dp" android:top="5dp">
        <shape> <solid android:color="#60000000"/> </shape>
    </item>
    <item android:bottom="5dp" android:right="5dp">
        <shape> <solid android:color="#000000"/> </shape>
    </item>
</layer-list>


<animation-list> # AnimationDrawable
	android:oneshot
<item>
	android:drawable
	android:duration


<scale> # ScaleDrawable
	android:drawable
	android:scaleGravity # center
	android:scaleWidth android:scaleHeight # 50%


<clip> # ClipDrawable 裁剪
	android:drawable
	android:clipOrientation # vertical
	android:gravity # center

<inset> # InsetDrawable 嵌入
	android:drawable # 
	android:inset
	android:insetLeft android:insetRight android:insetTop android:insetBottom


<transition> # TransitionDrawable
<item>
	android:drawable
	android:id
	android:left android:right android:top android:bottom


<bitmap> # BitmapDrawable Bitmap .png / .jpg / .gif
	android:src
	android:antialias
	android:dither
	android:filter
	android:gravity # center
	android:mipMap
	android:tileMode # clamp mirror 镜像平铺效果


<nine-patch> # NinePatchDrawable .9.png
	android:src
	android:dither


<vector>  VectorDrawable
	android:width android:height # dimen
	android:viewportWidth android:viewportHeight # int
<path>
	android:fillColor
	android:pathData
	android:strokeWidth
	android:strokeColor
	android:fillType # nonZero evenOdd
<aapt:attr> # xmlns:aapt="http://schemas.android.com/aapt"
	name # android:fillColor
<gradient>
	android:startX android:endX # 78.5885
	android:startY android:endY # 78.5885
	android:type # linear
<item>
	android:color
	android:offset # 0.0 1.0


<adaptive-icon> # AdaptiveIconDrawable mipmap
<background> # android:drawable
<foreground> # android:drawable






```

