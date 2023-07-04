<!--
 * @Description: 微信小程序使用小技巧
 * @Author: panrui
 * @Date: 2021-09-18 11:49:24
 * @LastEditTime: 2023-05-30 09:29:31
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-05-30 09-29-31

## 获取 appid、小程序版本、开发环境

```JS
// 获取当前小程序appid、develop：开发版、trial：体验版、release：正式版、version：线上小程序版本号
wx.getAccountInfoSync()
```

## DOM 动态添加 class 与动态设置 style

> class="{{ classA data ? 'classB' : '' }}"

> style="width:{{width + 'rpx'}}"

## 修改数组对象某个属性

```js
const property = `data[${index}].name`; // 此处直接使用属性名称即可，属于拼接字符串
this.setData({
  [property]: "xxxxxxxxx",
});
```

## 小程序页面通信之 event

```js
// 场景：页面A跳转页面B，并且需要传递大量数据

// 页面A
const data = {};
wx.navigateTo({
  url: `页面B路径`,
  success: function (res) {
    // 向打开页面传递数据
    res.eventChannel.emit("acceptDataFromBaglist", { data: data });
  },
});

// 页面B
const eventChannel = this.getOpenerEventChannel();
eventChannel.on("acceptDataFromBaglist", ({ data }) => {
  console.log(data);
});
```

## scroll-view 组件隐藏滚动条设置

```html
<scroll-view enhanced show-scrollbar="{{false}}"></scroll-view>
```

## textarea 组件设置双向绑定时，需要失焦状态，才会更新值

```html
<!-- 通过绑定input事件手动更新值 -->
<textarea bindinput="bindinput"></textarea>
```

## 组件通信的三种方式

> 1. 使用数据传递方式 properties 父传子

> 2. this.triggerEvent('myevent', myEventDetail, myEventOption)，触发父组件定义的方法 子传父

> 3. 父组件还可以通过 this.selectComponent 方法获取子组件实例对象，访问子组件的属性和方法

## 设置 WXS 文件脚本

```js
// 1：创建一个wxs的文件脚本
module.exports = {
  fnToFixed: function (value, number) {
    number = number ? number : 0
    return Number(value).toFixed(number)
  }
}

// 2：在wxml 页面引入该wxs, src表示路径 module表示对象引用
<wxs src="../../utils/filter.wxs" module="filter"></wxs>

// 3：在{{}} 语法中使用
<view> {{filter.fnToFixed(tools.FOO)}} </view>
```

## 自定义组件修改第三方 UI 组件库样式失效

> 组件当中开启开启 styleIsolation: 'shared'选项

## 分享页面参数设置

```js
onShareAppMessage() {
  return {
    title: '标题', //分享标题
    desc: '', //分享内容
    path: `/pages/actioncard/actioncard?id=${data}`
    imageUrl: '图片地址'
  }
}
```

## 二维码打开小程序&分享页面打开小程序之获取参数区别

> 通过二维码 使用 options.q 获取的是二维码地址 url

> 通过分享小程序 直接使用 options.property 获取对应的参数

## 获取上一个打开的页面信息

```js
const pages = getCurrentPages();
const route = pages[pages.length - 2]; // 路由信息 route:页面url
```

## 小程序下拉刷新，加载组件(三个小黑点)不显示原因

> 三个小黑点默认是白色，修改下拉刷新样式 "backgroundTextStyle": "dark"

## 设置标签 last-child、first-child 样式失效 bug

> 需要将子集包裹在一个父元素当中(不能是页面根节点)

## 判断是否为微信内置浏览器

```js
var agent = navigator.userAgent.toLowerCase();
if (agent.match(/MicroMessenger/i) == "micromessenger") {
  console.log("是在微信内置浏览器里面");
} else {
  console.log("不在微信内置浏览器里面");
}
```

## 小 tip

> block 组件与 vue 中 template 标签的作用一致

> wx:if 与 hiddle 的使用与 vue 类似

> 小程序原生组件层级最高，所有页面中其他组件无论设置 z-index 为多少，都无法覆盖在原生组件上面

> canvas 画布组件创建时，一定要保证 dom 标签存在且宽高都在。就算设置 display:none 都将创建失败

> canvas 在自定义组件中创建 canvas 画布时，需要绑定当前组件 this，或者使用 this.createSelectorQuery 来创建画布
