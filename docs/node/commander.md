<!--
 * @Description: 指令与处理命令行库
 * @Author: panrui
 * @Date: 2021-09-29 10:00:29
 * @LastEditTime: 2021-09-29 16:39:41
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 安装

> npm install commander

## 使用

#### 声明 program 变量

```js
const { program } = require("commander");
```

#### 选项

```js
// 定义选项
// 使用.option()方法来定义选项，同时可以附加选项的简介
// 每个选项可以定义一个短选项名称（-后面接单个字符）和一个长选项名称（--后面接一个或多个单词），使用逗号、空格或|分隔
program
  .option("-d, --debug", "output extra debugging")
  .option("-s, --small", "small pizza size")
  // 最常用的选项，一类是 boolean 型选项，选项无需配置参数
  // 另一类选项则可以设置参数使用尖括号声明在该选项后
  .option("-p, --pizza-type <type>", "flavour of pizza");

program.parse(process.argv);

// 获取选项
const options = program.opts();
if (options.debug) console.log(options);

// 设置选项默认值
program.option(
  "-c, --cheese <type>",
  "add the specified type of cheese",
  "blue"
);
program.parse();
console.log(`cheese: ${program.opts().cheese}`);
```

#### 版本选项

```js
// 定义版本 支持链式操作
program.version(require("../package").version);
```

#### 命令

```js
// 通过.command()或.addCommand()可以配置命令，有两种实现方式：为命令绑定处理函数，或者将命令单独写成一个可执行文件（详述见后文）
// 通过绑定处理函数实现命令（这里的指令描述为放在`.command`中）
// 返回新生成的命令（即该子命令）以供继续配置
program
  .command("clone <source> [destination]")
  .description("clone a repository into a newly created directory")
  .action((source, destination) => {
    console.log("clone command called");
  });

// 通过独立的的可执行文件实现命令 (注意这里指令描述是作为`.command`的第二个参数)
// 返回最顶层的命令以供继续添加子命令
program
  .command("start <service>", "start named service")
  .command("stop [service]", "stop named service, or all if no name supplied");

// 分别装配命令
// 返回最顶层的命令以供继续添加子命令
program.addCommand(build.makeBuildCommand());
```

#### 命令参数

```js

```

#### .usage 和 .name

!> 修改帮助信息的首行提示 name 属性也可以从参数中推导出来
