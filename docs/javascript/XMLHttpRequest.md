<!--
 * @Description: XMLHttpRequest 对象学习
 * @Author: panrui
 * @Date: 2021-08-13 10:36:57
 * @LastEditTime: 2021-08-13 10:39:05
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2023-11-17)

## XMLHttpRequest 取消请求

```js
// 通过 XMLHttpRequest 对象的 abort方法
let xhr = new XMLHttpRequest();
xhr.open("GET", "https://developer.mozilla.org/", true);
xhr.send();
setTimeout(() => xhr.abort(), 300);
```
