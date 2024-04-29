<!--
 * @Description: go语言使用规范
 * @Author: panrui
 * @Date: 2023-06-13 13:10:14
 * @LastEditTime: 2023-06-13 13:10:41
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->


## Go 文件声明、包、入口函数

```
package main - 每一个 Go 文件都应该在开头进行 package name 的声明（译注：只有可执行程序的包名应当为 main）。包（Packages）用于代码的封装与重用，这里的包名称是main

import "fmt" - 我们引入了 fmt 包，用于在 main 函数里面打印文本到标准输出

func main() - main 是一个特殊的函数。整个程序就是从 main 函数开始运行的。main 函数必须放置在 main 包中。{ 和 } 分别表示 main 函数的开始和结束部分
```

## 变量 声明

```
1.声明单个变量

var name type 是声明单个变量的语法

如果变量未被赋值，Go 会自动地将其初始化，赋值该变量类型的零值（Zero Value）

(变量可以赋值为本类型的任何值)

如果变量有初始值，那么 Go 能够自动推断具有初始值的变量的类型。因此，如果变量有初始值，就可以在变量声明中省略 type

2.声明多个变量

var (
        name   = "naveen"
        age    = 29
        height int
    )


3.简短声明(name := initialvalue)  :=操作符

3.1 简短声明的语法要求 := 操作符左边的所有变量都有初始值
3.2 简短声明的语法要求 := 操作符的左边至少有一个变量是尚未声明的
3.3 变量也可以在运行时进行赋值
```

## 类型

```
bool

数字类型
  int8, int16, int32, int64, int
  uint8, uint16, uint32, uint64, uint
  float32, float64
  complex64, complex128
  byte
  rune
sting
```

## 常量

```
const 声明常量

1.双引号中的任何值都是 Go 中的字符串常量

```

![logo](https://cdn.nlark.com/yuque/0/2022/png/683147/1664363677215-34055e6f-2814-4118-ad7a-921c77e2b2a5.png ":size=WIDTHxHEIGHT")

## 函数

```
func functionname(parametername type) returntype {
    // 函数体（具体实现的功能）
}

如果一个函数有多个返回值，那么这些返回值必须用 ( 和 ) 括起来。func rectProps(length, width float64)(float64, float64) 示例函数有两个 float64 类型的输入参数 length 和 width，并返回两个 float64 类型的值。

命名返回值(一旦命名了返回值，可以认为这些值在函数第一行就被声明为变量了)
func rectProps(length, width float64)(area, perimeter float64) {
    area = length * width
    perimeter = (length + width) * 2
    return // 不需要明确指定返回值，默认返回 area, perimeter 的值
}

_ 在 Go 中被用作空白符，可以用作表示任何类型的任何值。
```

## 包 pacage

```
所有可执行的 Go 程序都必须包含一个 main 函数,main 函数应该放置于 main 包中
```


最后更新时间：2024-4-29 14:56:34