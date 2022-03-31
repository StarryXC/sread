> Thinking

```
ImageView
ImageView.ScaleType
```

> Memory

```
ImageView imageView = new ImageView(context);
imageView.setScaleType(ImageView.ScaleType.CENTER_CROP);
imageView.setImageResource(R.mipmap.ic_launcher);
imageView.setImageDrawable(new ColorDrawable(Color.BLUE));
imageView.setAdjustViewBounds(true);

ImageView
	android:scaleType="centerInside"
	android:adjustViewBounds="true"
```

