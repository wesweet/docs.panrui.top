<!--
 * @Description: 记录文档
 * @Author: panrui
 * @Date: 2023-11-15 09:25:43
 * @LastEditTime: 2023-11-16 09:18:15
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 装饰器表格

| 名称          | 类型   | 描述                 | 功能说明 |
| ------------- | ------ | -------------------- | -------- |
| @ApiTags      | 装饰器 | 标签                 |          |
| @ApiOperation | 装饰器 | 描述这个方法是干啥的 |          |



## 文档

- [TypeORM](https://typeorm.biunav.com/zh/embedded-entities.html)
- [中文文档](https://typeorm.bootcss.com/)

## Entity 创建
```js
import {
  Column,
  Entity,
  PrimaryGeneratedColumn,
  BeforeInsert,
  CreateDateColumn,
  UpdateDateColumn,
} from 'typeorm';
import bcrypt from 'bcryptjs';

export enum GenderEnum {
  Male = 'M',
  Female = 'F',
  Other = 'O',
}

@Entity({ name: 'pr_id_users' })
export class Users {
  // 定义自增长数据类型
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  encryptedPassword: string;

  // 定义enum数据类型
  @Column({
    type: 'enum',
    enum: GenderEnum,
    default: GenderEnum.Other,
  })
  gender: GenderEnum;

  // 定义布尔类型
  @Column({
    type: 'boolean',
    default: false,
  })
  mobileConfirmed: boolean;

  // 定义时间类型
  @Column({
    type: 'timestamp',
  })
  registerDate: Date;

  // 定义自动更新时间类型
  @UpdateDateColumn()
  updateDate: Date;

  // 定义自动创建时间类型
  @CreateDateColumn()
  createDate: Date;

  public password: string;

  // 使用装饰器,定义函数，再执行save执行自动执行
  @BeforeInsert()
  async hashPassword() {
    try {
      console.log(this.password);
      this.encryptedPassword = await bcrypt.hash(this.password, 10); // 加强加密强度
      // const isMatch = await bcrypt.compare(this.password, this.encryptedPassword);  // 验证密码是否正确(因为无法解密的)
      console.log(this.encryptedPassword);
    } catch (error) {
      console.log(error);
      throw new Error('密码加密失败');
    }
  }

  async validatePassword(plainPassword: string): Promise<boolean> {
    try {
      return await bcrypt.compare(plainPassword, this.encryptedPassword);
    } catch (error) {
      throw new Error('密码验证失败');
    }
  }
}

// 使用
const user = new Users();
user.username = 'exampleUser';
user.password = 'examplePassword'; // 提供原始密码
await user.hashPassword(); // 调用 hashPassword 方法加密密码
await repository.save(user);
```

## mysql 列类型

| 类型                               | 解释                                                  |
| ---------------------------------- | ----------------------------------------------------- |
| tinyint                            | 无符号的 8 位整数类型，表示范围在 0 到 255 之间的整数 |
| smallint                           | 短整数类型，表示带符号的 16 位整数                    |
| int                                | 整数类型，表示带符号的 32 位整数                      |
| bigint                             | 长整数类型，表示带符号的 64 位整数                    |
| float                              | 浮点数类型，用于存储近似数值                          |
| real                               | 单精度浮点数类型，用于存储近似数值                    |
| bit                                | 位类型，表示存储 0 或 1 的布尔值                      |
| date                               | 日期类型，用于存储日期值                              |
| datetime2、datetime、smalldatetime | 日期和时间类型，用于存储日期和时间值                  |
| datetimeoffset                     | 带有时区偏移的日期和时间类型                          |
| time                               | 时间类型，用于存储时间值                              |
| timestamp                          | 时间戳类型，用于记录数据的版本信息                    |
| char、varchar、text                | 字符类型，用于存储字符数据                            |
| decimal、numeric                   | 精确数值类型，用于存储固定精度和小数位数的数值        |
| money、smallmoney                  | 货币类型，用于存储货币值                              |
| nchar、nvarchar、ntext             | Unicode 字符类型，用于存储 Unicode 字符数据           |
| binary、varbinary、image           | 二进制类型，用于存储二进制数据                        |
| hierarchyid                        | 层次结构标识类型，用于存储层次结构数据                |
| sql_variant                        | 可变类型，用于存储各种数据类型的值                    |
| uniqueidentifier                   | 唯一标识符类型，用于存储全局唯一标识符（GUID）        |
| xml                                | XML 类型，用于存储 XML 文档                           |
| geometry                           | 几何类型，用于存储平面几何数据                        |
| geography                          | 地理类型，用于存储地理空间数据                        |
| rowversion                         | 行版本类型，用于记录数据的版本信息                    |




最后更新时间：2024-4-28 16:16:14