<!--
 * @Author: panr99 1547177202@qq.com
 * @Date: 2024-10-17 09:43:24
 * @LastEditors: panr99 1547177202@qq.com
 * @LastEditTime: 2024-10-17 10:05:17
 * @FilePath: \docs.panrui.top\docs\vue\v2\components.md
 * @Description: vue组件使用文档
-->

## 拖拽组件&放大缩小(vue-draggable-resizable)

#### 安装

https://github.com/mauricius/vue-draggable-resizable/tree/v1?tab=readme-ov-file#events

```
npm install --save vue-draggable-resizable
```

#### 引入

```
import VueDraggableResizable from 'vue-draggable-resizable'
```

#### 使用

```html
<vue-draggable-resizable
  :minw="800"
  :minh="500"
  :x="x"
  :y="y"
  :w="w"
  :h="h"
  :resizable="true"
  :parent="false"
  class-name="dragging1"
  :z="9999"
  @dragstop="onDragstop"
  @resizestop="onResizstop"
>
  <imageViewer
    :urlList="priviewImages.map(item => item.filePath)"
    :onClose="handDraggable"
  ></imageViewer>
</vue-draggable-resizable>
```

```js
// 获取浏览器宽度已经拖动元素当前的宽高
// 先更新x,y 等到页面更新成功再判断是否拖拽出浏览器可视区域
onDragstop(x, y) {
  const innerWidth = window.innerWidth;
  const innerHeight = window.innerHeight;
  const width = this.w;
  const height = this.h;
  this.x = x;
  this.y = y;
  this.$nextTick(() => {
    if (this.x < 0) {
      this.x = 0
    }
    if (this.y < 0) {
      this.y = 0
    }
    if (this.x > innerWidth - width) {
      this.x = innerWidth - width
    }
    if (this.y > innerHeight - height) {
      this.y = innerHeight - height
    }
  });
},
// 调整元素大小的时候同步更新w h
onResizstop(x, y, w, h) {
  this.w = w;
  this.h = h;
}
```

#### 配置

- minw (最小宽度)
- minh (最小高度)
- w (宽度)
- h (高度)
- x (初始化横坐标)
- y (初始化纵坐标)
- z (z-index)
- resizable (是否可调整大小)
- parent (是否父元素为容器)
- dragHandle (定义拖拽元素的 class)
- 一般情况下，可以将 parent 设置为 false 这样使得拖动不在限制为父容器
- 通过 dragging1 将拖拽元素 position：fixed，达到在整个浏览器拖动的目的

最后更新时间：2024-10-22 17:09:18
