---
title: 理解WebView(一)
date: 2017-03-14 14:02:20
tags: Android
categories: Android
---

## 1.判断webview已经滚动到底部

在View中有一个getScrollY()方法，可以返回当前可见区域的顶端距整个页面顶端的距离,也就是当前内容滚动的距离。
还有getHeight()或者 getBottom()方法都返回当前 View 这个容器的高度
在ViewView中还有getContentHeight() 方法可以返回整个 html 页面的高度,但并不等同于当前整个页面的高度 ,因为 WebView 有缩放功能。你可以通过如下代码来启动或关闭webview的缩放功能。
```java
mWebView.getSettings().setSupportZoom(true);mWebView.getSettings().setBuiltInZoomControls(true);
```
所以当前整个页面的高度实际上应该是原始 html 的高度再乘上缩放比例. 因此,更正后的结果 ,准确的判断方法应该是:
```java
// 如果已经处于底端
if(WebView.getContentHeight*WebView.getScale() -(webview.getHeight()+WebView.getScrollY())){ 
  	//...
}
```

## 2.WebView会话保持

**Webview会自动保存Cookie和Session**