<!--
 * @Description: 数据库操作
 * @Author: panrui
 * @Date: 2022-01-04 17:54:54
 * @LastEditTime: 2022-01-04 18:18:39
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 表字段设计

```SQL
CREATE TABLE `TABLENAME` {
  `id` int(10) NOT NULL AUTO_INCREMENT COMMENT '表主键自增长不为空',
  `title` varchar(200) NOT NULL COMMENT '非空字符串字段',
  `remark` varchar(500) DEFAULT NULL COMMENT '可以为空的字符串字段',
  `create_time` int(10) NOT NULL DEFAULT '0' COMMENT '添加时间',
	`update_time` int(10) NOT NULL DEFAULT '0' COMMENT '更新时间',
  `type` tinyint(1) NOT NULL DEFAULT '0' COMMENT '状态字段',
  PRIMARY KEY (`id`) USING BTREE
} ENGINE=InnoDB AUTO_INCREMENT=60 DEFAULT CHARSET=utf8 ROW_FORMAT=COMPACT COMMENT='表介绍'
```

## 数据库语句操作

#### 基础查询

```JS
// 第一个参数是一个原生 SQL 查询语句 第二个参数则是需要绑定到查询中的参数值 用于约束 where 语句 返回一个包含查询结果的数组
$results = DB::select('select * from users where id = :id', ['id' => 1]);

DB::insert('insert into users (id, name) values (?, ?)', [1, 'Marc']);

$affected = DB::update('update users set votes = 100 where name = ?',['Anita']);// 返回受到本次操作影响的记录行数

$deleted = DB::delete('delete from users');// 返回受到本次操作影响的记录行数


// 以下在事务中使用时，务必注意会导致隐式提交的语句
// 没有返回值的查询
DB::statement('drop table users');
// 没有参数的更新
DB::unprepared('update users set votes = 100 where name = "Dries"');
```

#### 查询构造器

```JS
// table 方法为给定的表返回一个查询构造器实例 最后使用 get 方法获取结果

//获取单行
$user = DB::table('users')->where('name', 'John')->first();

// 获取指定值
$email = DB::table('users')->where('name', 'John')->value('email');

//通过ID获取一行数据
$user = DB::table('users')->find(3);

// 获取一列的值
$titles = DB::table('users')->pluck('title');
$titles = DB::table('users')->pluck('title', 'name');

// 分块处理大量数据 return false来停止处理其他块
DB::table('users')->orderBy('id')->chunk(100, function ($users) {
    foreach ($users as $user) {
        //
    }
});

// 聚合
count，max，min，avg，还有 sum

// 判断记录是否存在
exists 和 doesntExist
```

#### Select说明
```JS
// 查询
$users = DB::table('users')->select('name', 'email as user_email')->get();

// 去重
$users = DB::table('users')->distinct()->get();

// 使用原生表达式
DB::raw('count(*) as user_count, status') // 可能产生SQL注入漏洞  使用selectRaw代替 whereRaw orWhereRaw...
```

#### Join
```JS
// 内连接
```
