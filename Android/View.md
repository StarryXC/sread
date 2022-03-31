> Thinking

```
View
```

> Memory

```
View
	<findVi

View view = new View(context);
view = view.findViewById(android.R.id.icon);

view.setPadding(1, 1, 1, 1);
view.getPaddingLeft(); view.getPaddingRight();
view.getPaddingTop(); view.getPaddingBottom();
view.getPaddingStart(); view.getPaddingEnd();

view.callOnClick(); view.performClick();
view.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) { }
});
view.performLongClick();
view.setOnLongClickListener(new View.OnLongClickListener() {
    @Override
    public boolean onLongClick(View v) { return false; }
});
view.setOnKeyListener(new View.OnKeyListener() {
    @Override
    public boolean onKey(View v, int keyCode, KeyEvent event) { return false; }
});
view.setOnTouchListener(new View.OnTouchListener() {
    @Override
    public boolean onTouch(View v, MotionEvent event) { return false; }
});
view.post(new Runnable() {
    @Override
    public void run() { }
});
view.invalidate(); view.postInvalidate();
view.isSelected(); view.setSelected(true);

ViewCompat.getOverScrollMode(view); ViewCompat.setOverScrollMode(view, ViewCompat.OVER_SCROLL_ALWAYS);

```

