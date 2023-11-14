<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-11-14 11:22:37
 * @LastEditTime: 2023-11-14 11:23:28
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 函数与对象 prototype、**proto**、constructor 的关系

> 1.  函数是对象，对象是函数的实例，对象的原型是函数的原型对象
> 2.  函数的原型对象的原型是 Object.prototype
> 3.  函数拥有 prototype 属性，对象拥有**proto**属性

```js
function Person() {} // 函数是对象
var person = new Person(); // 对象是函数的实例
console.log(Person.prototype); // 函数的原型对象
console.log(person.__proto__); // 对象的原型 隐式原型
console.log(Person.prototype.constructor === Person); // true 函数的原型对象的构造函数是函数本身
console.log(person.__proto__ === Person.prototype); // true 对象的原型是函数的原型对象
console.log(Person.prototype.__proto__ === Object.prototype); // true 函数的原型对象的原型是Object.prototype
console.log(Object.prototype.__proto__ === null); // true Object.prototype的原型是null

instanceof // 判断对象是否是某个构造函数的实例 就是通过上面那种方式去找，如果两条线相交就是true
```

## 原型链 和 继承

> 1.  访问一个对象的属性时，会先在基本属性中查找，如果没有，就会沿着**proto**这条链向上查找，这就是原型链
> 2.  由于原型链的存在，我们可以在原型对象上定义方法和属性，这些方法和属性可以被该原型对象的所有实例对象共享，这就是继承

## 作用域

## 作用域链

## 闭包

## this

## call apply bind

## 事件循环

## 事件委托

## 事件模型

## 事件捕获

## 事件冒泡

## 事件流

## 事件对象

## 事件类型

## 事件处理程序

## 事件监听

## 事件绑定

## 事件代理
