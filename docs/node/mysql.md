<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-07-03 10:14:39
 * @LastEditTime: 2023-07-04 13:28:54
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2021-07-03 13-06-00

## 文档

## 基础使用

```sql
-- 创建表
CREATE TABLE `user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(255) NOT NULL,
  `password` varchar(255) NOT NULL,
  `email` varchar(255) NOT NULL,
  `phone` varchar(255) NOT NULL,
  `avatar` varchar(255) NOT NULL,
  `introduce` varchar(255) NOT NULL,
  `resume` varchar(255) NOT NULL,
  `create_time` datetime NOT NULL,
  `update_time` datetime NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8mb4;
```

## SELECT 子句

- 通常是按照 SELECT、FROM、WHERE、GROUP BY、HAVING、ORDER BY 的顺序排列
- SELECT 语句执行顺序：FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> DISTINCT -> ORDER BY -> LIMIT
- 通过上面的执行顺序，我们可以知道，为什么在 group by 中不能使用别名

## LIMIT 限制

```sql
-- 查询前 10 条数据
SELECT * FROM `user` LIMIT 10;

-- 查询前 10 条数据，且按照 id 降序排列
SELECT * FROM `user` ORDER BY `id` DESC LIMIT 10;

-- 查询前 10 条数据，且按照 id 降序排列，且跳过 10 条数据
SELECT * FROM `user` ORDER BY `id` DESC LIMIT 10 OFFSET 10;
```

## AS 别名

- AS 用于为列或表指定别名

```sql
-- 查询所有数据，且将 id 别名为 user_id
SELECT `id` AS `user_id` FROM `user`;

-- 查询所有数据，且将 id 别名为 user_id，且将 username 别名为 user_name
SELECT `id` AS `user_id`, `username` AS `user_name` FROM `user`;
```

## distinct 去重

- DISTINCT 关键字用于返回唯一不同的值

```sql
-- 查询所有数据
SELECT * FROM `user`;

-- 查询所有数据，且去重
SELECT DISTINCT * FROM `user`;
```

## WHERE 条件 AND OR 最好判断非空

```sql
-- 查询 id 为 1 的数据
SELECT * FROM `user` WHERE `id` = 1 AND `id` IS NOT NULL;

-- 查询 id 为 1 的数据，且 username 为 panrui
SELECT * FROM `user` WHERE `id` = 1 AND `username` = 'panrui';

-- 查询 id 为 1 的数据，或 username 为 panrui
SELECT * FROM `user` WHERE `id` = 1 OR `username` = 'panrui';

-- 查询 id 为 1 的数据，或 username 为 panrui，且 email 为 1
SELECT * FROM `user` WHERE `id` = 1 OR `username` = 'panrui' AND `email` = 1;

-- 查询 id 为 1 的数据，或 username 为 panrui，或 email 为 1
SELECT * FROM `user` WHERE `id` = 1 OR `username` = 'panrui' OR `email` = 1;
```

## 比较运算符

```sql
-- 查询 id 大于 1 的数据
SELECT * FROM `user` WHERE `id` > 1;

-- 查询 id 大于等于 1 的数据
SELECT * FROM `user` WHERE `id` >= 1;

-- 查询 id 小于 1 的数据
SELECT * FROM `user` WHERE `id` < 1;

-- 查询 id 小于等于 1 的数据
SELECT * FROM `user` WHERE `id` <= 1;

-- 查询 id 不等于 1 的数据
SELECT * FROM `user` WHERE `id` != 1;

-- 查询 id 不等于 1 的数据
SELECT * FROM `user` WHERE `id` <> 1;
```

## BETWEEN 区间

```sql
-- 查询 id 为 1 到 3 的数据
SELECT * FROM `user` WHERE `id` BETWEEN 1 AND 3;
```

## IN 包含

- IN 可以用来代替多个 OR 条件
- 将一个查询值与一组值进行比较时，IN 是一个有用的运算符

```sql
-- 查询 id 为 1 或 2 或 3 的数据
SELECT * FROM `user` WHERE `id` IN (1, 2, 3);
```

## NOT IN 不包含

```sql
-- 查询 id 不为 1 或 2 或 3 的数据
SELECT * FROM `user` WHERE `id` NOT IN (1, 2, 3);
```

## IS NULL 为空

```sql
-- 查询 id 为空的数据
SELECT * FROM `user` WHERE `id` IS NULL;
```

## IS NOT NULL 不为空

```sql
-- 查询 id 不为空的数据
SELECT * FROM `user` WHERE `id` IS NOT NULL;

