<!--
 * @Description: html2canvas使用文档
 * @Author: panrui
 * @Date: 2023-07-14 15:09:45
 * @LastEditTime: 2023-07-14 15:12:21
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2023-11-17)

- [英文文档](http://html2canvas.hertzen.com/documentation)

## 基础用法

```js
// 1. 通过id获取元素
const element = document.getElementById("elementId");

// 2. 使用html2canvas将元素转换为canvas
html2canvas(element).then((canvas) => {
  // 3. 将canvas转换为图片
  const img = canvas.toDataURL("image/png");
  // 4. 将图片添加到页面中
  document.body.appendChild(img);
});
```

## 选项配置

## 问题

> 1. 生成图片不完整。解决方案就是再父元素设置滚动条，这样就能生成完整的图片了
