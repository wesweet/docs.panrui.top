<!--
 * @Description: elementui组件使用技巧
 * @Author: panrui
 * @Date: 2023-05-22 15:40:54
 * @LastEditTime: 2023-07-13 09:52:35
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-07-13 09-52-35

## DatePicker 组件

```html
<el-date-picker
  v-model="date"
  type="date"
  :picker-options="pickerOptions"
  placeholder="选择日期"
>
</el-date-picker>
```

```js
// 单个时间
data() {
  return {
    date: '', // 绑定的日期值
    pickerOptions: {
      disabledDate(date) {
        // 设置时间范围从今天开始
        return date && date < new Date(new Date().toLocaleDateString());
        // 设置最大为今天
        return date.getTime() > Date.now();
      }
    }
  }
}
```

```html
<el-date-picker
  @change="handleDateRangeChange"
  format="yyyy-MM-dd"
  v-model="date"
  type="daterange"
  :picker-options="pickerOptionRange"
  size="mini"
  range-separator="至"
  start-placeholder="开始日期"
  end-placeholder="结束日期"
  :disabled-date="disabledDate"
  :clearable="true"
>
</el-date-picker>
```

```js
// 时间范围
data() {
  return {
    date: [],
    pickerOptionRange:{
        shortcuts: [
            {
                text: '最近一个月',
                onClick(picker) {
                    const end = new Date();
                    const start = new Date();
                    start.setMonth(start.getMonth() - 1);
                    picker.$emit('pick', [start, end]);
                }
            },
            {
                text: '最近一年',
                onClick(picker) {
                    const end = new Date();
                    const start = new Date();
                    start.setFullYear(end.getFullYear() - 1);
                    picker.$emit('pick', [start, end]);
                }
            }
        ]
    },
  }
},
// 设置时间跨度为30天  这里才是真正的控制时间范围
handleDateRangeChange() {
    const startDate = this.date[0];
    const endDate = this.date[1];

    // 计算两个日期的时间差（以天为单位）
    const timeDiff = Math.abs(endDate - startDate) / (1000 * 60 * 60 * 24);

    if (timeDiff > 30) {
        // 如果时间跨度超过30天，则自动调整结束日期
        const adjustedEndDate = new Date(startDate.getTime() + 30 * 24 * 60 * 60 * 1000);
        this.date[1] = adjustedEndDate;
        this.$message.error('时间跨度不能超过一个月');
    }
},
// 设置时间跨域 这里的bug在于从当前时间往前推
disabledDate(time) {
    const oneYearAgo = new Date(new Date() - 315360000000); // 当前时间减去一年
    return time.getTime() < oneYearAgo || time.getTime() > Date.now(); // 日期最大跨度不超过一年
},
// 设置默认时间
setDefaultDate() {
    const end = new Date();
    const start = new Date();
    start.setMonth(start.getMonth() - 1);
    this.date = [start, end]
},

```

## ELUpload 组件

```js
// 阻止默认提交
设置el-upload 中 action 参数值为#，auto-upload为false

// 调用组件的外部方法
给el-upload 添加ref属性,通过ref调用相关方法

// 上传图片显示本地地址
const handChange = (uploadFile) => {
  form.file = uploadFile.raw
  imageurl = URL.createObjectURL(uploadFile.raw)
}

// 删除指定的图片
handleRemove(file) {
  // 实现缩略图模板时删除文件
  let fileList = this.$refs.upload.uploadFiles;
  let index = fileList.findIndex( fileItem => {
    return fileItem.uid === file.uid
  })
  fileList.splice(index, 1)
}

```

## 嵌套 form 表单校验

```html
<el-form
  :model="dynamicValidateForm"
  ref="dynamicValidateForm"
  label-width="100px"
  class="demo-dynamic"
>
  <el-form-item
    v-for="(domain, index) in dynamicValidateForm.domains"
    :label="'域名' + index"
    :key="domain.key"
    :prop="'domains.' + index + '.value'"
    :rules="{
      required: true, message: '域名不能为空', trigger: 'blur'
    }"
  >
    <el-input v-model="domain.value"></el-input
    ><el-button @click.prevent="removeDomain(domain)">删除</el-button>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="submitForm('dynamicValidateForm')"
      >提交</el-button
    >
    <el-button @click="addDomain">新增域名</el-button>
    <el-button @click="resetForm('dynamicValidateForm')">重置</el-button>
  </el-form-item>
</el-form>
```

```js
export default {
  data() {
    return {
      dynamicValidateForm: {
        domains: [
          {
            value: "",
          },
        ],
      },
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    removeDomain(item) {
      var index = this.dynamicValidateForm.domains.indexOf(item);
      if (index !== -1) {
        this.dynamicValidateForm.domains.splice(index, 1);
      }
    },
    addDomain() {
      this.dynamicValidateForm.domains.push({
        value: "",
        key: Date.now(),
      });
    },
  },
};
```

## 嵌套表单传参

```html
<el-form-item
  v-for="(item, index) in formList"
  :key="index"
  :label="item.label"
  :prop="item.prop"
  :rules="item.rules"
>
  <el-select
    v-model="obj.dept"
    size="mini"
    @change="getEnableLicenseList(index, obj.dept)"
    placeholder="请选择"
    filterable
  >
  </el-select>
</el-form-item>
```

```js
getEnableLicenseList(index, val) {}
```