-- 空字符串也会导致空置
SELECT * FROM `user` WHERE `username` IS NOT NULL AND `username` != '';
```

## LIKE 模糊查询

```sql
-- 查询 username 包含 pan 的数据
SELECT * FROM `user` WHERE `username` LIKE '%pan%';

-- 查询 username 以 pan 开头的数据
SELECT * FROM `user` WHERE `username` LIKE 'pan%';

-- 查询 username 以 pan 结尾的数据
SELECT * FROM `user` WHERE `username` LIKE '%pan';
```

## MAX MIN AVG SUM COUNT

- 求某列的最大值

```sql
-- 查询所有数据的 id 的最大值
SELECT MAX(`id`) FROM `user`;

-- 查询所有数据的 id 的最小值
SELECT MIN(`id`) FROM `user`;

-- 查询所有数据的 id 的平均值
SELECT AVG(`id`) FROM `user`;

-- 查询所有数据的 id 的和
SELECT SUM(`id`) FROM `user`;

-- 查询所有数据的 id 的数量
SELECT COUNT(`id`) FROM `user`;
```

## GROUP BY 分组

```sql
-- 查询所有数据，且按照 id 分组
SELECT * FROM `user` GROUP BY `id`;
```

## HAVING 分组条件

- HAVING 子句是 SQL 中用于筛选分组后的结果的可选子句。它在 GROUP BY 语句之后使用，用于过滤聚合后的结果，只保留满足指定条件的分组。
- HAVING 子句使用和 WHERE 子句类似的逻辑运算符（如=、<>、>、<、>=、<=、AND、OR 等）来定义条件。这些条件可以包括聚合函数，比如 COUNT、SUM、AVG 等

```sql
-- 查询所有数据，且按照 id 分组，且 id 大于 1
SELECT * FROM `user` GROUP BY `id` HAVING `id` > 1;
```

## ORDER BY 排序

```sql
-- 查询所有数据，且按照 id 降序排列
SELECT * FROM `user` ORDER BY `id` DESC;

-- 查询所有数据，且按照 id 升序排列
SELECT * FROM `user` ORDER BY `id` ASC;
```

## 左连接 LEFT JOIN ON 右连接 RIGHT JOIN ON 内连接 INNER JOIN ON 外连接 OUTER JOIN ON 自连接 SELF JOIN ON 交叉连接 CROSS JOIN ON 自然连接 NATURAL JOIN ON 连接条件

- LEFT JOIN：左连接，左表（user）的记录将会全部表示出来，而右表（user_info）只会显示符合搜索条件的记录
- RIGHT JOIN：右连接，与 LEFT JOIN 相反
- INNER JOIN：内连接，只显示两个表中符合搜索条件的记录
- OUTER JOIN：外连接，与 INNER JOIN 相反
- SELF JOIN：自连接，将表本身作为连接表
- CROSS JOIN：交叉连接，又称笛卡尔积，返回两个表的所有行，没有任何连接条件
- NATURAL JOIN：自然连接，使用相同列名进行连接

```sql
-- 查询 user 表和 user_info 表的数据，且 user 表的 id 等于 user_info 表的 id
SELECT * FROM `user` LEFT JOIN `user_info` ON `user`.`id` = `user_info`.`id`;

SELECT * FROM `user` RIGHT JOIN `user_info` ON `user`.`id` = `user_info`.`id`;

SELECT * FROM `user` INNER JOIN `user_info` ON `user`.`id` = `user_info`.`id`;

SELECT * FROM `user` OUTER JOIN `user_info` ON `user`.`id` = `user_info`.`id`;

SELECT * FROM `user` SELF JOIN `user_info` ON `user`.`id` = `user_info`.`id`;

SELECT * FROM `user` CROSS JOIN `user_info` ON `user`.`id` = `user_info`.`id`;

