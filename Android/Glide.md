> Thinking

```
GlideModule
```

> Memory

```
https://github.com/bumptech/glide
// 4.7.1 4.12.0
implementation 'com.github.bumptech.glide:glide:4.12.0'
annotationProcessor 'com.github.bumptech.glide:compiler:4.12.0'

RequestOptions requestOptions = new RequestOptions()
        .placeholder(R.mipmap.ic_launcher)
        .error(R.mipmap.ic_launcher)
        .override(100, 100)
        .dontAnimate();
Glide.with(context)
        .load("url")
        .apply(requestOptions)
        .into(new ImageView(context));
```

