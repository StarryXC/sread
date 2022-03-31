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


RecyclerView recyclerView = new RecyclerView(context);

class AskBrainViewHolder extends RecyclerView.ViewHolder {
    public AskBrainViewHolder(@NonNull View itemView) { super(itemView); }
}
class AskBrainAdapter extends RecyclerView.Adapter<AskBrainViewHolder> {
    @NonNull
    @Override
    public AskBrainViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) { return null; }
    @Override
    public void onBindViewHolder(@NonNull AskBrainViewHolder holder, int position) { }
    @Override
    public int getItemCount() { return 0; }
}
recyclerView.getAdapter(); recyclerView.setAdapter(new AskBrainAdapter());

LinearLayoutManager linearLayoutManager = new LinearLayoutManager(context);
linearLayoutManager.setOrientation(LinearLayoutManager.VERTICAL);
GridLayoutManager gridLayoutManager = new GridLayoutManager(context, 4);
gridLayoutManager.getSpanCount(); gridLayoutManager.setSpanCount(3);
RecyclerView.LayoutManager layoutManager = new LinearLayoutManager(context);
recyclerView.getLayoutManager(); recyclerView.setLayoutManager(layoutManager);

recyclerView.setHasFixedSize(false);
recyclerView.setItemAnimator(new DefaultItemAnimator());

class AskBrainItemDecoration extends RecyclerView.ItemDecoration {
    @Override
    public void getItemOffsets(@NonNull Rect outRect, @NonNull View view, @NonNull RecyclerView parent, @NonNull RecyclerView.State state) { super.getItemOffsets(outRect, view, parent, state); }
    @Override
    public void onDraw(@NonNull Canvas c, @NonNull RecyclerView parent, @NonNull RecyclerView.State state) { super.onDraw(c, parent, state); }
    @Override
    public void onDrawOver(@NonNull Canvas c, @NonNull RecyclerView parent, @NonNull RecyclerView.State state) { super.onDrawOver(c, parent, state); }
}
recyclerView.addItemDecoration(new AskBrainItemDecoration());


```

