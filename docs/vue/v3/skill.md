<!--
 * @Description: vue3技巧文档
 * @Author: prui
 * @Date: 2024-04-25 15:14:33
 * @LastEditTime: 2024-04-25 16:05:05
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->


## 自定义组件之input，如何自动更新

```js
// 子组件 prinput
<input
    class="main-input"
    :placeholder="placeholder"
    :maxlength="maxlength"
    :value="value"
    @input="$emit('update:modelValue', $event.detail.value)"
/>
const props = defineProps({
  placeholder: {
    type: String,
    default: "请输入内容",
  },
  maxlength: {
    //最大长度
    type: [Number, String],
    default: 20,
  },
  value: {
    type: [String, Number],
    default: "",
  }, //值
});

// 父组件中使用
<prinput placeholder="请输入账号" v-model="formData.username"></prinput>

// 这种方式下，父组件中需要使用v-model绑定子组件的value值，子组件输入的时候也会自动更新父组件的value值
```

## 使用ref进行表单检验

```js
```


最后更新时间：2024-4-29 14:13:03