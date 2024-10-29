<!--
 * @Author: panr99 1547177202@qq.com
 * @Date: 2024-06-24 13:51:12
 * @LastEditors: panr99 1547177202@qq.com
 * @LastEditTime: 2024-10-28 09:06:35
 * @FilePath: \docs.panrui.top\docs\uniapp\uviewui.md
 * @Description: uview组件库使用记录
-->

## picker

- picker 组件滚动其他选项，再次打开的时候还会停留在上一次选择的值上面

```js
// 通过这种方式可以保证每次点开的时候，默认显示的是当前选择的值
const picker = this.$refs.picker;
picker.setIndexs([index]);
```

## DatetimePicker 选择器

- 修复时间插件回显异常 在插件外层嵌套一个标签，并使用 v-if 来控制显示隐藏，目的在于每次点开的时候，时间选择器都相当于重新创建，这样就不会保留上一次滚动的值

```html
<view v-if="time.show">
  <u-datetime-picker
    :show="time.show"
    v-model="time.value"
    :mode="time.mode"
    @close="time.show = false"
    @confirm="selectTime"
    @cancel="time.show = false"
  ></u-datetime-picker>
</view>
```

## checkbox 额外传递参数(使用 event 对象) (相似情况 input 标签)

```html
<view class="list-item" v-for="(item, index) in itemList">
  <u-checkbox-group>
    <u-checkbox
      v-model="item.btnType"
      shape="circle"
      @change="checkboxChange($event,index)"
    ></u-checkbox>
  </u-checkbox-group>
</view>
```

```js
checkboxChange(event, index) {
    conosole.log(event, index);
},
```

## u-modal 组件使用插槽自定义内容

```html
<u-modal
  v-model="modalShow"
  :mask-close-able="true"
  :show-title="false"
  :show-confirm-button="false"
  :useSlot="true"
>
  <view class="slot-content" style="padding: 10px 20px" slot="default">
    <view>叶酸代谢基因检测</view>
  </view>
</u-modal>
```

最后更新时间：2024-10-29 09:36:51
