<!--
 * @Description: typeorm文档
 * @Author: prui
 * @Date: 2024-04-26 09:45:09
 * @LastEditTime: 2024-04-26 09:50:48
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2024-04-26 09:49:20)

## 实体创建

#### PrimaryGeneratedColumn 使用

```ts
@PrimaryGeneratedColumn('uuid', { name: 'id', comment: '主键' })
id: number;
```

#### 一对多
