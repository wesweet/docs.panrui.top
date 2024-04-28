<!--
 * @Description: es6 使用文档
 * @Author: prui
 * @Date: 2024-04-28 16:18:15
 * @LastEditTime: 2024-04-28 16:21:42
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

- [ES6 文档](https://es6.ruanyifeng.com/)

## Promise

#### 基本使用

```js
const updateEducationInfo = (userId, educationInfo, connection) => {
  const { schoolName, major, startDate, endDate } = educationInfo;

  return new Promise((resolve, reject) => {
    const query = `UPDATE education_info SET school_name = ?, major = ?, start_date = ?, end_date = ? WHERE user_id = ?`;
    const values = [schoolName, major, startDate, endDate, userId];

    connection.query(query, values, (err, results) => {
      if (err) {
        reject(err);
      } else {
        resolve();
      }
    });
  });
};
```

#### all

> 1.  全部成功才成功,返回值组合成数组

```js
const insertWorkInfo = () => {
  const insertPromises = workInfoList.map((workInfo) => {
    const { companyName, startDate, endDate, projectInfoList } = workInfo;

    return new Promise((resolve, reject) => {
      const insertQuery = `INSERT INTO user_work (user_id, company_name, start_date, end_date) VALUES (?, ?, ?, ?)`;
      const insertValues = [userId, companyName, startDate, endDate];

      connection.query(insertQuery, insertValues, (err, results) => {
        if (err) {
          reject(err);
        } else {
          const workId = results.insertId;
          resolve();
        }
      });
    });
  });

  return Promise.all(insertPromises);
};
```

#### race

> 1.  有一个 promise 先改变状态，race 也就会跟着改变状态，那个率先改变的 Promise 实例的返回值，就传递给 race 的回调函数

#### allSettled

> 1. 所有异步操作都结束，不管每一个操作是成功还是失败。一旦发生状态变更，状态总是 fulfilled，不会变成 rejected。状态变成 fulfilled 后，它的回调函数会接收到一个数组作为参数，该数组的每个成员对应前面数组的每个 Promise 对象。

#### any

> 1.  只要参数实例有一个变成 fulfilled 状态，包装实例就会变成 fulfilled 状态；如果所有参数实例都变成 rejected 状态，包装实例就会变成 rejected 状态。
> 2.  Promise.any()不会因为某个 Promise 变成 rejected 状态而结束，必须等到所有参数 Promise 变成 rejected 状态才会结束。(与 race 的区别)

## export

#### export default

> 1.  export default 命令用于指定模块的默认输出。一个模块只能有一个默认输出，因此 export default 命令只能使用一次。所以，import 命令后面才不用加大括号，因为只可能唯一对应 export default 命令。

```js
// export-default.js
export default function () {
  console.log("foo");
}
```

```js
// import-default.js
import customName from "./export-default";
customName(); // 'foo'
```

#### export

> 1.  export 命令用于规定模块的对外接口，import 命令用于输入其他模块提供的功能。

```js
// export.js
export const name = "panrui";
export const age = 18;
export const address = "北京";
```

```js
// import.js
import { name, age, address } from "./export";
console.log(name, age, address); // panrui 18 北京
```

#### export 与 export default 的区别

> 1.  export 与 export default 均可用于导出常量、函数、文件、模块等
> 2.  你可以在其它文件或模块中通过 import 导入导出的内容
> 3.  在一个文件或模块中，export、import 可以有多个，export default 仅有一个
> 4.  通过 export 方式导出，在导入时要加{ }，export default 则不需要
> 5.  export 可以导出变量表达式，export default 不行
> 6.  export 导出的变量可以改名再导入，export default 不行

#### exports 与 module.exports 的区别

> 1.  module.exports 初始值为一个空对象 {}
> 2.  exports 是指向的 module.exports 的引用
> 3.  require() 返回的是 module.exports 而不是 exports
> 4.  exports 不能直接改变指向，而 module.exports 可以

## import

- import 命令用于加载模块，提供了一个对外接口，其他模块可以加载这个模块。

```js
import { name, age, address } from "./export";
```

#### import()

- import()函数可以用在任何地方，不仅仅是模块，非模块的脚本也可以使用。它是运行时执行，也就是说，什么时候运行到这一句，也会加载指定的模块。另外，import()函数与所加载的模块没有静态连接关系，这点也是与 import 不相同。import()类似于 Node 的 require 方法，区别主要是前者是异步加载，后者是同步加载。

```js
const main = document.querySelector("main");

import(`./section-modules/${someVariable}.js`)
  .then((module) => {
    module.loadPageInto(main);
  })
  .catch((err) => {
    main.textContent = err.message;
  });
```

#### import.meta.glob()

- import.meta.glob 是 JavaScript 中的一个特殊属性，用于在模块中获取匹配指定模式的模块路径列表。它通常与动态导入（dynamic import）结合使用，用于动态加载模块。
- import.meta.glob 属性返回一个异步迭代器（AsyncIterator），您可以使用 for await...of 循环来遍历匹配的模块路径列表。每个迭代的值都是一个包含 url 和 module 属性的对象，其中 url 是匹配的模块路径，module 是对应模块的默认导出

```js
// eager: true 表示立即加载匹配的模块。这意味着在调用 import.meta.glob 方法后，会立即开始加载匹配的模块，而不是在后续使用时再进行加载。
// import: 'default' 表示加载模块的默认导出。当模块被加载时，只会导入模块的默认导出，而不是导入整个模块对象。
const metaRouters: any = import.meta.glob("./modules/*.tsx", {
  eager: true,
  import: "default",
});
```

## require

#### require() 方法

> 1.  require() 方法用于加载模块，返回一个对象，这个对象代表的是模块的引用。require() 方法接受以下参数。
> 2.  id 参数是要加载的模块的 ID，它必须是字符串，不能是表达式。require() 方法用于加载模块，返回一个对象，这个对象代表的是模块的引用。require() 方法接受以下参数。
> 3.  只能在 node 环境下使用

```js
require(id);
```

## class

#### 基本使用

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  say() {
    console.log(`我叫${this.name},今年${this.age}岁`);
  }
}

const person = new Person("panrui", 18);

person.say(); // 我叫panrui,今年18岁
```

#### 继承

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  say() {
    console.log(`我叫${this.name},今年${this.age}岁`);
  }
}

class Student extends Person {
  constructor(name, age, school) {
    super(name, age);
    this.school = school;
  }

  say() {
    console.log(`我叫${this.name},今年${this.age}岁,就读于${this.school}`);
  }
}

const student = new Student("panrui", 18, "清华大学");

student.say(); // 我叫panrui,今年18岁,就读于清华大学
```

## async await 使用

最后更新时间：2024-4-28 16:20:25
