<!--
 * @Description: vue3记录文档
 * @Author: prui
 * @Date: 2024-04-25 15:14:16
 * @LastEditTime: 2024-05-23 10:36:38
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

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

## defineOptions

> name 属性
> 解决 vue 中修改组件名称时候需要创建额外 script 标签

```vue
defineOptions({ name: 'ComponentName' })
```

> inheritAttrs 属性
> 组件穿透属性配置(在组件上面添加属性，则会被穿透到组件的根标签上)

```vue
<script setup lang="ts">
import { defineOptions } from "vue";
defineOptions({
  inheritAttrs: false,
});
</script>
```

## defineModel

> props emit 的替代方案
> 使用 v-model 实现双向绑定

```html
<!-- 父组件 -->
<el-card class="box-card">
  <div slot="header" class="clearfix" style="margin-bottom: 20px">
    <span>测试vue3.4 defineModel 属性</span>
  </div>
  <el-row :gutter="20" class="form-row">
    <el-col :span="6">年龄：</el-col>
    <el-col :span="6">{{ form.age }}</el-col>
    <el-col :span="6"> <Children v-model="form" /> </el-col>
  </el-row>
</el-card>
<script lang="ts" setup>
  const form = ref({
    age: 18,
  });
</script>

<!-- 子组件 -->
<el-row :gutter="20" class="form-row">
  <el-col :span="10"
    ><el-button type="primary" @click="handleEditAge"
      >修改年龄</el-button
    ></el-col
  >
</el-row>
<script lang="ts" setup>
  const form: any = defineModel();

  const handleEditAge = () => {
    form.value.age = Math.floor(Math.random() * 100);
  };
</script>
```

## 渲染函数&JSX

> 1. 子节点的表示：子节点可以是一个字符串，用于表示文本内容；也可以是一个数组，用于表示多个子节点。如果子节点是一个数组，那么数组中的每个元素都可以是一个由 h 函数创建的虚拟节点。
> 2. 事件监听器的表示：在 props 对象中，可以使用 on 或 nativeOn 来添加事件监听器。例如，{ onClick: this.handleClick }。
> 3. 组件的表示：如果 tag 是一个组件，那么 props 就表示该组件的 props，children 表示该组件的默认插槽内容。
> 4. 自闭合元素：对于自闭合元素，例如 input，children 应该是 null 或 undefined
> 5. 特殊属性：对于某些特殊的属性，例如 style 和 class，Vue 提供了特殊的处理方式。例如，style 可以是一个字符串，也可以是一个对象；class 可以是一个字符串，也可以是一个数组或对象。
> 6. Fragment 和 Teleport：Vue 3 支持 Fragment 和 Teleport 这两种新的特性。Fragment 允许一个组件有多个根元素，而 Teleport 允许将子元素渲染到 DOM 树的其他位置。
> 7. 函数式组件：在 Vue 3 中，函数式组件的写法有所改变，现在需要使用 FunctionalComponent 类型，并且不再需要 functional: true 选项

```js
render() {
  return h('div', { class: 'my-div', id: 'myId' }, 'Hello, world!');
}
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

最后更新时间：2024-5-14 15:59:53
