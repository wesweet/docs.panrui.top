<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-06-12 13:23:59
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2021-06-12 13-23-59

## 文档

- [node-mysql](https://github.com/mysqljs/mysql#introduction)

```js
npm install mysql -S
```

## 基础使用

```js
const mysql = require("mysql");

// 配置数据库基本信息
const option = {
  host: "数据库地址",
  user: "账号",
  password: "密码",
  port: "端口",
  timezone: "08:00",
  multipleStatements: true,
};

// 根据环境构建需要使用的数据库
const db = Object.assign(
  {},
  process.env.NODE_ENV === "development"
    ? { database: "开发数据库" }
    : {
        database: "线上数据库",
      },
  option
);

// 使用连接池配置数据库连接
const pool = mysql.createPool(db);
pool.getConnection(async (err, connection) => {
  if (err) {
    // 连接数据库错误
    return;
  }
  try {
    // TODO 业务逻辑
  } catch (error) {
  } finally {
    // 释放数据库连接
    connection.release();
  }
});
```

## 完整配置

```js
const option = {
  host: '数据库的主机名', // The hostname of the database you are connecting to. (Default: localhost)
  port: '连接的端口号', // The port number to connect to. (Default: 3306)
  localAddress: '用于 TCP 连接的源 IP 地址', // The source IP address to use for TCP connection. (Optional)
  socketPath: '连接到 Unix 域套接字的路径' // The path to a unix domain socket to connect to. When used host and port are ignored.
  user: '账号', // The MySQL user to authenticate as.
  password: '密码', // The password of that MySQL user.
  database: '用于连接的数据库名称', // Name of the database to use for this connection (Optional).
  charset: '连接的字符集', // The charset for the connection. This is called "collation" in the SQL-level of MySQL (like utf8_general_ci). If a SQL-level charset is specified (like utf8mb4) then the default collation for that charset is used. (Default: 'UTF8_GENERAL_CI')
  timezone: '存储本地日期所使用的时区', // The timezone used to store local dates. (Default: 'local')
  connectTimeout: '超时', // The milliseconds before a timeout occurs during the initial connection to the MySQL server. (Default: 10000)
  stringifyObjects: '将对象串行化，而不是转换为值', // Stringify objects instead of converting to values. See issue #501. (Default: 'false')
  insecureAuth: '允许连接到要求旧（不安全）身份验证方式的 MySQL 实例', // Allow connecting to MySQL instances that ask for the old (insecure) authentication method. (Default: false)
  typeCast: '确定是否将列值转换为本机 JavaScript 类型', // Determines if column values should be converted to native JavaScript types. (Default: true)
  queryFormat: function (query, values) {
    // A custom query format function. See `Custom format`.
  },
  supportBigNumbers: '当处理数据库中的大数值（BIGINT 和 DECIMAL 列）时，应该启用此选项', // When dealing with big numbers (BIGINT and DECIMAL columns) in the database, you should enable this option (Default: false).
  bigNumberStrings: '启用 supportBigNumbers 和 bigNumberStrings 会强制将大数字（BIGINT 和 DECIMAL 列）始终作为 JavaScript 字符串对象返回', // Enabling both supportBigNumbers and bigNumberStrings forces big numbers (BIGINT and DECIMAL columns) to be always returned as JavaScript String objects (Default: false). Enabling supportBigNumbers but leaving bigNumberStrings disabled will return big numbers as String objects only when they cannot be accurately represented with JavaScript Number objects (which happens when they exceed the [-2^53, +2^53] range), otherwise they will be returned as Number objects. This option is ignored if supportBigNumbers is disabled.
  dateStrings: '强制日期类型（时间戳，日期时间，日期）返回为字符串', // Force date types (TIMESTAMP, DATETIME, DATE) to be returned as strings rather then inflated into JavaScript Date objects. Can be true/false or an array of type names to keep as strings. (Default: false)
  debug: '将协议细节打印到标准输出', // Prints protocol details to stdout. Can be true/false or an array of packet type names that should be printed. (Default: false)
  trace: '在错误时生成堆栈跟踪以包括库入口的调用站点（「长堆栈跟踪」）', // Generates stack traces on Error to include call site of library entrance ("long stack traces"). Slight performance penalty for most calls. (Default: true)
  multipleStatements: '允许在单个查询中使用多个 MySQL 语句', // Allow multiple mysql statements per query. Be careful with this, it exposes you to SQL injection attacks. (Default: false)
  flags: '', // List of connection flags to use other than the default ones. It is also possible to blacklist default ones. For more information, check Connection Flags.
  ssl: { // object with ssl parameters or a string containing name of ssl profile
    ca: '', // The path to the CA certificate
    cert: '', // The path to the client certificate
    key: '', // The path to the client key
    passphrase: '', // A passphrase for the client key
    rejectUnauthorized: false, // Reject unauthorized connection attempts or not (Default: true)
  },
};
```

## 提交事务

## API 使用

#### end 和 release 的区别

```
1. `end` 方法：
   - 用于关闭数据库连接池。
   - 调用 `end` 方法将关闭数据库连接池，并确保所有连接都被释放。
   - 适用于在应用程序结束时关闭数据库连接池，或者在不再需要连接时进行释放。
   - 一旦调用了 `end` 方法，就不能再使用该数据库连接池进行数据库操作。

2. `release` 方法：
   - 用于释放单个数据库连接到连接池。
   - 调用 `release` 方法将释放单个数据库连接，使其可供其他请求使用。
   - 适用于在单个请求处理完成后释放连接，以便将连接返回到连接池中以供其他请求使用。
   - 可以多次调用 `release` 方法，每次释放一个连接。
```

## 问题记录

#### 1. 数据库存放时间字段为 date 类型，存放的数据未 2013-09-01 但是取出来的数据为 2013-08-31T16:00:00.000Z

原因在于数据库存储的时间为 UTC 时间，而取出来的时间为本地时间，所以会有 8 小时的时差，解决办法如下：

```js
// 添加timezone时区配置
const option = {
  host: "数据库地址",
  user: "账号",
  password: "密码",
  port: "端口",
  timezone: "08:00",
};
```

#### 2. 定义多个语句同时执行时，需要开启 multipleStatements 配置

```js
const option = {
  host: "数据库地址",
  user: "账号",
  password: "密码",
  port: "端口",
  timezone: "08:00",
  multipleStatements: true,
};
```
