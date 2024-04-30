<!--
 * @Description:
 * @Author: prui
 * @Date: 2023-11-14 10:39:50
 * @LastEditTime: 2024-04-29 15:26:34
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## process

- [文档](http://nodejs.cn/api/process.html)

```js
const process = require("process");

process.cwd(); // 返回当前Node进程执行的目录

process.argv; // 返回终端通过Node执行命令时候 传入的命令行参数，返回值是一个数组 0：Node路径 1：被执行的JS文件路径 2~n：真实参数
const args = process.argv.slice(2);

process.env; // 返回一个存储当前环境相关的所有信息

process.platform; // 返回当前系统信息

// process.chdir() 方法更改 Node.js 进程的当前工作目录
```

## Path

```js
const path = require("path");
// path.basename 返回提供的 path 的最后一部分 参数 path:<string> ext:<string>
path.basename("/foo/bar/baz/asdf/quux.html");

// 返回: 'quux.html'
path.basename("/foo/bar/baz/asdf/quux.html", ".html");
// 返回: 'quux'

// path.join 使用特定于平台的分隔符作为界定符将所有给定的path片段连接在一起，然后规范化生成的路径
path.join("/foo", "bar", "baz/asdf", "quux", "..");
// 返回: '/foo/bar/baz/asdf'

// path.resolve 将路径或路径片段的序列解析为绝对路径 给定的路径序列从右到左处理 每个后续的 path 会被追加到前面，直到构建绝对路径 生成的路径被规范化，并删除尾部斜杠（除非路径解析为根目录）
path.resolve("/foo/bar", "./baz");
// 返回: '/foo/bar/baz'

path.resolve("/foo/bar", "/tmp/file/");
// 返回: '/tmp/file'

path.resolve("wwwroot", "static_files/png/", "../gif/image.gif");
// 如果当前工作目录是 /home/myself/node，
// 则返回 '/home/myself/node/wwwroot/static_files/gif/image.gif'

// 当前文件所在的目录位置
__dirname;

// 当前文件的位置
__filename;

// 获取当前package.json文件路径
const pkgPath = path.join(process.cwd(), "./package.json");
// 输出: /Users/xiaolian/Code/node-api-test/package.json
```

## fs

#### fs.existsSync(path)

判断文件是否存在,如果路径存在，则返回 true，否则返回 false,fs.existsSync() 不使用回调函数，直接返回布尔值。

```js
const fs = require("fs");
const path = require("path");
const filePath = path.resolve(__dirname, "test.txt");
const isExist = fs.existsSync(filePath);
console.log(isExist); // true
```

#### fs.statSync(path[, options])

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

#### fs.readFileSync(path[, options])

同步读取文件内容,返回值为 Buffer 对象,如果指定了 encoding，则返回字符串，否则返回 buffer。

```js
const fs = require("fs");
const path = require("path");
const filePath = path.resolve(__dirname, "test.txt");
const data = fs.readFileSync(filePath, "utf-8");
```

#### fs.writeFileSync(file, data[, options])

同步写入文件内容,如果文件不存在，则创建文件，如果文件存在，则覆盖文件内容。

```js
const fs = require("fs");
const path = require("path");
const filePath = path.resolve(__dirname, "test.txt");
fs.writeFileSync(filePath, "hello world");
```

最后更新时间：2024-4-30 09:56:59
