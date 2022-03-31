> Thinking

```
ImageView
    DraweeView
        GenericDraweeView
            SimpleDraweeView
```

> Memory

```
https://github.com/facebook/fresco
https://www.fresco-cn.org/
implementation 'com.facebook.fresco:fresco:2.6.0'
implementation 'com.facebook.fresco:imagepipeline-okhttp3:2.6.0'

DiskCacheConfig diskCacheConfig = DiskCacheConfig.newBuilder(context)
        .setBaseDirectoryPath(new File(""))
        .build();
ImagePipelineConfig imagePipelineConfig = OkHttpImagePipelineConfigFactory.newBuilder(context, new OkHttpClient())
        .setDownsampleEnabled(true)
        .setMainDiskCacheConfig(diskCacheConfig)
        .build();
Fresco.initialize(context, imagePipelineConfig);

DraweeView draweeView = new DraweeView(context);
ImageRequestBuilder imageRequestBuilder = ImageRequestBuilder.newBuilderWithSource(Uri.parse("uri"));
imageRequestBuilder.setResizeOptions(new ResizeOptions(100, 100));
ImageRequest imageRequest = imageRequestBuilder.build();
DraweeController draweeController = Fresco.newDraweeControllerBuilder()
        .setOldController(draweeView.getController())
        .setImageRequest(imageRequest).build();
draweeView.setController(draweeController);
draweeView.getHierarchy();

new SimpleDraweeView(context)
        .getHierarchy()
        .setActualImageScaleType(ScalingUtils.ScaleType.CENTER_CROP);
```

