# Lifecycles

```
LifecycleOwner # getLifecycle
Lifecycle
	addObserver removeObserver # LifecycleObserver
	getCurrentState # Lifecycle.State
Lifecycle.State
	isAtLeast
	INITIALIZED
	CREATED
	STARTED
	RESUMED
	DESTROYED
Lifecycle.Event #
	ON_ANY
	ON_CREATE ON_DESTROY
	ON_START ON_STOP
	ON_RESUME ON_PAUSE
LifecycleObserver
	LifecycleEventObserver # onStateChanged
	FullLifecycleObserver
		onCreate onDestroy
		onStart onStop
		onResume onPause

ComponentActivity
	mLifecycleRegistry
ReportFragment

SafeIterableMap<K, V>
SafeIterableMap<K, V> implements Iterable<Map.Entry<K, V>>

-Entry<K, V> mStart
-Entry<K, V> mEnd
-WeakHashMap<SupportRemove<K, V>, Boolean> mIterators

ListIterator<K, V> implements Iterator<Map.Entry<K, V>>, SupportRemove<K, V>
Entry<K, V> mExpectedEnd
Entry<K, V> mNext

AscendingIterator<K, V> extends ListIterator<K, V>
DescendingIterator<K, V> extends ListIterator<K, V>
IteratorWithAdditions implements Iterator<Map.Entry<K, V>>, SupportRemove<K, V>

SupportRemove<K, V>
Entry<K, V> implements Map.Entry<K, V>

```





# Android KTX

```
val mSharedPreferences = context.getSharedPreferences("", Context.MODE_PRIVATE)
        mSharedPreferences.edit() {
            putBoolean("boo",false)
        }

        val mView: View = View(context)
        mView.doOnLayout {
        }
        mView.setOnClickListener({v -> })
        mView.setOnClickListener {  }

        val string = "baidu.com"
//        string.javaClass.simpleName
        val uri = string.toUri()

        val mIntent = Intent(context, MyAppCompatActivity::class.java)
        context.startActivity(mIntent)


//        var stackTrace : Array<StackTraceElement>  = Thread.currentThread().stackTrace
//        var stackTraceElement : StackTraceElement = stackTrace[3]
```

# Design

```
com.google.android.material # com.android.support
	material(1.1.0) # design(28.0.0)
androidx.coordinatorlayout # com.android.support
	coordinatorlayout(1.1.0) # coordinatorlayout

CoordinatorLayout
CoordinatorLayout.Behavior
	getTag setTag
	onAttachedToLayoutParams onDetachedFromLayoutParams
	onInterceptTouchEvent onTouchEvent
	getScrimColor getScrimOpacity
	onSaveInstanceState onRestoreInstanceState
	onMeasureChild onLayoutChild
	layoutDependsOn
	onDependentViewChanged onDependentViewRemoved
	onNestedScrollAccepted
	onNestedScroll onNestedPreScroll
	onNestedFling onNestedPreFling
	onStartNestedScroll onStopNestedScroll
CoordinatorLayout.LayoutParams
	getBehavior setBehavior

AppBarLayout
	getTotalScrollRange
AppBarLayout.LayoutParams
	getScrollFlags setScrollFlags
	getScrollInterpolator setScrollInterpolator
AppBarLayout.Behavior
	setTopAndBottomOffset

CollapsingToolbarLayout
CollapsingToolbarLayout.LayoutParams

NavigationView
	setNavigationItemSelectedListener # NavigationView.OnNavigationItemSelectedListener onNavigationItemSelected
	getMenu inflateMenu

BottomNavigationView
	setOnNavigationItemSelectedListener # BottomNavigationView.OnNavigationItemSelectedListener onNavigationItemSelected
	getMenu inflateMenu # app:menu menu 资源

FloatingActionButton
	setOnClickListener

Snackbar
	make
	LENGTH_LONG
    setAction
    show

Toolbar # setSupportActionBar

```

# ConstraintLayout

