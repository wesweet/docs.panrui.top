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
  :w="800"
  :h="500"
  :x="x"
  :y="y"
  :resizable="true"
  :parent="false"
  class-name="dragging1"
  :z="9999"
>
  <imageViewer
    :urlList="priviewImages.map(item => item.filePath)"
    :onClose="handDraggable"
  ></imageViewer>
</vue-draggable-resizable>
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

最后更新时间：2024-10-17 10:04:13
