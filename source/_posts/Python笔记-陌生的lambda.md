---
title: Python笔记-陌生的lambda
date: 2018-07-23 22:21:26
tags: [Python,笔记]
preview: https://raw.githubusercontent.com/Laurence-042/Resources/master/jpg/anim/Lambda.jpg
---
在经历了小学期的Java蹂躏后，这个鶸决定继续折腾Python。（为啥说是蹂躏呢？你遇到过“一天里老师连上4节课而且一直在讲知识点毫不停歇，晚上接近九点下课下课后要在一天内开始运用这些知识点”的情况吗？没错，这个鶸遇到的就是这种情况······）然后就迎来了与lambda的初遇  
(图为当年舰R还是舰N时，此鶸受在开发商和运营商之间的法律问题的风波下无奈的转去尝试的一款架空世界的坦克拟人化游戏的一名角色，她名字就是Lambda,图源：[steamcardexchange](https://www.steamcardexchange.net/index.php?gamepage-appid-581130)
<!--more-->
~~然而这个鶸和舍友折腾了一晚上Java的基本数据类型，包装类和普通类之间的关系，为了搞明白背后的原理又反编译了代码，结果最后谁都看不懂反编译出来的结果。就这样，一晚上过去了······先设个哨点，明天补上~~
这个鶸跑来图书馆避暑了······
鶸码字中······  

> 本文是参考[@zjuxsl](https://blog.csdn.net/zjuxsl)的文章[《关于Python中的lambda，这可能是你见过的最完整的讲解》](https://blog.csdn.net/zjuxsl/article/details/79437563)写成的，感觉不太适应那篇文章的提纲，感觉略繁琐于是就写了篇新的方便查阅。

首先，要说明一点，pep8规范不建议使用lambda表达式，因为这虽然可能会让代码更紧凑，但会降低代码可读性。
> 注1：pep8：一种python代码编写规范，为提高代码可读性而制定，但不强制要求遵守。也就是说只要语法没问题，不遵守pep8也能正常运行。  

> 注2：事实上，lambda的争论一直没停，支持方认为lambda会让代码更紧凑，更“Python(adj.)”，反对方认为这会降低可读性。顺便一提，这个鶸是倾向支持使用lambda的。
---
### 格式
**`lambda argument_list: expression`**  
这是lambda唯一的一种写法，不存在其他写法
示例：
```python
lambda x: x ^ 2
lambda x, y: x + y
lambda x, y: return x * y + y ^ 2
lambda x: 1 if a > 0 else 0
lambda x: sum(x)
```
---
### 含义
**定义一个简单的匿名函数**
`lambda argument_list: expression`中的`argument_list`为匿名函数的参数，`expression`为匿名函数返回值  

---

### 使用

#### 一般可用于临时定义函数  

示例：
```python
function = lambda x, y: x * y + y ^ 2
print(function(1, 2))
```
等价于
```python
def function(x, y):
    return x * y + y ^ 2


print(function(1, 2))
```

#### 还可以用作屏蔽(Mock)
以下示例就屏蔽了`time.sleep`这个方法  
示例：
```python
time.sleep=lambda x:None
```
---
其他的用法就差不多都是“临时函数”的灵活使用了，比如作为参数传入：`sorted([1, 2, 3, 4, 5, 6, 7, 8, 9], key=lambda x: abs(5-x))`将列表 **[1, 2, 3, 4, 5, 6, 7, 8, 9]** 按照元素与5距离从小到大进行排序，其结果是 **[5, 4, 6, 3, 7, 2, 8, 1, 9]**

一般情况下了解这些了就够用了
<!--more-->