```
androidx.constraintlayout # com.android.support.constraint
	constraintlayout(1.1.3) # constraint-layout
	constraintlayout-solver(1.1.3) # constraint-layout-solver

ConstraintLayout
ConstraintLayout.LayoutParams
	<location> <circle> <goneMargin>
	
	leftToLeft leftToRight # app:layout_constraintLeft_toLeftOf app:layout_constraintLeft_toRightOf
	rightToRight rightToLeft # app:layout_constraintRight_toRightOf app:layout_constraintRight_toLeftOf
	topToTop topToBottom # app:layout_constraintTop_toTopOf app:layout_constraintTop_toBottomOf
	bottomToBottom bottomToTop # app:layout_constraintBottom_toBottomOf app:layout_constraintBottom_toTopOf
	startToStart startToEnd # app:layout_constraintStart_toStartOf app:layout_constraintStart_toEndOf
	endToEnd endToStart # app:layout_constraintEnd_toEndOf app:layout_constraintEnd_toStartOf
	baselineToBaseline # app:layout_constraintBaseline_toBaselineOf
	matchConstraintPercentWidth matchConstraintPercentHeight # app:layout_constraintWidth_percent app:layout_constraintHeight_percent
	matchConstraintMaxWidth matchConstraintMaxHeight # app:layout_constraintWidth_max app:layout_constraintHeight_max
	matchConstraintMinWidth matchConstraintMinHeight # app:layout_constraintWidth_min app:layout_constraintHeight_min
	horizontalBias verticalBias # app:layout_constraintHorizontal_bias app:layout_constraintVertical_bias
	circleAngle # app:layout_constraintCircleAngle
	circleConstraint # app:layout_constraintCircle
	circleRadius # app:layout_constraintCircleRadius
	constrainedWidth constrainedHeight # app:layout_constrainedWidth app:layout_constrainedHeight
	goneLeftMargin goneRightMargin # app:layout_goneMarginLeft app:layout_goneMarginRight
	goneTopMargin goneBottomMargin # app:layout_goneMarginTop app:layout_goneMarginBottom
	goneStartMargin goneEndMargin # app:layout_goneMarginStart app:layout_goneMarginEnd
	guideBegin guideEnd # app:layout_constraintGuide_begin app:layout_constraintGuide_end
	guidePercent # app:layout_constraintGuide_percent
	horizontalWeight verticalWeight # app:layout_constraintHorizontal_weight app:layout_constraintVertical_weight
	horizontalChainStyle verticalChainStyle # app:layout_constraintHorizontal_chainStyle app:layout_constraintVertical_chainStyle spread
	dimensionRatio # app:layout_constraintDimensionRatio 1:1
	matchConstraintDefaultWidth matchConstraintDefaultHeight # app:layout_constraintHeight_default app:layout_constraintWidth_default spread
	# app:layout_constraintLeft_creator app:layout_constraintRight_creator app:layout_constraintTop_creator app:layout_constraintBottom_creator
	# app:layout_constraintBaseline_creator
	# app:constraint_referenced_ids
	# app:constraintSet

Guideline
Placeholder
Barrier
ConstraintSet

```

# SwipeRefreshLayout

```
androidx.swiperefreshlayout # com.android.support 下拉刷新
	swiperefreshlayout(1.0.0) # swiperefreshlayout

SwipeRefreshLayout
	setOnRefreshListener # SwipeRefreshLayout.OnRefreshListener onRefresh
	isRefreshing setRefreshing
	setOnChildScrollUpCallback # SwipeRefreshLayout.OnChildScrollUpCallback canChildScrollUp
	canChildScrollUp
```

# RecyclerView

