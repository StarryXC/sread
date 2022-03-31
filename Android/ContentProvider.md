> Thinking

```
ContentResolver
```

> Memory

```
public static final String MIMETYPE_XML = "application/xml";
public static final String MIMETYPE_HTML = "text/html";
public static final String MIMETYPE_OCTET_STREAM = "application/octet-stream";
public static final String MIMETYPE_GZIP = "application/x-gzip";

Uri uri = Uri.EMPTY;
uri.getAuthority(); uri.getEncodedAuthority();
uri.getScheme();
uri.getHost();
uri.getPort();
uri.getPathSegments();
uri.getLastPathSegment();
uri.getFragment(); uri.getEncodedFragment();
uri.getQuery(); uri.getEncodedQuery();
uri.getPath(); uri.getEncodedPath();
uri.getUserInfo(); uri.getEncodedUserInfo();

public class AskBrainContentProvider extends ContentProvider {
    @Override
    public boolean onCreate() { return false; }
    @Nullable
    @Override
    public Cursor query(@NonNull Uri uri, @Nullable String[] strings, @Nullable String s, @Nullable String[] strings1, @Nullable String s1) { return null; }
    @Nullable
    @Override
    public String getType(@NonNull Uri uri) { return null; }
    @Nullable
    @Override
    public Uri insert(@NonNull Uri uri, @Nullable ContentValues contentValues) { return null; }
    @Override
    public int delete(@NonNull Uri uri, @Nullable String s, @Nullable String[] strings) { return 0; }
    @Override
    public int update(@NonNull Uri uri, @Nullable ContentValues contentValues, @Nullable String s, @Nullable String[] strings) { return 0; }
}

ContentResolver.SCHEME_ANDROID_RESOURCE
ContentResolver contentResolver = context.getContentResolver();
contentResolver.query();

```

