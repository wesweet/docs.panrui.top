<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-05-30 10:10:12
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-05-30 09-41-58

## 设计原则

> 1.  原子思想：即每个 function 就做一件事；
> 2.  归纳思想：将同一类的操作，全部整合到一起；
> 3.  方便维护：可以便于后来人进行快速维护；
> 4.  方便拓展：即可以根据每个不同的项目进行不同的更改；
> 5.  通用前端设计模式：一些前端可以通用的设计模式
> 6.  注意写好注释，将注释写的具体点；

## 变量命名

> 1.  函数命名不允许使用单个字母,并且需要使用驼峰式命名法(首字母小写,其他字母大写)
> 2.  变量前后不允许使用下划线
> 3.  全局变量为大写 (UPPERCASE )
> 4.  常量 (如 PI) 为大写 (UPPERCASE )
> 5.  私有变量以\_开头

```json
前缀规范
s：表示字符串。例如：sName，sHtml；
n：表示数字。例如：nPage，nTotal；
b：表示逻辑。例如：bChecked，bHasLogin；
a：表示数组。例如：aList，aGroup；
r：表示正则表达式。例如：rDomain，rEmail；
fn：表示函数。例如：fnGetHtml，fnInit；
o：表示以上未涉及到的其他对象，例如：oButton，oDate；
g：表示全局变量，例如：gUserName，gLoginTime
```

## 定义变量

> 使用 let 与 const 定义变量

> 对于多个变量 使用多个 let 和 const 分组设置

> let 和 const 定义变量的位置放在他们使用的地方,不要在函数最顶部就开始定义,因为他们的块级作用域,不是函数作用域

> 定义对象直接 const item = {}, 不要使用 new Object();定义对象的 key 不能使用关键字

> 定义数组直接 const items = [], 不要使用 new Array()

```js
// 如果对象属性是一个方法
const atom = {
  addValue(value) {},
};

// 创建具有动态属性名称的对象时，使用计算属性
const obj = {
  [getKey("enabled")]: true,
};

// 如果对象是 key 与 value 相同使用简写
const obj = {
  lukeSkywalker,
};

// 判断对象是否存在属性
const has = Object.prototype.hasOwnProperty;
console.log(has.call(object, key));
```

## 数组

```js
// 复制数组 使用扩展运算符
const a = [1, 2, 3, 4, 5];
const b = [...a];

// 使用Array.from 将类数组转换为数组
const foo = document.querySelectorAll(".foo");
const nodes = Array.from(foo);
```

## 函数

> 使用函数声明而不是函数表达式创建函数

> 对于立即执行函数,将括号放在里面 (function (){}())

> 不允许在非函数块(if while)中声明函数,而是将函数分配给变量

> 函数参数不能命名为 arguments

> 可选参数尽量放在参数列表最后 function handleThings(name, opts = {}){}

```js
// 函数的参数使用对象形式,这样取参数的时候可以使用对象结构赋值
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}

// 尽量使用对象作为函数返回值
function processInput(input) {
  // then a miracle occurs
  return { left, right, top, bottom };
}

// 尽量不要改变函数的参数,在参数中对可选参数设置
function handleThings(opts = {}) {
  // ...
}
```

## 字符串

> 字符串值使用单引号而不是双引号

> 对于字符串尽量使用模板字符串 `${}`

## Class

## Modules

```js
// 对象的导入和导出方式
import { es6 } from "./AirbnbStyleGuide";
export default es6;
```

## 函数取名

> 获取(get) 设置(set) 增加(add) 删除(remove) 编辑(edit) 创建(create) 销毁(destory) 启动(start) 停止(stop)

> 打开(open) 关闭(close) 读取(read) 写入(write) 载入(load) 保存(save) 分离(separate) 刷新(refresh) 同步(synchronize)

> 开始(begin) 结束(end) 备份(backup) 回复(restore) 导入(import) 导出(export) 下载(download) 上传(upload)

