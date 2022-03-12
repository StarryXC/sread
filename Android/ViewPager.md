> Thinking

```
ViewPager2
```

> Memory

```
androidx.viewpager:viewpager:1.0.0
com.android.support:viewpager:

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

