> Thinking

```

```

> Memory

```
https://github.com/jeasonlzy/ImagePicker
implementation 'com.lzy.widget:imagepicker:0.6.1'

ImagePicker imagePicker = ImagePicker.getInstance();
imagePicker.setImageLoader(new ImageLoader() {
    @Override
    public void displayImage(Activity activity, String path, ImageView imageView, int width, int height) { }
    @Override
    public void displayImagePreview(Activity activity, String path, ImageView imageView, int width, int height) { }
    @Override
    public void clearMemoryCache() { }
});
imagePicker.setImageLoader(null); // 设置图片加载器
imagePicker.setShowCamera(true); // 显示拍照按钮
imagePicker.setCrop(false); // 允许裁剪（单选才有效）
imagePicker.setSaveRectangle(true); // 是否按矩形区域保存
imagePicker.setSelectLimit(70); // 选中数量限制
imagePicker.setStyle(CropImageView.Style.RECTANGLE); // 裁剪框的形状
imagePicker.setFocusWidth(800); // 裁剪框的宽度。单位像素（圆形自动取宽高最小值）
imagePicker.setFocusHeight(800); // 裁剪框的高度。单位像素（圆形自动取宽高最小值）
imagePicker.setOutPutX(1000); // 保存文件的宽度。单位像素
imagePicker.setOutPutY(1000); // 保存文件的高度。单位像素

Intent intent = new Intent(context, ImageGridActivity.class);
intent.putExtra(ImageGridActivity.EXTRAS_TAKE_PICKERS, true); // 是否是直接打开相机
intent.putExtra(ImageGridActivity.EXTRAS_IMAGES,new ArrayList<ImageItem>());
context.startActivityForResult(intent, 100);

Intent intentPreview = new Intent(context, ImagePreviewDelActivity.class);
intentPreview.putExtra(ImagePicker.EXTRA_IMAGE_ITEMS, new ArrayList<ImageItem>());
intentPreview.putExtra(ImagePicker.EXTRA_SELECTED_IMAGE_POSITION, 8);
intentPreview.putExtra(ImagePicker.EXTRA_FROM_ITEMS, true);
activity.startActivityForResult(intentPreview, 200);

```

