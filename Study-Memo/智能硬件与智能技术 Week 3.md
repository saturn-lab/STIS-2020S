### 智能硬件与智能技术 Week 3

###### 经62 周远泽 2016012585

#### Lambda calculus

- 概要
  - 点之前是自变量，之后是函数体
  - Curried function：两个参数的函数=两个单参数函数套用
  - 可以加入条件判断 lambda x . if (=x 0) then 1 else x^2
  - alpha转换
  - beta reduction：(lambda x.x+1)3 把x=3代入前面的式子
- 特点：
  - 三个转换规则：alpha beta eta
  - 易于读写、可扩展
- lambda-Term 3种表达式
  - 变量：lambda x.x+y FV()函数表示自由变量y，BV()表示绑定变量x
  - 抽象：lambda x.M，把x作为M函数的参数传入
  - 应用：M N，表示将函数M应用于参数N——实例：(lambda x.x)y 将前面function作用到y，得到结果y
  - 以上并列时，左结合优先
  - 符号习惯：**<u>待补充</u>**
  - 多参数与curring化（局部嵌套）
- 规约方式
  - alpha：lambda x.x = lambda y.y 解决命名冲突
  - beta-归约：lambda x. M N = M[x:=N]将M中所有**自由变量**x用N替换
  - eta:lambda x.M x = M 解决函数冗余
  - 解长式子首先要解决命名冲突 不是一个lambda下的变量要避免重名
  - \可以代替lambda
  - [\y.y /x ]=用\y.y替换x
  - 次序：
    - 应用次序（立即求值）：先找到最里面的表达式，并按从右往左次序进行beta归约
    - 标准次序（惰性求值）：从最外面的表达式开始从外往里归约
      - Haskell和Miranda
- 组合子 Combinator
  - 定义：没有自由变量的M，函数抽象
  - Y组合子可以用于生成X YX = X (YX)，做递归，让一个函数先调用自身
- 应用案例
  - Church 布尔值，lambda 为逻辑常量
    - PAB
  - Church numerals 数码
    - 用lambda 表达式来记数字

- 类型化lambda运算
  - x:sigma = x具有类型sigma
  - lambda x.x+3 : sigma->sigma, 等价于lambda x: sigma x +3 ,x是sigma类型，+是一个sigma->sigma的函数

#### Haskell

- 保存为.hs文件

- :cd :load载入文件 :quit推出ghci
- 使用缩进来表示上一行的续写

- 类型
  - Int 一个字的大小，有限；Integer无限整数
  - 浮点数非精确，“小于一定范围”
  - 有理数类型：import Data.Ratio
  - 'char'
  - "string"

**课后练习**

```haskell
is_a::Char->Bool
is_a x = if x == 'a' then True else False

is_hello::String->Bool
is_hello "hello" = True
is_hello x = False
--这个没搞明白要怎么specifying each element in the list


space_strip::String->String
space_strip x= if head x == ' ' then tail x else x

--test
*Main Data.Char> is_a 'b'
False
*Main Data.Char> is_a 'a'
True
*Main Data.Char Data.String> is_hello "hello"
True
*Main Data.Char Data.String> is_hello "love"
False
*Main Data.Char Data.String> space_strip " I love Beijing"
"I love Beijing"
*Main Data.Char Data.String> space_strip "I love Beijing"
"I love Beijing"


--这样会报错
hello::String->Bool
hello len = length x
hello x = \i -> (if ((x !! i) == (('h':'e':'l':'l':'o':[]) !! i ))then True else False) ([0,1..length x])
hello x = False


```



