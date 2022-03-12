> Thinking

```
NotificationManager
Notification
```

> Memory

```
// 此处必须兼容android O设备，否则系统版本在O以上可能不展示通知栏
        String channelId = ctx.getPackageName();
        String channelName = ctx.getPackageName();
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            NotificationChannel channel = new NotificationChannel(channelId, channelName, NotificationManager.IMPORTANCE_DEFAULT);
            NotificationManager manager = (NotificationManager) ctx.getSystemService(NOTIFICATION_SERVICE);
            manager.createNotificationChannel(channel);
        }

        NotificationCompat.Builder builder = new NotificationCompat.Builder(ctx, channelId)
                .setContentTitle(data.title)
                .setSmallIcon(SmartCloudSdk.AppIcon)
                .setContentText(data.content)
                .setStyle(new NotificationCompat.BigTextStyle().bigText(data.content).setBigContentTitle(data.title))
                .setContentIntent(_createPendingIntent(ctx,SmartCloudAgooNotificationContentAction, data))
                .setDeleteIntent(_createPendingIntent(ctx,SmartCloudAgooNotificationDeleteAction, data))
                .setWhen(System.currentTimeMillis())
                .setOngoing(false)
                .setChannelId(channelId)
                ;

        if(data.sound != null){
            Uri uri = Uri.parse(data.sound);
            builder.setSound(uri);
        }else{
            builder.setDefaults(NotificationCompat.DEFAULT_ALL);
        }

        if(data.imageUrl != null){
            if(data.imageUrl.startsWith("/")) {
                Bitmap bitmap = BitmapFactory.decodeFile(data.imageUrl);
                if(bitmap != null) {
                    builder.setLargeIcon(bitmap);
                }
            }else {
                Bitmap bitmap = getBitmap(data.imageUrl);
                if(bitmap != null) {
                    builder.setLargeIcon(bitmap);
                }
            }
        }

        if(SmartCloudSdk.isDebug){
            builder.setPriority(NotificationCompat.PRIORITY_MAX);
        }

        NotificationManager manager = (NotificationManager) ctx.getSystemService(NOTIFICATION_SERVICE);
        manager.notify(counter++, builder.build());

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.GINGERBREAD) {
            StrictMode.setThreadPolicy(new StrictMode.ThreadPolicy.Builder().detectAll().penaltyLog().build());
            StrictMode.setVmPolicy(new StrictMode.VmPolicy.Builder().detectAll().penaltyLog().build());
        }
        
```

