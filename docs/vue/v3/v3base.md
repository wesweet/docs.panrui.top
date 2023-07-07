<!--
 * @Description: v3使用指南
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-05-18 14:48:22
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-05-18 10-03-25

- v3 使用文档

## defineComponent

> 1. 定义组件的函数，接收一个配置对象，返回一个组件对象，可以通过 app.component 方法注册到应用中

```js
export default defineComponent({
  name: "UserBasicPage",
});
```

## setup

> 1. 组件配置的一个选项，是一个函数。接受两个参数：props 和 context。setup 函数必须返回一个对象，这个对象中包含组件的模板中需要使用的数据、方法以及生命周期钩子函数。

```js
setup(props, context){
  return {}
}
```

## ref

> 1. 接收一个参数并返回一个响应式对象，这个对象有一个.value 属性，他是一个可变的值

```js
const emailType = ref < string > "@qq.com";
console.log(emailType.value);
```

## reactive

> 1. 将一个普通对象转换成响应式对象，reactive 函数返回的是一个 Proxy 对象

```js
interface FormState {
  username: string;
  password: string;
  remember: boolean;
}
const formState =
  reactive <
  FormState >
  {
    username: "",
    password: "",
    remember: true,
  };
```

## onMounted

> 1. 钩子函数，它在组件挂载后执行，只能在 setup 函数中使用，而不能在模板中使用。接收一个回调函数作为参数

```js
setup() {
    onMounted(() => {
      console.log('Component mounted')
      // 执行一些操作，比如请求数据、初始化变量等
    })
  }
```