SELECT * FROM `user` NATURAL JOIN `user_info` ON `user`.`id` = `user_info`.`id`;
```

## UNION 联合查询 UNION ALL 联合查询 UNION DISTINCT 联合查询 UNION DISTINCTROW 联合查询 UNION ALL DISTINCT 联合查询 UNION ALL DISTINCTROW 联合查询

- UNION：联合查询，用于合并两个或多个 SELECT 语句的结果集
- UNION ALL：联合查询，与 UNION 相比，UNION ALL 不会自动去除重复行
- UNION DISTINCT：联合查询，与 UNION 相比，UNION DISTINCT 不会自动去除重复行
- UNION DISTINCTROW：联合查询，与 UNION 相比，UNION DISTINCTROW 不会自动去除重复行
- UNION ALL DISTINCT：联合查询，与 UNION 相比，UNION ALL DISTINCT 不会自动去除重复行
- UNION ALL DISTINCTROW：联合查询，与 UNION 相比，UNION ALL DISTINCTROW 不会自动去除重复行
- UNION 要求两个或多个 SELECT 语句的结果集具有相同的列数，并且对应的列具有相容的数据类型。UNION ALL 没有这个要求，允许结果集具有不同的列数和数据类型。
- UNION 和 UNION ALL 只能用于查询语句，不能用于其他类型的 SQL 语句（如 INSERT、UPDATE 等

```sql
-- 查询 username 为 panrui 的数据，或 username 为 panrui1 的数据
SELECT * FROM `user` WHERE `username` = 'panrui' UNION SELECT * FROM `user` WHERE `username` = 'panrui1';
```

## CASE WHEN THEN ELSE END

- CASE 表示条件，WHEN 表示条件成立时的返回值，ELSE 表示条件不成立时的返回值，END 表示结束

```sql
-- 查询 id 为 1 的数据，且 id 为 1 时，返回 1，id 为 2 时，返回 2，id 为 3 时，返回 3，其他情况返回 0
SELECT `id`, CASE `id` WHEN 1 THEN 1 WHEN 2 THEN 2 WHEN 3 THEN 3 ELSE 0 END AS `id` FROM `user`;
```

## year month day hour minute second

- year：返回日期的年份
- month：返回日期的月份
- day：返回日期的天数
- hour：返回日期的小时数
- minute：返回日期的分钟数
- second：返回日期的秒数

```sql
-- 查询所有数据，且返回 create_time 的年份
SELECT *, YEAR(`create_time`) AS `year` FROM `user`;

-- 查询所有数据，且返回 create_time 的月份
SELECT *, MONTH(`create_time`) AS `month` FROM `user`;

-- 查询所有数据，且返回 create_time 的天数
SELECT *, DAY(`create_time`) AS `day` FROM `user`;

-- 查询所有数据，且返回 create_time 的小时数
SELECT *, HOUR(`create_time`) AS `hour` FROM `user`;

-- 查询所有数据，且返回 create_time 的分钟数
SELECT *, MINUTE(`create_time`) AS `minute` FROM `user`;

-- 查询所有数据，且返回 create_time 的秒数
SELECT *, SECOND(`create_time`) AS `second` FROM `user`;
```

## lead date_add date_sub date_format date_diff date_part date_trunc date_parse date_format date_extract

## 细节与区别

#### distinct 与 group by 相同点和不同点

- 相同点：都可以用来消除重复行
- 不同点：group by 除了消除重复行，还可以进行分组聚合

#### != <> not in not like 区别

- != 和 <> 是等价的，都表示不等于
- not in 和 not like 是不等价的，not in 表示不在某个集合中，not like 表示不匹配某个模式

#### HAVING 与 WHERE 区别

- WHERE 在分组前进行过滤，HAVING 在分组后进行过滤
- WHERE 后不可以使用聚合函数，HAVING 后可以使用聚合函数
- WHERE 后不可以使用别名，HAVING 后可以使用别名

## 语句实习

```sql
select user_profile.university,count(question_id)/ count(distinct question_practice_detail.device_id) as avg_answer_cnt from question_practice_detail left join user_profile on question_practice_detail.device_id = user_profile.device_id where question_practice_detail.question_id <> "" group by user_profile.university;

