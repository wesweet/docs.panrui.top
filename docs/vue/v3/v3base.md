<!--
 * @Description: v3使用指南
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2024-04-25 13:32:30
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2024-04-25)

## mixin 使用

!> 利用 Vue 的组合式 API 来封装和复用有状态逻辑的函数

> 1. 替代 v2 中的 mixin 功能
> 2. vue-composable 或 @vueuse/core (专门支持 Composition API 的第三方库)

1. 封装无状态逻辑的函数

```js
// 按照惯例，组合式函数名以“use”开头
import { ref } from "vue";

export default function useUser(initialName = "", initialAge = 0) {
  const userName = ref(initialName);
  const userAge = ref(initialAge);

  const greetUser = (name) => `Hello, ${name}!`;

  return { userName, userAge, greetUser };
}
```

2. 使用组合式函数

```vue
<template>
  <div>
    <h1>{{ greetUser }}</h1>
    <!-- ... -->
  </div>
</template>

<script setup>
import { defineComponent } from "vue";
import useUser from "@/composables/useUser";
const { userName, userAge, greetUser } = useUser("John", 25);
</script>
```

## ref 使用(获取原生 DOM 与组件实例)

```html
<!-- 单个DOM 元素 或者组件实例 -->
<div ref="myDiv">Hello, Vue 3!</div>
<child-component ref="myChild"></child-component>
<script setup>
  import { ref, onMounted } from "vue";
  import ChildComponent from './ChildComponent.vue';

  const myDiv = ref(null);
  const myChild = ref<InstanceType<typeof ChildComponent> | null>(null);

  onMounted(() => {
    // 在组件挂载后，myDiv.value 就指向了真实的 DOM 元素
    const domElement = myDiv.value;
    console.log(domElement.tagName); // 输出：'DIV'

    // 在组件挂载后，myChild.value 就指向了子组件实例
    const childInstance = myChild.value;
    if (childInstance) {
      childInstance.someMethod();
    }
  });
</script>
```

```html
<!-- 数组形式DOM 元素 或者组件实例 -->
<div v-for="(item, index) in items" :ref="`itemRef-${index}`">
  {{ item.text }}
</div>
<child-component
  v-for="(item, index) in items"
  :ref="`childRef-${index}`"
  :item="item"
></child-component>
<script setup>
  import { ref, onMounted } from 'vue';
  import ChildComponent from './ChildComponent.vue';

  const items = [/*...*/];
  const itemRefs = ref<Array<HTMLDivElement | null>>([]);
  const childRefs = ref<Array<InstanceType<typeof ChildComponent> | null>>([]);

  onMounted(() => {
    // 在组件挂载后，填充 itemRefs 数组
    for (let i = 0; i < items.length; i++) {
      itemRefs.value[i] = document.querySelector(`[ref="itemRef-${i}"]`);
    }
    // 在组件挂载后，填充 childRefs 数组
    for (let i = 0; i < items.length; i++) {
      childRefs.value[i] = getChildComponentByRef(`childRef-${i}`);
    }
    function getChildComponentByRef(refName: string): InstanceType<typeof ChildComponent> | null {
      const el = document.querySelector(`[ref="${refName}"]`);
      if (el instanceof ChildComponent) {
        return el;
      }
      return null;
    }
  });
</script>
```

## Provide / Inject

!> Vue 3 中 provide 和 inject 的绑定现在是响应式的。无论是直接提供的值还是提供的对象的属性，只要它们是响应式的，子组件都能自动响应其变化。
!> Vue 3 中也保留了祖先组件提供的值被最近祖先覆盖的特性。

```js
// 祖先组件
import { provide } from 'vue';

const someValue = 'Hello from Parent';
const someFunction = () => 'Parent function called';

provide('someValue', someValue);
provide('someFunction', someFunction);
</script>

// 子孙组件
import { inject } from 'vue';

const someValue = inject('someValue');
const someFunction = inject('someFunction');

if (!someValue) {
  throw new Error('someValue not provided');
}

console.log(someValue); // 输出：'Hello from Parent'
console.log(someFunction()); // 输出：'Parent function called'
```

## defineProps

!> 接收父组件传递的属性

```vue
// ParentComponent.vue
<template>
  <div>
    <h2>Parent Component</h2>
    <ChildComponent
      v-bind:title="parentTitle"
      :isEnabled="parentIsEnabled"
      :items="parentItems"
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import ChildComponent from "./ChildComponent.vue";

// 定义父组件内部状态
const parentTitle = ref<string>("From Parent");
const parentIsEnabled = ref<boolean>(true);
const parentItems = ref<string[]>(["Item 1", "Item 2", "Item 3"]);
</script>

// ChildComponent.vue
<template>
  <div>
    <h3>{{ title }}</h3>
    <p v-if="isEnabled">This feature is enabled.</p>
    <ul>
      <li v-for="(item, index) in items" :key="index">{{ item }}</li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from "vue";

// 声明 props 类型
interface Props {
  title: string;
  isEnabled: boolean;
  items: string[];
}

// 定义并获取 props
const props = defineProps<Props>();
</script>
```

## defineEmits

!> 通过 emit 触发父组件自定义函数

```vue
// ParentComponent.vue
<template>
  <div>
    <ChildComponent @customEvent="handleCustomEvent" />
  </div>
</template>

<script setup lang="ts">
function handleCustomEvent() {
  console.log("Custom event received in parent component!");
}
</script>

// ChildComponent.vue
<template>
  <div>
    <!-- ... existing content ... -->
    <button @click="handleClick">Trigger Custom Event</button>
  </div>
</template>

<script setup lang="ts">
import { defineEmits } from "vue";

interface EmittedEvents {
  (event: "customEvent"): void;
}

const emit = defineEmits<EmittedEvents>();

function handleClick() {
  emit("customEvent");
}
</script>
```

## defineExpose

!> 暴露内部属性和方法，帮助父组件通过 ref 调用子组件方法和属性

```vue
<template>
  <div>
    <span>{{ count }}</span>
    <button @click="increment">Increment</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

// 响应式状态
const count = ref(0);

// 内部方法
function increment() {
  count.value++;
}

// 显式暴露 count 和 increment 给外部
defineExpose({
  count,
  increment,
});
</script>
```

## defineComponent(待修改)

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
