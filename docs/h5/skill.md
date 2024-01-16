<!--
 * @Description: html5使用技巧
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2024-01-16 16:55:06
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2024-01-16)

## 页面开发注意细节

- 文字注意是否换行或者超出

- 按钮注意是否阻止重复点击

- select是否需要提供过滤和清除功能

## 移动端调试工具

```Javascript
<script src="//cdn.bootcss.com/eruda/1.2.4/eruda.min.js"></script>
<script>eruda.init();</script>

<script src="https://cdn.bootcdn.net/ajax/libs/vConsole/3.9.1/vconsole.min.js"></script>
<script>
	// 初始化
	var vConsole = new VConsole();
	console.log('VConsole is cool');
</script>
```

## 解决移动端 click 事件延迟 300ms 和点击穿透问题

```Javascript
<script src="https://cdn.bootcdn.net/ajax/libs/fastclick/1.0.6/fastclick.min.js"></script>

// JavaScript版本
if ('addEventListener' in document) {
    document.addEventListener('DOMContentLoaded', function() {
        FastClick.attach(document.body);
    }, false);
}

// jquery版本
$(function() {
    FastClick.attach(document.body);
});

// Common JS 模块版本
var attachFastClick = require('fastclick');
attachFastClick(document.body);

// 使用needsclick过滤特定的元素  特定的元素不需要使用fastclick来立刻触发点击事件 可以在元素的class上添加needsclick
<a class="needsclick">Ignored by FastClick</a>

```

## 阻止 a 标签默认事件：href="javaScript:;"

```Javascript
<a href="javaScript:;">阻止a标签默认事件</a>
```

<!-- ## window.open 在 ios 上兼容问题

```js
// 使用window.open在ios上面可能打开新页面
window.location.href = "http://www.baidu.com";
``` -->