```
androidx.recyclerview:recyclerview:1.1.0
androidx.recyclerview # com.android.support
	recyclerview-selection # recyclerview-selection
	recyclerview # recyclerview-v7

RecyclerView.LayoutManager
	LinearLayoutManager
		GridLayoutManager
	StaggeredGridLayoutManager

RecyclerView
	setAdapter # RecyclerView.Adapter BaseAdapter<Bean, Holder> OnItemClickListener<Bean>
		# onCreateViewHolder(viewType) onBindViewHolder getItemCount
	setLayoutManager # 
	addItemDecoration # RecyclerView.ItemDecoration getItemOffsets
	setHasFixedSize
	addOnScrollListener setOnScrollListener # RecyclerView.OnScrollListener onScrolled onScrollStateChanged
	setItemAnimator # RecyclerView.ItemAnimator
	addOnItemTouchListener # RecyclerView.OnItemTouchListener

RecyclerView.Adapter
	getItemCount # == null
	onBindViewHolder
	onCreateViewHolder # LayoutInflater.from(viewGroup.getContext()).inflate(R.layout.item_chat, viewGroup, false);
	notifyDataSetChanged

RecyclerView.ViewHolder
	getAdapterPosition
	getLayoutPosition

GridLayoutManager
	getSpanSizeLookup setSpanSizeLookup # GridLayoutManager.SpanSizeLookup getSpanSize
	getSpanCount setSpanCount

RecyclerView.ItemDecoration
	getItemOffsets
	onDraw
	onDrawOver

RecyclerView.OnItemTouchListener # SimpleOnItemTouchListener
	onInterceptTouchEvent
	onTouchEvent
	onRequestDisallowInterceptTouchEvent

ItemTouchHelper
ItemTouchHelper.Callback
	getMovementFlags
	onMove
	onSwiped
```

# DrawerLayout

```
androidx.drawerlayout # com.android.support
	drawerlayout # drawerlayout

DrawerLayout
	addDrawerListener # DrawerLayout.DrawerListener

DrawerLayout.DrawerListener # SimpleDrawerListener
	onDrawerSlide
	onDrawerOpened
	onDrawerClosed
	onDrawerStateChanged
```

# CardView

```
androidx.cardview # com.android.support
	cardview(1.0.0) # cardview-v7

CardView
	getRadius setRadius
```

# ViewPager

```
androidx.viewpager:viewpager:1.0.0
androidx.viewpager # com.android.support
	viewpager # viewpager

ViewPager
	setPageTransformer # ViewPager.PageTransformer transformPage
	addOnAdapterChangeListener removeOnAdapterChangeListener # ViewPager.OnAdapterChangeListener onAdapterChanged
		
	addOnPageChangeListener removeOnPageChangeListener # ViewPager.OnPageChangeListener
		# onPageScrolled onPageSelected onPageScrollStateChanged
		# ViewPager.SimpleOnPageChangeListener
	getAdapter setAdapter
	getCurrentItem setCurrentItem
	getOffscreenPageLimit setOffscreenPageLimit
	getPageMargin setPageMargin
	setPageMarginDrawable
	onInterceptTouchEvent # false 禁止滑动
PagerAdapter
	getCount
	isViewFromObject # view == object
	instantiateItem # addView
	destroyItem # removeView
FragmentPagerAdapter FragmentStatePagerAdapter
	getItem
	getCount
	getPageTitle
```

# 

```











```



# Compats

```
ContextCompat
	getColor
	checkSelfPermission
ActivityCompat
	requestPermissions
```



# 注解

