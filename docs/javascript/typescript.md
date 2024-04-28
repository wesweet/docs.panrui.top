<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-06-05 19:48:30
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

-  [官方文档](https://ts.xcatliu.com/)
> 2.  [github 中文仓库指南](https://github.com/zhongsp/TypeScript)
> 3.  [中文文档](https://zhongsp.gitbooks.io/typescript-handbook/content/)

```js
npm install -g typescript
```

## ts 类型

#### 基本类型

```
boolean、number、string、void(表示没有任何返回值的函数)、null、undefined
```

> 1.  声明一个 void 类型的变量没有什么用，因为你只能将它赋值为 undefined 和 null

> 2.  undefined 和 null 是所有类型的子类型

> 3. symbol 表示唯一的、不可变的值，通常用作对象的属性名。

#### 复合类型

```
array、tuple、object、enum、any、unknown、never
```

> 1. unknown 类型，表示一个值的类型是未知 与 any 类型不同，unknown 类型是类型安全的。

> 2. unknown 与 any 的区别

```
any：表示任意类型,使用any可以跳过类型检查
unknown：表示不确定的类型, 需要进行类型检查
```

#### 高级类型

```
union、intersection、type、interface、class、function
```

##### interface

> 1. 定义接口的关键字，通过定义接口，规范数据类型，函数签名等形式

```js
// 定义接口 FormState, 该接口包含三个字段
interface FormState {
  username: string;
  password: string;
  remember: boolean;
}
```

##### class

> 1.

```js
class Product {
  name: string;
  price: number;
}
```

##### enum

> 1. 一种用于定义一组常量的数据类型,这些成员的值默认从 0 开始自动递增,也可以手动指定值

```js
// 默认值从0开始
enum Color {
  Red,
  Green,
  Blue,
}

// 手动指定值
enum Api {
  ACCOUNT_INFO = '/account/getAccountInfo',
  SESSION_TIMEOUT = '/user/sessionTimeout',
  TOKEN_EXPIRED = '/user/tokenExpired',
}
```

##### 元组

>1. 数组合并了相同类型的对象，而元组（Tuple）合并了不同类型的对象


##### 泛型

>1. 泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。

#### 其他类型

##### Promise 类型

> 1. Promise<T> 表示一个异步操作，该操作最终会产生类型为 T 的值。T 是一个类型参数，表示异步操作返回的值的类型。

```js
function fetchData(): Promise<string> {
  return new Promise((resolve, reject) => {
    // 异步操作
    // 如果操作成功，调用 resolve(value) 返回结果
    // 如果操作失败，调用 reject(error) 返回错误
  });
}
```

##### & 交叉类型

> 1. 交叉类型的特点是，它将多个类型的成员合并到一个类型中

```js
interface Dog {
  breed: string;
  bark(): void;
}

interface Cat {
  breed: string;
  meow(): void;
}

type DogCat = Dog & Cat;

const pet: DogCat = {
  breed: "Mixed",
  bark() {
    console.log("Woof!");
  },
  meow() {
    console.log("Meow!");
  },
};
```

## type

> 1. 创建类型别名的关键字 类型别名允许你为一个类型起一个新的名字

```js
interface Dog {
  breed: string;
  bark(): void;
}

interface Cat {
  breed: string;
  meow(): void;
}

type DogCat = Dog & Cat;
```

## as 运算符

> 1. 类型断言运算符，用于将一个表达式的类型指定为特定的类型

## | 运算符

> 1. 联合类型运算符
> 2. 当一个变量被设置为联合类型时候，只能访问联合类型的所有类型里共有的属性或方法

## 函数

#### 函数表达式

<!-- TODO 待删除

## 对象的类型-接口

```js
interface Person {
  name: string;
  age: number;
}
// 赋值的时候，变量的形状必须和接口的形状保持一致
let tom: Person = {
  name: "Tom",
  age: 25,
};
// 可选属性
interface Person {
  name: string;
  age?: number;
}

let tom: Person = {
  name: "Tom",
};

// 但是仍然不允许添加未定义的属性

// 任意属性
interface Person {
  name: string;
  age?: number;
  [propName: string]: any;
}

let tom: Person = {
  name: "Tom",
  gender: "male",
};
```

## 数组的类型

```js
// 数组的类型
let fibonacci: number[] = [1, 1, 2, 3, 5]; // 数组中不允许非数字

// 数组泛型 Array<elemType>
let fibonacci: Array<number> = [1, 1, 2, 3, 5];

// 用接口表示数组
interface NumberArray {
  [index: number]: number;
}
let fibonacci: NumberArray = [1, 1, 2, 3, 5];

// 类数组
function sum() {
  let args: number[] = arguments;
}
```

## 函数的类型

```js
// 函数的类型 (一个函数有输入和输出)
// 函数声明
function sum(x: number, y: number): number {
  return x + y;
}

// 函数表达式
let mySum: (x: number, y: number) => number = function (
  x: number,
  y: number
): number {
  return x + y;
};
// 在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型

// 用接口定义函数的形状
interface SearchFunc {
  (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function (source: string, subString: string) {
  return source.search(subString) !== -1;
};
```

## 类型断言

```js
// 值 as 类型 或者 <类型>值
// 注意事项：与 void 的区别是，undefined 和 null 是所有类型的子类型。也就是说 undefined 类型的变量，可以赋值给 number 类型的变量

// 这样不会报错
let num: number = undefined;

// 这样也不会报错
let u: undefined;
let num: number = u;
```

## 类型检查

```js
// 1：函数参数需要指定类型
// 2：定义变量时指定类型

// 我们使用 : 指定变量的类型，: 的前后有没有空格都可以
function sayHello(person: string) {
  return "Hello, " + person;
}

let user: number[] = [0, 1, 2];
```

## 泛型
```js
// 泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性
```

## 声明文件

> 创建声明文件 typings.d.ts

```js
declare var 声明全局变量
declare function 声明全局方法
declare class 声明全局类
declare enum 声明全局枚举类型
declare namespace 声明（含有子属性的）全局对象
declare global 扩展全局变量
declare module 扩展模块
interface 和 type 声明全局类型
export 导出变量
export namespace 导出（含有子属性的）对象
export default ES6 默认导出
export = commonjs 导出模块
export as namespace UMD 库声明全局变量

/// <reference /> 三斜线指令
```

## 函数类型 -->


最后更新时间：2024-4-28 16:11:49