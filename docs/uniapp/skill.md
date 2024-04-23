<!--
 * @Description: uniapp 技巧文档
 * @Author: prui
 * @Date: 2024-04-23 13:09:57
 * @LastEditTime: 2024-04-23 13:10:48
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2024-04-23)

## app 端使用 webview

```js
// #ifdef APP-PLUS
wv = plus.webview.create("", "custom-webview", {
  plusrequire: "none", //禁止远程网页使用plus的API，有些使用mui制作的网页可能会监听plus.key，造成关闭页面混乱，可以通过这种方式禁止
  "uni-app": "none", //不加载uni-app渲染层框架，避免样式冲突
  // scalable: true,
  top: uni.getSystemInfoSync().statusBarHeight + 44, //放置在titleNView下方。如果还想在webview上方加个地址栏的什么的，可以继续降低TOP值
  bottom: 44,
});
wv.loadURL("http://wesweet_admin.gitee.io/docs.panrui.top/");
var currentWebview = this.$scope.$getAppWebview(); //此对象相当于html5plus里的plus.webview.currentWebview()。在uni-app里vue页面直接使用plus.webview.currentWebview()无效
currentWebview.append(wv); //一定要append到当前的页面里！！！才能跟随当前页面一起做动画，一起关闭
setTimeout(function () {
  //   console.log(wv.getStyle());
}, 1000); //如果是首页的onload调用时需要延时一下，二级页面无需延时，可直接获取
// #endif
```
