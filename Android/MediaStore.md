> Thinking

```
MediaStore.Audio.AudioColumns
ALBUM string 缩略图
TITLE string 标题

MediaStore.Audio.Media
EXTERNAL_CONTENT_URI

```

> Memory

```
ContentValues values = new ContentValues();
values.put(MediaStore.Images.Media.TITLE, "");
values.put(MediaStore.Images.Media.DISPLAY_NAME, "name.jpeg");
values.put(MediaStore.Images.Media.MIME_TYPE, "image/jpeg");
// 创建一条图片uri,用于保存拍照后的照片
Uri uri = context.getContentResolver().insert(MediaStore.Images.Media.EXTERNAL_CONTENT_URI, values);

// MediaStore.Images.Media.INTERNAL_CONTENT_URI
// MediaStore.Images.Thumbnails.EXTERNAL_CONTENT_URI
Uri imageUri = MediaStore.Images.Media.EXTERNAL_CONTENT_URI;
ContentResolver mContentResolver = context.getContentResolver();
Cursor cursor = mContentResolver.query(imageUri, null,MediaStore.Images.Media.MIME_TYPE + "=? or " + MediaStore.Images.Media.MIME_TYPE + "=?",new String[] { "image/jpeg", "image/png" }, MediaStore.Images.Media.DATE_MODIFIED);
String path = cursor.getString(cursor.getColumnIndex(MediaStore.Images.Media.DATA));




```

