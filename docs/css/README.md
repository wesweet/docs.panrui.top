<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-05-19 09:04:31
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

# CSS 最后更新时间：2023-05-19 09-04-31

#### 基础

```
window.innerHeight：浏览器可视化大小(不包含滚动条)
window.outerHeight：浏览器分辨率大小(不包含滚动条)

设置阴影
box-shadow: 水平阴影的位置 垂直阴影的位置 模糊距离 阴影的颜色

设置渐变
background-image: linear-gradient(to right, red , yellow); 从左到右 默认从上到下啊
```

#### background-clip

定义背景的绘制区域

```css
background-clip: border-box; // 背景被裁剪到边框盒
background-clip: padding-box; // 背景被裁剪到内边距框
background-clip: content-box; // 背景被裁剪到内容框
```

#### background-origin

定义背景图片的定位区域

```css
background-origin: border-box; // 背景图片相对于边框盒定位
background-origin: padding-box; // 背景图片相对于内边距框定位
background-origin: content-box; // 背景图片相对于内容框定位
```

<!-- #### border 属性

```css
border: 1px solid red; // 1px 线宽 solid 实线 red 颜色
border: 1px dashed red; // 1px 线宽 dashed 虚线 red 颜色
border: 1px dotted red; // 1px 线宽 dotted 点线 red 颜色
border: 1px double red; // 1px 线宽 double 双线 red 颜色
border: 1px groove red; // 1px 线宽 groove 3D凹 red 颜色
border: 1px ridge red; // 1px 线宽 ridge 3D凸 red 颜色
border: 1px inset red; // 1px 线宽 inset 3D inset red 颜色
border: 1px outset red; // 1px 线宽 outset 3D outset red 颜色
```

```css
border-top: 1px solid red; // 上边框
border-right: 1px solid red; // 右边框
border-bottom: 1px solid red; // 下边框
border-left: 1px solid red; // 左边框
```

```css
border-width: 1px; // 线宽
border-style: solid; // 线型
border-color: red; // 颜色
```

```css
border-top-width: 1px; // 上边框线宽
border-top-style: solid; // 上边框线型
border-top-color: red; // 上边框颜色
``` -->
