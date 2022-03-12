> Thinking

```
Intent intent = new Intent(Intent.ACTION_PICK, ContactsContract.Contacts.CONTENT_URI);
      intent.addFlags(Intents.FLAG_NEW_DOC);
      startActivityForResult(intent, PICK_CONTACT);
      Intent intent = new Intent(Intent.ACTION_PICK);
      intent.addFlags(Intents.FLAG_NEW_DOC);
      intent.setClassName(ShareActivity.this, BookmarkPickerActivity.class.getName());
      startActivityForResult(intent, PICK_BOOKMARK);
```

> Memory

```
            Intent localIntent = new Intent();
            localIntent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
            if (Build.VERSION.SDK_INT >= 9) {
                localIntent.setAction("android.settings.APPLICATION_DETAILS_SETTINGS");
                localIntent.setData(Uri.fromParts("package", context.getPackageName(), null));
            } else if (Build.VERSION.SDK_INT <= 8) {
                localIntent.setAction(Intent.ACTION_VIEW);
                localIntent.setClassName("com.android.settings", "com.android.settings.InstalledAppDetails");
                localIntent.putExtra("com.android.settings.ApplicationPkgName", context.getPackageName());
            }
            context.startActivity(localIntent);

预览录像
intent.setAction(Intent.ACTION_VIEW);
intent.setDataAndType(Uri.parse("file://path"), "video/mp4");

intent.addCategory(Intent.CATEGORY_APP_BROWSER);
intent.removeCategory(Intent.CATEGORY_APP_BROWSER);
Set<String> categories = intent.getCategories();

intent.putExtra("key", "value");
intent.getStringExtra("key");

intent.setAction(Intent.ACTION_DIAL);
intent.setData(Uri.parse(""));
intent.setType("video/mp4");
intent.setDataAndType(Uri.parse(""), "video/mp4");

Intent intent = new Intent(Intent.ACTION_INSERT);
    intent.setType("vnd.android.cursor.item/event");
    intent.putExtra("beginTime", start);
    if (allDay) {
      intent.putExtra("allDay", true);
    }
    if (end < 0L) {
      if (allDay) {
        // + 1 day
        end = start + 24 * 60 * 60 * 1000;
      } else {
        end = start;
      }
    }
    intent.putExtra("endTime", end);
    intent.putExtra("title", summary);
    intent.putExtra("eventLocation", location);
    intent.putExtra("description", description);
    if (attendees != null) {
      intent.putExtra(Intent.EXTRA_EMAIL, attendees);
      // Documentation says this is either a String[] or comma-separated String, which is right?
    }

    try {
      // Do this manually at first
      rawLaunchIntent(intent);
    } catch (ActivityNotFoundException anfe) {
      Log.w(TAG, "No calendar app available that responds to " + Intent.ACTION_INSERT);
      // For calendar apps that don't like "INSERT":
      intent.setAction(Intent.ACTION_EDIT);
      launchIntent(intent); // Fail here for real if nothing can handle it
    }

action：MediaStore.ACTION_IMAGE_CAPTURE
extra MediaStore.EXTRA_OUTPUT, imageUriFromCamera
result： imageUriFromCamera

action：Intent.ACTION_OPEN_DOCUMENT
Category：Intent.CATEGORY_OPENABLE
type："image/*"

Intent.ACTION_PICK
data MediaStore.Images.Media.EXTERNAL_CONTENT_URI
type "image/*"

result: intent.getData()

action com.android.camera.action.CROP
data uri
type image/*
Flags Intent.FLAG_GRANT_READ_URI_PERMISSION
Intent.FLAG_GRANT_WRITE_URI_PERMISSION
Extra
crop true string
宽高的比例
aspectX 1 int
aspectY 1 int
裁剪图片宽高
outputX 300 int
outputY 300 int
return-data false boolean
outputFormat Bitmap.CompressFormat.JPEG.toString() 输出格式，一般设为Bitmap格式及图片类型
intent.setClipData(ClipData.newRawUri(MediaStore.EXTRA_OUTPUT, uri));
MediaStore.EXTRA_OUTPUT, uriClipUri // 输出图片路径
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N){
            //将存储图片的uri读写权限授权给相机应用
            List<ResolveInfo> resInfoList = activity.getPackageManager().queryIntentActivities(intent, PackageManager.MATCH_DEFAULT_ONLY);
            for (ResolveInfo resolveInfo : resInfoList) {
                String packageName = resolveInfo.activityInfo.packageName;
                activity.grantUriPermission(packageName, uriClipUri , Intent.FLAG_GRANT_WRITE_URI_PERMISSION | Intent.FLAG_GRANT_READ_URI_PERMISSION);
            }
        }
result uriClipUri
6 api
result resultData.getExtras().getParcelable("data") bitmap

android n
FileProvider.getUriForFile(context,BuildConfig.APPLICATION_ID + ".fileprovider", file);



```

