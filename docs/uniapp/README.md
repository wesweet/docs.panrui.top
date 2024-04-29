<!--
 * @Description: uniapp文档
 * @Author: panrui
 * @Date: 2021-05-20 16:44:03
 * @LastEditTime: 2023-11-30 14:36:43
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

# uniapp

- [uniapp 官方文档](https://uniapp.dcloud.net.cn/)

### 子菜单技术文档

| 菜单        | 说明           | 包含文件 | 功能说明 |
| ----------- | -------------- | -------- | -------- |
| base.md     | 基础文档       | -------- | -------- |
| record.md   | 记录文档       | -------- | -------- |
| skill.md   | 技巧文档       | -------- | -------- |
| uniCloud.md | ----           | -------- | -------- |
| uviewui.md  | uviewui 组件库 | -------- | -------- |

### 基础文档

### 记录文档

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

最后更新时间：2024-4-29 15:04:48
