> Thinking

```
HttpClient
```

> Memory

```
https://github.com/AsyncHttpClient/async-http-client

HttpClient
implementation 'commons-httpclient:commons-httpclient:3.1'
implementation 'org.apache.httpcomponents:httpcore:4.3.3'
implementation 'org.apache.httpcomponents:httpmime:4.3.6'

// formFile.getInputStream();
NameValuePair nameValuePair = new BasicNameValuePair("", "");
HttpEntity entity = new UrlEncodedFormEntity(new ArrayList<NameValuePair>() {{
    add(nameValuePair);
}});
HttpGet httpGet = new HttpGet();
HttpPost httpPost = new HttpPost();
httpPost.setEntity(entity);
HttpClient httpClient = new DefaultHttpClient();
HttpResponse httpResponse = httpClient.execute(httpGet);
HttpEntity httpEntity = httpResponse.getEntity();
InputStream inputStream = httpEntity.getContent();
httpEntity.getContentType();
httpEntity.getContentLength();
httpEntity.getContentEncoding();



```

