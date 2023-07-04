<!--
 * @Description: node 开发cli工具
 * @Author: panrui
 * @Date: 2021-06-21 14:42:47
 * @LastEditTime: 2021-10-19 16:18:23
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 开发

#### 开发文档

##### 1. 项目安装

```
1. git clone git@gitee.com:wesweet/mujoy-ow-cli.git (下载项目)
2. npm i (更新依赖)
```

#### 工程结构

```js
├── bin                       # 命令目录
│   ├── mjow.js               # 入口命令
│   ├── create.js             # 创建项目命令
│   ├── addtpl.js             # 新增模板命令
│   ├── deletetpl.js          # 删除模板命令
│   ├── listpl.js             # 展示模板命令
├── lib                       # 工具模块
│   ├── download.js           # 模板下载模块
│   ├── install.js            # 第三库依赖安装模块
│   ├── generator.js          # 模板插入模块快
│   ├── template.json         # 模板配置模块
├── package.json              # 模块文件
```

#### 测试

1. npm unlink (移除软连接)
2. npm link (添加软连接测试)
3. mjow command <options> (测试不同命令)

#### 更新发布

1. 修改版本号
2. npm login
3. npm publish

#### 参考文档

[从 0 构建自己的脚手架/CLI 知识体系](https://juejin.cn/post/6966119324478079007#heading-0)

[Commander 命令编写库](https://github.com/tj/commander.js/blob/master/Readme_zh-CN.md#%e5%91%bd%e4%bb%a4)

[download-git-repo 下载远程模板](https://gitlab.com/flippidippi/download-git-repo)

[inquirer 交互式处理库](https://github.com/SBoudrias/Inquirer.js)

[glob 规则匹配文件库](https://github.com/isaacs/node-glob)

[ejs 模板应用库](https://github.com/mde/ejs)

[chalk log 染色库](https://github.com/chalk/chalk)

[fs-extra fs 扩展库](https://github.com/jprichardson/node-fs-extra)

[ora 优雅的终端转轮](https://github.com/sindresorhus/ora)

[semver 语义规范版本库](https://github.com/npm/node-semver)

[minimist](https://github.com/substack/minimist)

[validate-npm-package-name 校验名称合法性](https://github.com/npm/validate-npm-package-name)

[cross-spawn spawn 命令扩展库](https://github.com/moxystudio/node-cross-spawn)

## 使用

#### 使用文档

##### 1. nvm 安装

```
注释：nvm和node安装路径尽量不要出现中文和空格
nvm-noinstall.zip：绿色免安装版，但使用时需进行配置。
nvm-setup.zip：安装版，推荐使用
```

##### 2. 安装确认，打开 cmd，输入命令 nvm，安装成功则如下显示

![nvm](http://work.panrui.top:8083/static/images/nvm.png)

##### 3. 安装/管理 node 版本

```
1、查看本地安装的所有版本；有可选参数available，显示所有可下载的版本
nvm list [available]
```

```
2、安装，命令中的版本号可自定义，具体参考命令1查询出来的列表
nvm install 11.13.0
```

```
3、查看node版本
打开cmd，输入命令 node -v,成功安装如下显示
```

![node-v](http://work.panrui.top:8083/static/images/node-v.png)

```
4、使用特定版本/切换不同版本
nvm use 14.16.1
```

##### 4. 安装脚手架

```
npm i mujoy-ow-cli -g
```

如果 npm 安装速度较慢，可替换城 cnpm(淘宝镜像)

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm i mujoy-ow-cli -g
```

##### 5. 脚手架安装确认，安装成功以后，打开命令行 cmd，输入 mjow 成功则如下显示

![mjow](http://work.panrui.top:8083/static/images/mjow.png)

##### 6. 项目创建

```
mjow create app-name
```

![mjow-create](http://work.panrui.top:8083/static/images/mjow-create.png)

##### 7. 命令参数

> 创建项目 mjow create app-name

> 新增模板 mjow addtpl tpl-name

> 删除模板 mjow deletetpl

> 展示模板 mjow listpl

> 命令帮助 mjow -h
