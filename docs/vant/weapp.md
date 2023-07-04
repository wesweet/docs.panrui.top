<!--
 * @Description: 小程序UI组件库
 * @Author: panrui
 * @Date: 2023-03-29 19:52:44
 * @LastEditTime: 2023-04-16 11:11:08
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->
## 最后更新时间：2023-04-16 11-11-08

## dialog组件使用

> 如果dialog组件在小程序自定义组件库中使用，需要设置context：this 绑定当前页面this，否则会提示找不到selector

## calendar组件 bug(1.10.15 已修复)
```js
// vant-weapp calendar组件 show-confirm为false的时候，同时设置allow-same-day 为true，点击同一天并不会触发confirm
// 解决方案
手动监听select事件，判断detail属性中，第二项数据是否为null来解决，手动关闭日历插件
```

## ActionSheet组件 
```js
点击遮蔽层关闭菜单的前置条件是需要绑定关闭事件，否则点击遮蔽层不会关闭
```