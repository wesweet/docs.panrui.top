<!--
 * @Description: css使用技巧
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-11-14 11:04:21
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2023-11-14)

## 设置 input 标签 placeholder 的字体样式

```css
input::-webkit-input-placeholder {
  /* Chrome/Opera/Safari */
  color: red;
}
input::-moz-placeholder {
  /* Firefox 19+ */
  color: red;
}
input:-ms-input-placeholder {
  /* IE 10+ */
  color: red;
}
input:-moz-placeholder {
  /* Firefox 18- */
  color: red;
}
```

## 设置 input 聚焦时的样式取消 input 的边框

```css
input:focus {
  border: none;
  outline: none;
}
```

## 设置字体竖直样式

```css
.vertical-text {
  writing-mode: vertical-rl; /* 设置为竖排文字 */
  height: 100px; /* 设置容器元素的高度 */
  width: 50px; /* 设置容器元素的宽度 */
  line-height: 100px; /* 设置文本在容器元素中的位置垂直居中 */
  text-align: center; /* 设置文本在容器元素中的位置水平居中 */
}
```

## 单行和多行文本超出省略号

```css
// 单行文本出现省略号
width: 300px;
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
word-break: break-all;

// 多行文本出现省略号
display: -webkit-box; /*重点，不能用block等其他，将对象作为弹性伸缩盒子模型显示*/
-webkit-box-orient: vertical; /*从上到下垂直排列子元素（设置伸缩盒子的子元素排列方式）*/
-webkit-line-clamp: 3; /*行数，超出三行隐藏且多余的用省略号表示...*/
line-clamp: 3;
word-break: break-all;
overflow: hidden;
max-width: 100%;
```

## 设置滚动条样式

```css
.scroll-container {
  width: 500px;
  height: 150px;
  border: 1px solid #ddd;
  padding: 15px;
  overflow: auto; /*必须*/
}

.scroll-container::-webkit-scrollbar {
  width: 8px;
  background: white;
}

.scroll-container::-webkit-scrollbar-corner,
   /* 滚动条角落 */
 .scroll-container::-webkit-scrollbar-thumb,
 .scroll-container::-webkit-scrollbar-track {
  /*滚动条的轨道*/
  border-radius: 4px;
}

.scroll-container::-webkit-scrollbar-corner,
.scroll-container::-webkit-scrollbar-track {
  /* 滚动条轨道 */
  background-color: rgba(180, 160, 120, 0.1);
  box-shadow: inset 0 0 1px rgba(180, 160, 120, 0.5);
}

.scroll-container::-webkit-scrollbar-thumb {
  /* 滚动条手柄 */
  background-color: #00adb5;
}
```

## 纯 css 绘制三角形

```css
/* 正三角 */
.up-triangle {
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 0 25px 40px 25px;
  border-color: transparent transparent rgb(245, 129, 127) transparent;
}

/* 倒三角 */
.down-triangle {
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 40px 25px 0 25px;
  border-color: rgb(245, 129, 127) transparent transparent transparent;
}
div:last-child {
  margin-top: 1rem;
}
```

## 圆环进度条

```css

```

## 背景图片水平居中

```css
background-image: url("图片地址");
background-position: center;
background-size: cover;
```

## 移除背景颜色

```css
background-color: transparent;
```

## 三棱柱五边形

```css
.pentagon {
  width: 100px;
  height: 100px;
  position: relative;
  background-color: #f00;
  transform: rotate(36deg);
}

.pentagon:before {
  content: "";
  position: absolute;
  top: -50px;
  left: 0;
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 50px solid #f00;
}

.pentagon:after {
  content: "";
  position: absolute;
  top: -50px;
  left: 0;
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-bottom: 50px solid #f00;
  transform: rotate(72deg);
}
```

## 实现圆环渐变色

border-image 与 border-radius 的使用

## clip-path 使用

## css3过渡效果