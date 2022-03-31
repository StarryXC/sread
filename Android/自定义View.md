> Thinking

```
View.MeasureSpec # makeMeasureSpec size mode EXACTLY
```

> Memory

```
class AskBrainView extends View {
    public AskBrainView(Context context) { super(context); }
    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
        setMeasuredDimension(1, 1);
    }
    @Override
    protected void onLayout(boolean changed, int left, int top, int right, int bottom) { super.onLayout(changed, left, top, right, bottom); }
    @Override
    public boolean onKeyDown(int keyCode, KeyEvent event) { return super.onKeyDown(keyCode, event); }
}

view.getMeasuredWidth(); view.getMeasuredHeight();
view.getWidth(); view.getHeight();
View.MeasureSpec.getMode(1); View.MeasureSpec.getSize(1);

```

