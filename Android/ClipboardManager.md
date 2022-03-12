> Thinking

```
ClipboardManager clipboard = getManager(context);
    ClipData clip = clipboard.getPrimaryClip();
    return hasText(context) ? clip.getItemAt(0).coerceToText(context) : null;
    
    getManager(context).setPrimaryClip(ClipData.newPlainText(null, text));

    ClipboardManager clipboard = getManager(context);
    ClipData clip = clipboard.getPrimaryClip();
    return clip != null && clip.getItemCount() > 0;
```

> Memory

```
ClipData
```