```
androidx.annotation # com.android.support
	annotation # support-annotations(23.4.0)

Nullness注解
    @Nullable 参数可null
    @NonNull 参数不可null
Resource Type 注解
    @LayoutRes
    @AnimatorRes
    @AnimRes
    @AnyRes 任意资源类型
    @ArrayRes
    @AttrRes
    @BoolRes
    @ColorRes
    @DimenRes
    @DrawableRes
    @FractionRes
    @IdRes
    @IntegerRes
    @InterpolatorRes
    @IntDef
    @LongDef
    @Dimension
    @MenuRes
    @PluralsRes
    @RawRes
    @StringRes
    @StyleableRes
    @StyleRes
    @TransitionRes
    @XmlRes
    @ColorInt
    @ColorLong
Threading 注解
    @UiThread UI线程
    @MainThread 主线程
    @WorkerThread 子线程
    @BinderThread 绑定线程
Typedef 注解
    @IntDef
    @StringDef
Value Constraints注解
    @IntRange
    @FloatRange
    @Size

    集合不能为空: @Size(min=1)
    字符串最大只能有23个字符: @Size(max=23)
    数组只能有2个元素: @Size(2)
    数组的大小必须是2的倍数 (例如图形API中获取位置的x/y坐标数组: @Size(multiple=2)
Permissions 注解
    @RequiresPermission
    @RequiresPermission(Manifest.permission.SET_WALLPAPER)
    @RequiresPermission(anyOf = {
    Manifest.permission.ACCESS_COARSE_LOCATION,
    Manifest.permission.ACCESS_FINE_LOCATION}) // 至少需要权限集合中的一个
    @RequiresPermission(allOf = {
    Manifest.permission.READ_HISTORY_BOOKMARKS,
    Manifest.permission.WRITE_HISTORY_BOOKMARKS}) // 如果你同时需要多个权限

    对于intents的权限 直接在定义的intent常量字符串字段上标注权限需求
    @RequiresPermission(android.Manifest.permission.BLUETOOTH)
public static final String ACTION_REQUEST_DISCOVERABLE =
            "android.bluetooth.adapter.action.REQUEST_DISCOVERABLE";

            对于content providers的权限，你可能需要单独的标注读和写的权限访问，所以可以用@Read或者@Write标注每一个权限需求
            @RequiresPermission.Read(@RequiresPermission(READ_HISTORY_BOOKMARKS))
@RequiresPermission.Write(@RequiresPermission(WRITE_HISTORY_BOOKMARKS))
public static final Uri BOOKMARKS_URI = Uri.parse("content://browser/bookmarks");

Overriding Methods 注解
    @CallSuper
Return Values注解
    @CheckResult
    如果你的方法返回一个值，你期望调用者用这个值做些事情，那么你可以使用@CheckResult注解标注这个方法。
 这个在具体使用中用的比较少，除非特殊情况，比如在项目中对一个数据进行处理，这个处理比较耗时，我们希望调用该函数的调用者在不需要处理结果的时候，提示没有使用，酌情删除调用。
Keep：指出一个方法在被混淆的时候应该被保留。
   VisibleForTesting：可注解一个类，方法，或变量，表示有更宽松的可见性，这样它能够有更宽泛的可见性，使代码可以被测试。
Support Annotations中的注解的生命周期全部是RetentionPolicy.CLASS

IntelliJ注解

    IntelliJ，Android Studio就是基于它开发的，IntelliJ有一套它自己的注解；IntDef分析其实重用的是MagicConstant分析的代码，IntelliJ null分析其实用的是一组配置好的null注解。如果你执行Analyze > Infer Nullity…，它会试图找出所有的null约束并添加他们。这个检查有时会插入IntelliJ注解。你可以通过搜索,替换为Android注解库的注解，或者你也可以直接用IntelliJ注解。在build.gradle里或者通过Project Structure对话框的Dependencies面板都可以添加如下依赖
compile 'com.intellij:annotations:12.0'

经过查阅资料，系统了学习了Support Annotations注解，学以致用，通过这个Support Annotations可以提高代码可读性，同时可以在类加载时就可以检查一些错误，同时不会对性能有任何影响，因为Support Annotations中的注解的生命周期全部是RetentionPolicy.CLASS。接下来准备在项目中大量推广使用。
```

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

## 工件映射 Artifact Mappings

