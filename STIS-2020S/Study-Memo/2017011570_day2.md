# Learning_log _2

**姓名**：吉雅太  **学号**：2017011570

系统学习了python的语法知识：

Python包含五种主要的数据类型，分别是

- Numbers(数字)
- String(字符串)
- List(列表)：append(元素); insert(位置，元素); pop(位置)
- Tuple(元组)
- Dictionary(字典)

python函数传参时有一点要注意：string, tuple, 和 number 是不可更改的对象，而 list，dict 等则是可以更改的对象，即在函数中改变了列表或字典，就是改变了原本的值。

学习了对文件及路径的操作。

map()函数可以将一个list中的所有元素都执行某个函数操作，与lambda表达式相结合，可以用一句简单的代码执行本应需要几行代码才能完成的功能。

>\#该程序可以将a中所有tuple的第一个元素取出 
>
>a = [('a',1),('b',2),('c',3),('d',4)] 
>
>a_1 = list(map(lambda x:x[0],a))   
>
>print(a_1) 
>
>\#输出结果： 
>
>['a', 'b', 'c', 'd']

filter()函数可以将list中满足某个条件的元素筛选出来，我们可以和lambda表达式结合，筛选出一个list中所有小于4的数字。

> \#该程序会将list中所有小于4的数筛选出来 
>
> a = [1,2,3,4,5,6,7] 
>
> a_1 = list(filter(lambda x:x<4,a)) 
>
> print(a_1) 
>
> \#输出结果： 
>
> [1, 2, 3]

