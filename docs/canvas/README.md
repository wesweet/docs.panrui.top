<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-06-30 13:13:08
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

# canvas 最后更新时间: 2023-06-30 13-13-08

## 创建画布

```html
<canvas id="circleProgress" ref="canvas"></canvas>
```

```js
const canvas = this.$refs.canvas;
const ctx = canvas.getContext("2d");
// 设置canvas css 宽高
canvas.style.width = "100%";
canvas.style.height = "100%";
// 设置canvas 画布宽高
canvas.width = canvas.offsetWidth;
canvas.height = canvas.offsetHeight;
```

## 获取画布上下文

```js
const ctx = canvas.getContext("2d");
```

## 常用 api

```js
// 设置坐标原点 默认为左上角 x轴的正方向是向右的，负方向是向左的 y轴的正方向是向下的，负方向是向上的
ctx.translate(x, y); // x,y 坐标原点
// 旋转角度
ctx.rotate(angle); // angle 旋转角度
// 保存画布状态
ctx.save(); 
// 恢复画布状态
ctx.restore();
// 清除画布 x,y,width,height
ctx.clearRect(x, y, width, height); // x,y,width,height 清除的区域
// 绘制矩形 x,y,width,height
ctx.fillRect(x, y, width, height); // x,y,width,height 填充的区域
// 绘制圆形 x,y,radius,startAngle,endAngle,anticlockwise 是否逆时针
ctx.arc(x, y, radius, startAngle, endAngle, anticlockwise); // x,y,radius 圆心坐标和半径 startAngle,endAngle 起始角度和结束角度 anticlockwise 是否逆时针
// 绘制圆角矩形 x,y,width,height,radius
ctx.roundRect(x, y, width, height, radius); // x,y,width,height,radius 圆角矩形的坐标和宽高和圆角半径
// 绘制文字 text,x,y,maxWidth
ctx.fillText(text, x, y, maxWidth); // text,x,y,maxWidth 文字,x,y 坐标,maxWidth 最大宽度
// 绘制图片 image,x,y,width,height
ctx.drawImage(image, x, y, width, height); // image,x,y,width,height 图片,x,y 坐标,width,height 宽高
// 绘制线条 x1,y1,x2,y2
ctx.moveTo(x1, y1); // 起点坐标
ctx.lineTo(x2, y2); // 终点坐标
// 绘制贝塞尔曲线 x1,y1,x2,y2,controlX,controlY
ctx.quadraticCurveTo(x1, y1, x2, y2); // x1,y1,x2,y2 起点坐标和终点坐标 controlX,controlY 控制点坐标
// 绘制三次贝塞尔曲线 x1,y1,x2,y2,controlX1,controlY1,controlX2,controlY2
ctx.bezierCurveTo(x1, y1, x2, y2, controlX1, controlY1, controlX2, controlY2); // x1,y1,x2,y2 起点坐标和终点坐标 controlX1,controlY1,controlX2,controlY2 控制点坐标
// 绘制虚线 x1,y1,x2,y2
ctx.setLineDash([x1, y1, x2, y2]); // x1,y1,x2,y2 起点坐标和终点坐标
```

## fillStyle 和 strokeStyle 的区别

```js
// 设置填充颜色
ctx.fillStyle = "red";
// 设置描边颜色
ctx.strokeStyle = "red";
```

## beginPath 和 closePath

```js
// 开始绘制路径
ctx.beginPath();
// 关闭绘制路径
ctx.closePath();
```

## stroke 和 fill 的区别

```js
// 描边
ctx.stroke();
// 填充
ctx.fill();
```

## createLinearGradient 和 createRadialGradient

```js
// 线性渐变 x1,y1,x2,y2 
const linearGradient = ctx.createLinearGradient(x1, y1, x2, y2); // x1,y1 起点坐标 x2,y2 终点坐标 
// 径向渐变
const radialGradient = ctx.createRadialGradient(x1, y1, r1, x2, y2, r2); // x1,y1,r1 起点坐标和半径 x2,y2,r2 终点坐标和半径
```
