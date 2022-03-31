> Thinking

```
RequestBody
    FormBody
    MultipartBody

OkHttpClient
Request
Response
Call
WebSocket

http 断点下载

HttpLoggingInterceptor # level | Level.BODY
```

> Memory

```
https://square.github.io/okhttp/
implementation 'com.squareup.okhttp3:okhttp:3.12.0'

FormBody formBody = new FormBody.Builder(Charset.defaultCharset())
        .add("", "")
        .build();

MultipartBody multipartBody = new MultipartBody.Builder()
        .setType(MultipartBody.FORM)
        .addFormDataPart("", "")
        .addFormDataPart("", "", formBody)
        .build();

// mime "application/json" "application/json;charset=utf-8"
RequestBody requestBody = RequestBody.create(MediaType.parse("image/png"), new File(""));
Request request = new Request.Builder()
        .url("")
        .header("", "")
        .addHeader("", "")
        .get()
        .post(requestBody)
        .build();
Request.Builder builder = request.newBuilder();

OkHttpClient okHttpClient = new OkHttpClient();
okHttpClient = new OkHttpClient.Builder()
        .addInterceptor(new Interceptor() {
            @NonNull
            @Override
            public Response intercept(@NonNull Chain chain) throws IOException {
                Call call = chain.call();
                Connection connection = chain.connection();
                int timeoutMillis = chain.connectTimeoutMillis();
                chain.readTimeoutMillis();
                chain.writeTimeoutMillis();
                chain.proceed(chain.request());
                return null;
            }
        })
        .retryOnConnectionFailure(true)
        .hostnameVerifier(new HostnameVerifier() {
            @Override
            public boolean verify(String hostname, SSLSession session) { return false; }
        })
        .sslSocketFactory(new SSLCertificateSocketFactory(1))
        .connectTimeout(1, TimeUnit.SECONDS)
        .readTimeout(1, TimeUnit.SECONDS)
        .writeTimeout(1, TimeUnit.SECONDS)
        .callTimeout(1, TimeUnit.SECONDS)
        .build();
OkHttpClient.Builder builder = okHttpClient.newBuilder();

Call call = okHttpClient.newCall(request);
call.cancel(); call.isCanceled()
call.timeout();
call.isExecuted();
call.clone();
call.enqueue(new Callback() {
    @Override
    public void onFailure(@NonNull Call call, @NonNull IOException e) { }
    @Override
    public void onResponse(@NonNull Call call, @NonNull Response response) throws IOException { }
});

Response response = call.execute();
response.header("", "");
ResponseBody responseBody = response.body();
BufferedSource source = responseBody.source();
String string = responseBody.string();
byte bytes[] = responseBody.bytes();
InputStream inputStream = responseBody.byteStream();
ByteString byteString = responseBody.byteString();
Reader reader = responseBody.charStream();
long length = responseBody.contentLength();
MediaType mediaType = responseBody.contentType();
responseBody.close();
Response.Builder builder = response.newBuilder();

WebSocket webSocket = okHttpClient.newWebSocket(request, new WebSocketListener() {
    @Override
    public void onClosed(@NonNull WebSocket webSocket, int code, @NonNull String reason) { super.onClosed(webSocket, code, reason); }
    @Override
    public void onClosing(@NonNull WebSocket webSocket, int code, @NonNull String reason) { super.onClosing(webSocket, code, reason); }
    @Override
    public void onFailure(@NonNull WebSocket webSocket, @NonNull Throwable t, @Nullable Response response) { super.onFailure(webSocket, t, response); }
    @Override
    public void onMessage(@NonNull WebSocket webSocket, @NonNull String text) { super.onMessage(webSocket, text); }
    @Override
    public void onMessage(@NonNull WebSocket webSocket, @NonNull ByteString bytes) { super.onMessage(webSocket, bytes); }
    @Override
    public void onOpen(@NonNull WebSocket webSocket, @NonNull Response response) { super.onOpen(webSocket, response); }
});
webSocket.send("");
webSocket.cancel();
```

```
class AskBrainInterceptor implements Interceptor {
    @Override
    public Response intercept(Chain chain) throws IOException {
        Request.Builder builder = chain.request().newBuilder();
        builder.header("Content-Type", "application/json;charset=utf-8")
                .header("Network-CU","");
        return chain.proceed(builder.build());
    }
}
```

