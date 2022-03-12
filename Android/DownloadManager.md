> Thinking

```
DownloadManager
```

> Memory

```
DownloadManager Context.DOWNLOAD_SERVICE

DownloadManager downloadManager = (DownloadManager) getSystemService(Context.DOWNLOAD_SERVICE);
DownloadManager.Query query = new DownloadManager.Query();
Cursor cursor = downloadManager.query(query);
if (!cursor.moveToFirst()) {
    // "无下载内容"
}
do {
    int status = cursor.getInt(cursor.getColumnIndex(DownloadManager.COLUMN_STATUS));
    String title = cursor.getString(cursor.getColumnIndex(DownloadManager.COLUMN_TITLE));
    if (title.equals("title")) {
        switch (status) {
            case DownloadManager.STATUS_SUCCESSFUL:
                String uri = cursor.getString(cursor.getColumnIndex(DownloadManager.COLUMN_LOCAL_URI));
                // 下载完成
                break;
            case DownloadManager.STATUS_RUNNING:
            case DownloadManager.STATUS_PAUSED:
            case DownloadManager.STATUS_PENDING:
                // 正在下载
                break;
            default:
                // 失败也视为可以再次下载
        }
        break;
    }
} while (cursor.moveToNext());

long enqueueId = 0;
query.setFilterById(enqueueId);
cursor = downloadManager.query(query);
if (cursor.moveToFirst()) {
    int columnIndex = cursor.getColumnIndex(DownloadManager.COLUMN_STATUS);
    if (DownloadManager.STATUS_SUCCESSFUL == cursor.getInt(columnIndex)) {
        String uri = cursor.getString(cursor.getColumnIndex(DownloadManager.COLUMN_LOCAL_URI));
//                return Uri.parse(uri);根据下载队列id获取下载Uri
    }
}

DownloadManager.Request request = new DownloadManager.Request(Uri.parse("parse"));
request.setDestinationInExternalPublicDir(Environment.DIRECTORY_DOWNLOADS, "downloadName");
request.setNotificationVisibility(DownloadManager.Request.VISIBILITY_VISIBLE_NOTIFY_COMPLETED);
request.setMimeType("application/vnd.android.package-archive");
downloadManager.enqueue(request);

DownloadManager.ACTION_DOWNLOAD_COMPLETE action
long enqueueId = intent.getLongExtra(DownloadManager.EXTRA_DOWNLOAD_ID, 0);
Uri uri = DownloadHelperSys.getDownloadUriById(context, enqueueId);

```

