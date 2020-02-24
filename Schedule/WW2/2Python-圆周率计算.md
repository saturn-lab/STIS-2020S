# 圆周率算法-计算Pi

## 蒙特卡洛Monte Carlo

### 原理

大数定理思想，频率估计概率

### 代码实现


```python
import random
import math


def draw(inner_points, outer_points):
    import matplotlib.pyplot as plt
    %matplotlib inline
    fig, ax = plt.subplots(figsize=(5, 5))
    inner_x = [x[0] for x in inner_points]
    inner_y = [x[1] for x in inner_points]
    outer_x = [x[0] for x in outer_points]
    outer_y = [x[1] for x in outer_points]
    ax.scatter(inner_x, inner_y, color="r", s=1)
    ax.scatter(outer_x, outer_y, color="g", s=1)

    ax.set_xlim(0, 1)
    ax.set_ylim(0, 1)

    import numpy as np
    theta = np.linspace(0, 2*np.pi, 100)
    r = 1
    x1 = r*np.cos(theta)
    x2 = r*np.sin(theta)
    ax.plot(x1, x2, color='black')
    plt.show()


def MonPi(number):
    N2 = number
    N1 = 0.
    inner_points = []
    outer_points = []
    for i in range(N2):
        x = random.random()
        y = random.random()
        if x*x+y*y <= 1:
            N1 += 1
            inner_points.append([x, y])
        else:
            outer_points.append([x, y])

    print("Monte PI:", 4*N1/N2)
    draw(inner_points, outer_points)
```

### 示例


```python
MonPi(30000)
```

    Monte PI: 3.1490666666666667



![png](./1_0.png)


### 启发

1. 用不同的color标记内外点
2. 用三角函数画弧
3. draw和calc函数分开写

## Taylor Series

### 原理

对于反正切函数的泰勒级数展开：

$$
\arctan (x)=\sum_{k=0}^{\infty}(-1)^{k} \frac{x^{2 k+1}}{2 k+1}=x-\frac{1}{3} x^{3}+\frac{1}{5} x^{5}-\frac{1}{7} x^{7}+\cdots
$$

当$x=1$时，$\arctan (x)=\pi/4$，即有：

$$
\frac{\pi}{4}=\sum_{n=0}^{\infty} \frac{(-1)^{n}}{2 n+1}
$$

### 代码实现


```python
def TaylorPi(k):
    sum, odd = 0, True
    for i in range(1, k):
        sum += 1/(2*i-1) if odd == True else -1/(2*i-1)
        odd = not odd
    print("Taylor PI:", sum*4)
```

### 示例


```python
TaylorPi(1000000)
```

    Taylor PI: 3.1415936535907742


### 启发

1. 使用odd这个布尔变量来辅助判断简化代码

## Chudnovsky

### 原理

Chundnovsky公式：

$$
\pi=\frac{426880 \sqrt{10005}}{\sum_{k=0}^{\infty} \frac{(6 k) !(13591409+545140134 k)}{(3 k) !(k !)^{3}(-640320)^{3 k}}}
$$

[公式证明](https://en.wikipedia.org/wiki/Chudnovsky_algorithm)

### 代码实现


```python
def Ch_cal(k):
    uper_value = math.factorial(6*k)*(13591409+545140134*k)
    lower_value = math.factorial(3*k)*math.pow(math.factorial(k),3)*math.pow((-640320),3*k)
    return uper_value/lower_value

def Chudnovsky(number):
    uper_value = 426880*math.sqrt(10005)
    lower_sum = 0.
    for k in range(number):
        lower_sum+=Ch_cal(k)
    print("Chudnovsky PI:",uper_value/lower_sum)
```

### 示例


```python
Chudnovsky(10)
```

    Chudnovsky PI: 3.141592653589793



```python
def Ch_cal(k):
    uper_value = math.factorial(6*k)*(13591409+545140134*k)
    lower_value = math.factorial(3*k)*math.pow(math.factorial(k),3)*math.pow((-640320),3*k)
    return uper_value/lower_value

def Chudnovsky(number):
    uper_value = 426880*math.sqrt(10005)
    lower_sum = 0.
    for k in range(number):
        lower_sum+=Ch_cal(k)
    print("Chudnovsky PI:",uper_value/lower_sum)
```

### 启发

1. 观察公式，只计算变动的分母部分，并分为上下部分分开计算

### 改进（不一定

当$k$值增加的时候，$k$的阶乘也会迅速飙升，再进行幂指操作很容易超出`math`函数的计算限，例如：


```python
Chudnovsky(20)
```


    ---------------------------------------------------------------------------
    
    OverflowError                             Traceback (most recent call last)
    
    <ipython-input-8-62b9c5c50958> in <module>
    ----> 1 Chudnovsky(20)


    <ipython-input-7-54d71762bb50> in Chudnovsky(number)
          8     lower_sum = 0.
          9     for k in range(number):
    ---> 10         lower_sum+=Ch_cal(k)
         11     print("Chudnovsky PI:",uper_value/lower_sum)


    <ipython-input-7-54d71762bb50> in Ch_cal(k)
          1 def Ch_cal(k):
          2     uper_value = math.factorial(6*k)*(13591409+545140134*k)
    ----> 3     lower_value = math.factorial(3*k)*math.pow(math.factorial(k),3)*math.pow((-640320),3*k)
          4     return uper_value/lower_value
          5 


    OverflowError: math range error


但Python本身对于数字是没有长度限制的，所以幂指操作我们没必要用`math.pow`函数来做，这样可以进一步扩大我们的计算范围：


```python
def Ch_cal_new(k):
    uper_value = math.factorial(6*k)*(13591409+545140134*k)
    lower_value = math.factorial(3*k)*((math.factorial(k))**3)*((-640320)**(3*k))
    return uper_value/lower_value

def Chudnovsky_new(number):
    uper_value = 426880*math.sqrt(10005)
    lower_sum = 0.
    for k in range(number):
        lower_sum+=Ch_cal_new(k)
    print("Chudnovsky PI:",uper_value/lower_sum)
```


```python
Chudnovsky_new(20)
```

    Chudnovsky PI: 3.141592653589793


因为这个公式收敛得很快，所以这种操作可能对计算精度提高没有多少实质性作用（如果设置多显示几位小数应该可以看到差别吧），但谁让我们内存大呢

## Iterative

### 原理

[高斯-勒让德算法](https://zh.wikipedia.org/wiki/高斯-勒让德算法)

### 代码实现


```python
def Iterative_cal(number):
    a_now = 1.
    b_now = 1./math.sqrt(2)
    t_now = .25
    p_now = 1.
    for i in range(number):
        a = (a_now+b_now)/2
        b = math.sqrt(a_now*b_now)
        t = t_now-p_now*math.pow((a_now-a),2)
        p = 2*p_now

        a_now = a
        b_now = b
        t_now = t
        p_now = p
    print("Iterative PI:",math.pow(a_now+b_now,2)/(4*t_now))
```

### 示例


```python
Iterative_cal(100)
```

    Iterative PI: 3.141592653589794


### 启发

1. 用数字后带点的形式`1.`来告诉Python这是浮点数