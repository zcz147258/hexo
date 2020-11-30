---
title: Python
date:
updated:
type: "tags"
comments:
categories: Python
description: Python
keywords: Python
top_img: https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2106761184,125216953&fm=26&gp=0.jpg
cover: https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2106761184,125216953&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 一.变量的类型

```python
python 里面的变量类型有5个标准的数据类型
    Numbers（数字）
    String（字符串）
    List（列表）
    Tuple（元组）
    Dictionary（字典）
 数字类型有四种 
    int 整型 100
    long  长整型 	51924361L
    float  浮点数  15.20
    complex 复数  3.14j 	9.322e-36j 	-.6545+0J
字符串类型
    从左到右索引默认0开始的，最大范围是字符串长度少1
    从右到左索引默认-1开始的，最大范围是字符串开头
python列表
	List（列表） 是 Python 中使用最频繁的数据类型。
    列表可以完成大多数集合类的数据结构实现。它支持字符，数字，字符串甚至可以包含列表（即嵌套）。
    列表用 [ ] 标识，是 python 最通用的复合数据类型。
    从左到右索引默认 0 开始，从右到左索引默认 -1 开始，
   	''''''
    下标可以为空表示取到头或尾
    ''''''
    print list[1:3]          # 输出第二个至第三个元素 
	print list[2:]           # 输出从第三个开始至列表末尾的所有元素
    
    加号 + 是列表连接运算符，星号 * 是重复操作
Python 元组
	元组是另一个数据类型，类似于 List（列表）。
    元组用 () 标识。内部元素用逗号隔开。但是元组不能二次赋值，相当于只读列表。
    
    print tuple[1:3]          # 输出第二个至第四个（不包含）的元素 
	print tuple[2:]           # 输出从第三个开始至列表末尾的所有元素
    
    以下是元组无效的，因为元组是不允许更新的。而列表是允许更新的：
Python 字典
	字典(dictionary)是除列表以外python之中最灵活的内置数据结构类型。列表是有序的对象集合，字典是无序的		对象集合。
    两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。
    字典用"{ }"标识。字典由索引(key)和它对应的值value组成。
```

# 二 python的数据类型转换

```python
Python数据类型转换
	int()  class int(x, base=10)  x -- 字符串或数字 base -- 进制数，默认十进制
	int('0xa',16)    10   16进制
	
	long() class long(x, base=10)
	long('123')   123L
	
	float()  float(112)  112.0
	
	complex()
	complex("1")  # 当做字符串处理(1 + 0j)
	
	str()   str(dict)  "{'google': 'google.com', 'runoob': 'runoob.com'}"
	
	repr()   返回一个对象的 string 格式。
	
	eval()  eval() 函数用来执行一个字符串表达式，并返回表达式的值。
	
	tuple()  将列表 s 转换为一个元组
	
	list()  list() 方法用于将元组转换为列表。
	
	set() 函数创建一个无序不重复元素集，可进行关系测试，删除重复数据，还可以计算交集、差集、并集等。
     >>>x = set('runoob')
    >>> y = set('google')
    >>> x, y
    (set(['b', 'r', 'u', 'o', 'n']), set(['e', 'o', 'g', 'l']))   # 重复的被删除
    >>> x & y         # 交集
    set(['o'])
    >>> x | y         # 并集
    set(['b', 'e', 'g', 'l', 'o', 'n', 'r', 'u'])
    >>> x - y         # 差集
    set(['r', 'b', 'u', 'n'])
    >>>
    
    dict() 函数用于创建一个字典。
    >>> dict(zip(['one', 'two', 'three'], [1, 2, 3]))   # 映射函数方式来构造字典
    {'three': 3, 'two': 2, 'one': 1} 
    >>> dict([('one', 1), ('two', 2), ('three', 3)])    # 可迭代对象方式来构造字典
    {'three': 3, 'two': 2, 'one': 1}
    >>>
    
    frozenset() 返回一个冻结的集合，冻结后集合不能再添加或删除任何元素。
	
	
```

# 三  运算符

## 3.1算术运算符

```
+ - * /   %  
** 去幂 返回x的y次幂 
//  取整除

```

## 3.2比较运算符

```
==
！=
>
<
>=
<=
```

## 3.3赋值运算符

```
=
+=
—=
*=
/=
%=
**=	取次幂运算符
//=  取整出运算符
```

## 3.4位运算符

```
按位运算符是把数字看作二进制来进行计算的。Python中的按位运算法则如下

&	按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0
|	按位或运算符 按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。
^	按位异或运算符 按位异或运算符：当两对应的二进位相异时，结果为1
~	按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1 。~x 类似于 -x-1
<<	左移动运算符  运算数的各二进位全部左移若干位，由 << 右边的数字指定了移动的位数，高位丢弃，低位补0。
>>	右移动运算符： 把">>"左边的运算数的各二进位全部右移若干位，>> 右边的数字指定了移动的位数
```

