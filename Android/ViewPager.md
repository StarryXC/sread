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

class AskBrainPagerAdapter extends PagerAdapter {
    @Override
    public int getCount() { return 0; }
    @Override
    public boolean isViewFromObject(@NonNull View view, @NonNull Object object) { return false; }
    @NonNull
    @Override
    public Object instantiateItem(@NonNull ViewGroup container, int position) { return super.instantiateItem(container, position); }
    @Override
    public void destroyItem(@NonNull ViewGroup container, int position, @NonNull Object object) { super.destroyItem(container, position, object); }
}
class AskBrainFragmentPagerAdapter extends FragmentPagerAdapter {
    public AskBrainFragmentPagerAdapter(@NonNull FragmentManager fm, int behavior) { super(fm, behavior); }
    @NonNull
    @Override
    public Fragment getItem(int position) { return null; }
    @Override
    public int getCount() { return 0; }
    @Nullable
    @Override
    public CharSequence getPageTitle(int position) { return super.getPageTitle(position); }
}
class AskBrainFragmentStatePagerAdapter extends FragmentStatePagerAdapter {
    public AskBrainFragmentStatePagerAdapter(@NonNull FragmentManager fm, int behavior) { super(fm, behavior); }
    @NonNull
    @Override
    public Fragment getItem(int position) { return null; }
    @Override
    public int getCount() { return 0; }
}
ViewPager viewPager = new ViewPager(context);
viewPager.getAdapter(); viewPager.setAdapter(new AskBrainPagerAdapter());
viewPager.getCurrentItem(); viewPager.setCurrentItem(0);
viewPager.getOffscreenPageLimit(); viewPager.setOffscreenPageLimit(1);
viewPager.addOnPageChangeListener(new ViewPager.OnPageChangeListener() {
    @Override
    public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) { }
    @Override
    public void onPageSelected(int position) { }
    @Override
    public void onPageScrollStateChanged(int state) { }
});
viewPager.addOnAdapterChangeListener(new ViewPager.OnAdapterChangeListener() {
    @Override
    public void onAdapterChanged(@NonNull ViewPager viewPager, @Nullable PagerAdapter oldAdapter, @Nullable PagerAdapter newAdapter) { }
});

```

