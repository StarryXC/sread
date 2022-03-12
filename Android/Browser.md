> Thinking

```
content://browser/bookmarks ndroid.provider.Browser.BOOKMARKS_URI:
title Browser.BookmarkColumns.TITLE
url Browser.BookmarkColumns.URL
Intent intent = new Intent();
    intent.addFlags(Intents.FLAG_NEW_DOC);
    intent.putExtra("title", titleURL[0]); // Browser.BookmarkColumns.TITLE
    intent.putExtra("url", titleURL[1]); // Browser.BookmarkColumns.URL
    setResult(RESULT_OK, intent);
```

> Memory

```

```

