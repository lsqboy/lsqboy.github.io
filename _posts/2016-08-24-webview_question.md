---
layout: post
title: WebView 使用问题
tags: [android]
---

在海之讯二期开发过程中使用WebView遇到的问题。


1. 下拉加载更多SwipeRefreshLayout与WebView滚动事件冲突
  
   > web端滚动写于div里面导致android端  `mWebView.getScrollY()`一直为0；  
   
   ___解决方法:___
   web端需要把页面滚动写于body层。或者body层高度与div高度一致即可解决。   
2. WebView 缓存问题  

   > web端的`百度统计`发送两次请求，使得Android端的WebView缓存样式显示不出来。

   ___解决方法：___ 
   去掉web端的`百度统计`
     
```  
   WebSettings settings = mWebView.getSettings();
   // 开启javascript设置
   settings.setJavaScriptEnabled(true);
   // 设置可以使用localStorage
   settings.setDomStorageEnabled(true);
   // 应用可以有缓存
   String cacheDir = getContext().getCacheDir().getPath();
   settings.setAppCachePath(cacheDir);
   settings.setAppCacheEnabled(true);
   // settings.setUseWideViewPort(true);
   settings.setAllowContentAccess(true);
   settings.setAllowFileAccess(true);
   if (NetworkUtil.isOnline(getContext())) {
      settings.setCacheMode(WebSettings.LOAD_DEFAULT);
   } else {
      settings.setCacheMode(WebSettings.LOAD_CACHE_ONLY);
   }
```
  
  
