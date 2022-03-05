#### 前言
Python中一切皆是对象，在阅读本笔记前，需要先了解`id()`和`is`运算符。

`id()`是用于返回变量的内存地址

###### 小问题
```py
class A:  
    def f(self):  
        print(self.b)  
    @staticmethod  
	def g():  
        pass

In [6]: b, c = A(), A() 

In [7]: b is c 
Out[7]: False 

In [9]: id(b) == id(c) 
Out[9]: False 

In [10]: id(b.f) == id(c.f) 
Out[10]: True 

In [11]: b.f is c.f 
Out[11]: False 

In [12]: f_b, f_c = b.f, c.f 

In [13]: id(f_b) == id(f_c) 
Out[13]: False
```

思考为什么`id(b.f) == id(c.f)`结果为`True`?

两个生命周期不相交的不同对象，可能有一个地址，本例中其实是发现b.f不存在，所以临时创建了把a绑定到A.f上的bound method，然后销毁，紧接着又发现c.f不存在，再在同一个地址上，临时创建了另一个bound method。就好比一栋房子，b.f先住进来了，搬走之后c.f又住进来了，居住时间没有交集，但是收信地址是一样的，你不能因此就说他们两是一个人。。。我们把b.f和c.f赋值之后，因为有了引用就不会被销毁，强行令他们的生存周期有重叠，然后发现他们作为不同对象，其地址确实是不一样的。

此外，当你尝试`id(b.g) == id(c.g)`时会发现，结果也为`True`！

这是因为该方法是个静态方法，通过对象来访问静态成员是不会再进行浅拷贝的，因此`b.g`和`c.g`其实是货真价实的同一对象。

#### 常量池
###### 小整数对象池
\[-5, 256\] 这些小整数被定义在了一个整数对象池里，当引用小整数时会自动引用整数对象池里的对象，所以这些小整数不会重复创建，当多个变量指向同一个小整数时，实质上它们指向的是同一个对象。

###### 字符串
字符串对象是不可变对象，python内部会维护一个字典，字典中已创建的字符串(key)和对应的字符串对象地址(value)，每次创建字符串对象前都会先和字典进行匹配，如有则直接引用，否则将在字典中，直接创建。内部机制处理字符串长度小于等于20且仅由数字字母下划线组成，仅创建一次。

[浅析Python中字符串的intern机制 / 张生荣 (zhangshengrong.com)](https://www.zhangshengrong.com/p/3mNmdPZDaj/)

###### 浮点型
float类型可以认为每个值都创建一个对象，因为float值几乎不会重复。

###### 元组
Tuple是不可变对象，由于查找开销过大，因此内部并无实现intern机制，每次创建都会分配内存空间

#### 交互式解释器与源代码执行
有时，交互式解释器与源代码解释器获得的结果并不相同
```py
## 交互式解释器
>>> a = -6

>>> b = -6

>>> a is b

False

>>> a = -5

>>> b = -5

>>> a is b

True

>>> a = 256

>>> b = 256

>>> a is b

True

>>> a = 257

>>> b = 257

>>> a is b

False

## 源代码执行

a = -5

b = -5

print(a is b) # True

a = -6

b = -6

print(a is b) # False

a = 256

b = 256

print(a is b) # True

a = 257

b = 257

print(a is b) # True
```
[python 常量池_python中的对象池_weixin_39540178的博客-CSDN博客](https://blog.csdn.net/weixin_39540178/article/details/111430469)