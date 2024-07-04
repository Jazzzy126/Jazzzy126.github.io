---
title: Uniapp Base64转图片
date: 2024-07-04 14:01:51
tags: uniapp
cover: https://cdn.pixabay.com/photo/2023/10/14/09/20/mountains-8314422_1280.png
---

{% note red 'fa fa-circle-exclamation' flat %}
此方法仅用于uniapp手机端
{% endnote %}

## 创建

[创建 Bitmap 对象](https://www.html5plus.org/doc/zh_cn/nativeobj.html#plus.nativeObj.Bitmap)

```JS
var bitmap = new plus.nativeObj.Bitmap(id, path);
```

`说明：` 创建后为空Bitmap对象，需要调用Webview对象的draw方法更新，或者调用load/loadBase64Data方法加载图片。

## 加载

[loadBase64Data加载Base64编码格式图片到Bitmap对象](https://www.html5plus.org/doc/zh_cn/nativeobj.html#plus.nativeObj.Bitmap.loadBase64Data)

```JS
void bitmap.loadBase64Data(data, successCallback, errorCallback);
```

`说明：` 从Base64编码格式图片数据中加载图片，此操作将覆盖之前的图片内容， 如果加载图片失败则保留之前的图片内容。
`返回值：` Bitmap图片对象

## 保存

[save保存图片](https://www.html5plus.org/doc/zh_cn/nativeobj.html#plus.nativeObj.Bitmap.save)

```JS
void bitmap.save(path, options, successCallback, errorCallback);
```

`说明：` 将图片保存到指定的路径（仅支持本地文件系统），如果图片为空或者指定的路径文件已经存在则返回失败。

## CODE

方法如下

```JS
    baseToPath(base64) {
      return new Promise((resolve, reject) => {
        const bitmap = new plus.nativeObj.Bitmap('name');
        bitmap.loadBase64Data(
          base64,
          () => {
            const url = '_doc/' + new Date().getTime() + '.png'; // url为时间戳命名方式
            bitmap.save(
              url, {
                overwrite: true // 是否覆盖
                // quality: 'quality'  // 图片清晰度
              },
              (success) => {
                resolve(url);
              },
              (error) => {
                reject(error)
                bitmap.clear();
              }
            );
          },
          (error) => {
            reject(error)
            bitmap.clear();
          }
        );
      });
    },
```
