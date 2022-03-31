> Thinking

```
ButterKnife
Unbinder

@BindView # Int Float Bool String Color Dimen Anim Font Bitmap Array Drawable
@OnClick # LongClick Touch CheckedChanged FocusChange PageChange TextChanged ItemClick ItemLongClick ItemSelected

```

> Memory

```
https://github.com/JakeWharton/butterknife
// 10.2.3 7.0.1 8.8.1
implementation 'com.jakewharton:butterknife:10.2.3'
annotationProcessor 'com.jakewharton:butterknife-compiler:10.2.3'

Unbinder unbinder = ButterKnife.bind(this, new View(this));
unbinder.unbind();

```

