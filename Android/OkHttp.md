> Thinking

```
OkHttp

Interceptor.Chain
chain.connection(),
chain.proceed(request);

http 断点下载

HttpLoggingInterceptor # level | Level.BODY
```

> Memory

```
https://square.github.io/okhttp/


FormBody # Builder add build
Request # newBuilder | Builder url get post header build
RequestBody
Response # newBuilder | body
ResponseBody # source header contentLength contentType close string bytes byteStream charStream
OkHttpClient # newCall newBuilder | Builder timeout interceptor build
Call # cancel clone execute enqueue | Callback onFailure onResponse
Interceptor
WebSocket
WebSocketListener

File file = new File(URI.create(choosedUri.toString()));
MediaType MEDIA_TYPE_PNG = MediaType.parse("image/png");
RequestBody requestBody = new MultipartBody.Builder().setType(MultipartBody.FORM)
.addFormDataPart("avatar","avatar",RequestBody.create(MEDIA_TYPE_PNG,file)).build();








```

