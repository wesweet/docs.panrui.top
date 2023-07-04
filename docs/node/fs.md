<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-06-07 09:41:23
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-06-06 15-42-25

## fs.existsSync(path)

判断文件是否存在,如果路径存在，则返回 true，否则返回 false,fs.existsSync() 不使用回调函数，直接返回布尔值。

```js
const fs = require("fs");
const path = require("path");
const filePath = path.resolve(__dirname, "test.txt");
const isExist = fs.existsSync(filePath);
console.log(isExist); // true
```

## fs.statSync(path[, options])

同步读取文件信息,返回值为 fs.Stats 对象,如果文件不存在，则抛出异常。

```js
const fs = require("fs");
const path = require("path");
const filePath = path.resolve(__dirname, "test.txt");
const stats = fs.statSync(filePath);
console.log(stats.isFile()); // true
```

> 1.  fs.stat() 和 fs.existsSync() 还有一个主要区别。fs.stat() 提供了有关文件的更多信息，而 fs.existsSync() 只是简单地检查文件是否存在
> 2.  fs.stat() 的回调函数的第二个参数是一个 stats 对象，它包含有关文件的详细信息，例如文件大小、创建时间和修改时间等。这些信息可以用来执行更复杂的操作，例如检查文件是否过期或确定文件是否需要更新。

## fs.readFileSync(path[, options])

同步读取文件内容,返回值为 Buffer 对象,如果指定了 encoding，则返回字符串，否则返回 buffer。

```js
const fs = require("fs");
const path = require("path");
const filePath = path.resolve(__dirname, "test.txt");
const data = fs.readFileSync(filePath, "utf-8");
```

## fs.writeFileSync(file, data[, options])

同步写入文件内容,如果文件不存在，则创建文件，如果文件存在，则覆盖文件内容。

```js
const fs = require("fs");
const path = require("path");
const filePath = path.resolve(__dirname, "test.txt");
fs.writeFileSync(filePath, "hello world");
```