select user_profile.university,question_detail.difficult_level,count(distinct user_profile.device_id) / count(user_profile.answer_cnt) as avg_answer_cnt from question_practice_detail left join user_profile on question_practice_detail.device_id = user_profile.device_id left join question_detail on question_practice_detail.question_id = question_detail.question_id where question_practice_detail.question_id <> "" group by user_profile.university,question_detail.difficult_level

select university, difficult_level, count(user_profile.answer_cnt) / count(distinct user_profile.device_id) as avg_answer_cnt from user_profile join question_practice_detail on user_profile.device_id = question_practice_detail.device_id join question_detail on question_practice_detail.question_id = question_detail.question_id where user_profile.university = '山东大学' and question_practice_detail.question_id <> '' group by difficult_level;

select
    device_id, gender, age, gpa
from user_profile
where university='山东大学'

union all

select
    device_id, gender, age, gpa
from user_profile
where gender='male'

select case when age is null then '25岁以下' when age < 25 then '25岁以下' when age >= 25 then '25岁及以上' end as age_cut, count(device_id) as number from user_profile group by age_cut;

select device_id, gender, case when age is null then '其他' when age < 20 then '20岁以下' when age >= 20 and age < 24 then '20-24岁' when age >= 25 then '25岁及以上' end as age_cut from user_profile;

select day(date) as day, count(question_id) as question_cnt from question_practice_detail where month(date) = 8 group by day;
```

<!--

## EXISTS 存在

```sql
-- 查询 id 为 1 的数据，且 id 为 1 的数据存在
SELECT * FROM `user` WHERE EXISTS (SELECT * FROM `user` WHERE `id` = 1);

-- 查询 id 为 1 的数据，且 id 为 1 的数据存在，且按照 id 降序排列
SELECT * FROM `user` WHERE EXISTS (SELECT * FROM `user` WHERE `id` = 1) ORDER BY `id` DESC;
```

## ANY 任意

```sql
-- 查询 id 为 1 的数据，且 id 为 1 的数据存在
SELECT * FROM `user` WHERE `id` = ANY (SELECT * FROM `user` WHERE `id` = 1);

-- 查询 id 为 1 的数据，且 id 为 1 的数据存在，且按照 id 降序排列
SELECT * FROM `user` WHERE `id` = ANY (SELECT * FROM `user` WHERE `id` = 1) ORDER BY `id` DESC;
```

## ALL 所有

```sql
-- 查询 id 为 1 的数据，且 id 为 1 的数据存在
SELECT * FROM `user` WHERE `id` = ALL (SELECT * FROM `user` WHERE `id` = 1);

-- 查询 id 为 1 的数据，且 id 为 1 的数据存在，且按照 id 降序排列
SELECT * FROM `user` WHERE `id` = ALL (SELECT * FROM `user` WHERE `id` = 1) ORDER BY `id` DESC;
```

## JOIN ON 连接条件

```sql
-- 查询 user 表和 user_info 表的数据，且 user 表的 id 等于 user_info 表的 id
SELECT * FROM `user` JOIN `user_info` ON `user`.`id` = `user_info`.`id`;

-- 查询 user 表和 user_info 表的数据，且 user 表的 id 等于 user_info 表的 id，且按照 id 降序排列
SELECT * FROM `user` JOIN `user_info` ON `user`.`id` = `user_info`.`id` ORDER BY `id` DESC;
```

## UPDATE 更新

```sql
-- 更新 id 为 1 的数据，username 为 panrui
UPDATE `user` SET `username`='panrui' WHERE `id` = 1;

-- 更新 id 为 1 的数据，username 为 panrui，email 为 1
UPDATE `user` SET `username`='panrui', `email` = 1 WHERE `id` = 1;
```

## DELETE 删除

```sql
-- 删除 id 为 1 的数据
DELETE FROM `user` WHERE `id` = 1;
```

## INSERT 插入

````sql
-- 插入数据
INSERT INTO `user` (`username`, `password`, `email`, `phone`, `avatar`, `introduce`, `resume`, `create_time`, `update_time`) VALUES ('panrui', '123456', '1', '1', '1', '1', '1', '2021-07-03 10:17:00', '2021-07-03 10:17:00');
``` -->