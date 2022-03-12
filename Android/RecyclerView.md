> Thinking

```
RecyclerView.ItemDecoration

RecyclerView.LayoutManager
	LinearLayoutManager
		GridLayoutManager
	StaggeredGridLayoutManager
```

> Memory

```
androidx.recyclerview:recyclerview:1.1.0
androidx.recyclerview:recyclerview-selection:1.1.0
com.android.support:recyclerview-v7:
com.android.support:recyclerview-selection:

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

<androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recycler_list"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:paddingStart="10dp"
        android:paddingEnd="10dp"
        tools:itemCount="10"
        tools:listitem="@layout/machine_item_income" />
```

