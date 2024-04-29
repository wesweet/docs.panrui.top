<!--
 * @Description:
 * @Author: prui
 * @Date: 2023-11-28 09:29:26
 * @LastEditTime: 2024-04-29 15:06:45
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## checkbox 传递参数(使用 event 对象)

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

最后更新时间：2024-4-29 15:07:06
