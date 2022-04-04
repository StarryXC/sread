> Thinking

```

```

> Memory

### Android

```
WebView webView = new WebView(ctx);
WebSettings webSettings = webView.getSettings();
webSettings.getCacheMode(); webSettings.setCacheMode(0);
webSettings.getAllowFileAccess(); webSettings.setAllowFileAccess(true);
webSettings.getDefaultFontSize(); webSettings.setDefaultFontSize(0);
webSettings.getDatabaseEnabled(); webSettings.setDatabaseEnabled(true);
webSettings.getUseWideViewPort(); webSettings.setUseWideViewPort(true);
webSettings.getDomStorageEnabled(); webSettings.setDomStorageEnabled(true);
webSettings.getJavaScriptEnabled(); webSettings.setJavaScriptEnabled(true);
webSettings.getUserAgentString(); webSettings.setUserAgentString("");
webView.setScrollBarStyle(0);
webView.setWebViewClient(new WebViewClient() {
    @Override
    public void onPageStarted(WebView view, String url, Bitmap favicon) {
        super.onPageStarted(view, url, favicon);
    }

    @Override
    public void onPageFinished(WebView view, String url) {
        super.onPageFinished(view, url);
    }

    @Override
    public void onReceivedError(WebView view, WebResourceRequest request, WebResourceError error) {
        super.onReceivedError(view, request, error);
    }

    @Override
    public boolean shouldOverrideUrlLoading(WebView view, WebResourceRequest request) {
        return super.shouldOverrideUrlLoading(view, request);
    }

    @Nullable
    @Override
    public WebResourceResponse shouldInterceptRequest(WebView view, WebResourceRequest request) {
        return super.shouldInterceptRequest(view, request);
    }
});

webView.setWebChromeClient(new WebChromeClient() {
    @Override
    public boolean onConsoleMessage(ConsoleMessage consoleMessage) {
        return super.onConsoleMessage(consoleMessage);
    }

    @Override
    public boolean onJsPrompt(WebView view, String url, String message, String defaultValue, JsPromptResult result) {
        return super.onJsPrompt(view, url, message, defaultValue, result);
    }

    @Override
    public void onProgressChanged(WebView view, int newProgress) {
        super.onProgressChanged(view, newProgress);
    }
});
webView.loadUrl("");
webView.destroy();
webView.onResume();
webView.onPause();
webView.canGoBack(); webView.goBack();
webView.canGoForward(); webView.goForward();
```



