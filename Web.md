> Thinking

```

```

> Memory

### Android

```
AbsoluteLayout
    WebView

WebView
    getSettings
    setScrollBarStyle
    setWebViewClient WebViewClient
        onPageStarted
        onPageFinished
        onReceivedError
        shouldOverrideUrlLoading
        shouldInterceptRequest
    setWebChromeClient WebChromeClient
        onConsoleMessage
        onJsPrompt
        onJsAlert
            runOnUiThread
            JsResult confirm
        onProgressChanged
        onShowCustomView
        onHideCustomView
        onReceivedTitle
        openFileChooser Android5之前回调
            单个方法都要重写
            intent
            action Intent.ACTION_GET_CONTENT
            Category(Intent.CATEGORY_OPENABLE
            Type("image/*"
            Intent.createChooser(i, "File Chooser")
            startActivityForResult
            ValueCallback<Uri>
                onReceiveValue getdata
        onShowFileChooser return true Android5回调
            Intent.ACTION_GET_CONTENT
            Intent.CATEGORY_OPENABLE
            Type("image/*")
            
            Intent.ACTION_CHOOSER
            Intent.EXTRA_INTENT, contentSelectionIntent
            Intent.EXTRA_TITLE, "Image Chooser"
            startActivityForResult
            ValueCallback<Uri[]>
                onReceiveValue new Uri[]{getdata}
                    new Uri[]{}
    loadUrl
    destroy
    onResume
    onPause
    canGoBack
    goBack
    canGoForward
    goForward

WebSettings
    load
        file:///android_asset/
    setCacheMode
    getCacheMode
    setAllowFileAccess
    getAllowFileAccess
    setDefaultFontSize
    getDefaultFontSize
    setDatabaseEnabled
    getDatabaseEnabled
    setUseWideViewPort
    getUseWideViewPort
    setDomStorageEnabled
    getDomStorageEnabled
    setJavaScriptEnabled
    getJavaScriptEnabled
    setUserAgentString
    getUserAgentString
    setLoadWithOverviewMode
    setSupportZoom
    setBuiltInZoomControls
    setDisplayZoomControls
    setLayoutAlgorithm
        LayoutAlgorithm.SINGLE_COLUMN
    addJavascriptInterface
        @JavascriptInterface

```



