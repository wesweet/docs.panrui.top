<!--
 * @Description:
 * @Author: prui
 * @Date: 2023-11-30 14:36:30
 * @LastEditTime: 2024-04-29 15:05:40
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 页面加载循序以及适合的操作

#### onload

> 接受上页的参数，联网取数据，更新 data。

#### onReady

> ref 获取节点，页面元素自由操作

#### onShow

#### onHide

## 常用页面接口

#### getApp()

> getApp() 函数用于获取当前应用实例，一般用于获取 globalData

#### getCurrentPages()

> getCurrentPages() 函数用于获取当前页面栈的实例，以数组形式按栈的顺序给出，数组中的元素为页面实例，第一个元素为首页，最后一个元素为当前页面。

```js
page.$getAppWebview(); // 获取当前页面的webview对象实例	App
page.route; // 获取当前页面的路由
```

最后更新时间：2024-4-29 15:05:59
