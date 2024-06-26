<!--
 * @Description: vue基础文档
 * @Author: prui
 * @Date: 2023-11-23 13:39:00
 * @LastEditTime: 2024-04-25 13:47:56
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 混合(mixin)

!> 一个包含组件选项对象的数组，这些选项都将被混入到当前组件的实例中

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

## 组件通信

> 1. 父子组件通信 Props
> 2. 子到父通信 Emit
> 3. $parent 和 $children 直接访问父组件的实例方法或子组件实例
> 4. ref 获取对子组件或 DOM 元素的直接引用，以便直接调用子组件的方法或访问其属性
> 5. $attrs 和 $listeners
> 6. Event Bus（事件总线）（当这些组件没有直接的父子关系）

```js
// event-bus.js
import Vue from "vue";

export const EventBus = new Vue();

// 发送组件
import { EventBus } from "./event-bus.js";

// 触发一个名为 'customEvent' 的事件，并附带数据
EventBus.$emit("customEvent", eventData);

// 接收组件
import { EventBus } from "./event-bus.js";

// 监听 'customEvent' 事件
EventBus.$on("customEvent", handleCustomEvent);

function handleCustomEvent(receivedEventData) {
  console.log("Received event data:", receivedEventData);
  // 在这里处理接收到的数据
}

// 在组件卸载时移除事件监听
export default {
  beforeDestroy() {
    EventBus.$off("customEvent", handleCustomEvent);
  },
};
```

> 7. Provide/Inject
> 8. Vuex
> 9. 本地存储

## 组件(components 待修改)

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

## 插件(plugins)

## 指令(directives) TODO 优先开发

## 过滤器(filters)

## 全局方法(globalMethods)

## 全局混合(globalMixin)

## 全局组件(globalComponents)

## 全局指令(globalDirectives)

```js

/**
 * 如果需要支持多个颜色变量的话，可以使用一个对象来映射，需要在这里添加对应的颜色值
 * 通过 v-highLight:yellow 来使用, 可以自定义颜色
 * 如果没有传入颜色值，则使用默认颜色，也可以修改默认颜色
 */
const defaultColor = '#F47D20'
const colorMap = {
    yellow: 'yellow',
}

// 通过传入高亮关键字
const highLightByKeyword = (el, binding, vnode, prevVnode) => {
    const color = colorMap[binding.arg] || defaultColor
    const value = binding.value.replace(/[.*+?^${}()|[\]\\]/g, '\\$&'); // 转义特殊字符
    const text = el.innerText
    if (value) {
        const regex = new RegExp(value, 'gi')
        const result = text.replace(regex, (matched) => `<span style="color:${color}">${matched}</span>`)
        el.innerHTML = result
    }
}


// 通过标签名高亮
const highLightByTag = (el, binding, vnode, prevVnode) => {
    let emElements = el.querySelectorAll('em');
    emElements.forEach(em => {
        em.style.color = colorMap[binding.arg] || defaultColor;
        em.style.fontStyle = 'unset';
    });
}


const highLightEnv = (el, binding, vnode, prevVnode) => {
    if(binding.value) {
        highLightByKeyword(el, binding, vnode, prevVnode)
    } else {
        highLightByTag(el, binding, vnode, prevVnode)
    }

}

// 控制页面高亮元素的自定义指令
const highLight = {
    // 在绑定元素的 attribute 前
    // 或事件监听器应用前调用
    created(el, binding, vnode, prevVnode) {
        // 下面会介绍各个参数的细节
    },
    // 在元素被插入到 DOM 前调用
    beforeMount(el, binding, vnode, prevVnode) {
        highLightEnv(el, binding, vnode, prevVnode)
    },
    // 在绑定元素的父组件
    // 及他自己的所有子节点都挂载完成后调用
    mounted(el, binding, vnode, prevVnode) {

    },
    // 绑定元素的父组件更新前调用
    beforeUpdate(el, binding, vnode, prevVnode) {
        highLightEnv(el, binding, vnode, prevVnode)
    },
    // 在绑定元素的父组件
    // 及他自己的所有子节点都更新后调用
    updated(el, binding, vnode, prevVnode) { },
    // 绑定元素的父组件卸载前调用
    beforeUnmount(el, binding, vnode, prevVnode) { },
    // 绑定元素的父组件卸载后调用
    unmounted(el, binding, vnode, prevVnode) { }

}



export default highLight
```

## 全局过滤器(globalFilters)

## 全局钩子(globalHooks)


最后更新时间：2024-6-4 10:17:38