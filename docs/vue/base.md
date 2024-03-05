<!--
 * @Description:
 * @Author: prui
 * @Date: 2023-11-23 13:39:00
 * @LastEditTime: 2024-03-05 15:33:17
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2024-03-05)

## 组件(components)

> 组件注册的方式

```js
// 全局注册
import { createApp } from "vue";
import MyComponent from "./App.vue";

const app = createApp({});
app.component("MyComponent", MyComponent);
```

```js
// 局部注册
<template>
  <ComponentA />
</template>
<script>
import ComponentA from './ComponentA.vue'

export default {
  components: {
    ComponentA
  }
}
</script>
```

> 组件接收数据的方式

```js
// 接收参数
// v2版本
export default {
  props: ["foo"],
  created() {
    // props 会暴露到 `this` 上
    console.log(this.foo);
  },
};
```

```html
// v3版本
<script setup>
  const props = defineProps(["foo"]);
  console.log(props.foo);
</script>
;
```

> 组件继承未定义的属性

```js
// 透传(Attributes 继承)
<!-- <MyButton> 的模板 -->
<button>click me</button>

<MyButton class="large" />

// 最终渲染的结果
<button class="large">click me</button>
```

> 使用依赖注入解决组件多层级传递

```js
// 依赖注入
// 父组件作为提供者
export default {
  provide: {
    message: "hello!",
  },
  provide() {
    // 使用函数的形式，可以访问到 `this`
    return {
      message: this.message,
    };
  },
};
// 再整个应用层添加依赖
import { createApp } from "vue";

const app = createApp({});

app.provide(/* 注入名 */ "message", /* 值 */ "hello!");
```

```js
// 将数据注入到子组件
export default {
  inject: ["message"],
  created() {
    console.log(this.message); // injected value
  },
};
```

```html
<script setup>
  import { inject } from "vue";
  const message = inject("message");
</script>
```

> 异步加载组件

```js
// 异步组件
// 使用defineAsyncComponent异步加载组件
app.component(
  "MyComponent",
  defineAsyncComponent(() => import("./components/MyComponent.vue"))
);
```

## 混合(mixin)

> 一个包含组件选项对象的数组，这些选项都将被混入到当前组件的实例中

- 执行顺序、合并规则、冲突以组件数据优先

```
当组件和混入中都定义了同一个生命周期钩子时，它们会被合并为一个数组。在执行时，会先按照混入注册的顺序执行混入中的钩子函数，然后执行组件自身的钩子函数。
例如，如果有两个混入 mixin1 和 mixin2，以及组件 MyComponent，它们都定义了 created 钩子，那么执行顺序将是
mixin1.created
mixin2.created
MyComponent.created
当组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”。
比如，数据对象在内部会进行递归合并，并在发生冲突时以组件数据优先
```

## 组合式函数

> 在 Vue 应用的概念中，“组合式函数”(Composables) 是一个利用 Vue 的组合式 API 来封装和复用有状态逻辑的函数。

```js
// mouse.js
import { ref, onMounted, onUnmounted } from "vue";

// 按照惯例，组合式函数名以“use”开头
export function useMouse() {
  // 被组合式函数封装和管理的状态
  const x = ref(0);
  const y = ref(0);

  // 组合式函数可以随时更改其状态。
  function update(event) {
    x.value = event.pageX;
    y.value = event.pageY;
  }

  // 一个组合式函数也可以挂靠在所属组件的生命周期上
  // 来启动和卸载副作用
  onMounted(() => window.addEventListener("mousemove", update));
  onUnmounted(() => window.removeEventListener("mousemove", update));

  // 通过返回值暴露所管理的状态
  return { x, y };
}
```

```html
<script setup>
  import { useMouse } from "./mouse.js";

  const { x, y } = useMouse();
</script>

<template>Mouse position is at: {{ x }}, {{ y }}</template>
```

## 插件(plugins)

## 指令(directives) TODO 优先开发

## 过滤器(filters)

## 全局方法(globalMethods)

## 全局混合(globalMixin)

## 全局组件(globalComponents)

## 全局指令(globalDirectives)

## 全局过滤器(globalFilters)

## 全局钩子(globalHooks)
