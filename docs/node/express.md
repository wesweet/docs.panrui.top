<!--
 * @Description: express 文档
 * @Author: panrui
 * @Date: 2021-06-24 09:59:43
 * @LastEditTime: 2023-07-26 13:37:21
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-07-26 13-37-21

## 文档

- [express](http://expressjs.com/)
- [中文文档](http://www.expressjs.com.cn/4x/api.html#express)
- [7189074.html](https://www.cnblogs.com/xiaohuochai/p/7189074.html)

```js
npm i express -S
```

## 后端接口规范

```js
export interface response {
  success: boolean; // if request is success
  data?: any; // response data
  errorCode?: string; // code for errorType
  errorMessage?: string; // message display to user
  showType?: number; // error display type： 0 silent; 1 message.warn; 2 message.error; 4 notification; 9 page
  traceId?: string; // Convenient for back-end Troubleshooting: unique request ID
  host?: string; // onvenient for backend Troubleshooting: host of current access server
}

// data 内数据格式规范 以分页作为例子
{
   list: [
   ],
   current?: number,
   pageSize?: number,
   total?: number,
}

// 异常错误代码
200: '服务器成功返回请求的数据。',
201: '新建或修改数据成功。',
202: '一个请求已经进入后台排队（异步任务）。',
204: '删除数据成功。',
400: '发出的请求有错误，服务器没有进行新建或修改数据的操作。',
401: '用户没有权限（令牌、用户名、密码错误）。',
403: '用户得到授权，但是访问是被禁止的。',
404: '发出的请求针对的是不存在的记录，服务器没有进行操作。',
405: '请求方法不被允许。',
406: '请求的格式不可得。',
410: '请求的资源被永久删除，且不会再得到的。',
422: '当创建一个对象时，发生一个验证错误。',
500: '服务器发生错误，请检查服务器。',
502: '网关错误。',
503: '服务不可用，服务器暂时过载或维护。',
504: '网关超时。',
```

## 中间件

- Express的中间件，本质上就是一个function处理函数，函数的形参列表中，必须包含next参数，而路由处理函数中只包含req和res。next函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

<!-- ## 配置 -->

<!-- ## 学习文档 -->

<!-- 1:use是express注册中间件的方法,它返回一个函数
2:use方法允许将请求的网址写在第一个参数,只有请求匹配,后面的中间件才会生效
3:app.use(express.static('public'));//将静态资源文件所在的目录作为参数传递给 express.static 中间件就可以提供静态资源文件的访问了
4:常用中间件
    {
        cookie-parser():用于解析cookie的中间件，添加中间后，req具备cookies属性。通过req.cookies.xxx可以访问cookie的值
            使用方法：var cookieParser = require('cookie-parser');app.use(cookieParser(secret, options))
        express-session:session运行在服务器端，当客户端第一次访问服务器时，可以将客户的登录信息保存
            使用方法:var session = require('express-session');app.use(session(options))
        serve-favicon:设置网站的 favicon图标
            使用方法:var favicon = require('serve-favicon');var path = require('path');app.use(favicon(path.join(__dirname, 'public', 'favicon.ico')))
        body-parser:bodyParser用于解析客户端请求的body中的内容，内部使用JSON编码处理，url编码处理以及对于文件的上传处理
            使用方法:var bodyParser = require('body-parser')
            {
                底层中间件用法：这将拦截和解析所有的请求；也即这种用法是全局的
                    app.use(bodyParser.urlencoded({ extended: false }));app.use(bodyParser.json())
                    use方法调用body-parser实例；且use方法没有设置路由路径；这样的body-parser实例就会对该app所有的请求进行拦截和解析
                特定路由下的中间件用法:对于特定的路径使用
                    var urlencodedParser = bodyParser.urlencoded({ extended: false })
                    app.post('/login', urlencodedParser, function (req, res) {
                        if (!req.body) return res.sendStatus(400)
                        res.send('welcome, ' + req.body.username)
                    })

                    var jsonParser = bodyParser.json();
                    // POST /api/users gets JSON bodies
                    app.post('/api/users', jsonParser, function (req, res) {
                        if (!req.body) return res.sendStatus(400)
                        // create user in req.body
                    })
            }
    }
5:路由方法--针对不同的接口,Express提供了use方法的一些别名,这些别名是和http对应的路由方法
    路由路径
        {
            字符串匹配:app.get('/about',function(){}),
            字符串模式匹配:app.get('/ab?cd',function(){}),
            正则表达式匹配:app.get(/a/,function(){})
        }
    路由句柄
        {
            可以是单个函数,也可以是函数数组,或者多个函数,或者函数+函数数组
        }
    链式路由句柄
        {
            app.router('/block')
                .get(function(){})
                .post(function(){})
                .put(function(){})
        }
    {

    }
    app.all():他的作用的对于一个路径上的所有请求加载中间件
-------------------------------------------------------------------------------------------------------------------------------------------
express()
    express()是express模块导出的顶层方法
    {
        Methods:{
            express.static(root, [options]) //express.static是Express中唯一的内建中间件,负责托管 Express 应用内的静态资源
        }

    }
-------------------------------------------------------------------------------------------------------------------------------------------
Application()
    app对象一般用来表示Express程序。通过调用Express模块导出的顶层的express()方法来创建它
    var express = require('express');
    var app = express();
    {
        路由:{
            app.METHOD：路由一个HTTP请求,METHOD是这个请求的HTTP方法 使用方法：app.METHOD(path, callback [, callback ...])
            app.param:给路由参数添加回调触发器，这里的name是参数名或者参数数组，function是回调方法
        },
        配置中间件:app.route
        渲染html视图:app.render
        注册模板引擎:app.engine
    }
-------------------------------------------------------------------------------------------------------------------------------------------
Properties
    app.locals对象是一个javascript对象，它的属性就是程序本地的变量
    app.locals.title
    //一旦设定,app.locals的各属性值将贯穿程序的整个生命周期
    //与其相反的是 res.locals,它只在这次请求的生命周期中有效
-------------------------------------------------------------------------------------------------------------------------------------------
Events
    app.on('mount', callback(parent))
-------------------------------------------------------------------------------------------------------------------------------------------
Methods
    {
        app.all(path, callback[, callback ...]:
        app.delete(path, callback[, callback ...])
        app.disable(name)
        app.disabled(name)
        app.enable(name)
        app.enabled(name)
        app.engine(ext, callback)
        app.get(name)
        app.get(path, callback [, callback ...])
        app.listen(port, [hostname], [backlog], [callback])
        app.METHOD(path, callback [, callback ...]){
            路由一个HTTP请求,METHOD是这个请求的HTTP方法

        }
        app.param([name], callback)
        app.path()
        app.post(path, callback, [callback ...])
        app.put(path, callback, [callback ...])
        app.render(view, [locals], callback)
        app.route(path)
        app.set(name, value)
    }
-------------------------------------------------------------------------------------------------------------------------------------------
Application Settings
-------------------------------------------------------------------------------------------------------------------------------------------
Request
-------------------------------------------------------------------------------------------------------------------------------------------
Properties
-------------------------------------------------------------------------------------------------------------------------------------------
Methods

-------------------------------------------------------------------------------------------------------------------------------------------
Response
-------------------------------------------------------------------------------------------------------------------------------------------
Properties
-------------------------------------------------------------------------------------------------------------------------------------------
Methods
-------------------------------------------------------------------------------------------------------------------------------------------
Router
-------------------------------------------------------------------------------------------------------------------------------------------
Methods
------------------------------------------------------------------------------------------------------------------------------------------- -->

<!-- ## 开始使用

```js
// 设置状态码并返回数据
res.status(403).send("Sorry! You can't see that.");
``` -->

<!-- TODO 待删除 -->

<!-- #### 待学习 -->
<!--
- [ ] 消息队列
- [ ] 高并发
- [ ] 应用重启 -->

<!-- #### 学习文档 -->

<!-- 1:events模块存在一个EventEmitter对象,通过实例化EventEmitter来绑定和监听事件
2:fs是文件模块,fs(stream)可以创建四种不同的流类型,然后所有的流对象又都是EventEmitter的实例(也就是说他们拥有绑定和监听事件的功能),同时默认绑定了(data,end,error,finish)

------------------------------------------------------------删除-------------------------------------------------------------------------------
events模块
EventEmitter
1:实例化EventEmitter来绑定和监听事件(绑定事件--帮助这个事件注册一个监听器)
    实例化 var eventEmitter = new events.EventEmitter();
    绑定 eventEmitter.on('eventName', eventHandler);
    执行异步操作的函数都是将回调函数作为最后一个参数,回调函数接受错误对象作为第一个参数

2:EventEmitter 的核心就是事件触发与事件监听器功能的封装
    触发 eventEmitter.emit('eventName');
    {
        addListener(event, listener):为指定事件添加一个监听器到监听器数组的尾部
        on(event, listener):为指定事件注册一个监听器，接受一个字符串 event 和一个回调函数
        once(event, listener):为指定事件注册一个单次监听器，即 监听器最多只会触发一次，触发后立刻解除该监听器
        removeListener(event, listener):移除指定事件的某个监听器，监听器必须是该事件已经注册过的监听器
        removeAllListeners([event]):移除所有事件的所有监听器， 如果指定事件，则移除指定事件的所有监听器
        setMaxListeners(n):默认最多十个,提高默认监听器的数量
        listeners(event):返回指定事件的监听器数组 //数组的每一项都是监听函数
        emit(event, [arg1], [arg2], [...]):按参数的顺序执行每个监听器，如果事件有注册监听返回 true，否则返回 false
        listenerCount:返回监听器的数量 Number类型
    }
    //newListener 当添加新的监听器时触发
    //removeListener 当监听器被移除时触发
3:error事件
    当 error 被触发时，EventEmitter 规定如果没有响 应的监听器，Node.js 会把它当作异常
    我们一般要为会触发 error 事件的对象设置监听器

-----------------------------------------------------------删除--------------------------------------------------------------------------------
Buffer
    创建Buffer类//一个 Buffer 类似于一个整数数组,所以他有很多和数据相似的API
    {
        Buffer()
        Buffer.alloc(size[, fill[, encoding]])： 返回一个指定大小的 Buffer 实例，如果没有设置 fill，则默认填满 0
        Buffer.allocUnsafe(size)： 返回一个指定大小的 Buffer 实例，但是它不会被初始化，所以它可能包含敏感的数据
        Buffer.allocUnsafeSlow(size)
        Buffer.from(array)： 返回一个被 array 的值初始化的新的 Buffer 实例（传入的 array 的元素只能是数字，不然就会自动被 0 覆盖）
        Buffer.from(arrayBuffer[, byteOffset[, length]])： 返回一个新建的与给定的 ArrayBuffer 共享同一内存的 Buffer。
        Buffer.from(buffer)： 复制传入的 Buffer 实例的数据，并返回一个新的 Buffer 实例
        Buffer.from(string[, encoding])： 返回一个被 string 的值初始化的新的 Buffer 实例
    }
    写入缓冲区
    buf.write(string[, offset[, length]][, encoding]) //返回实际写入的大小。如果 buffer 空间不足， 则只会写入部分字符串。
    {
        string - 写入缓冲区的字符串。
        offset - 缓冲区开始写入的索引值，默认为 0 。
        length - 写入的字节数，默认为 buffer.length
        encoding - 使用的编码。默认为 'utf8' 。
    }
    从缓冲区读取数据
    buf.toString([encoding[, start[, end]]]) //解码缓冲区数据并使用指定的编码返回字符串
    {
        encoding - 使用的编码。默认为 'utf8' 。
        start - 指定开始读取的索引位置，默认为 0。
        end - 结束位置，默认为缓冲区的末尾。
    }
    将Buffer转换为JSON对象
    buf.toJSON()
    缓冲区合并
    Buffer.concat(list[, totalLength])
    {
        list - 用于合并的 Buffer 对象数组列表。
        totalLength - 指定合并后Buffer对象的总长度。
    }
    缓冲区比较
    buf.compare(otherBuffer);
    {
        otherBuffer - 与 buf 对象比较的另外一个 Buffer 对象
    }
    拷贝缓冲区
    buf.copy(targetBuffer[, targetStart[, sourceStart[, sourceEnd]]])
    {
        targetBuffer - 要拷贝的 Buffer 对象。
        targetStart - 数字, 可选, 默认: 0
        sourceStart - 数字, 可选, 默认: 0
        sourceEnd - 数字, 可选, 默认: buffer.length
    }
    缓冲区裁剪
    buf.slice([start[, end]])
    {
        start - 数字, 可选, 默认: 0
        end - 数字, 可选, 默认: buffer.length
    }
    缓冲区长度
    buf.length;

-------------------------------------------------------------------------------------------------------------------------------------------
写入流
管道流
链式流
-------------------------------------------------------------------------------------------------------------------------------------------
模块系统
-------------------------------------------------------------------------------------------------------------------------------------------
函数
-------------------------------------------------------------------------------------------------------------------------------------------
路由
-------------------------------------------------------------------------------------------------------------------------------------------
全局对象
-------------------------------------------------------------------------------------------------------------------------------------------
常用工具
-------------------------------------------------------------------------------------------------------------------------------------------
文件系统
-------------------------------------------------------------------------------------------------------------------------------------------
GET/POST请求
-------------------------------------------------------------------------------------------------------------------------------------------
工具模块
-------------------------------------------------------------------------------------------------------------------------------------------
Web模块
-------------------------------------------------------------------------------------------------------------------------------------------
Express模块
-------------------------------------------------------------------------------------------------------------------------------------------
RESTful API
-------------------------------------------------------------------------------------------------------------------------------------------
多进程
-------------------------------------------------------------------------------------------------------------------------------------------
JXcore打包
-------------------------------------------------------------------------------------------------------------------------------------------
Mysql
-------------------------------------------------------------------------------------------------------------------------------------------
MongoDB -->
