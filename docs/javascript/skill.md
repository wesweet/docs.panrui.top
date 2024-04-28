<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2024-04-28 15:16:57
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 常用小技巧

#### ?? || ?. && 使用方式

```js
// 只有value 为 null 或者undefined时才会返回 'jack'，否则返回value
const name = value ?? 'jack'

// 会先将value转化为布尔值判断，为true时返回value，否则返回'jack'
const name = value || 'jack'

// 可选链操作符 ?.
主要用与访问对象数据的时候, 不清楚该字段是否存在.

// 逻辑操作符 &&
使用&& 代替 if 条件判断语句
```

#### if 条件中存在多个 || 情况

```js
if (x === "abc" || x === "def" || x === "ghi" || x === "jkl") {
  //logic
}
//shorthand
if (["abc", "def", "ghi", "jkl"].includes(x)) {
  //logic
}
```

#### 多个 if 判断，不想使用 switch 情况

```js
const add_level = { 5: 1, 10: 2, 12: 3, 15: 4 }[add_step] || 0;
```

#### 数字取整

```js
// 1 使用 |
const num = 123.456;
console.log(num | 0); // 123

// 2 使用 ~~
console.log(~~num);

// 3 使用 >>
console.log(num >> 0);
```

#### string 转换为数字

```js
// 使用 * 1 来转换为数字
"32" * 1; // 32
"ds" * 1; // NaN
null * 1; // 0
undefined * 1; // NaN
1 * { valueOf: () => "3" }; // 3

// 使用 + 来转化字符串为数字
+"123"; // 123
```

#### 判断奇偶数,负数同样适用

#### 判断一个对象是不是空对象

```js
// 方法1
Object.keys(obj).length === 0;
// 方法2
JSON.stringify(obj) === "{}";
```

#### 对象转数组

```js
// Object.keys 返回对象的属性名数组
// Object.values 返回对象的属性值数组
const obj = { a: 1, b: 2, c: 3 };
const arr = Object.keys(obj).map((key) => {
  return {
    value: Number(key),
    label: obj[key],
  };
});
```

## 优化方案

#### 解决接口重复请求

```js

```

#### 尾调用优化

> 1. 函数的最后一步是调用函数(减少内存)

#### 尾递归

> 1. 函数调用自身，称为递归。如果尾调用自身，就称为尾递归。

```js
const num = 3;
!!(num & 1); // true
!!(num % 2); // true
```

## 高阶函数

> 接收另一个函数作为参数或者返回值是一个函数的函数称之为高阶函数

#### 柯里化

```js
function curry(fn) {
  let slice = Array.prototype.slice, // 将slice缓存起来
    args = slice.call(arguments, 1); // 这里将arguments转成数组并保存

  return function () {
    // 将新旧的参数拼接起来
    let newArgs = args.concat(slice.call(arguments));
    return fn.apply(null, newArgs); // 返回执行的fn并传递最新的参数
  };
}
```

#### 节流

```js
// func 函数; delay 延迟执行毫秒数; type  1 时间戳版(立即执行)，2 定时器版(结束在执行一次)
let delay = 3000;
let type = 1;
function throttle() {
  if (type == 1) {
    let previous = 0;
    let now = Date.now();
    if (now - previous > delay) {
      previous = now;
      console.log("执行业务逻辑");
    }
  } else {
    let timeout;
    if (!timeout) {
      timeout = setTimeout(() => {
        timeout = null;
        console.log("执行业务逻辑");
      }, delay);
    }
  }
}
```

#### 防抖

```js
// timeout 存储定时函数变量; immediate 是否立即执行版本; delay 延迟时间
let timeout = ''
let immediate = false
let delay = 3000
debounce() {
  if (timeout) {
    clearTimeout(timeout)
  }
  if (immediate) {
    // 立即执行版本
    let callNow = !timeout
    timeout = setTimeout(() => {
      timeout = null
    }, delay)
    if (callNow) {
      console.log('执行业务逻辑')
    }
  } else {
    timeout = setTimeout(() => {
      console.log('执行业务逻辑')
    }, delay)
  }
},
```

#### 组合函数

## 宽松相等 || 隐式转换真值表

![宽松相等真值表](http://work.panrui.top:8083/static/ToPrimitive_20210630102406.jpg)

## 前端实现图片下载 通过 Blob 对象

```js
let imgDom = document.querySelector(".el-image__inner");
// 创建canvas
let canvas = document.createElement("canvas");
const context = canvas.getContext("2d");
canvas.width = imgDom.width;
canvas.height = imgDom.height;
context.drawImage(imgDom, 0, 0, imgDom.width, imgDom.height);
// 转成Blob
canvas.toBlob(
  function (blob) {
    // 创建隐藏的可下载链接
    let url = URL.createObjectURL(blob);
    let a = document.createElement("a");
    a.href = url;
    // 时间戳
    let timestamp = new Date().getTime();
    a.download = timestamp + ".jpg";
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    // 释放掉blob对象
    URL.revokeObjectURL(url);
  },
  "image/jpeg",
  1
);
```

## PC 端实现点击复制功能

```js
navigator.clipboard
  .writeText('要复制的文案')
  .then(() => {
    this.$message.success("复制成功");
  })
  .catch(() => {
    this.$message.error("复制失败");
  });
```

最后更新时间：2024-4-28 15:58:09