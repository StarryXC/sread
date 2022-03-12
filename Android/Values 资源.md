> Thinking

```
Vibrator
```

> Memory

```
<resources> # 值资源
<integer> # name integers.xml
<integer-array> # name <item>
<dimen> # name dimens.xml 尺寸资源 尺寸计量 dp sp px pt mm in
<color> # name colors.xml transparent white
<bool> # name bools.xml
<string> # name strings.xml
<string-array> # name <item>
<plurals> # name
	<item> # quantity zero one two few many other
<array> # name <item>
<item>
	name # 
	type # id
	format # reference
<declare-styleable> # name
<attr>
	name
	format
<enum>
	name
	value

Resources # Context.getResources	
	getResourceName
	getResourcePackageName getResourceTypeName getResourceEntryName
	getIdentifier # ("name", "id", context.getPackageName())
	getInteger getIntArray
	getDimension getDimensionPixelOffset getDimensionPixelSize
	getColor
	getBoolean
	getString getStringArray
	getText getTextArray
	getDisplayMetrics
	getDrawable
TypedValue
	COMPLEX_UNIT_DIP
	applyDimension
DisplayMetrics
	widthPixels heightPixels
Context
	obtainStyledAttributes # attrs styleable
TypedArray
	getString
	getBoolean
	getInt getInteger getFloat
	getDimension getDimensionPixelSize
	getFraction # string
	getColor
	recycle
android.R.color.transparent
```

