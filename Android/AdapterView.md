> Thinking

```
AdapterView
    AbsSpinner
        Spinner
        Gallery
    AbsListView
        ListView
            ExpandableListView
        GridView
BaseAdapter
    ArrayAdapter
    SimpleAdapter
    CursorAdapter
        ResourceCursorAdapter
            SimpleCursorAdapter
```

> Memory

```
spinner.setPrompt("");

ListView listView = new ListView(context);
listView.smoothScrollToPosition(10, 12);

ArrayAdapter<String> arrayAdapter = ArrayAdapter.createFromResource(this, android.R.array.emailAddressTypes, android.R.id.content);
arrayAdapter.setDropDownViewResource(android.R.layout.simple_list_item_1);

class AskBrainBaseExpandableListAdapter extends BaseExpandableListAdapter {
    @Override
    public int getGroupCount() { return 0; }
    @Override
    public int getChildrenCount(int groupPosition) { return 0; }
    @Override
    public Object getGroup(int groupPosition) { return null; }
    @Override
    public Object getChild(int groupPosition, int childPosition) { return null; }
    @Override
    public long getGroupId(int groupPosition) { return 0; }
    @Override
    public long getChildId(int groupPosition, int childPosition) { return 0; }
    @Override
    public boolean hasStableIds() { return false; }
    @Override
    public View getGroupView(int groupPosition, boolean isExpanded, View convertView, ViewGroup parent) { return null; }
    @Override
    public View getChildView(int groupPosition, int childPosition, boolean isLastChild, View convertView, ViewGroup parent) { return null; }
    @Override
    public boolean isChildSelectable(int groupPosition, int childPosition) { return false; }
}



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

