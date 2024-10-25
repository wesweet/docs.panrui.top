<!--
 * @Author: panr99 1547177202@qq.com
 * @Date: 2024-06-24 13:51:12
 * @LastEditors: panr99 1547177202@qq.com
 * @LastEditTime: 2024-10-25 16:04:43
 * @FilePath: \docs.panrui.top\docs\uniapp\uviewui.md
 * @Description: uview组件库使用记录
-->

## DatetimePicker选择器

- mode设置成datetime时，通过时间戳设置组件默认选中时间，回显异常。

- 出现问题的原因在于我v-model绑定的默认值时候设为0，最好设置一个时间

## checkbox 额外传递参数(使用 event 对象) (相似情况input标签)

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

最后更新时间：2024-10-25 16:07:37
