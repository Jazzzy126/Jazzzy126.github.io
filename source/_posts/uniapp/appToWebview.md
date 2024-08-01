---
title: Uniapp App 向 Webview 通信
date: 2024-08-01 10:48:06
tags: uniapp
cover: https://cdn.pixabay.com/photo/2016/02/19/22/35/ferrari-1211253_960_720.jpg
---

{% note red 'fa fa-circle-exclamation' flat %}
此方法仅用于 uniapp 手机端
{% endnote %}

## APP端

### 创建

[创建新的 Webview 窗口](https://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.create)

```JS
WebviewObject plus.webview.create(url, id, styles, extras);
```

`说明：` 创建 Webview 窗口，用于加载新的 HTML 页面，可通过 styles 设置 Webview 窗口的样式，创建完成后需要调用 show 方法才能将 Webview 窗口显示出来。

### 获取

获取到当前的 Webview

```JS
let currentWebview = this.$mp.page.$getAppWebview();
```

### 添加

[在 Webview 窗口中添加子窗口](https://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject.append)

```JS
void wobj.append(webview);
```

`说明：` 将另一个 Webview 窗口作为子窗口添加到当前 Webview 窗口中，添加后其所有权归父 Webview 窗口，当父窗口关闭时子窗口自动关闭。

### CODE

代码如下

```JS
let wv = plus.webview.create(
    url, // url
    'webviewId', // webviewId 有唯一性 
    {
      top: `10vh`,
      height: `90vh`
    }, // 样式 具体看文档
    {
      token: 'xxx'
    } // 携带的   );
    let currentWebview = this.$mp.page.$getAppWebview(); currentWebview.append(wv);
```

## H5端

### CODE

代码如下

```JS
  document.addEventListener(
    "plusready",
    function() {
      const value = plus.webview.getWebviewById("webviewId")
      console.log(value);
    },
    false
  );
```

`说明：` 监听 plusready 事件，获取到webview传过来的值
