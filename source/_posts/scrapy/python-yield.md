---
title: Python yield 的用法和意义解析
date: 2020-03-08 19:54:20
tags: [Python]
---

[知乎：Python 的关键字 yield 有哪些用法和用途？](https://www.zhihu.com/question/345210030/answer/841903171)讲的相对透彻。
[知乎：yield详解](https://zhuanlan.zhihu.com/p/32178981)

Python的生成器函数为数据和计算资源管理提供了强大的机制，但对于Python初学者而言，理解它们并非易事。  
很多程序员都学过“惰性计算”以及如何写代码来实现这一操作。但Python语言本身就支持这种计算（只需一个关键词就可轻易实现），这种有效性和表达性在其他程序语言中非常罕见。所以，惰性计算这个概念被引入“拉达姆演算”，而Python尽管并非专门的功能语言（例如Lisp），也体现出功能编程的特性，也就不足为奇了，Python使用闭包函数也是拉达姆演算特性的一部分。
<!--more-->
  
2001年，“PEP 255 — Simple Generators”（https://www.python.org/dev/peps/pep-0255/）介绍了生成器，提出动机是对惰性计算更加直接的表达：  

当一个生产函数遇到需要保持在产出值之间的状态，面对这一难题，很多程序语言无法提供令人满意的有效解决方案……  

{% asset_img python-yield.jpg yield机制 %} 

* 通常的for…in…循环中，in后面是一个数组，这个数组就是一个可迭代对象，类似的还有链表，字符串，文件。它可以是
  ```python
  mylist = [1, 2, 3]
  ```
  也可以是
  ```python
  mylist = [x*x for x in range(3)]
  ```
  它的缺陷是所有数据都在内存中，如果有海量数据的话将会非常耗内存。
* 生成器是可以迭代的，但只可以读取它一次。因为用的时候才生成。比如:
  ```python
  mygenerator = (x*x for x in range(3))
  ```
  注意这里用到了()，它就不是数组，而上面的例子是[]。
* 我理解的生成器(generator)能够迭代的关键是它有一个next()方法，工作原理就是通过重复调用next()方法，直到捕获一个异常。可以用上面的mygenerator测试。
* 带有 yield 的函数不再是一个普通函数，而是一个生成器generator，可用于迭代，工作原理同上。
* yield 是一个类似 return 的关键字，迭代一次遇到yield时就返回yield后面的值。重点是：下一次迭代时，从上一次迭代遇到的yield后面的代码开始执行。
* 简要理解：yield就是 return 返回一个值，并且记住这个返回的位置，下次迭代就从这个位置后开始。
* 带有yield的函数不仅仅只用于for循环中，而且可用于某个函数的参数，只要这个函数的参数允许迭代参数。比如array.extend函数，它的原型是array.extend(iterable)。这个特性让我们在给函数传递参数的时候非常有意思。
* send(msg)与next()的区别在于send可以传递参数给yield表达式，这时传递的参数会作为yield表达式的值，而yield的参数是返回给调用者的值。——换句话说，就是send可以强行修改上一个yield表达式值。比如函数中有一个yield赋值，a 
= yield 5，第一次迭代到这里会返回5，a还没有赋值。第二次迭代时，使用.send(10)，那么，就是强行修改yield 5表达式的值为10，本来是5的，那么a=10
* send(msg)与next()都有返回值，它们的返回值是当前迭代遇到yield时，yield后面表达式的值，其实就是当前迭代中yield后面的参数。
* 第一次调用时必须先next()或send(None)，否则会报错，send后之所以为None是因为这时候没有上一个yield(根据第8条)。可以认为，next()等同于send(None)。
  
```python
    #encoding:UTF-8  
    def yield_test(n):  
        for i in range(n):  
            yield call(i)  
            print("i=",i)  
        #做一些其它的事情      
        print("do something.")      
        print("end.")  
    
    def call(i):  
        return i*2  

    #使用for循环  
    for i in yield_test(5):  
        print(i,",")
```
结果是：
>>>
    0 ,  
    i= 0  
    2 ,  
    i= 1  
    4 ,  
    i= 2  
    6 ,  
    i= 3  
    8 ,  
    i= 4  
    do something.  
    end.  
>>>
理解的关键在于：下次迭代时，代码从yield的下一跳语句开始执行。 
  
for循环就用到了next(),所以到yield能再执行。
  

```python
def node._get_child_candidates(self, distance, min_dist, max_dist):
    if self._leftchild and distance - max_dist < self._median:
        yield self._leftchild
    if self._rightchild and distance + max_dist >= self._median:
        yield self._rightchild
```
与前面不同的是，这个函数中没有for循环，但它依然可以用于迭代。   
node._get_child_candidates函数中有yield，所以它变成了一个迭代器，可以用于迭代。  
执行第一次迭代时（其实就是调用next()方法），如果有左节点并且距离满足要求，会执行第一个yield，这时会返回self._leftchild并完成第一个迭代。 
执行第二次迭代时，从第一个yield后面开始，如果有右节点并且距离满足要求，会执行第二个yield，这时会返回self._rightchild并完成第一个迭代。 
执行第三次迭代时，第二个yield后再无代码，捕获异常，退出迭代。

```python
result, candidates = list(), [self]
while candidates:
    node = candidates.pop()
    distance = node._get_dist(obj)
    if distance <= max_dist and distance >= min_dist:
        result.extend(node._values)
    candidates.extend(node._get_child_candidates(distance, min_dist, max_dist))
return result
```
上面的node._get_child_candidates(self, distance, min_dist, max_dist)是放在extend()函数中作为参数的，为什么可以这么用，就因为extend函数的参数不仅仅支持array，只要它是一个迭代器就可以。它的原型是array.extend(iterable)。