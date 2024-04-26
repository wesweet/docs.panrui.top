<!--
 * @Description: typeorm文档
 * @Author: prui
 * @Date: 2024-04-26 09:45:09
 * @LastEditTime: 2024-04-26 15:32:32
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

#### OneToMany 使用

> 1. 第一个参数：() => TargetEntity，这是一个函数，返回与当前实体类关联的目标实体类（即“多”端实体类）。例如，如果“一”端实体类是 User，而“多”端实体类是 Post，则应传入 () => Post

> 2. 第二个参数：(targetEntity) => targetEntity.propertyName，这是一个函数，接收目标实体类（即“多”端实体类）作为参数，并返回一个属性访问器，该属性指向“一”端实体类的主键。例如，在 Post 类中，如果有一个属性 userId 指向 User 的主键，应传入 (post) => post.userId

```ts
@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  // ... 其他用户信息字段

  @OneToMany(() => Post, (post) => post.userId)
  posts: Post[];
}
```

#### ManyToOne 使用

> 1. 第一个参数：() => TargetEntity，与“一”端实体类相同，返回与当前实体类关联的目标实体类（即“一”端实体类）
> 2. 第二个参数：(targetEntity) => targetEntity.propertyName，与“一”端实体类相同，返回一个属性访问器，该属性指向“一”端实体类的主键(这里指的是 ManyToOne 定义的那列)

```ts
@Entity()
export class Post {
  @PrimaryGeneratedColumn()
  id: number;

  @ManyToOne(() => User, (user) => user.id)
  userId: number;

  // ... 其他帖子信息字段
}
```
