> Thinking

```
CoordinatorLayout
AppBarLayout
CollapsingToolbarLayout
FloatingActionButton
Snackbar
Toolbar

NavigationView
BottomNavigationView
```

> Memory

```
com.google.android.material:material:1.1.0
com.android.support:design:28.0.0
androidx.coordinatorlayout:coordinatorlayout:1.1.0
com.android.support:coordinatorlayout:

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
	android:theme="@style/AppTheme.AppBarOverlay"
AppBarLayout.LayoutParams
	getScrollFlags setScrollFlags
	getScrollInterpolator setScrollInterpolator
AppBarLayout.Behavior
	setTopAndBottomOffset

CollapsingToolbarLayout
CollapsingToolbarLayout.LayoutParams

FloatingActionButton
	setOnClickListener
	app:srcCompat="@android:drawable/ic_dialog_email"
Snackbar
	make
	LENGTH_LONG
    setAction
    show
Snackbar.make(view, "Replace with your own action", Snackbar.LENGTH_LONG)
                        .setAction("Action", null).show();
                        
Toolbar # setSupportActionBar
androidx.appcompat.widget.Toolbar
app:popupTheme="@style/AppTheme.PopupOverlay"

NavigationView
	setNavigationItemSelectedListener # NavigationView.OnNavigationItemSelectedListener onNavigationItemSelected
	getMenu inflateMenu

BottomNavigationView
	setOnNavigationItemSelectedListener # BottomNavigationView.OnNavigationItemSelectedListener onNavigationItemSelected
	getMenu inflateMenu # app:menu menu 资源
```

