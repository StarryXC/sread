> Thinking

```
ClipboardManager
ClipData
```

> Memory

```
ClipboardManager clipboardManager = (ClipboardManager) context.getSystemService(Context.CLIPBOARD_SERVICE);
ClipData clipData = clipboardManager.getPrimaryClip(); clipboardManager.setPrimaryClip(ClipData.newPlainText("", ""));
clipData.getItemCount();
ClipData.Item item = clipData.getItemAt(0);
item.coerceToHtmlText(context);
item.coerceToStyledText(context);
```