## 3.5Python逻辑运算符

```
and   	x and y
or	    x or y
not	    not x
```

## 3.6 成员运算符

```python
Python成员运算符
in	如果在指定的序列中找到值返回 True，否则返回 False。
not in	如果在指定的序列中没有找到值返回 True，否则返回 False。
is	is 是判断两个标识符是不是引用自一个对象
is not	is not 是判断两个标识符是不是引用自不同对象
```

## 3.7Python运算符优先级

## 四，流程控制语句

## 4.1 if语句

```python
if 判断条件：
    执行语句……
else：
    执行语句……
    
flag = False
name = 'luren'
if name == 'python':         # 判断变量是否为 python 
    flag = True              # 条件成立时设置标志为真
    print 'welcome boss'     # 并输出欢迎信息
else:
    print name               # 条件不成立时输出变量名称
    
    
 elif ~~~~else if
```

## 4.2do while 循环

```python
while 判断条件(condition)：
    执行语句(statements)……
    
    numbers = [1,5,6,7,8,44,58,98,-15,-45,-88]
even = []
odd = []
while len(numbers) > 0:
    number = numbers.pop()
    if(number % 2 == 1):
        even.append(number)
    else:
        odd.append(number)
print(even)

while 语句时还有另外两个重要的命令 continue，break 来跳过循环，continue 用于跳过该次循环，break 则是用于退出循环

循环使用 else 语句
在 python 中，while … else 在循环条件为 false 时执行 else 语句块：
```

## 4.3 for循环

```python

Python for循环可以遍历任何序列的项目，如一个列表或者一个字符串。


for num in range(10,20):  # 迭代 10 到 20 之间的数字
   for i in range(2,num): # 根据因子迭代
      if num%i == 0:      # 确定第一个因子
         j=num/i          # 计算第二个因子
         print '%d 等于 %d * %d' % (num,i,j)
         break            # 跳出当前循环
   else:                  # 循环的 else 部分
      print num, '是一个质数'

循环使用else语句
在 python 中，for … else 表示这样的意思，for 中的语句和普通的没有区别，else 中的语句会在循环正常执行完（即 for 不是通过 break 跳出而中断的）的情况下执行，while … else 也是一样。

实例
fruits = ['banana', 'apple',  'mango']
for fruit in fruits:        # 第二个实例
   print '当前水果 :', fruit
   
   
循环嵌套
i = 2
while(i < 100):
   j = 2
   while(j <= (i/j)):
      if not(i%j): break
      j = j + 1
   if (j > i/j) : print i, " 是素数"
   i = i + 1
```

## 4.4Python pass 语句

```
Python pass 是空语句，是为了保持程序结构的完整性。

pass 不做任何事情，一般用做占位语句
```

## 五 五个基础变量

## 5.1数字类型

```python
Python Number(数字)
Python Number 数据类型用于存储数值。
数据类型是不允许改变的,这就意味着如果改变 Number 数据类型的值，将重新分配内存空间。

您可以通过使用del语句删除单个或多个对象，例如：
del var_a, var_b


Python math 模块、cmath 模块
Python 中数学运算常用的函数基本都在 math 模块、cmath 模块中。
Python math 模块提供了许多对浮点数的数学运算函数。
Python cmath 模块包含了一些用于复数运算的函数。
cmath 模块的函数跟 math 模块函数基本一致，区别是 cmath 模块运算的是复数，math 模块运算的是数学运算。
dir(math)  查看 math 查看包中的内容:
常用方法
cmp(x, y)	如果 x < y 返回 -1, 如果 x == y 返回 0, 如果 x > y 返回 1
abs(x)	返回数字的绝对值，如abs(-10) 返回 10
ceil(x)	返回数字的上入整数，如math.ceil(4.1) 返回 5
fabs(x)	返回数字的绝对值，如math.fabs(-10) 返回10.0
floor(x)	返回数字的下舍整数，如math.floor(4.9)返回 4
max(x1, x2,...)	返回给定参数的最大值，参数可以为序列。
modf(x)	返回x的整数部分与小数部分，两部分的数值符号与x相同，整数部分以浮点型表示。
pow(x, y)	x**y 运算后的值。
round(x [,n])	返回浮点数x的四舍五入值，如给出n值，则代表舍入到小数点后的位数。
sqrt(x)	返回数字x的平方根


Python随机数函数  import random
choice(seq)	从序列的元素中随机挑选一个元素，比如random.choice(range(10))，从0到9中随机挑选一个整数。
random()	随机生成下一个实数，它在[0,1)范围内。
uniform(x, y)	随机生成下一个实数，它在[x,y]范围内。
shuffle(lst)	将序列的所有元素随机排序
```

## 5.2Python 字符串

