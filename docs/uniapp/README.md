<!--
 * @Description: uniapp文档
 * @Author: panrui
 * @Date: 2021-05-20 16:44:03
 * @LastEditTime: 2022-12-07 17:08:20
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

# uniapp

> uniCloud 使用文档

#### 使用文档

```js
// 底部tabbar不显示
pages.json 文件中  tabBar中list的pagePath需要与pages中path保持一致

// 页面不显示导航栏
pages.json 文件中 pages 选项中 navigationStyle 设置为custom

// APP环境中需要状态栏，但是不希望随页面一起滚动
在manifest.json 源码视图中 app-plus 中配置 statusbar

// APP环境请求
一定需要使用https 或者http 不允许使用双 //
```
