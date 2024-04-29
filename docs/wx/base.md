<!--
 * @Description: 
 * @Author: prui
 * @Date: 2024-04-29 14:36:17
 * @LastEditTime: 2024-04-29 14:36:35
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->
## 注意事项 

> wx.navigateTo、wx.redirectTo 不允许跳转到 tabbar 页面；wx.reLaunch 可以跳转

> 自定义组件默认只有一个插槽，开启多个插槽时，需要在组件js中启用options: { multipleSlots: true }，多个插槽以name来区分，也就是命名插槽

> wxs文件目前仅支持es5，很多新的语法暂不支持