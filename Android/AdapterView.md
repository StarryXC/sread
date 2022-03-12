> Thinking

```
GridView
```

> Memory

```
<GridView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:listSelector="#00000000"
    android:numColumns="7"
    android:scrollbars="none"
    android:verticalSpacing="5dp"
    android:gravity="center"
    android:fadingEdge="none"
    />
GridView
    @Override
    public void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        int expandSpec = MeasureSpec.makeMeasureSpec(Integer.MAX_VALUE >> 2, MeasureSpec.AT_MOST);
        super.onMeasure(widthMeasureSpec, expandSpec);
    }

protected void onListItemClick(ListView l, View view, int position, long id) {
    Adapter adapter = getListAdapter();
    if (position >= 0 && position < adapter.getCount()) {
      String packageName = ((AppInfo) adapter.getItem(position)).getPackageName();
      Intent intent = new Intent();
      intent.addFlags(Intents.FLAG_NEW_DOC);
      intent.putExtra("url", "market://details?id=" + packageName); // Browser.BookmarkColumns.URL
      setResult(RESULT_OK, intent);
    } else {
      setResult(RESULT_CANCELED);      
    }
    finish();
  }

BaseAdapter
	<count> <item> <view>
```