> 分割(split) 合并(merge) 注入(inject) 提取(extract) 绑定(bind) 查看(view) 浏览(browse) 更新(update) 复原(revert)

> 修改(modify) 选取(select) 标记(mark) 复制(copy) 粘贴(paste) 撤销(undo) 重做(redo) 插入(insert) 移除(delete)

> 清理(clean) 清除(clear) 索引(index) 排序(sort) 查找(find) 搜索(search) 播放(play) 暂停(pause) 启动(launch)

> 允许(run) 编译(compile) 执行(execute) 调试(debug) 跟踪(trace) 观察(observe) 监听(listen) 构建(build) 发布(publish)

> 输入(input) 输出(output) 编码(encode) 解码(decode) 加密(encrypt) 解密(decrypt) 压缩(compress) 解压(decompress)

> 打包(pack) 解包(unpack) 解析(parse) 生成(emit) 连接(connect) 断开(disconnect) 发送(send) 接收(receive)

> 锁定(lock) 解锁(unlock) 签出(checkout) 签入(checkin) 提交(submit) 交付(commit) 推送(push) 拉取(pull)

> 展开(expand) 折叠(collapse) 完成(finish) 进入(enter) 退出(exit) 放弃(abort) 离开(quit) 废弃(obsolete)

> 废旧(depreciate) 收集(collect) 聚集(aggregate)

```json
命名规范
函数命名采用动词 ＋ 名词形式进行命名
is can has 表示返回布尔值类型函数
get 表示获取属性
set 表示设置属性
do  表示操作具体事务
isSelected();  // 返回值为bool类型
canUpdate();  // 返回值为bool类型
hasNext(); // 返回值为bool类型
getAccount();  // 返回值为一个Account 对象
getUserList();  // 返回值为一个 用户列表
setValue(); // 设置操作
changeDoctorName(); // 修改医生名称
```

## 文件命名

| 文件夹名称                              | 含义                                                                      |
| --------------------------------------- | ------------------------------------------------------------------------- |
| src,source                              | 源代码，用 src 居多                                                       |
| test                                    | 测试文件，facebook 的测试框架 jest 默认的测试文件目录就是                 |
| docs                                    | 文档                                                                      |
| lib                                     | 库文件，library 的缩写                                                    |
| dist                                    | 用来放打包编译后的文件，distribution 的缩写                               |
| build，scripts                          | 构建脚本                                                                  |
| utils，tools，helpers                   | 工具代码                                                                  |
| controllers，views，middlewares，models | MVC 对应的 models，views，controllers，还有中间件 middlewares             |
| router                                  | 路由                                                                      |
| server                                  | 用来放服务端代码                                                          |
| adapters                                | 适配器，适配器模式是一种很常用的设计模式                                  |
| legacy                                  | 一般用来放兼容历史版本或兼容旧浏览器的代码                                |
| config                                  | 配置文件                                                                  |
| benchmarks benchmarks                   | 测试，又叫基准测试或性能测试。用来测试版本的性能变化                      |
| unit，spec                              | 单元测试，一般在 test 目录下                                              |
| e2e                                     | 端对端测试，一般在 test 目录下                                            |
| assets，vendor                          | 资源，一般用来放图片或 css 文件                                           |
| css，styles                             | css 文件                                                                  |
| js                                      | javascript 文件                                                           |
| images，img                             | 图片文件                                                                  |
| fonts                                   | 字体文件                                                                  |
| pages                                   | 页面文件                                                                  |
| static                                  | 静态资源                                                                  |
| examples，demo                          | 示例                                                                      |
| component                               | 组件                                                                      |
| plugins                                 | 插件                                                                      |
| bin                                     | 命令脚本，命令行工具经常会用到                                            |
| common，public                          | 公用的文件                                                                |
| packages                                | 很多项目会打包出多个 npm 包，用来减小体积，一般会用 packages 来放不同的包 |
| misc                                    | 杂项，miscellaneous 的缩写                                                |
| core                                    | 核心文件                                                                  |
