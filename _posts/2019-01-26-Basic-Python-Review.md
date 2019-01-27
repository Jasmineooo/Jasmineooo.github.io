---
layout:     post
title:      Basic Python Review
subtitle:   Python基础语法复习小结
date:       2019-01-26
author:     Ama
header-img: img/post-bg-python.jpg
catalog: true
tags:
    - Python
---

## 前言

多年前因做二次开发接触到Python，当初入了个门，顺带写了个爬虫玩（详见 [2017温哥华马拉松“大”数据](http://amathlover.com/2017/05/13/2017-Vancouver-Marathon-Big-Data/)），如今想来，这能叫大数据？两年没碰了，重新把Python捡起来，侧重Data Science。


## 库

比如：
- 科学计算：NumPy, Pandas
- 深度学习：Keras, TensorFlow
- 机器学习：Scikit-learn

## 2.7 or 3.x?

语法差异不大。

看是否依赖于2.7的包，若否，则用3.x。本文采用python 3.6.2，IDE为Anaconda

## 基础语法

>注意：Python用代码缩进和冒号区分代码之间的层次关系，故代码缩进是一种语法。

>以下代码中右边的注释部分为运行结果，特此说明。
>本文代码已上传至Github: https://github.com/Jasmineooo/Data-Analysis

### 输入输出、判断、循环

```python
# 如果注释中有中文，加上这一句：
#-*- coding:utf-8 -*-
# input
# 2.7用 raw_input()，否则会得到int
name = input("What's your name?") # What's your name? 输入Ama，回车
score = 40 + 45

# print 
# %s字符串，%d十进制整数，%f浮点数
print ('Hello, %s' %name)         # Hello, Ama
print ('sum = %d' %score)         # score = 85

# 判断
# if和else后面都有冒号
# 2.7在写下面的print时，都无需加()
if score >= 90:
       print ('Excellent')
else:
       if score < 60:
           print ('Fail')
       else:
           print ('Good Job')     # Good Job

# 循环 for
# range(11)为0到10，不包括11
# range(1,11,2)为[1,3,5,7,9]
sum = 0
for number in range(11):
    sum = sum + number
print sum                         # 55

# 循环 while
# while适合循环次数不确定的循环，for适合固定次数的循环
sum = 0
number = 1
while number < 11:
       sum = sum + number
       number = number + 1
print sum                         # 55
```

### 数据类型

#### 列表 []
```python
# 列表 []
lists = ['a','b','c']

# append() 尾部添加元素
lists.append('d')
print (lists)            # ['a', 'b', 'c', 'd']

# len() 元素个数
print (len(lists))       # 4

# insert() 插入元素
lists.insert(0,'mm')

# pop() 尾部删除元素
lists.pop()
print (lists)            # ['mm', 'a', 'b', 'c']
```

#### 元组

```python
# 元组 tuple
# 初始化后不能修改，可访问，如tuples[0]，不能赋值
tuples = ('tupleA','tupleB')
print (tuples[0])        # tupleA

```

#### 字典 {dictionary}
```python
# 字典 
# {key, value}, 可增删改查

# 定义一个 dictionary
score = {'guanyu':95,'zhangfei':96}

# 添加一个元素
score['zhaoyun'] = 98
print (score)    # {'guanyu': 95, 'zhangfei': 96, 'zhaoyun': 98}

# 删除一个元素
score.pop('zhangfei')

# 查看 key 是否存在
print ('guanyu' in score)    # True

# 查看一个 key 对应的值
print (score.get('guanyu'))  # 95
print (score.get('yase',99)) # 99
```

#### 集合 set
```python
# 集合
# key的集合，不存储value，可增删查

s = set(['a', 'b', 'c'])

# 添加
s.add('d')

# 删除
s.remove('b')

print (s)               # {'d', 'a', 'c'}

# 查看 key 是否存在
print ('c' in s)        # True
```

### 引入模块/包 import
```python
# 导入一个模块
import model_name
# 导入多个模块
import module_name1,module_name2
# 导入包中指定模块 
from package_name import moudule_name
# 导入包中所有模块 
from package_name import *

# 引入scikit-learn库
import sklearn
```

### 函数
```python
# 定义函数
def addone(score):
   return score + 1
print (addone(99))      # 100
```

## 刷题增加熟练度
[Kaggle](https://www.kaggle.com/)
[浙江大学ACM的Online Judge](http://acm.zju.edu.cn/onlinejudge/showProblemsets.do)

###  [A+B Problem](http://acm.zju.edu.cn/onlinejudge/showProblem.do?problemCode=1001)

- Input
The input will consist of a series of pairs of integers a and b,separated by a space, one pair of integers per line. 
- Output
For each pair of input integers a and b you should output the sum of a and b in one line,and with one line of output for each line in input.
- Sample Input
1 5
- Sample Output
6

参考1：
```python
# sys.stdin也可以实现和input一样的功能，但更常见的是另外一种使用方式，可以直接使用文件作为整体的输入，可以很简洁。
# 用split将该行的单词分割成列表，每个单词就是一个列表项目，split的默认参数是空格，所以不传递任何参数时分割空格，在英文中也就等同于分割单词
import sys
for line in sys.stdin:
    a = line.split()
    print int(a[0]) + int(a[1])
```

参考2：
```python
# 当得到结果不再需要循环时，则用break语句跳出循环，避免程序进入死循环
# 捕捉异常可以使用try/except语句。try/except语句用来检测try语句块中的错误，从而让except语句捕获异常信息并处理。 
while True:
       try:
              line = input()
              a = line.split()
              print (int(a[0]) + int(a[1]))
       except:
              break
```

### 求和 1+3+5+...+99

```python
# 方法一：sum函数

print(sum(range(1,100,2)))

# 方法二：if

a = 0
for i in range(1,100,2):
    a += i 
print(a)

# 方法三：while
i = 1
s = 0
while i < 100:
    if (i % 2 != 0):
        s += i
    i += 1    
print (s)
```

## 参考资料
[1] 极客时间-数据分析实战第三讲
[2] [异常处理](http://www.runoob.com/python/python-exceptions.html)