```python
var1 = 'Hello World!'
var2 = "Python Runoob"
 
print "var1[0]: ", var1[0]
print "var2[1:5]: ", var2[1:5]
var1[0]:  H
var2[1:5]:  ytho


字符串运算
+	字符串连接
*	重复输出字符串
[]	通过索引获取字符串中字符
[ : ]	截取字符串中的一部分
in	成员运算符 - 如果字符串中包含给定的字符返回 True
not in	成员运算符 - 如果字符串中不包含给定的字符返回 True
%	格式字符串

Python 字符串格式化
print "My name is %s and weight is %d kg!" % ('Zara', 21) 
My name is Zara and weight is 21 kg!

%s	 格式化字符串
%d	 格式化整数
%o	 格式化无符号八进制数
%f	 格式化浮点数字，可指定小数点后的精度
%c	 格式化字符及其ASCII码

*	定义宽度或者小数点精度
-	用做左对齐
+	在正数前面显示加号( + )
<sp>	在正数前面显示空格
m.n.	m 是显示的最小总宽度,n 是小数点后的位数(如果可用的话)


Python三引号（triple quotes）
python中三引号可以将复杂的字符串进行复制:

python三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符。


字符串常用函数
find()  检查字符串是否包含指定的字符，
        没包含返回-1，
        包含返回开始的索引值
index() 检查字符串是否包含指定的字符，
        包含-返回开始的索引值
        不包含-提示错误
count 返回str1在string中指定索引返回内[start, end]出现的次数

replace 将str1中的str1替换成str2，如果指定count，则不超过count次数

split 如果maxsplit有指定值，则仅分割maxsplit个子字符串
len()   返回字符串长度

join() 在字符串后面插入一个指定字符，构造一个新的字符串
upper() 将所有的字符转换为大写
title() 首字母转换为大写
isalpha() 检测字符串是否只包含字母
isdigit() 检测字符是否只包含数字， 返回Trun 和 False
isalnum() 检测是否只包含数字或字母。用处：可以用于判断密码，一般情况下密码不能输入汉字或空格。
isspace() 检测字符串中是否只包含空格，如果有返回Trun反之返回False,通俗的讲就是判断非空验证


```

## 5.3Python3 列表

```python
python 表达式
[1, 2, 3] + [4, 5, 6]
['Hi!'] * 4
3 in [1, 2, 3]

Python列表截取与拼接
list_1.insert(2,插入的值)   在指定位置插入
list_1.append(插入的值)		在末尾插入
list_1.pop()  删除
list_1.pop(-2)  删除指定位置元素
list_2.reverse()  反转顺序
list_2.sort() 按照Ascll排序
list_1.extend(list_2)  合并列表
list_2.clear() 清楚数据 空数组
index函数与字符串中的index函数很类似，也是用于查找某个元素在列表中的索引位置，
count函数用于统计列表中某个元素在列表中出现的次数。

del
根据下标进行删除

in/not in
in用于判断某个元素是否在列表中存在，如果存在则返回True否则返回False

not in用于判断某个元素不存在与列表中，如果不存在则返回True 否则返回False

remove
根据列表中的元素进行删除
sorted
sorted方法也是用于列表排序，但与sort方法不同的是，sorted函数不会改变原来的列表的顺序，而是返回一个排序后的新的列表
```

## 5.4Python3 元组

Python 的元组与列表类似，不同之处在于元组的元素不能修改。

元组使用小括号，列表使用方括号。

元组创建很简单，只需要在括号中添加元素，并使用逗号隔开即可。

```
删除元组
元组中的元素值是不允许删除的，但我们可以使用del语句来删除整个元组，如下实例:
```

## 5.5Python3 字典

```
字典是另一种可变容器模型，且可存储任意类型对象。
访问字典里的值
类似 js
dict['Name']:  Runoob
dict['Age']:  7

删除字典元素
能删单一的元素也能清空字典，清空只需一项操作
del dict['Name'] # 删除键 'Name'

方法和属性
len(dict)   计算字典元素的个数
str()  输出字典
type()  返回输入的变量类型


1.Python 字典 clear() 函数用于删除字典内所有元素
2.Python 字典 copy() 函数返回一个字典的浅复制。
3.Python 字典 fromkeys() 函数用于创建一个新字典，以序列seq中元素做字典的键，value为字典所有键对应的初始值
4.Python 字典 get() 函数返回指定键的值，如果值不在字典中返回默认值。
5.Python 字典 in 操作符用于判断键是否存在于字典中，如果键在字典dict里返回true，否则返回false。
6.Python 字典 items() 方法以列表返回可遍历的(键, 值) 元组数组。
7.Python 字典 keys() 方法以列表返回一个字典所有的键。
8.Python 字典 setdefault() 方法和get()方法类似, 如果键不已经存在于字典中，将会添加键并将值设为默认值。
9.Python 字典 update() 函数把字典参数 dict2 的 key/value(键/值) 对更新到字典 dict 里。
10.Python 字典 values() 方法以列表返回字典中的所有值。
11.Python 字典 pop() 方法删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值
12.Python 字典 popitem() 方法随机返回并删除字典中的一对键和值(一般删除末尾对)。

如果字典已经为空，却调用了此方法，就报出KeyError异常。
```

