> Thinking

```

```

> Memory

```
public static final String GOOGLE_PHOTOS_URI = "com.google.android.apps.photos.content";
public static final String MEDIA_DOCUMENT_URI = "com.android.providers.media.documents";
public static final String DOWNLOADS_DOCUMENT_URI = "com.android.providers.downloads.documents";
public static final String EXTERNALSTORAGE_DOCUMENT_URI = "com.android.externalstorage.documents";

// 根据Uri获取图片绝对路径，解决Android4.4以上版本Uri转换
@TargetApi(Build.VERSION_CODES.KITKAT)
public static String getImageAbsolutePath19(Context context, Uri imageUri) {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT && DocumentsContract.isDocumentUri(context, imageUri)) {
        if (EXTERNALSTORAGE_DOCUMENT_URI.equals(imageUri.getAuthority())) {
            String docId = DocumentsContract.getDocumentId(imageUri);
            String[] split = docId.split(":"); // 0 type 1 path
            String type = split[0];
            if ("primary".equalsIgnoreCase(type)) {
                return Environment.getExternalStorageDirectory() + "/" + split[1];
            }
        } else if (DOWNLOADS_DOCUMENT_URI.equals(imageUri.getAuthority())) {
            String id = DocumentsContract.getDocumentId(imageUri);
            Uri contentUri = ContentUris.withAppendedId(Uri.parse("content://downloads/public_downloads"), Long.valueOf(id));
            return getDataColumn(context, contentUri, null, null);
        } else if (MEDIA_DOCUMENT_URI.equals(imageUri.getAuthority())) {
            String docId = DocumentsContract.getDocumentId(imageUri);
            String[] split = docId.split(":");
            String type = split[0];
            Uri contentUri = null;
            if ("image".equals(type)) {
                contentUri = MediaStore.Images.Media.EXTERNAL_CONTENT_URI;
            } else if ("video".equals(type)) {
                contentUri = MediaStore.Video.Media.EXTERNAL_CONTENT_URI;
            } else if ("audio".equals(type)) {
                contentUri = MediaStore.Audio.Media.EXTERNAL_CONTENT_URI;
            }
            String selection = MediaStore.Images.Media._ID + "=?";
            String[] selectionArgs = new String[] { split[1] };
            return getDataColumn(context, contentUri, selection, selectionArgs);
        }
    }
    // MediaStore (and general)
    if ("content".equalsIgnoreCase(imageUri.getScheme())) {
        // Return the remote address
        if (GOOGLE_PHOTOS_URI.equals(imageUri.getAuthority()))
            return imageUri.getLastPathSegment();
        return getDataColumn(context, imageUri, null, null);
    }
    // File
    else if ("file".equalsIgnoreCase(imageUri.getScheme())) {
        return imageUri.getPath();
    }
    return null;
}

private static String getDataColumn(Context context, Uri uri, String selection, String[] selectionArgs) {
    Cursor cursor = null;
    String column = MediaStore.Images.Media.DATA;
    String[] projection = { column };
    try {
        cursor = context.getContentResolver().query(uri, projection, selection, selectionArgs, null);
        if (cursor != null && cursor.moveToFirst()) {
            int index = cursor.getColumnIndexOrThrow(column);
            return cursor.getString(index);
        }
    } finally {
        if (cursor != null)
            cursor.close();
    }
    return null;
}

```