```
implementation 'com.android.support:support-vector-drawable:28.0.0'
AndroidX build artifact # Old build artifact
androidx.arch.core # android.arch.core
	core-common # common
	core # core
	core-testing # core-testing
	core-runtime # runtime

androidx.paging # android.arch.paging
	paging-common # common
	paging-runtime # runtime
	paging-rxjava2 # rxjava2
androidx.room # android.arch.persistence.room
	room-common # common
	room-compiler # compiler
	room-guava # guava
	room-migration # migration
	room-runtime # runtime
	room-rxjava2 # rxjava2
	room-testing # testing
androidx.sqlite # android.arch.persistence
	sqlite # db
	sqlite-framework # db-framework
androidx.test.espresso.idling # com.android.support.test.espresso.idling
	idling-concurrent # idling-concurrent
	idling-net # idling-net
androidx.test.espresso # com.android.support.test.espresso
	espresso-core # espresso-core 3.2.0 3.0.2
	espresso-accessibility # espresso-accessibility
	espresso-contrib # espresso-contrib
	espresso-idling-resource # espresso-idling-resource
	espresso-intents # espresso-intents
	espresso-remote # espresso-remote
	espresso-web # espresso-web
androidx.test.jank # com.android.support.test.janktesthelper
	janktesthelper # janktesthelper
androidx.test # com.android.support.test.services
	test-services # test-services
androidx.test.uiautomator # com.android.support.test.uiautomator
	uiautomator # uiautomator
androidx.test # com.android.support.test
	monitor # monitor
	orchestrator # orchestrator
	rules # rules
	runner # runner
androidx.vectordrawable # com.android.support
	vectordrawable-animated # animated-vector-drawable
androidx.appcompat # com.android.support
	appcompat # appcompat-v7 28.0.0
androidx.asynclayoutinflater # com.android.support
	asynclayoutinflater # asynclayoutinflater
androidx.car # com.android.support
	car # car
androidx.collection # com.android.support
	collection # collections

androidx.cursoradapter # com.android.support
	cursoradapter # cursoradapter
androidx.browser # com.android.support
	browser # customtabs
androidx.customview # com.android.support
	customview # customview
androidx.documentfile # com.android.support
	documentfile # documentfile

androidx.exifinterface # com.android.support
	exifinterface # exifinterface
androidx.gridlayout # com.android.support
	gridlayout # gridlayout-v7
androidx.heifwriter # com.android.support
	heifwriter # heifwriter
androidx.interpolator # com.android.support
	interpolator # interpolator
androidx.leanback # com.android.support
	leanback # leanback-v17
androidx.loader # com.android.support
	loader # loader
androidx.localbroadcastmanager # com.android.support
	localbroadcastmanager # localbroadcastmanager
androidx.media2 # com.android.support
	media2 # media2
    media2-exoplayer # media2-exoplayer
androidx.mediarouter # com.android.support
	mediarouter # mediarouter-v7
androidx.multidex # com.android.support
	multidex # multidex
	multidex-instrumentation # multidex-instrumentation
androidx.palette # com.android.support
	palette # palette-v7
androidx.percentlayout # com.android.support
	percentlayout # percent
androidx.leanback # com.android.support
	leanback-preference # preference-leanback-v17
androidx.legacy # com.android.support
	legacy-preference-v14 # preference-v14
androidx.preference # com.android.support
	preference # preference-v7
androidx.print # com.android.support
	print # print
androidx.recommendation # com.android.support
	recommendation # recommendation
androidx.slice # com.android.support
	slice-builders # slices-builders
	slice-core # slices-core
	slice-view # slices-view
androidx.slidingpanelayout # com.android.support
	slidingpanelayout # slidingpanelayout

androidx.core # com.android.support
	core # support-compat
androidx.contentpager # com.android.support
	contentpager # support-content
androidx.legacy # com.android.support
	legacy-support-core-ui # support-core-ui
androidx.legacy # com.android.support
	legacy-support-core-utils # support-core-utils
androidx.dynamicanimation # com.android.support
	dynamicanimation # support-dynamic-animation
androidx.emoji # com.android.support
	emoji # support-emoji
	emoji-appcompat # support-emoji-appcompat
	emoji-bundled # support-emoji-bundled
androidx.fragment # com.android.support
	fragment # support-fragment
androidx.media # com.android.support
	media # support-media-compat
androidx.tvprovider # com.android.support
	tvprovider # support-tv-provider
androidx.legacy # com.android.support
	legacy-support-v13 # support-v13
	legacy-support-v4 # support-v4
androidx.vectordrawable # com.android.support
	vectordrawable # support-vector-drawable
androidx.textclassifier # com.android.support
	textclassifier # textclassifier
androidx.transition # com.android.support
	transition # transition
androidx.versionedparcelable # com.android.support
	versionedparcelable # versionedparcelable

androidx.wear # com.android.support
	wear # wear
androidx.webkit # com.android.support
	webkit # webkit
junit:junit:4.12/4.+ # junit:junit:4.12
```