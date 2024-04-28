<!--
 * @Description: 记录文档
 * @Author: prui
 * @Date: 2024-04-28 14:11:31
 * @LastEditTime: 2024-04-28 14:14:45
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(`2024-4-28 14:15:20`)

## switch

- 使用严格运算符 === 进行判断
- 多个 case 与提供的值匹配，则选择匹配的第一个 case
- break 确保程序立即从相关的 case 子句中跳出 switch，并接着执行 switch 之后的语句，若 break 被省略，程序会继续执行 switch 语句中的下一条语句。
- 默认情况下，整个 switch 为一个块级作用域

```js
// 基于第三点产生骚操作
// 多case - 单一操作
var Animal = "Giraffe";
switch (Animal) {
  case "Cow":
  case "Giraffe":
  case "Dog":
  case "Pig":
    console.log("This animal will go on Noah's Ark.");
    break;
  case "Dinosaur":
  default:
    console.log("This animal will not.");
}
// 多case - 关联操作 (应用范围属实有点难匹配)
var foo = 1;
var output = "Output: ";
switch (foo) {
  case 0:
    output += "So ";
  case 1:
    output += "What ";
    output += "Is ";
  case 2:
    output += "Your ";
  case 3:
    output += "Name";
  case 4:
    output += "?";
    console.log(output);
    break;
  case 5:
    output += "!";
    console.log(output);
    break;
  default:
    console.log("Please pick a number from 0 to 5!");
}
```

```js
// 基于第四点作用域解释
// 第一种解决方式 (使用括号包裹) // Unexpected lexical declaration in case block 不知道这个错误还会不会提示，因为 ECMAScript 规定，在 switch 语句的 case 或 default 子句内部不允许直接声明变量。TODO待验证....
const action = "say_hello";
switch (action) {
  case "say_hello": {
    // added brackets
    let message = "hello";
    console.log(message);
    break;
  } // added brackets
  case "say_hi": {
    // added brackets
    let message = "hi";
    console.log(message);
    break;
  } // added brackets
  default: {
    // added brackets
    console.log("Empty action received.");
    break;
  } // added brackets
}
```
