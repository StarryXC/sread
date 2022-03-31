> Thinking

```
Retrofit
```

> Memory

```
https://square.github.io/retrofit/

// 2.4.0 2.9.0
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:adapter-rxjava2:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0'

Retrofit retrofit = new Retrofit.Builder()
        .baseUrl("")
        .addConverterFactory(GsonConverterFactory.create())
        .client(new OkHttpClient())
        .build();



```

