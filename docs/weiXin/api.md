<!--
 * @Description:
 * @Author: panrui
 * @Date: 2021-09-14 15:19:49
 * @LastEditTime: 2023-04-16 11:20:34
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-04-16 11-18-14
## 注意事项 

> wx.navigateTo、wx.redirectTo 不允许跳转到 tabbar 页面；wx.reLaunch 可以跳转

> 自定义组件默认只有一个插槽，开启多个插槽时，需要在组件js中启用options: { multipleSlots: true }，多个插槽以name来区分，也就是命名插槽

> wxs文件目前仅支持es5，很多新的语法暂不支持
