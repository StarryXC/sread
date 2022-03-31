> Thinking

```
ConnectivityManager
NetworkInfo
```

> Memory

```
ConnectivityManager connectivityManager = (ConnectivityManager) getSystemService(Context.CONNECTIVITY_SERVICE);
NetworkInfo networkInfo = connectivityManager.getActiveNetworkInfo();
networkInfo.isAvailable();
boolean a = networkInfo.getType() == ConnectivityManager.TYPE_MOBILE; networkInfo.getTypeName();
networkInfo.getSubtype(); networkInfo.getSubtypeName();



```

