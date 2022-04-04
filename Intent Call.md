> Thinking

```

```

> Memory



```
Intent intent = new Intent();
intent.getAction(); intent.setAction("");
intent.getComponent(); intent.setClassName("", "");
// Intent.FLAG_ACTIVITY_REORDER_TO_FRONT
// Intent.FLAG_ACTIVITY_CLEAR_TOP
// Intent.FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET
intent.getFlags(); intent.addFlags(0); intent.setFlags(0);
intent.getData(); intent.getDataString(); intent.setData(Uri.EMPTY);
intent.getType(); intent.setType("");
intent.setDataAndType(Uri.EMPTY, "");
intent.setDataAndNormalize(Uri.EMPTY); intent.setDataAndTypeAndNormalize(Uri.EMPTY, "");
intent.getCategories(); intent.addCategory(""); intent.removeCategory(""); intent.hasCategory("");
intent.getClipData(); intent.setClipData(ClipData.newPlainText("", ""));
intent.getExtras(); intent.putExtra("", "");
intent.putExtra("key", "value"); intent.getStringExtra("key");

Intent intent = new Intent(Intent.ACTION_VIEW);
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
// Uri.parse("file://path") "video/mp4"
intent.setDataAndType(Uri.parse("file://...apk"), "application/vnd.android.package-archive");
context.startActivity(intent);

Intent intent = new Intent();
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
if (Build.VERSION.SDK_INT >= 9) {
    intent.setAction("android.settings.APPLICATION_DETAILS_SETTINGS");
    intent.setData(Uri.fromParts("package", context.getPackageName(), null));
} else if (Build.VERSION.SDK_INT <= 8) {
    intent.setAction(Intent.ACTION_VIEW);
    intent.setClassName("com.android.settings", "com.android.settings.InstalledAppDetails");
    intent.putExtra("com.android.settings.ApplicationPkgName", context.getPackageName());
}
context.startActivity(intent);

Intent intent = new Intent(Intent.ACTION_INSERT);
intent.setType("vnd.android.cursor.item/event");
intent.putExtra("beginTime", System.currentTimeMillis());
intent.putExtra("allDay", true);
intent.putExtra("endTime", System.currentTimeMillis() + 24 * 60 * 60 * 1000);
intent.putExtra("title", "summary");
intent.putExtra("eventLocation", "location");
intent.putExtra("description", "description");
intent.putExtra(Intent.EXTRA_EMAIL, "attendees");

Intent intent = intent.setAction(Intent.ACTION_EDIT);

android n
FileProvider.getUriForFile(context,BuildConfig.APPLICATION_ID + ".fileprovider", file);

tableName
tableUri content://authori
vnd.android.cursor.dir/vnd.
vnd.android.cursor.item/vnd.

Intent intent = new Intent(Intent.ACTION_MAIN);
intent.addCategory(Intent.CATEGORY_HOME);
startActivity(intent);

Intent intent = new Intent("com.android.camera.action.CROP");
intent.setDataAndType(uri, "image/*");
intent.putExtra("crop", "true"); // 设置在开启的Intent中设置显示的VIEW可裁剪
intent.putExtra("aspectX", 1); // aspectX aspectY 是宽高的比例
intent.putExtra("aspectY", 1);
intent.putExtra("outputX", 150); // outputX outputY 是裁剪图片宽高
intent.putExtra("outputY", 150);
intent.putExtra("noFaceDetection", true);// 取消人脸识别
intent.putExtra("outputFormat", "JPEG");// 图片格式
intent.putExtra("return-data", true);
startActivityForResult(intent, 100);
Bitmap bitmap = data.getParcelableExtra("data");

Intent intent = new Intent(Intent.ACTION_PICK);
intent.setData(MediaStore.Images.Media.EXTERNAL_CONTENT_URI);
intent.setType("image/*");
activity.startActivityForResult(intent, 100);
Uri uri = intent.getData();

Intent intent = new Intent(Intent.ACTION_PICK, ContactsContract.Contacts.CONTENT_URI);
intent.addFlags(ContactsContract.Intents.FLAG_NEW_DOC);
activity.startActivityForResult(intent, 100);

Intent intent = new Intent(Settings.ACTION_APPLICATION_DETAILS_SETTINGS, Uri.parse("package:" + context.getPackageName()));
intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
context.startActivity(intent);

Uri imageUri = Uri.parse("");
Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
intent.putExtra(MediaStore.EXTRA_OUTPUT, imageUri);
activity.startActivityForResult(intent, 100);
Uri uri = imageUri;
Uri uri = data.getData();

Intent intent = new Intent(Intent.ACTION_OPEN_DOCUMENT);
intent.addCategory(Intent.CATEGORY_OPENABLE);
intent.setType("image/*");
activity.startActivityForResult(intent, 100);

Intent intent = new Intent(Intent.ACTION_DIAL);
activity.startActivity(intent);

Uri imageUri = Uri.EMPTY;
Intent intent = new Intent("com.android.camera.action.CROP");
intent.setDataAndType(imageUri, "image/*");
intent.putExtra("crop", "true"); // 设置在开启的Intent中设置显示的VIEW可裁剪
intent.putExtra("aspectX", 1); // aspectX aspectY 是宽高的比例
intent.putExtra("aspectY", 1);
intent.putExtra("outputX", 150); // outputX outputY 是裁剪图片宽高
intent.putExtra("outputY", 150);
intent.putExtra("outputFormat", Bitmap.CompressFormat.JPEG.toString()); // 输出格式，一般设为Bitmap格式及图片类型
intent.putExtra("return-data", true);
intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION | Intent.FLAG_GRANT_WRITE_URI_PERMISSION);
intent.setClipData(ClipData.newRawUri(MediaStore.EXTRA_OUTPUT, Uri.EMPTY)); // 输出图片路径
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N){ // 将存储图片的uri读写权限授权给相机应用
    activity.grantUriPermission(activity.getPackageName(), imageUri , Intent.FLAG_GRANT_WRITE_URI_PERMISSION | Intent.FLAG_GRANT_READ_URI_PERMISSION);
}
startActivityForResult(intent, 100);
Bitmap bitmap = intent.getExtras().getParcelable("data"); // 6 api
```

