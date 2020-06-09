# Python程序设计语言

# Python3语言基础

## [File I/O](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)

### Working with paths


```python
import os

current_file = os.path.realpath('Week2.ipynb')
print(f'current file: {current_file}')
# Note: in .py files you can get the path of current file by __file__（双下划线）

current_dir = os.path.dirname(current_file)
print(f'current directory: {current_dir}')
# Note: in .py files you can get the dir of current file by os.path.dirname(__file__)

data_dir = os.path.join(os.path.dirname(current_dir), 'data')
print(f'data directory: {data_dir}')
```

    current file: D:\02_Document\02_Work\JupyterWorkspace\Courses\BDMI\Memo\Week2.ipynb
    current directory: D:\02_Document\02_Work\JupyterWorkspace\Courses\BDMI\Memo
    data directory: D:\02_Document\02_Work\JupyterWorkspace\Courses\BDMI\data


#### Checking if path exists


```python
print('exists: {}'.format(os.path.exists(data_dir)))
print('is file: {}'.format(os.path.isfile(data_dir)))
print('is directory: {}'.format(os.path.isdir(data_dir)))
```

    exists: True
    is file: False
    is directory: True


#### Creating path


```python
if not os.path.isdir(data_dir):
    os.makedirs(data_dir)
```

### Reading files


```python
file_path = os.path.join(data_dir, 'simple_file.txt')

with open(file_path, 'r') as simple_file:
    for line in simple_file:
        print(line.strip())
```

### Writing files


```python
new_file_path = os.path.join(data_dir, 'new_file.txt')

with open(new_file_path, 'w') as my_file:
    my_file.write('This is my first file that I wrote with Python.')
```

### Deleting files


```python
if os.path.exists(new_file_path):  # make sure it's there
    os.remove(new_file_path)
```

### 启发

1. `os.path.join`和`os.path.exists`函数很好使啊！
2. `with`函数也很好使啊！不用手动关闭文件

## [Lists](https://docs.python.org/3/library/stdtypes.html#lists)

这个比较熟一点，感觉需要注意的就是`Lists`是mutable的，直接用等号的时候传递的是指针，要保留原数据的话要用`list()`函数初始化或者使用`.copy()`方法：


```python
original = [1, 2, 3]
modified = original
modified[0] = 99
print('original: {}, modified: {}'.format(original, modified))
```

    original: [99, 2, 3], modified: [99, 2, 3]



```python
original = [1, 2, 3]
modified = list(original)  # Note list() 
# Alternatively, you can use copy method
# modified = original.copy()
modified[0] = 99
print('original: {}, modified: {}'.format(original, modified))
```

    original: [1, 2, 3], modified: [99, 2, 3]


## Funtions

### Default arguments

主要也是不要用mutable的对象来做缺省参数：


```python
def append_if_multiple_of_five(number, magical_list=[]):
    if number % 5 == 0:
        magical_list.append(number)
    return magical_list

print(append_if_multiple_of_five(100))
print(append_if_multiple_of_five(105))
print(append_if_multiple_of_five(123))
print(append_if_multiple_of_five(123, []))
print(append_if_multiple_of_five(123))
```

    [100]
    [100, 105]
    [100, 105]
    []
    [100, 105]


Here's how you can achieve desired behavior:


```python
def append_if_multiple_of_five(number, magical_list=None):
    if not magical_list:
        magical_list = []
    if number % 5 == 0:
        magical_list.append(number)
    return magical_list

print(append_if_multiple_of_five(100))
print(append_if_multiple_of_five(105))
print(append_if_multiple_of_five(123))
print(append_if_multiple_of_five(123, []))
print(append_if_multiple_of_five(123))
```

    [100]
    [105]
    []
    []
    []


### Docstrings

学会了写帮助文档……


```python
def calculate_sum(val1, val2):
    """This is a longer docstring defining also the args and the return value. 

    Args:
        val1: The first parameter.
        val2: The second parameter.

    Returns:
        The sum of val1 and val2.
        
    """
    return val1 + val2

print(help(calculate_sum))
```

    Help on function calculate_sum in module __main__:
    
    calculate_sum(val1, val2)
        This is a longer docstring defining also the args and the return value. 
        
        Args:
            val1: The first parameter.
            val2: The second parameter.
        
        Returns:
            The sum of val1 and val2.
    
    None


## Loops

### `enumerate()`

In case you need to also know the index:


```python
my_list = [1, 2, 3, 4, 'Python', 'is', 'neat']
for idx, val in enumerate(my_list):
    print('idx: {}, value: {}'.format(idx, val))
```

    idx: 0, value: 1
    idx: 1, value: 2
    idx: 2, value: 3
    idx: 3, value: 4
    idx: 4, value: Python
    idx: 5, value: is
    idx: 6, value: neat


## Strings

### Respecting [PEP8](https://www.python.org/dev/peps/pep-0008/#maximum-line-length) with long strings


```python
long_story = ('Lorem ipsum dolor sit amet, consectetur adipiscing elit.' 
              'Pellentesque eget tincidunt felis. Ut ac vestibulum est.' 
              'In sed ipsum sit amet sapien scelerisque bibendum. Sed ' 
              'sagittis purus eu diam fermentum pellentesque.')
long_story
```




    'Lorem ipsum dolor sit amet, consectetur adipiscing elit.Pellentesque eget tincidunt felis. Ut ac vestibulum est.In sed ipsum sit amet sapien scelerisque bibendum. Sed sagittis purus eu diam fermentum pellentesque.'



### `str.format()`


```python
secret = '{} is cool'.format('Python')
print(secret)
```

    Python is cool



```python
print('My name is {} {}, you can call me {}.'.format('John', 'Doe', 'John'))
# is the same as:
print('My name is {first} {family}, you can call me {first}.'.format(first='John', family='Doe'))
```

    My name is John Doe, you can call me John.
    My name is John Doe, you can call me John.


### `str.join()`


```python
pandas = 'pandas'
numpy = 'numpy'
requests = 'requests'
cool_python_libs = ', '.join([pandas, numpy, requests])

print('Some cool python libraries: {}'.format(cool_python_libs))
```

    Some cool python libraries: pandas, numpy, requests


