<!--
 * @Description: 微信文档
 * @Author: panrui
 * @Date: 2021-05-20 16:44:03
 * @LastEditTime: 2024-04-29 14:34:51
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

# WeiXin

### 登录

### 静默登录

### 版本更新

```js
const updateManager = wx.getUpdateManager();

// 判断是否有版本更新
updateManager.onCheckForUpdate(function (res) {
  // 请求完新版本信息的回调
  console.log(res.hasUpdate);
});

updateManager.onUpdateReady(function () {
  wx.showModal({
    title: "更新提示",
    content: "新版本已经准备好，是否重启应用？",
    success: function (res) {
      if (res.confirm) {
        // 新的版本已经下载好，调用 applyUpdate 应用新版本并重启
        updateManager.applyUpdate();
      }
    },
  });
});

updateManager.onUpdateFailed(function () {
  // 新版本下载失败
});
```

### 接入腾讯地图

> 1. [腾讯地图SDK](https://lbs.qq.com/miniProgram/jsSdk/jsSdkGuide/jsSdkOverview)

> 2. [微信小程序官方API文档](https://developers.weixin.qq.com/miniprogram/dev/api/location/wx.openLocation.html)

> 3. [微信小程序基础组件文档](https://developers.weixin.qq.com/miniprogram/dev/component/map.html)
### 小程序优化手段

> 1. 使用 wxs 实现相当于 vue 管道符的相关类似功能

### 小程序文档

```js
小程序的运行环境分成渲染层和逻辑层，其中 WXML 模板和 WXSS 样式工作在渲染层，JS 脚本工作在逻辑层。
小程序的渲染层和逻辑层分别由2个线程管理：渲染层的界面使用了WebView 进行渲染；逻辑层采用JsCore线程运行JS脚本，
这两个线程的通信会经由微信客户端（下文中也会采用Native来代指微信客户端）做中转，逻辑层发送网络请求也经由Native转发
```

最后更新时间：2024-4-29 14:31:22