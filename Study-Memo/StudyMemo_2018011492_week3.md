## Week 3

**姓名：阿璐思    学号：2018011492**

***

**lambda演算**：

* lambda演算的产生背景、特点
  * Alonzo Church 提出
  * 基于表达式、易于读写且可扩展

* lambda表达式的相关语法
  * 表达式形式、符号习惯
  * 绑定变量与自由变量
  * 多参数与Curring化
  * 归约方式：alpha-转换、beta-归约、etah-归约
  * 求值顺序：立即、惰性
  * 组合子：K、I、Y组合子，其中Y组合子能够复制自身
* 图灵完备性
  * 四大要求：存储、算术、条件执行、重复
  * Lambda演算满足图灵完备性

* 应用案例
  * Church布尔值、Church数码、递归

***

**Haskell**：

* 一种函数式编程语言

* 特点：

  * 引用透明性（适合并发编程）
  * 惰性（允许创建无限长度的数据结构）
  * 静态类型

* 内容介绍

  * 若表达式中有负数常量则应选择用括号将其括起来
  * 函数装载与调用方式

  * 整数、浮点数、有理数、布尔、字符、字符串等数据类型

  * 元组、列表等数据结构

  * 加减乘除以及其他相关的基本操作符，与C语言相似
  * 一些常用的固定函数的介绍
  * 定义函数的具体方法
    * 函数的声明
    * 函数体的定义

***

**Haskell实践练习**：

**代码1：**

isA :: Char->Bool
isA 'a' = True
isA x = False

**代码2：**

isHello :: String->Bool
isHello "hello" = True
isHello x = False

**代码3:**

removeSpace :: String->String
removeSpace oldString = [new | new <- oldString, new /= ' ']

***

**总结：**

​	通过本周课的学习，我了解到了Lambda演算的相关内容、Haskell语言的特点与语法以及如何利用Haskell语言编写简单的程序，同时在完成Haskell实践的课后作业过程中，练习了如何在.hs文件中定义并封装函数、如何装载函数以及如何使用编写好的函数实现具体的功能，因此对lambda表达式与Haskell语言的相关知识点有了更深刻的认识和理解。

