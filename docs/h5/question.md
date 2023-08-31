<!--
 * @Description: HTML5问题记录
 * @Author: panrui
 * @Date: 2023-08-31 11:27:02
 * @LastEditTime: 2023-08-31 11:27:08
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-08-31 11-27-08

## HTML5 问题记录

## 页面使用 img 标签引入图片时，图片不显示，并提示 403 错误

```Javascript
// 问题原因：图片服务器设置了防盗链，只允许指定域名访问
// 在header中添加Referer字段，值为图片所在的域名即可
<head>
    <meta name="referrer" content="no-referrer" />
</head>

// 解决方法：在img标签上添加crossorigin属性 这种方案待测试
<img crossorigin="anonymous" src="https://xxx.com/xxx.jpg" />
```
