<!--
 * @Description: 自定义组件库开发指南
 * @Author: panrui
 * @Date: 2021-07-08 11:36:43
 * @LastEditTime: 2023-07-05 13:21:09
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2024-03-25)

- vue2.x 自定义组件库开发指南

## 项目目录结构

- ├── example // 测试组件的项目目录
  - └── assets // 静态资源
  - └── mds // 组件使用说明文档
  - └── router // 路由配置文件
  - └── views // 页面
- ├── lib // 发布到 npm 仓库的文件
- ├── package // 组件源码目录
  - └── componentName // 组件
  - └── index.js // 注册组件

## 组件开发

在 package 文件夹下面创建对应组件文件夹 例如：

- ├── citypicker // 城市联动组件
  - └── src // 组件源码目录
    - └── CityPicker // 组件源码
  - └── index.js // 为组件添加 install 方法

```js
// 例如城市联动组件
export default {
  name: "PrCityPicker",
};

// 为组件添加install方法
import PrCityPicker from "./src/CityPicker";

PrCityPicker.install = function (Vue) {
  Vue.component(PrCityPicker.name, PrCityPicker);
};

export default PrCityPicker;
```

## 组件注册

```js
在 package 文件夹下 index.js 文件中,注册对应的组件,为组件添加installed方法
```

```js
// 例如城市联动组件
import PrCityPicker from "./citypicker";

const components = [PrCityPicker];

const install = function (Vue) {
  if (install.installed) return;
  install.installed = true;
  components.forEach((component) => {
    Vue.component(component.name, component);
  });
};

if (typeof window !== "undefined" && window.Vue) {
  install(window.Vue);
}

export { PrCityPicker };

export default {
  install,
  ...components,
};
```

## 组件发布

```js
// 打包组件库
npm run lib

// 登录 输入对应的账号、密码、邮箱
npm login

// 发布
npm publish
```