## 5.3Python3 集合

```
集合（set）是一个无序的不重复元素序列。
可以使用大括号 { } 或者 set() 函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。

1、添加元素    s.add( x )
2、移除元素   s.remove( x )
3.len(s)  计算集合中的元素
4、清空集合  s.clear()

```

# 六 迭代器和生成器

```
迭代是Python最强大的功能之一，是访问集合元素的一种方式。
迭代器是一个可以记住遍历的位置的对象。
迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。
迭代器有两个基本的方法：iter() 和 next()。
字符串，列表或元组对象都可用于创建迭代器：

>>> list=[1,2,3,4]
>>> it = iter(list)    # 创建迭代器对象
>>> print (next(it))   # 输出迭代器的下一个元素

生成器
在 Python 中，使用了 yield 的函数被称为生成器（generator）。
跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器。
在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回 yield 的值, 并在下一次执行 next() 方法时从当前位置继续运行。
调用一个生成器函数，返回的是一个迭代器对象。
```

# 七Python3 函数

## 7.1函数的写法

```python
 函数代码块以 def 关键词开头，后接函数标识符名称和圆括号 ()。
 **return [表达式]** 结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回 None。 
 
 >>>def hello() :
   print("Hello World!")
 
 
 传入的参数
 加了星号 * 的参数会以元组(tuple)的形式导入，存放所有未命名的变量参数。
 加了两个星号 ** 的参数会以字典的形式导入。
  声明函数时，参数中星号 * 可以单独出现
  
 如果单独出现星号 * 后的参数必须用关键字传入。
  f(1,2,c=3) # 正常
  
  强制位置参数
Python3.8 新增了一个函数形参语法 / 用来指明函数形参必须使用指定位置参数，不能使用关键字参数的形式。

在以下的例子中，形参 a 和 b 必须使用指定位置参数，c 或 d 可以是位置形参或关键字形参，而 e 或 f 要求为关键字形参:
```

 在 python 中，strings, tuples, 和 numbers 是不可更改的对象，而 list,dict 等则是可以修改的对象 

## 7.2匿名函数

```
python 使用 lambda 来创建匿名函数。
lambda 只是一个表达式，函数体比 def 简单很多。
lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
lambda 函数拥有自己的命名空间，且不能访问自己参数列表之外或全局命名空间里的参数。
虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率
```

# 八Python3 数据结构

```
ython中列表是可变的，这是它区别于字符串和元组的最重要的特点，一句话概括即：列表可以修改，而字符串和元组不能。
```

# 九。模块

```
import 语句
想使用 Python 源文件，只需在另一个源文件里执行 import 语句，语法如下
from … import 语句
Python 的 from 语句让你从模块中导入一个指定的部分到当前命名空间中，语法如下
dir() 函数
内置的函数 dir() 可以找到模块内定义的所有名称。以一个字符串列表的形式返回:
__name__属性
一个模块被另一个程序第一次引入时，其主程序将运行。如果我们想在模块被引入时，模块中的某一程序块不执行，我们可以用__name__属性来使该程序块仅在该模块自身运行时执行。
```

# 十正则表达式

```python
Python 自1.5版本起增加了re 模块，它提供 Perl 风格的正则表达式模式。
re 模块使 Python 语言拥有全部的正则表达式功能。


re.match(pattern, string, flags=0)
pattern	匹配的正则表达式
string	要匹配的字符串。
flags	标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。

re.match函数
re.match 尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match()就返回none。

re.search方法
re.search 扫描整个字符串并返回第一个成功的匹配。

```

# 十一 爬虫

```
网络爬虫（Web Spider），又被称为网页蜘蛛，是一种按照一定的规则，自动地抓取网站信息的程序或者脚本。

爬虫流程：

①先由urllib的request打开Url得到网页html文档

②浏览器打开网页源代码分析元素节点

③通过Beautiful Soup或则正则表达式提取想要的数据

④存储数据到本地磁盘或数据库（抓取，分析，存储）
```

```python
一个简单的爬虫
import requests

if __name__ == '__main__':
    target = 'http://www.biqukan.com/1_1094/5403177.html'
    req = requests.get(url=target)
    print(req.text)
    
    if __name__ == '__main__'的意思是：当.py文件被直接运行时，if __name__ == '__main__'之下的代码块将被运行；当.py文件以模块形式被导入时，if __name__ == '__main__'之下的代码块不被运行。
```

