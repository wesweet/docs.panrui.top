<!--
 * @Description: css使用规范
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-11-14 10:57:09
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

# CSS 最后更新时间(2023-11-14)

### 子菜单技术文档

| 菜单        | 说明     | 包含文件 | 功能说明         |
| ----------- | -------- | -------- | ---------------- |
| less.md     |          |          |                  |
| sass.md     |          |          |                  |
| skill.md    | 技巧文档 |          | css 常用技巧代码 |
| standard.md | 标准文档 |          | css 边写标准规则 |

### 基础文档

### 记录文档

###### 窗口

```
window.innerHeight：浏览器可视化大小(不包含滚动条)
window.outerHeight：浏览器分辨率大小(不包含滚动条)
window.innerWidth：浏览器可视化大小(不包含滚动条)
window.outerWidth：浏览器分辨率大小(不包含滚动条)

clientWidth：元素的内部宽度(包含内边距)
clientHeight：元素的内部高度(包含内边距)
clientTop：元素的上边框宽度
clientLeft：元素的左边框宽度

offsetWidth：元素的外部宽度(包含内边距、边框、滚动条)
offsetHeight：元素的外部高度(包含内边距、边框、滚动条)
offsetTop：元素的上外边框至包含元素的上内边框之间的像素距离
offsetLeft：元素的左外边框至包含元素的左内边框之间的像素距离
```

###### 阴影

```
box-shadow: 水平阴影的位置 垂直阴影的位置 模糊距离 阴影的颜色
```

###### 渐变

```
background-image: linear-gradient(to right, red , yellow); 从左到右 默认从上到下啊

```

###### 背景

```
// 定义背景被裁剪的区域
background-clip: border-box; // 背景被裁剪到边框盒
background-clip: padding-box; // 背景被裁剪到内边距框
background-clip: content-box; // 背景被裁剪到内容框

// 定义背景图片的定位区域
background-origin: border-box; // 背景图片相对于边框盒定位
background-origin: padding-box; // 背景图片相对于内边距框定位
background-origin: content-box; // 背景图片相对于内容框定位
```

###### 边框

```
border: 1px solid red; // 1px 线宽 solid 实线 red 颜色
border: 1px dashed red; // 1px 线宽 dashed 虚线 red 颜色
border: 1px dotted red; // 1px 线宽 dotted 点线 red 颜色
border: 1px double red; // 1px 线宽 double 双线 red 颜色
border: 1px groove red; // 1px 线宽 groove 3D凹 red 颜色
border: 1px ridge red; // 1px 线宽 ridge 3D凸 red 颜色
border: 1px inset red; // 1px 线宽 inset 3D inset red 颜色
border: 1px outset red; // 1px 线宽 outset 3D outset red 颜色

border-width: 1px; // 线宽
border-style: solid; // 线型
border-color: red; // 颜色

border-top: 1px solid red; // 上边框
border-right: 1px solid red; // 右边框
border-bottom: 1px solid red; // 下边框

border-top-width: 1px; // 上边框线宽
border-top-style: solid; // 上边框线型
border-top-color: red; // 上边框颜色

```
