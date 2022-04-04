> Thinking

```

```

> Memory

```

```

#### UltraViewPager

```
https://github.com/alibaba/UltraViewPager
```

#### PagerBottomTabStrip

```
https://github.com/tyzlmjj/PagerBottomTabStrip
implementation 'me.majiajie:pager-bottom-tab-strip:2.4.0'

PageNavigationView pageNavigationView = new PageNavigationView(context);
BaseTabItem baseTabItem = new BaseTabItem(context) {
    @Override
    public void setChecked(boolean checked) { }
    @Override
    public void setMessageNumber(int number) { }
    @Override
    public void setHasMessage(boolean hasMessage) { }
    @Override
    public void setTitle(String title) { }
    @Override
    public void setDefaultDrawable(Drawable drawable) { }
    @Override
    public void setSelectedDrawable(Drawable drawable) { }
    @Override
    public String getTitle() { return null; }
};
ViewPager viewPager = new ViewPager(context);
PageNavigationView.CustomBuilder customBuilder = pageNavigationView.custom();
NavigationController navigationController = customBuilder.addItem(baseTabItem).build();
navigationController.getItemCount();
navigationController.setupWithViewPager(viewPager);
```

#### ViewPagerIndicator

```
https://github.com/JakeWharton/ViewPagerIndicator
```

```

```

