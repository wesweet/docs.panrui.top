<!--
 * @Description:
 * @Author: panrui
 * @Date: 2022-12-07 16:24:11
 * @LastEditTime: 2022-12-07 16:29:31
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->
  
## Path 模块

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
