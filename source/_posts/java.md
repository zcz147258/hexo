---
title: Java
date:
updated:
type: "tags"
categories: Java
comments:
description: Java牛逼！
keywords: Java,大数据开发
top_img: https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2756099248,2036703181&fm=26&gp=0.jpg
cover: https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=2756099248,2036703181&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
一.java介绍

```java
Java虚拟机   jvm 可以运行在任何操作系统上面 
jdk     是java 程序开发工具包，包含开发人员使用的工具   开发需要 
jre  java程序运行的环境，包含jvm和运行时候的核心类库	运行需要


jdk =》 包含jre =》 包含 jvm


程序开发步骤说明
	java源程序---->编译源程序-->java字节码文件--->jvm运行
	
	
	编译用 javac 应用程序.java
	运行用  java 应用程序  省略 class
```

# 二.规范

```java
java程序固定
package com.company;

public class Main {//文件名保持一致

    public static void main(String[] args) {//主函数  从这里程序开始执行
	// write your code here
    }
}

```

# 三.数据类型

```java
基本数据类型
	四类八种
		整数
			byte  short  int   long
			1字节  2字节  4字节  8字节
		浮点型
			float double    加后缀
			4字节  8字节
		字符型
			char  2字节
		布尔型
			boolean  1字节
引用数据类型
	字符串
	数组
	类
	接口
	lamda
	
	
	数据范围和字节数不一定相关， float 比 long 广泛
	变量一定要进行赋值
```

## 3.1数据类型转化

### 3.1.1自动转化

```java
隐式转化
	数据范围从小到大    long num = 100; double num2 = 2.5F; float num3 = 30L;
```

### 3.1.2强制类型转化

```java
范围从大到小
	int num = (int)100L;
	
	强制类型转化一般不推荐使用，因为可能发生精度损失，数据溢出
	 char b = 'A';
     System.out.println(b + 1);
     如果char/byte/short/ 类型进行计算的时候，会自动提升为  int 再计算
     
 boolean 不能发生数据类型转化
```

# 四.方法

```java
定义一个方法的格式
	public function viod（）{
        方法体
	}
方法的定义不能嵌套
```

## 4.1定义

```java
定义方法的完整格式
	修饰符 返回值类型 方法名称 （参数，参数）
	public static int sum(int a, int b){
        int result = a + b;
        return result;
	}
```

## 4.2方法的三种调用方法

```java
1.单独调用			方法名称(参数)；
2.打印调用			打印里面调用
3.赋值调用			返回值赋值给另外一个变量

方法应该定义在类当中，方法不能嵌套，
方法定义的前后顺序无所谓
return 后面的返回值类型必须和函数定义的类型一致
对于一个  void 方法类型，不能写return后面的返回值，可以  return；
一个方法可以有多个return值，凡是必须保证只有同一个被执行
```

## 4.3方法的重载

```java
对于功能类似的方法来说，因为参数列表不一样，可以用重载；
overload
多个方法的名字一样，参数有几个那么对应调用有几个参数的方法；


方法重载的注意事项相关
	1.参数的个数不同
	2.参数的类型不同，
	3.参数的多类型顺序不同 那么函数构成重载
	4.和函数名字的大小写有关
	
无关因素
	和参数的名称无关
	与方法的返回值类型无关  函数的返回值无关
	

```



# 五.idea中快捷键

```java
alt + enter  修复错误
ctrl + y;
格式化代码  ctrl + alt + L;
自动生成代码	alt + ins ；
shift + f6 所有相同变量一起变
alt + enter 可以自动生成错误提示代码
```

# 六.数组

```java
数组是一种引用数据类型；
数组当中的多个数据，类型必须统一
数组的长度在数组运行期间不能改变；

数组的定义
	动态初始化指定长度
		int[] arr = new int[300];能放300个数据；其中的元素将会自动拥有一个默认值
		如果是整数，那么就是 0；
		如果是浮点类型 ，那么就是0.0；
		如果是字符类型，那么就是 ‘\u0000’;
		如果是布尔类型，那就是false；
		如果是引用类型，那么就是null；
	静态初始化指定内容
		int[] arr1 = new int[] {5,15,25 };
		
	省略格式：：：静态初始化  
		int[] arr2 = {"name","java"};
		注意事项，int[] arr; arr = new int[]{11,12,13};拆分两个
	静态初始化一旦省略就不能拆分两个步骤；
	
	
	直接打印数组名称，得到的是数组对应的内存地址，哈希值！！后面出现的是16进制；
```

## 6.1同一个数组

```java
产生影响
	int[] arr1 = new int[] {5,15,25 };
	int[] arr2 = arr1;
	
	方法传参，传数组就是 传地址值；
```

## 6.2数组索引越界；空指针异常

```java
数组索引越界
	如果索引不存在，那么就会发生索引越界异常；
空指针异常
	所有引用变量，都可以赋值为以一个null值，但是代表其中什么都没有
```

## 6.3数组方法

```java
打印数组  调用 jdk库 Arrays.toString(arr);
```

## 6.4 Arrays

```java
是一个和数组相关的工具类，里面提供了大量的静态方法；
	toString();  将参数数组变成字符串
	sort();  默认升序，排序  数值按照升序从小到大，如果是字母按照升序
			如果是自定义类型，那么这个自定义类型需要comparable接口的支持
```



# 七.java的内存

```java
划分为五个内存；
1.栈内存  stack ： 存放的都是方法中的局部变量
				局部变量，就是{}内部的变量；
				作用域，一旦超出作用域；立刻从栈内存中消失；
				方法的运行都是在栈当中
2.堆内存 heap  ; 凡是new出来的东西，都在堆内存中间
				堆内存里面的东西都有一个地址值
				堆内存里面的数据都有一个默认值
                    如果是整数，那么就是 0；
                    如果是浮点类型 ，那么就是0.0；
                    如果是字符类型，那么就是 ‘\u0000’;
                    如果是布尔类型，那就是false；
                    如果是引用类型，那么就是null；
 3.方法区： 存储class相关信息，包含方法信息
 4.本地方法栈  与操作系统相关
 5.寄存器  与CPU相关
				
				
				
	类是对象的模板，对象是类的实体
```

# 八.类

```java
定义类   
		定义在方法区
		属性（是什么）	姓名 年龄    具体保存在堆里面
		行为（能做什么）学习  吃饭 睡觉   具体保存在堆里面
    对应到 java的类中
		成员变量，（属性）
		成员方法（行为）public void eat(){}  没有static
		
		public class Student{
            String name;
            int age;
            public void eat(){};
            public void sleep(){};
            public void study(){};
		}
		
		注意： 成员变量直接定义在类中，
				成员方法不要写 static 关键字
				
		通常情况下，一个类不能直接使用，需要根据一个类来实现，
			1.导包，			import   包名称.类名称 同一个包可以省略导包语句
			2.创建，			Student stu = new Student();
			3.使用			
				两种情况
						使用成员变量	对象.变量名
						使用成员方法	对象.方法名
						
						
						
	压栈
		方法执行在栈中，成员变量直接存储在堆中，成员方法的地址存在堆中，运行找到地址，然后去方法区里面找方法，压栈到栈内存中开始执行
```

## 8.1变量的区别

```java
定义的位置不一样  
	局部变量 方法内部
	成员变量 在方法的外部，直接写在类中
作用范围不一样
	局部变量	只有方法当中才可以使用
	成员变量	整个类都可以用
默认值不一样
	局部变量	没有默认值 必须手动赋值
	成员变量	如果没有赋值，规则和数组一样 
```

## 8.2面向对象三大特征 封装

```java
在java中的体现
	1.方法就是一种分装
	2.关键字private也是一种封装
	
	无法阻止不合理的数值设置进来，用private关键字将需要保护的成员变量修饰
	一旦使用private进行修饰，在本类中可以随意访问，但是超过了本类范围之外就不能访问
	private关键字的使用
	
		只能通过间接访问，间接访问必须是setxxx或者getxxx get不能有参数，set不能有返回值
			访问方法修改属性
	注意事项
		对于基本数据类型当中的  布尔类型 get方法一定要写成 isxxx的方法
```

## 8.3 this

```java
当方法的局部变量和类的成员变量重名的时候，根据就近原则，优先使用局部变量
如果需要访问本类的变量，需要使用格式
	this.成员变量名 
	注意： this 一定是写在方法内部的
				通过谁调用的方法，就是谁的this
				
				
	this的用法
		访问本类内容
		1.在本类的成员方法中访问本类的成员变量
		2.在本类的成员方法中访问本类的另一个成员方法
		3.在本类的构造方法中访问本类的另一个构造方法 只能调用一个构造
		super和this两种构造调用，不能同时使用
```

## 8.4构造方法

```java
构造方法是专门用来创建对象的方法，当我们用关键字new来创建对象的时候，其实就是在调用构造方法
	格式
		public 类名字（参数类型 参数名称）{
            方法体
		}
	注意
		构造方法的名称必须和类名一致
		构造方法不要写返回值类型，连void都不用写
		构造方法不能return返回值
		如果没有编写构造方法，那么就会默认生成一个构造方法，内容为空，参数为空
		构造方法也是可以重载的
		
		public class Different {
            /*构造方法*/
            private String name;
            private int age;
            public Different(String name, int age){
                this.name = name;
                this.age = age;
            }
            public int getAge(){
                return age;
            }
            public String getName(){
                return name;
            }
        }
        
        调用
        	public class Constru {
                public static void main(String[] args) {
                    Different one = new Different("赵丽颖",18);

                    System.out.println( one.getAge());
                    System.out.println( one.getName());

                }

标准的类
	1.所有成员变量都要使用private关键字修斯
	2.为每一个成员变量添加getter/setter方法
	3.编写一个无参数的构造方法
	4.编写一个全参数的构造方法
	
	也叫做 java bean 
	编辑器自动生成
```

## 8.4面向对象三大特性 继承

```java
继承是多态的前提  继承主要解决的问题就是  共性抽取
	
	java继承的三个特点
		1.一个类的直接父亲只有唯一一个
		2.java可以多级继承
		3.一个父类可以拥有很多个子类
	
	
	父类 基类 超类 

	子类 派生类
	
	继承的格式
		定义子类 public class 子类名称 extends 父类名称{
            
		}
		在父子类的继承关系中，如果成员变量名称重名，则创建子类对象时候，有两种方式
			直接访问 通过子类对象访问成员变量  等号左边是谁，就是谁
			间接访问 通过成员方法访问  看方法属于谁，是谁创建的
			
			
			访问变量
				num   局部变量
				this.num 本类的成员变量
				super.num 父类的成员变量
			访问方法
				创建的对象是谁，就优先使用谁，如果没有那就向上找
		
	方法的重写  创建的是子类对象，那就优先用子类方法
			1.重写 方法的名称一样，参数列表也一样
			重载 方法的名称一样，参数列表不一样
			
			检测重写 @Overide 用来检测是不是正确有效的重写 写到函数上面
			
			2.注意事项 ：子类方法的返回值必须小于等于父类方法的返回值范围
			
			3.子类方法的权限必须大于等于父类的权限修饰符
			public > protected > (default) > private
			
	构造方法父子类访问特点
		1.父类构造方法先执行，子类构造方法后执行 赠送一个super执行  无参数
		2.可以通过super关键字来子类构造父类 重载构造   
			有参数需要 用super(params)  调用
		3.super的父类构造调用，必须是子类构造方法的第一个语句
			只有子类构造方法才可以调用父类构造方法
			super构造只能调用一次
```

## 8.5 super

```java
  super关键字的三种用法
  	1.在子类的成员方法中，访问父类的成员变量  
    2.在子类的成员方法中，访问父类的成员方法
    3.在子类的构造方法中，访问父类的构造方法
```

## 8.6抽象 方法abstract

```java
// 抽象类
public abstract class Animal{

    实例 public abstract void eat(); //抽象方法java
    
}
如何使用抽象类抽象方法
	1.不能直接new抽象类对象
	2.必须用一个子类来继承抽象父类
	3.子类必须覆盖重写抽象父类当中的所有抽象方法；
		子类去掉抽象方法的abstract关键字，然后补上方法体大括号
	4.创建子类对象进行使用
注意事项
	1.抽象类不能创建对象
	2.抽象类中，可以有构造方法
	3.抽象类中，不一定包含抽象方法
	4.抽象类的子类，必须要重写抽象父类中所有的抽象方法

```

## 8.7 Object

```java
是类的根类 
	方法
		toString();
			直接打印的是对象的名字，其实就是调用object的tostring方法
			可以重写 toString方法
			
		equals(); 比较两个对象是否相等
			重写equals（）方法比较 属性值
			向下转型
				this.name.equals(obj.name)
```

## 8.8 Objects

```java
Objects.equals(obj1,obj2)  
可以避免空指针调用
```

## 8.9可变参数

```java
当方法的参数列表数据类型已经确定，但是参数的个数不确定，我们就可以使用可变参数

修饰符 返回值 方法名 (数据类型...变量名)
	底层原理是一个数组，根据传递参数的长短，创建不同长度的数组，来存储这些参数
	public static int add(int...arr){
        sout(arr)
	}
	
	注意
	1.，一个方法的参数列表，只能有一个可变参数
	2.如果方法的参数有很多个，那么可变参数必须写在参数的末尾	
```



# 九. api的使用

## 1.键盘输入Scanner

```java
引用类型
	1.导包
		import java.util.Scanner;
		只有java.lang包不需要导包
	2.创建
		代表从键盘输入
		Scanner sc = new Scanner(Syetem.in);
	3.使用
		int num = sc.nextInt();键盘输入的都是字符串，但是这个方法可以转化
```

## 2.random

```java
	1.导包
		import java.util.Random;
		只有java.lang包不需要导包
	2.创建
		代表从键盘输入
		Random sc = new Random();
	3.使用
		int num = sc.nextInt();不带参数，指的是所有范围
		int num = sc.nextInt(3);  指的是【0，3)  左闭右开
```

## 3.math

```java
java.utils.Math是数学相关的工具类
Math.abs() 绝对值
Math.ceil() 向上取整
Math.floor() 向下取整
Math.round() 四舍五入
```



# 十.匿名对象

```java
		new Hello().name = "赵又廷";
        System.out.println(new Hello().name);
        
        匿名对象只能使用一次，这里创建了两个值
        
        匿名对象作为方法的参数
        匿名对象作为返回值
```

# 十一.,集合

```java
1.定义一个数组，用来存放对象 集合可以
2.什么是arraylist 和普通数组的区别是可以在运行中变换长度

只能存  引用类型；

ArrayList<String> list = new ArrayList<>();
创建了一个ArrayList集合，里面装的都是String类型；

而且打印出来不是地址值，而是内容

Java中的集合框架大类可分为Collection和Map；两者的区别：
1、Collection是单列集合；Map是双列集合
2、Collection中只有Set系列要求元素唯一；Map中键需要唯一，值可以重复
3、Collection的数据结构是针对元素的；Map的数据结构是针对键的。

如果有泛型，不使用时，参数的类型会自动提升成Object类型，如果再取出来的话就需要向下强转，就可能发生类型转化异常(ClassCaseException)；不加泛型就不能在编译期限定向集合中添加元素的类型，导致后期的处理麻烦。


实现带有泛型的接口类型：
	1.public class GenericImpl1 implements GenericInter<String> {}
	2.public class GenericImpl2<T> implements GenericInter<T> {}
使用泛型的注意点:
	1、泛型不支持基本数据类型
	2、泛型不支持继承，必须保持前后一致（比如这样是错误的：List<Object> list = new ArrayList<String>();
	
	
```

## 11.1ArrayList

```java
元素增删慢，查询快，最常用，多线程

list.add("赵丽颖");往最后加一个内容
list.get(2)  返回索引值对应的
list.remove(3)  删除的索引对应，原来的集合就没了
list.size()  得到长度
```

## 11.2包装类

```java
如果希望向集合ArrayList中存储基本数据类型，必须使用基本类型对应的包装类
包装类都位于 java.lang包下面

	Byte Short Integer Long Float Double Character Boolean
	
	ArrayList<Integer> list = new ArrayList<>();
	
	
	基本数据类型的数据，没有对应的方法来操作这些数据，
		我们使用一个类，把这些基本数据类型包装起来，叫做包装类
	
	自动装箱	基本类型---->包装类型
	自动拆箱	包装类型---->基本类型
	
	基本类型转化 字符串
			1.toString() 
			2.+
			3.valueOf()
	字符串转化为基本类型
	
		Integer.parseInt()
	
	
```

## 11.3集合

```java
集合和数组的区别
	arraylist就是一个集合
	1.数组的长度是固定不变的，集合的长度是可变的
	2.数组中存储的都是同一个类型的元素，可以存储基本数据类型
		集合存储的都是对象，而且对象的类型可以不一致，
		在开发中，当对象比较多时候，可以使用集合进行存储
		
		
	分类 
			1.Vector集合		了解
			2.ArrayList集合	重点			前三个都是List接口
			3.Linkedlist集合		次之
			4.TreeSet集合		了解
			5.HashSet集合		重点			后三个都是三个Set接口
				5.1.LinkedHashSet  次之
	接口
			1.List接口
				有序的集合，取出和存储的顺序一致
				允许存储重复的元素
				有索引，可以使用for循环遍历				抽取共性得到Collections接口
			2.Set接口
				不允许存储重复元素
				没有索引
				无序的集合
    学习目标
            1.会使用集合存储数据
            2.会遍历集合，把数据取出来
            3.掌握每一种集合的特性
```

## 11.4集合的方法

```java
1.arrayList  底层是数组实现的  查询快，增加删除慢
2.linkedlist 底层是链表实现的，查询慢，增删快
3.hashset  底层是哈希表，红黑树实现的，无索引，不可以重复储存，存储无序
4.linkedHashset 底层是哈希表加链表实现的，无索引，不能重复存储，可以保证存储顺序
5.treeset 底层是二叉树实现的，一般用于排序

add()  向集合中添加元素
remove()  删除集合中某个元素
clear()  清空集合中所有的元素
contains()  判断集合中是否包含某个元素
isEmpty()  判断集合是不是为空
size()    获取集合的长度
toArray()  将集合转化成一个数组  返回的数组是一个object类型的数组
```

## 11.5 iterator迭代器

```java
迭代的概念
	再取出元素之前判断集合之中有没有元素，如果有，就把这个元素取出来，然后继续判断，如果还有那么继续取；
	这种专业术语成为迭代
	
	通过集合接口中 interator()来返回实现类对象
	
	两个常用方法
		hasNext()  集合中还有没有下一个元素，返回布尔值
		next()  返回迭代的下一个元素
		
	迭代器的泛型跟着集合走，集合什么泛型，迭代器就是什么泛型
	Iterator<String> it = coll.iterator()   //多态
	it.hasnext()  判断有没有元素
	it.next();
	没有元素再取出元素就会抛出异常
```

## 11.6增强for循环  foreach

```java
格式
	for(集合/数组  变量名：集合名/数组名){
        变量名
	}
	
	for(int[] i:arr){
        
	}
```

## 11.7泛型

```java
是一种位置的数据类型，不知道使用什么数据类型的时候，使用泛型
泛型也可以看作一个变量，用来接收数据

	E；未知的数据类型 
		创建集合的时候，E就确定为 字符串
		
		
	使用泛型的好处
		1.集合不使用泛型，默认就是Object，可以存储任意的数据类型；但是不安全
		2.避免了向上向下类型的转化，
		3.把运行期的异常提到了编译期
		
	定义和使用含有泛型的类，方法，
		含有泛型的方法，再调用方法的时候确定泛型
		传递什么类型的参数，泛型就是什么
		
		public class classfanxing<E> {
            private E name;

            public E getName() {
                return name;
            }

            public void setName(E name) {
                this.name = name;
            }
        }
        
          public <E> void method(E e){
          	System.out.println(e);
          }
          public static <N> void methods(N n){
          	System.out.println(n);
          }
          
          
          泛型接口
          	第一种
          	public class fanxingimpl implements fanxing22<String>{
            	@Override
           		 public void method(String s) {

            	}
            }
            
            第二种 
            	接口使用什么泛型，实现类就因该是什么泛型，类跟着接口走
            	public class fanxingimpl<String> implements fanxing22<String>{
                    @Override
                     public void method(String s) {

                    }
                }
            	
          
         泛型通配符
         	不知道使用什么类型来接受的时候，可以使用 ？ 表示未知通配符
         	此时只能接收数据，不能往集合中传递数据
         	泛型是没有继承概念的
```

## 11.8数据结构

```java
栈  
	先进后出 压栈  弹栈   进123   出321
队列
	先进先出  进123   出123
数组
	查询快，增删慢  因为数组的地址是连续的；慢是因为数组的长度是固定的
链表
	查询慢，增删快	地址不是连续的，每次查询从头开始；快是因为堆整体结构没有影响
		一个节点分为三部分  存储前一个节点地址，一个存储数据，一个存储后一个节点
	单项链表  不能保证顺序
	双向链表	一个存储顺序，另外一个是一个有序的集合
红黑树
		二叉树上面
	排序树
		 左子树小，右子树大
		 
	平衡树
		左孩子，右孩子相等
	不平衡树
		左孩子不等于右孩子
	红黑树
		趋近于平衡树，查询速度快，查询叶子节点最大次数和最小次数不能超过二倍
		约束条件
			1.节点可以是红色或者黑色
			2.根节点是黑色
			3.叶子节点是黑色的
			4.每个红色节点的子节点都是黑色的
			5.任何一个节点到其每一个叶子节点的路径上的所有黑色节点相同
```

## 11.9 List

```java
1.有序的集合  存储 123  取值 123
2.有索引，包含了一些带索引的方法
3.允许存储重复的元素
```

## 11.10 linkedList

```java
是一个双向链表，是一个链表结构，查询慢，增删快；多线程
有大量操作首位元素的方法
不能使用多态
```

## 11.11 Vector

```java
底层结构也是一个数组，单线程
```

## 11.12 HashSet

```java
1.哈希表结构
2.没有顺序，无序结构
3.没有索引，没有带索引的方法
4.存储和取出的速度不一样，是一个无序的集合
5.查询的速度比较快

// 要让哈希表存储不重复的元素，就必须重写hasCode和equals方法
	哈希值
		是一个十进制的整数，有系统随机给出，是一个模拟逻辑地址
		Object下面有一个方法，可以获取哈希值
		native 是代表该方法调用本地操作系统的方法
		
		
	哈希表
		！！！就是数组加链表或者数组加红黑树
		
		把元素进行了分组，哈希值相同的元素是同一组，链表红黑树把哈希值相同的元素存到一起
		如果链表的长度超过了8为，那么就会把链表转化为红黑树 提高查询速度
		先计算哈希值，然后存储会调用 equals方法
		
		
	使用 HashSet 来存储自定义元素，
		所以需要重写 hascode方法  和  equals方法
```

## 11.13 linkedHashSet

```java
底层是一个哈希表  和 链表  多了一条链表  用来记录元素的存储顺序

相比HashSet  是一个有序的集合
```

## 11.14 集合工具类的方法

```java
Collections.addAll("a","b","c","d");  往集合中添加多个元素
Collections.shuffle(list)    打乱集合
Collections.sort(list)   排序 从小到大  注意 只能是 list接口的实现类
		这个方法 自定义类使用前提 必须重写接口 comparable 方法
			this.getAge() - O.getAge()   按照年龄升序
		comprator
			Collections.sort(list,new comprator<Integer>{
                //重写比较规则
			})
			
			
		可以组合排序 设置第二个排序的字段
```

## 11.15 Map集合

```java
每一个元素包含两个值，也叫做双列集合
	键值对
		1.键不能重复，值可以重复
		2.key 和 value 的数据类型可以相同也可以不同
		3.key 和 value 是一一对应的 
		
		Hashmap集合
			1.底层是哈希表，查询速度特别快
			2.是一个无序的集合，存储和取出元素的顺序不一致
		linkedhashmap的特点
			1.底层是哈希表加链表
			2.是一个有序的集合，保证迭代的顺序
			
	常用方法
		put(key,value)
		get()
		remove()
		containskey()   判断是否包含 key
		
		
		遍历
			keyset()
				把map集合中的所有的key取出来存储到Set()集合中
				使用迭代器/增强for循环来遍历，获取到每一个key
				然后通过get(key)获取值
			entryset()
				在map中有一个内部接口 entry，
				当map集合创建的时候，就会在map集合中创建一个entry对象，用来记录键和值
				
				遍历的时候会把map内部的多个entry对象取出来，存储到一个Set集合中，遍历set
				然后使用 entry的  getkey()  getvalue();
				
				
			存储自定义类键值对
```

## 11.16 linkedhashmap

```java
底层原理
	哈希表 + 链表
	可以保证顺序，存储顺序一致
```

## 11.17 hashtable

```java
是一个个哈希表
	1.不能存储  空对象  null
	2.单线程同步，是一个安全的集合
	
	
	properties集合是他的子类
```

## 11.18 jdk9 新增对集合

```java
新增了一个 静态的方法  of，可以给集合一次性添加多个元素
1.of方法只适用于  List,Map,Set接口，不适用于接口的实现类
2.of方法的返回值是一个不能改变的集合
3.Set接口和map接口在调用 of 方法的时候，不能有重复的元素

	List.of("a","b","c","d","e“);
```



# 十二.字符串

```java
字符串的特点
	1.字符串的内容不可改变
	2.正因为字符串的内容不可以改变，所以字符串是可以共享使用的
	3.字符串效果上是相当于char[]字符数组，但是底层原理是字节数组byte	[]
```

## 12.1创建字符串

```java
三种构造方法
		public String(); 创建一个空白字符串，不含有任何内容
			String str = new String();
		public String(char[] array); 根据字符数组的内容，来创建
			char[] charArray = {‘A’,'B','C'};
			String str = new String(charArray);
		public String(byte[] array); 根据字节数组的内容，来创建
			byte[] charArray = {97,98,99};
			String str = new String(charArray);
一种直接创建
		String str = "Hello"  直接写上，照样是字符串对象
```

## 12.2字符串的常量池

```java
！！！！在堆当中
程序当中直接写上的双引号字符串，就在常量池中；
对于基本数据类型，是值的比较
引用类型来说 是地址的比较 
```

## 12.3字符串的方法

```java
str1.equals(str2);   比较两个值是不是一样  只有参数是一个字符串并且值相等才会相同
	注意事项 1.具有对称性  a,b互相比较一样
			2.常量变量  "hello".equals(a); 推荐  反过来会报错
str1.equalsIgnoreCase(str2)  忽略大小写 


str1.length();  返回字符串的长度；
str1.concat(str2);  将两个字符串拼接并且返回新的字符串；
str1.charAt(1)  返回索引位置的单个字符；
str1.indexOf('a'),查找小字符串在本来字符串当中的第一次的索引位置 

字符串的截取方法
str1.substring(index);  截取参数位置到结束位置
str1.substring(a,b);	截取 a,b中间的字符串


转化：：：
str1.toCharArray();  将当前字符串拆分成为字符数组的返回值；
str1.getBytes(); 获取当前字符串的底层字节数组；
str1.replace(old,new);

分割：：：
str1.split(regex); 按照参数的规则，将字符串分成若干部分；返回一个数组；
注意事项 如果按照英文 .  进行分割，那么需要“\\.”才可以分割
```

# 十三.权限控制

## 13.1 static

```java
静态关键字
	一旦使用了static关键字，那么这样的内容不再属于对象自己，而是属于类的，凡是本类的对象，dou共享同一份数据
	
	关键字 static修饰成员变量的时候，
		privat static int idCounter = 0;学号计数器
		静态变量也可以通过对象名进行调用，也可以通过类名直接调用
	修饰成员方法
		静态方法：静态方法不属于对象，而是属于类的
			对于静态方法来说，可以通过对象名进行调用，也可以通过类名直接调用
			推荐用 类名进行调用
			对于本类当中的静态方法，可以省略类名
		注意方法：1. 静态方法不能访问非静态
					因为在内存里面现有的静态内容，然后有非静态内容
				2.静态方法中不能使用 this
				
				
方法区里面有一个静态区 静态变量和静态方法在里面

	静态代码快 
		第一次用到本类是，静态代码块执行唯一的一次
		静态代码快比构造方法先执行
		static{
            
		}
```

## 13.2 final

```java
1.可以用来修饰一个类
	当前这个类不能有任何的子类，一定有父类  public final class 名称  {}；
	其中所有的方法都不能覆盖重写
2.可以用来修饰一个方法
	这个方法就是最终方法，不能被覆盖重写
	对于类方法，不能同时使用 abstarct 和 final；
3.可以用来修饰一个局部变量
	一次赋值，终身不变
	保证有唯一一次赋值
	int num; num = 100; 正确
	对于基本数据类型来说，说的是值不变；
	对于引用数据类型来说，说的是引用地址不变
4.可以用来修饰一个成员变量
	这个声明变量不可变，但是成员变量具有默认值，这也算赋值，final必须手动立马赋值
```

## 13.3四种权限修饰符

```java
			public   >  protected > (default)  >  private
同一个类 		Y          Y			Y			Y
同一个包		Y			Y			Y			N
不同包子类		Y			Y			N			N
不同包非子类		Y			N			N			N

```



# 十四.interface

```java
接口就是多个类的公共规范
	接口就是引用数据类型，最重要的就是抽象方法
	
	定义一个接口
		如果是java7,接口可以包含 
			1.常量
			2.抽象方法
		如果是java8，还可以包含
			3.默认方法
			4.静态方法
        如果是java9,还可以包含
        	5.私有方法
        	
    
       
```

## 14.1接口抽象方法

```java
 接口注意事项
     		1.必须修饰符 有 public abstract
            2.可以省略
            
     public interface inerface {
            public abstract void methods();
        }
        注意事项
       1.接口不能直接使用，必须有实现类来实现接口
       2.接口的实现类必须覆盖重写(实现)接口中的所有抽象方法，去掉abstract，加上大括号
       
       抽象方法：：：：：
       		//        创建实现类的对象
        	myInterface imp1 = new myInterface();
        	imp1.methods();
```

## 14.2接口默认方法

```java
 默认方法：：：
        	是为了解决接口升级的问题，比如新添加抽象类
        	默认方法会被实现类继承下去
        	public default void methods2(){
        
   			 }
   			 可以直接调用，默认方法会被继承下去
        	注意事项
        		1.接口的默认方法，可以通过接口实现类直接调用
        		2.接口的默认方法，也可以被接口实现类进行覆盖重写
```

## 14.3接口的静态方法

```java
简单定义
	public static 返回值类型 方法名称（参数列表）{
    
	}
	1.不能用实现类对象调用接口当中的静态方法
	2.通过接口调用，直接调用静态方法
	interface.methods();
```

## 14.4接口的私有方法

```java
问题描述，解决重复代码的问题，不应该让实现类使用，应该实现私有化
1.普通私有方法 解决多个默认方法之间的重复代码问题
	private 返回值类型 方法名称（参数列表）{
        
	}
2.静态私有方法	解决多个静态方法之间重复代码问题
	private static 返回值类型 方法名称（参数列表）{
	}
```

## 14.5接口的常量的定义和使用

```java
接口当中也可以定义 ‘成员变量’，而且必须由三个关键字修饰 public static final
	一旦使用final变量，那就不能改变
	1.可以省略这三个关键字，但是照样是这样；
	2.接口当中的常量，必须进行赋值，不能不赋值；
	3.不能变的常量，尽量使用大写
```

## 14.6继承父类并且实现多个接口

```java
1.接口是没有静态代码块或者构造方法的
2.一个类的父类是唯一的，但是一个类可以实现多个接口
3.如果实现类中的多个接口中，存在相同的抽象方法，重写即可，；
4.如果实现类中没有实现重写覆盖所有接口的所有抽象方法，那么实现类必须是一个抽象类
5.如果实现类实现的多个接口中，存在重复的默认方法，这种情况下一定要进行覆盖重写
6.优先级：一个类直接父类的方法和接口中的默认方法，产生了冲突，会优先用父类中的方法
```

## 14.7接口之间的多继承

```java
1.类和类之间是单继承的，直接父类只有一个
2.类与接口是多实现的，一个类可以实现多个接口
3.接口和接口之间是多继承的
	接口可以继承接口；
	如果接口继承的父接口的抽象方法重复，没关系
	如果接口继承的父接口的默认方法重复，有关系，子接口必须进行父接口默认方法的重新，带defult
```

## 14.8 面向对象三大特性 多态

```java
extends继承和 implements实现，是多态性的前提
1，需要有继承关系的存在。
2，需要有方法的重写。
3，需要有父类的引用指向子类对象。
	
	一个对象有多种形态，这就是对象的多态性
	代码体现多态性， 父类引用指向子类对象
	
	父类名称 对象名 = new 子类名称();
	接口名称 对象名 = new 实现类名称();
	
	方法
	可以调用子类父类的方法
		！！！！同一个方法，看等号右边
		
		
	成员变量
		1.直接通过对象名称访问成员变量，看等号左边是谁，谁就优先，没有那就想上找
		2.间接通过成员方法调用
		
		
	成员方法
		1.看new是谁，没有那就想上找父类
		2.编译看左边，运行看右边
		
	当超类类变量引用子类对象
				访问成员变量时：访问的是父类的成员变量
				访问成员方法时：先访问的是超类的此方法，如果此方法被子类覆盖，则调用子类的方法。并且不能访问子类特有的方法
```

## 14.9使用多态的好处

```
用了多态，等号左边统一，
无论右边换成那个子对象，等号左边的调用方法不会变化
```

## 14.11向上转型和向下转型

```java
向上转型
	其实就是多态写法，创建一个子类对象，当作一个父类来看待使用；

	注意事项： 向上转型一定是安全的 小范围转向了大范围；
			一但向上转型为父类，那么就无法调用子类原本特有的内容
向下转型
	其实是一个还原动作
		子类名称 对象名 = （子类名称）父类对象；
	将父类对象还原为原来的子类对象
		Animal animal = new Cat();  向上转型
		Cat cat = (Cat) animal;		向下转型
		
		注意事项
			1.必须保证对象本来创建的时候是猫，才能向下转型为猫
			2.如果不是那么就会报错
			
			
判断一个父类引用的对象，本来是什么子类
	instance
		对象 instanceof 类型 ：会得到到Boolean判断，
		animal instanceof Dog	false
		animal instanceof Cat  true
		
		
	实现计算机 键盘 鼠标 接口USB
		  Computer computer = new Computer();
                computer.powerOn();

        //        创建完毕计算机，准备鼠标键盘
                mouse ms = new mouse();
                /*向上转型*/
                Usb usbmouse = new mouse();
                computer.useDevice(usbmouse);

                //创建一个usb键盘
                keyboard kb = new keyboard();
                computer.useDevice(kb);//这里发生了向上转型

                computer.powerOff();
                
                
                 public void useDevice(Usb usb){
                    usb.open();
                    if(usb instanceof mouse){
                        mouse ms = (mouse) usb;
                        ms.click();
                    }else if (usb instanceof keyboard){
                        keyboard kb = (keyboard) usb;
                        kb.input();
                    }
                    usb.close();
                }
```

# 十五.内部类

```java
如果一个事物包含另外一个事物，那么就是一个类包含另外一个类

分类 1.成员内部类
	2.局部内部类（包含匿名内部类）
	
	
			
			
		
```

## 15.1成员内部类

```java
内部类
		修饰符 class body{  //外部类
            修饰符 class heart{  //成员内部类
                public void heart(){
                    
                }
            }
		}
		
	如何使用成员内部类？
		1.间接方法：在外部类的方法中，使用内部类，然后main只是调用外部类的方法
			在外部类的方法中，
				new heart().beat();
				通过外部类对象，调用外部类方法，里面间接使用内部类Heart
		2.直接调用	外部类名称.内部类名称  对象名 = new 外部类名称().new 内部类名称()
			body.heart  ht = new body().new heart
			
		访问变量
			内部类的方法局部变量 直接  num
			内部类的成员变量   this.num;
			外部类的成员变量   外部类名.this.num;
```

## 15.2 局部内部类

```java
如果一个类是定义在一个成员方法内部的，那就是一个局部内部类
public void method(){
    class heart(){ //局部内部类
        
    }
}
	调用局部内部类的方法，在方法内部使用 new 创建一个对象，然后这个对象调用方法；
	主函数调用外部方法；
	
	注意事项 ：
			1.外部类		public/default
			2.外部内部类		四种修饰符都可以
			3.局部内部类  	什么都不能写
			
			如果希望访问所在方法的局部变量，那么这个局部变量必须是 有效 final的
			原因是因为 
				class对象的生命周期比方法的成员变量的生命周期更加长
```

## 15.3匿名内部类

```java
如果接口的实现类(或者父类的子类)只需要使用唯一的一次；
那么这种情况下就可以省略掉 该类的定义，而改为使用  匿名内部类

	定义格式
		接口名称 对象名 = new 接口名称(){
            //覆盖重写所有的接口方法
		};
		
		
	注意事项
		1.匿名内部类在创建对象的时候只能使用唯一一次
		2.如果省略了对象名称 直接 new  ，就只能调用一次
```

## 15.4类，接口作为成员变量类型

```java
可以把匿名内部类 类对象，接口实现 传入 函数方法里面
也可以当作返回值 参数
```

# 十六.时间日期类

```java
java.util.Date
	构造方法
		System.cunrrentTimeMillis()  计算时间原点到现在经历了多少毫秒
		Date date = new date();
		Date date = new date(long date);
	成员方法
		getTime()当前日期转化为毫秒
	
```

## 16.1 DateFormat类

```java
java.text.Dateformat
	返回指定格式日期
		SimpleDateformate sdf = new SimpleDateformate('yyyy-MM-dd HH:mm:ss')
		Date date = new Date();
		sdf.format(date)
	
```

## 16.1 Calendar类

```java
Calendar c = Canlendar.getinstance();

	c.get()返回给定日历的字段
	c.set()给指定的日历字段设置值
	c.add() 增加日期
```

## 16.2 System类

```java
1. currentTimeMillis() 返回以毫秒为单位的当前时间
2. arraycopy() 将数组中指定的数据拷贝到另外一个数组里面
```

## 16.3 StringBuilder类

```java
字符串的相加，内存就有多个字符串，效率低下
	字符串缓冲区： 提高字符串的操作效率
				可以看作一个长度变化的字符串；底层没有final修饰
				
				
	append()  添加任意数据类型的字符串形式，并且返回当前对象自身  可以链式操作
	tostring()  将stringBuilder 转化为  Strin对象
```

# 十七.异常

```java
语法不是语法错误，
throwable
		1.error  错误
			非常严重
		2.exception  异常  编译器异常
			runtimeexception 运行期异常
		
		1.抛出异常
				虚拟机执行，中断程序
		2.try catch
				抛出数组，后面代码继续执行
				
				
		try{
            可能会出现异常的代码
		}catch(Exception e){
            出现异常解决
            sout  e
		}
		
		
		jvm会检测出程序的异常
			1.会根据异常产生的原因创建一个异常对象，这个对象包含个原因，内容，位置
			2.在方法中没有异常处理逻辑，那么jvm就会把异常对象抛出给方法的调用者Main 来处理
			3.main收到异常对象，但是也没有处理机制，就会给jvm处理4
			4.jvm会把异常对象打印在控制台，终止当前的运行程序
```

## 17.1 throw

```java
使用格式
	throw new Exception("异常产生的原因”);
注意
	1.throw 必须写在方法的内部
	2.throw 关键字后面的对象必须是Exception或者他的子类对象
	3.我们必须处理这个对象
	
	例如
		if(arr ==null){
            throw new nullpointerexception(“传递的数组是空”)
		}
		
		
		非空判断
			Object.requireNonnull(obj)  判断空指针异常
```

## 17.2 throws

```java
异常处理的第一种方法
	
	注意事项 1.必须写在方法声明处
			2.声明的异常必须是 Exception或者Exception的子类
			3.如果方法内部抛出了多个异常，throws必须声明多个异常
				如果抛出多个异常对象有子类父类关系，直接交给父类
			4.调用了一个声明抛出异常的方法，必须处理
			
			
			方法  throws 异常类型{
                throw new 异常类型
			}
```

## 17.3 try catch

```java
	try{
            可能会出现异常的代码
		}catch(Exception e){//定义一个变量接受异常对象
            出现异常解决
            sout  e
            //一般异常会记录到一个日志中
		}
		
	1.try会抛出多个异常，那么就可以使用多个catch来处理这些异常
	2.如果try中产生了异常，就会执行catch的异常处理逻辑
	
	
	throwable定义了三个异常处理的方法
		e.getmessage() 返回详细消息字符串
		e.tostring()	返回简短描述
		e.printstacktrace()  jvm打印对象，最详细
```

## 17.4 final代码快

```java
如果有一些代码 无论是否发生异常，都需要执行，一定会执行
	try{
        
	}catch(){
        
	}finally{
        
	}
	
	注意事项  1.不能单独处理
			2.一般用于资源释放，无论资源是否异常，都要资源释放(IO)
			
		finally不要写 return
```

## 17.5多异常处理

```java
1.多个异常，多次捕获，分别处理
		一个异常一个try catch
2.多个异常，一次捕获，多次处理
		写一个try 多个catch
		
		注意一场变量如果有子父类关系，子类必须在上面
3. 多次异常一次捕获，一次处理
	
	
	
	子父类异常
		1.如果父类抛出了多个异常，子类重写父类方法时候，抛出和父类相同的异常或者是父类异常的子类或者不抛出异常
		2.父类没有抛出异常，子类重写父类该方法时候也不能抛出异常，此时
			子类异常，只能捕获处理，不能声明抛出
```

## 17.6自定义异常类

```java
格式
	public class xxxException extends Exception/runtimeException{
        添加一个空的构造方法
        添加一个带异常信息的构造方法
	}
```

# 十八.多线程

```java
并发和并行
	并发：指的是两个或者多个时间在同一个时间段发生，交替执行
	并行：指的是两个或者多个事件在同一时刻发生，
	
线程进程
	线程 线程是进程的执行单元，一个进程至少有一个线程，应用程序到cpu的路径
	进程 一个内存中运行的程序，进入到内润的叫进程
	
线程调度
	分时调度
		所有线程轮流使用CPU的使用权，平均分配每一个线程占用的cpu时间
	抢占式调度
		优先让优先级高的线程使用cpu，如果优先级相同，会随机选择一个(线程随机性)，java为抢占式调度；
		线程的优先级可以设置
```

## 18.1主线程，多线程

```java
主线程：执行主线程的程序
单线程程序 java只有一个单线程
从main开始执行
	
	Thread类
		1.创建一个他的子类，
		2.在这个类中重写 run 方法，设置线程任务
		3.创建thread类的子对象
		4.调用类中的方法  start，开启新的线程
			多次启动一个线程是非法的，特别是当线程已经结束之后，不能在重新执行
			
	
            
            
	获取当前执行的线程  Thread.currentThread()
	
	设置线程的方法
		1.thread类中的 setname();
		2.创建一个带参数的构造方法，调用父类的  super方法，让父亲给自己起名
		
		thread.sleep() 让程序休眠一会，然后执行
		

		
```

## 18.2多线程的创建

```java
第一种创建线程的方法		
        public class duoxiancheng extends Thread{
            @Override
            public void run() {
                for (int i = 0; i <20 ; i++) {
                    System.out.println("run" + i);
                }
            }
        }
        
    第二种创建线程的方法
       1.创建一个runable接口实现类
       2.在实现类中重写 runable方法  run方法
       3.创建一个runable接口实现类对象
       4.创建 thread 类 对象，构造方法中传递 runable 接口的实现类对象
       5.调用thread类中的 start方法
       
       	runable接口，接口实现对象
       		 public static void main(String[] args) {
                MyThread mt = new MyThread();

                Thread t = new Thread(mt);
                t.start();
                for (int i = 0; i < 20 ; i++) {
                    System.out.println("main: " + i);
                }
            }
         runable接口的好处
         	1.一个类只能继承一个类，runable接口，还可以继承其他类
         	2.增强了程序的扩展性，降低了程序的耦合性
            
            
```

## 18.3匿名内部类实现多线程的创建

```java
		第一种
		new Thread(){
            @Override
            public void run() {
                for (int i = 0; i <20 ; i++) {
                    System.out.println("zi线程"+ i);
                }
            }
        }.start();
        for (int i = 0; i < 20 ; i++) {
            System.out.println("main: " + i);
        }
        
        第二种
        new Thread( new Runnable(){
            @Override
            public void run() {
                for (int i = 0; i <20 ; i++) {
                    System.out.println("zi线程"+ i);
                }
            }
        }).start();
```

## 18.4线程安全

```java
多线程访问了共享的数据，就会产生线程安全问题
		runableomp1 run = new runableomp1();
        Thread to = new Thread(run);
        Thread t1 = new Thread(run);
        Thread t2 = new Thread(run);
        to.start();
        t1.start();
        t2.start();
        
        
        public void run() {
        while (true){
            if(ticket > 0){
                try {
                    Thread.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread().getName() + "正在卖第"
                        + ticket + "张票");
                ticket--;
            }
        }

    }
    
    
    	如何解决
    		1.同步代码块
    			通过同步代码块中的锁对象，可以使用任意对象
    			但是必须保证多个线程使用的锁对象是同一个
    			吧同步代码块锁住，只让一个线程执行
    			
    				  /*创建一个锁对象*/
    					Object obj = new Object();
    					synchronized (obj){
                            共享的资源
    					}

    		2.同步方法
    			把共享数据的方法抽取出来，方法一个方法中，加一个修饰符 synchronized
    			    public synchronized  void tic(){
                        放入里面，然后调用
    			    }
    			    
    			  只让一个线程执行，
    			  锁对象是this
    			  静态方法也可以保证安全
    			  锁对象不是this
    		3.锁机制
    			lock，比以上两种方法的操作更加广泛
    			lock()
    			unlock()
    			1.在成员位置创建一个reentranlock对象
    			2.在可能出现问题的前面 加一个 lock()
    			3.在可能出现问题的后面 加一个 unlock()
```

## 18.5线程状态

```java
阻塞状态	具有执行资格，等待cpu空闲执行,没有争取到锁对象
休眠状态	放弃执行资格，cpu空闲也不执行，计时等待状态 sleep()
			1.sleep()  进入计时等待
			2.wait() 如果wait没有在毫秒结束，那么就会自动醒来状态
无限等待状态  wait() 等待  notify()唤醒
			保证等待和唤醒只有一个可以执行，需要只用同步技术
			顾客 synchronized(obj){
                obj.wait()
			}
			老板 synchronized(obj){
                obj.notify()
			}
			
			唤醒方法
				1.notify
				2.notifyALL  唤醒所有等待线程
死亡状态
新建状态
运行状态
		可以相互转化
```

## 18.6线程通信状态

```java
多个线程之间进行协调通信，共同操作同一个数据
		wait
		notify
		
		锁对象调用的时候，唤醒和等待必须是同一个锁对象
```

## 18.7线程池

```java
我们使用线程的时候是创建一个线程，这样就有了一个问题
	如果并发的数量很多，这样频繁的创建就会大大降低系统的效率，因为创建销毁需要时间
	有了线程池
	
	线程池，容器 集合 Arraylist Hashset LinkedLish  hashmap
	
	list.remove()  返回的是被移除的线程，
	list.add()   添加使用完毕的线程
	
	jdk1.5之后
	内置了线程池，我们可以直接使用
		java.util.concurrent.executors  线程池的工厂类，可以用来创建线程池
			这是一个静态方法
			参数   nthreads  线程的数量
			返回值  executorService接口
				submit() 提交
				shutdown()  销毁
				
		使用步骤
			1.使用线程池的工厂类创建一个指定数量的线程池
			2.创建一个类 ，实现runable接口，重写run方法，设置线程任务
			3.调用executorService中的方法 submit() 传递线程任务，开启线程，执行run方法
			4.销毁线程池（一般不会销毁）
			
			  ExecutorService es = Executors.newFixedThreadPool(2);
                es.submit(new impl4());
                es.submit(new impl4());
                es.submit(new impl4());
                
                线程池使用完了，会自动归还给线程池，
			
```

## 18.8 lambda表达式

```java
函数编程式思想
	强调做什么，而不是以什么形式去做
	（）->{
        业务逻辑
	}
	无参无返回
	cookie(()->{
            System.out.println("吃饭了");
        });
     有参有返回
      Arrays.sort(pe,(Person o1, Person o2)->{
            return o1.getAge()-o2.getAge();
        });
        
        
       lambda表达式是可推导可以省略的
       	 凡是上下文推导的内容，都可以省略
       	 1.(参数列表): 括号中的参数列表数据类型可以不写
       	 2.参数列表括号中的参数如果只有一个，那么类型和（）都可以省略
       	 3.如果大括号中，只有一行，无论是否有返回值，都可以省略{}，return。分号
       	 
       	 Arrays.sort(pe,(o1,o2)->o1.getAge()-o2.getAge());
```

# 十九.File 类

```java
windows   //////    有区别
linux			\\\\\\

pathseparator

			1.注意路径是不区分大小写的
			2.路径中的文件名称分隔符windows使用反斜杠，两个反斜杠是一个普通的反斜杠，因为转义字符
```

## 19.1构造方法

```java
File f1 = new File("pathname")
		一个参数 选择路径
File f1 = new File("父"，“子”)  参数都是 String
		父路径和子路径可以单独书写
File f1 = new File("父"，“子”)  参数1是 File类，参数2是 String
	父类可以调用File的方法
	
常用方法
    file.getAbsolutepath  获取绝对路径
    file.getepath  获取路径，传入构造方法的就是什么
    file.getname()    返回文件夹名称或者是文件名称
    file.length()  返回的是文件的大小，返回的是字节

判断
	exists()  判断构造方法的路径是否存在
	isDirectory()  判断是否为目录
	isFile()  判断是否为文件
```

## 19.2创建删除遍历

```java
file.createNewFile()  当且仅当该名称的文件不存在的时候，创建一个新的空文件
file.delete()   删除由文件或者目录
file.mkdir()  创建File表示的目录
file.mkdirs()   创建file表示的目录，包括不存在的父目录


遍历文件夹
	file.list()		返回一个String数组，表示目录中所有的子文件或者目录
	file.listFiles()  返回一个File数组，表示目录中所有的子文件或者目录
	注意
		1.只能遍历文件夹
		2.路径必须存在
		3.可以遍历到隐藏文件夹
		
		
	过滤器
		第一种
		public class filter implements FileFilter {
        @Override
        public boolean accept(File pathname) {
            if (pathname.isDirectory()){
                return true;
            }
            return pathname.getName().toLowerCase().endsWith(".php");
        }
    }
    
    	匿名内部类写法
    		 File[] files = fi.listFiles(new FileFilter() {
            @Override
            public boolean accept(File pathname) {
                if (pathname.isDirectory()){
                    return true;
                }
                return pathname.getName().toLowerCase().endsWith(".php");
            }
        });
        
        lambda优化
        File[] files = fi.listFiles(pathname->{
            if (pathname.isDirectory()){
                return true;
            }
            return pathname.getName().toLowerCase().endsWith(".php");
        });
```

## 19.3 IO流

```java
分为  		输入     输出
	字符流	INputsteam	OUtputstream
	字节流		 Render  Outrender
```

### 19.3.1字节输出流

```java
OUtputstream 抽象类 
	用子类继承  FileOutputStream;把内存中的数据写入硬盘的文件中
	 
	 构造函数
	 		FileOutputStream(String name)
	 		FileOutputStream(File file)
            作用:
            	1.创建一个FileOutputStream对象
            	2.根据构造方法中的文件路径，创建一个空文件
            	3.会把FileOutputStream对象指向创建好的文件
            	
            使用步骤
            	1.创建一个FileOutputStream对象，传递写入的目的地
            	2.调用FileOutputStream对象中的方法write，把数据写入文件
            	3.释放资源
       写入数据	
            public static void main(String[] args) throws IOException {
            FileOutputStream fos = new FileOutputStream("D:\\java\\学习\\a.txt");
            fos.write(97);//写入一个字符
            fos.close();
        		}
        	写很多
        	byte[] by = {65,66,67,68,69};
        		fos.write(by);
        
        数据的追加写入
        	  FileOutputStream fos = new FileOutputStream(
        	  "D:\\java\\学习\\a.txt",true);
        	换行
        	windows  \r \n
        	linux /n
        	mac /r
        
       任意的文本编辑器
       	打开会查询编码表
       		0-127 查询ascll表
       		其他  查询系统默认编码表
       		gbk编码表
```

### 19.3.2 字节输入流

```java
INputsteam
	继承  FileInputStream
	
		读取
			 public static void main(String[] args) throws IOException {
                FileInputStream fis = new FileInputStream("D:\\java\\学习\\a.txt");
                int len = fis.read();
                System.out.println(len);
            }
            
         读取所有
         	 FileInputStream fis = new FileInputStream("D:\\java\\学习\\a.txt");
                int len = 0;
                while ((len = fis.read()) != -1){
                    System.out.print((char)len);
                }
                
          /*一次读取多个字节*/
                byte[] bts = new byte[10];
                int len = fis.read(bts);
                System.out.println(new String(bts));
```

### 19.3.3 字符输入流

```java
一个中文
	gbk 中文占两个字节
	utf8 中文占3个字节
	Render   FileRender
```

### 19.3.4字符输出流

```java
Outrender

	写入字符需要调用  flush()方法  刷新
			close()   关闭也可以写入‘
	区别是   close()关闭流  flush()没有关闭
```

### 19.3.5 处理IO流中的异常

```java
 FileInputStream fis = null;
        byte[] bts = new byte[10];
        try{
            fis = new FileInputStream("D:\\java\\学习\\a.txt");
            int len = fis.read(bts);
        }catch (IOException e){
            System.out.println();
        }finally {
            if(fis != null){
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
        System.out.println(new String(bts));
        
        
        
       jdk7新特性
       		try后面加一个(),在括号中定义流对象，执行完毕自动释放，不需要finally
       		
       		try(流对象定义){
                
       		}catch(){
                
       		}
```

### 19.3.6 properties集合

```java
继承  Hashtab集合，有key value  双链集合
是唯一一个和  IO流 相关的方法
		可以使用properties集合中的方法Store，把集合中的临时数据，持久化写入硬盘中
		可以使用properties集合中的方法load，把硬盘中保存的键值对，读取到集合中使用
		
		
		setproperties()
		getproperties()
		
	操作方法集合的使用
	private static void  show(){
        Properties prop = new Properties();
        prop.setProperty("赵丽颖","168");
        prop.setProperty("高圆圆","175");
        prop.setProperty("刘诗诗","172");
        //遍历
        Set<String> set = prop.stringPropertyNames();
        for (String key: set){
            String value = prop.getProperty(key);
            System.out.print(key + value);
        }
    }
    
    
    	写入
    		Properties prop = new Properties();
        prop.setProperty("赵丽颖","168");
        prop.setProperty("高圆圆","175");
        prop.setProperty("刘诗诗","172");
        FileWriter fw = new FileWriter("D:\\java\\学习\\a.txt");
        prop.store(fw,"保存数据");
        fw.close();
        
        读取
        	 Properties prop = new Properties();
        FileReader fr = new FileReader("D:\\java\\学习\\a.txt");
        prop.load(fr);
        Set<String> set = prop.stringPropertyNames();
        for (String key: set){
            String value = prop.getProperty(key);
            System.out.print(key + value);
        }
```

## 19.4 缓冲流

```java
给基本的字节输入流增加一个缓冲区，提高基本的字符输入输出流的读取效率
			
			
			 FileReader fis = new FileReader("D:\\java\\学习\\a.txt");
        BufferedReader bis = new BufferedReader(fis);
        int len = 0;
        while ((len = bis.read()) != -1){
            System.out.print((char)len);
        }
        bis.close();
```

## 19.5 转化流

```java
字符编码
字符集
		对应
		
		unicode  万国码
		
		OUtputStreamWrite转码
		和缓冲流一个原理，参数可以传 编码表
```

## 19.6序列化和反序列化

```java
将对象写入文件或者读取对象，使用它
	什么是Serializable接口
		一个对象序列化的接口，一个类只有实现了Serializable接口，它的对象才能被序列化
	什么是序列化？
		序列化是将对象状态转换为可保持或传输的格式的过程。与序列化相对的是反序列化，它将流转换为对象。这两个过程结合起来，可以轻松地存储和传输数据。
	具体概念
		把对象转换为字节序列的过程称为对象的序列化
		把字节序列恢复为对象的过程称为对象的反序列化
	什么情况下需要序列化
		当我们需要把对象的状态信息通过网络进行传输，或者需要将对象的状态信息持久化，以便将来使用时都需要把对象进行序列化

	ObjectInputStream
	ObjectOutputStream
	
	
	transient  瞬态关键字  被修饰的关键字不能被序列化
	static  不能序列化
	
	异常解决INvalidClassException异常  p402
```

# 二十.网络编程

```java
Tcp/Ip 协议
	分为四层
		应用层			Http/https/dns
		传输层			Tcp/Udp
		网络层			ip
		数据链路层/物理层		计算机底层网络协议
		
	协议分类
		UDp		
			无连接通信，音频，视频，消耗资源小，通信效率高，
			不能保证数据的完整行
			数据被限制 64kb以内
		Tcp
			传输控制协议，面向连接
			三次握手
				1.客户端向服务器发送连接请求，等待服务器确认
				2.服务器端给客户端一个相应，通知客户端收到了连接请求
				3.客户端再次向服务器发送请求，确认连接
				
		三要素
			协议
			ip地址
				ipv4  32位
				ipv6  128位
                    ipconfig
                    ping ip地址
			端口号
```

## 20.1 TCP通信

```java
java.net.Socket  客户端
java.net.ServerSocket 服务端

	1.服务器端先启动
	2.客户端请求服务器端
	3.建立逻辑连接
	4.这个对象就是 IO对象 字节流对象
	
	注意
		1.服务器端有一个方法，叫accept可以获取到请求的对象，
		2.多个客户端同时和服务器进行交互，就需要使用多个IO流对象
```

## 20.2客户端实现

```java
      方法
    	getOutputStream()		输出流
        getIutputStream()		输入流
        close()   				关闭流
        
         public static void main(String[] args) throws IOException {
            Socket sc = new Socket("127.0.0.1",7888);
            OutputStream ops = sc.getOutputStream();
            ops.write("你好服务器".getBytes());
            InputStream is = sc.getInputStream();
            byte[] bytes = new byte[1024];
            int len = is.read(bytes);
            System.out.println(new String(bytes,0,len));
            sc.close();
    }
```

## 20.3服务器端代码实现

```java
用accept 获取到客户端对象
	 public static void main(String[] args) throws IOException {
        ServerSocket ss = new ServerSocket(7888);
        Socket socket = ss.accept();
        InputStream is = socket.getInputStream();
        byte[] bytes = new byte[1024];
        int len = is.read(bytes);
        System.out.println(new String(bytes,0,len));
        OutputStream os = socket.getOutputStream();
        os.write("收到谢谢！".getBytes());
        socket.close();
        ss.close();
    }
    
    上传文件
```

# 二十一.函数式接口

```java
只能有一个抽象方法的接口
注解
	@functioninterce  检测
	
	 public static void main(String[] args) {
        ad(new interimp() {
            @Override
            public void method() {
                System.out.println("函数式编程");
            }
        });
    }

    private static void ad(interimp imp) {
        imp.method();
    }
    简化	 ad(()->System.out.println("函数式编程"));
```

# 二十二. Java web基础加强

## 1. Junit 单元测试

```java
黑盒测试
	输入一个值，看能否达到预期，不关心逻辑内容，不需要写代码
白盒测试
	需要写入代码，关注代码具体的执行流程
	Junit就是白盒测试
	
	步骤
		1.定义一个测试类
		2.定义一个测试方法
				返回值 void
				参数 空参
				给方法加@test
		3.导入
		4.断言
		
			  @Test
                public void test(){
                    int a = 1;
                    System.out.println("111");
                    /*断言*/
                    Assert.assertEquals(3,a);
                }
                
        初始化
        		@before
        		public void init(){
        			//资源申请，所有测试方法之前
        		}
        		
        		@after
        		public void init(){
        			//资源释放，所有测试方法之后
        		}
```

## 2.反射

```java
将类的各个组成部分封装为其他对象，这就是反射机制

	
	三个阶段
        1.source源代码阶段
        2.class类对象阶段
        	通过ClassLoader类加载器把 .class字节码文件加载进入内存
			然后加载成 class类对象
				成员变量封装被fields对象
				构造方法封装成construct对象
				成员方法封装成methods对象
        3.runtime阶段
        
        
        好处，
        	1.在程序运行过程中，例如代码提示，操作这些对象
        	2.解耦，提高程序的可扩展性
        	
        	
        获取class对象的方式
        	1.静态方法Class.forName("全类名“);
        		多用于配置文件
        	2.通过类名的属性class来获取，
        		多用于参数的传递
        	3.对象.getclass()  在Object中 
        		多用于对象的获取
       		 同一个字节码文件在一次的程序运行过程中只会被加载一次，三个方法获取的方法一样
       		 
       		 
       class对象功能，
       	1.获取成员变量
       		getFields()   获取所有Public修饰的变量
       		getField(String name )
       		getdeclaredFields()	获取所有的成员变量
       		getdeclaredField(String name)
       	2.获取构造方法
       		getConstructs()
       		getConstruct(String name )
       		getdeclaredConstructs()
       		getdeclaredConstruct(String name)
       		
       		newInstance(p)  构造器创建对象
       	3.获取成员方法
       		getMethods() 获取所有Public修饰的变量
       		getMethod(String name )
       		getdeclaredMethods()  获取所有的成员变量
       		getdeclaredMethod(String name)
       		
       		invoke(p)执行方法
       	4.获取类名
       		getName()
       		
       		
       		暴力反射
       			忽略访问权限修饰符安全检查
       			 setAccessible()
       	自己写一个框架的步骤
       		1.将对象的类名和方法定义在配置文件中
       		2.在程序中加载配置文件
       		3.使用反射技术加载进入内存
       		4.创建对象
       		5.执行方法
       		
       		 Properties pro = new Properties();
                ClassLoader classLoader = reflect.class.getClassLoader();
                InputStream io = classLoader.getResourceAsStream("pro.properties");
                pro.load(io);

                /*获取数据*/
                String cs = pro.getProperty("className");
                String method = pro.getProperty("methodName");

                /*加载进入内存*/
                Class cl = Class.forName(cs);
                Object obj = cl.newInstance();
                Method md = cl.getMethod(method);
                md.invoke(obj);
```

## 3.注解

```java
用文字来描述程序，说明程序
	1.编写文档
	2.代码分析
	3.编译检查
	
	javadoc 文件名  可以生成文档
	javac 	编译
	javap  反编译
	
	内置注解
		@override			重写父类的方法
		@Deprecated			该注解标注的内容已经过时
							两个方法，以前的方法不删除
							该用还是用
		@suppressWarning("all")	压制警告
							不想看到提示
				
     /**
     * 
     * @version 1.2
     * @author
     */
	自定义注解
		
		注解的本质：就是一个接口，该接口默认继承其他接口	
        元注解
        	@Target  描述注解能够作用的位置
        	@Rentention 描述注解保留的阶段
            @Documented 描述注解是否能够被抽取到api文档中
            @inherited 描述注解是否能被子类继承
		public @interface 注解名称{
            
		}
		属性：接口中的抽象方法
```

# 二十三.数据库操作

## 23.1数据库范式

```java
第一范式	
		每一列都是不可分割的原子数据项
		不是合并的列，一列不能再分成其他列，
			存在非常严重的数据冗余，
			数据添加数据不合法
			数据删除存在问题，会将其他的数据也会删除
第二范式
		在第一范式的基础上，非码属性必须完全依赖于主码
		例如学号和姓名相互依赖
		码 如果在一张表上面，一个属性或者属性组，被其他属性所完全依赖，称为表
		
		例如 分数依赖于课程和学号
			学生表和成绩表必须分开；
第三范式
		在第二范式(2NF)任何非主属性不依赖于其他非主属性
		消除传递依赖
				
		越高的范式数据库冗余越小
		
		
		通俗理解
第一范式就是属性不可分割，每个字段都应该是不可再拆分的。比如一个字段是姓名（NAME），在国内的话通常理解都是姓名是一个不可再拆分的单位，这时候就符合第一范式；但是在国外的话还要分为FIRST NAME和LAST NAME，这时候姓名这个字段就是还可以拆分为更小的单位的字段，就不符合第一范式了。

第二范式就是要求表中要有主键，表中其他其他字段都依赖于主键，因此第二范式只要记住主键约束就好了。比如说有一个表是学生表，学生表中有一个值唯一的字段学号，那么学生表中的其他所有字段都可以根据这个学号字段去获取，依赖主键的意思也就是相关的意思，因为学号的值是唯一的，因此就不会造成存储的信息对不上的问题，即学生001的姓名不会存到学生002那里去。

第三范式就是要求表中不能有其他表中存在的、存储相同信息的字段，通常实现是在通过外键去建立关联，因此第三范式只要记住外键约束就好了。比如说有一个表是学生表，学生表中有学号，姓名等字段，那如果要把他的系编号，系主任，系主任也存到这个学生表中，那就会造成数据大量的冗余，一是这些信息在系信息表中已存在，二是系中有1000个学生的话这些信息就要存1000遍。因此第三范式的做法是在学生表中增加一个系编号的字段（外键），与系信息表做关联。
```

## 23.2事务

```java
如果一个包含多个步骤的业务操作，被事务管理，要么这些都操作成功，要么都操作失败
例如打钱失败，回退款回来
	出现异常，回滚操作，提交事务
	
	开启事务 strat transaction
	回滚	rollback
	提交事务  commit
	
	在 MYSQl中事务默认自动提交，
		自动提交
		手动提交
		
	四大特征
		1.原子性；要么同时成功要么同时失败，不可分割的最小操作单位
		2.持久性 如果事务一旦提交或者回滚，那么数据库表会被持久的更新
		3.隔离性：多个事物之间，相互影响，相互独立
		4.一致性，事务操作前后，数据总量不变  
		
		存在问题：
			脏读：一个事务，读取到另外一个事务中没有提交的事务
			不可重复读(虚读) 在同一个事务中，两次读取到的数据不一样	
			幻读	一个事务操作数据表中的所有记录，另一个事务添加了一条数据，那么第一个事务查询不到数据
		隔离级别
			read uncommited 读未提交，三种问题都会产生
			read commited 读已提交 会产生后面两种问题 oracle
			repeated read 可重复读  会产生 幻读 mysql
			serializable 串行话，可以解决所有问题
			
			注意隔离级别，从小到大，安全性越来越高，但是效率越来越低
			sql可以设置
```

## 23.3 JDBC

```java
使用一套代码操作所有的关系数据库，就是JDBC
	定义了操作所有关系型数据库的规则
	定义了一套接口
	不同的厂商实现了不同的实现类，我们把这些实现类叫做数据库驱动
	
	步骤
		1.导入jar包
		2.注册驱动
		3.获取数据库连接对象
		4.定义sql
		5.获取执行sql语句的对象 statement
		6.执行sql返回结果
		7.处理结果
		8.释放资源
		
		详细解释对象
			1.DriverManager : 驱动管理对象
				1.注册驱动
				2.获取数据库连接
			2.Connection ； 数据库连接对象
				1.执行sql的对象
				2.管理事务
			3.Statement 执行sql的对象  静态sql
				1.执行sql
					excute
					excuteupdate
			4.ResultSet 结果集对象
			5.perparedstatement 执行sql对象  预编译 sql
			参数使用占位符替代
			setxxx(参数1，参数2)
			
			
	简单操作
		  /*导入驱动jar包*/
        Statement statement = null;
        Connection connection = null;
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            connection = DriverManager.getConnection("jdbc:mysql:///jdbc?serverTimezone=UTC", "root", "root");

            String sql = "insert into student values (18,'赵某')";
            statement = connection.createStatement();

            int count = statement.executeUpdate(sql);
            if(count>0){
                System.out.println(count);
                System.out.println("添加成功");
            }

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            if(statement != null){
                try {
                    statement.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }

            }
            if(connection != null){
                try {
                    connection.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }

            }
        }
        
        
        sql注入
        	在拼接sql时候有些关键字参与拼接，解决安全性问题
        	password = ‘a’ or ‘a’ = ‘a’;
        	
        	
       事务
       		1.开启事务 setAutoCommit(false);
       		2.回滚	commit();
       		3.提交事务	rollback();
```

## 23.4数据库连接池

```java
实现DATASource接口
	1.获取连接	getconnection()
	2.归还连接	close();

1.C3P0	数据库连接池
2.DRuid  阿里巴巴连接池
	1.导入jar包
	2.定义配置文件
		1.是 properties形式的
		2.可以叫任意名称
	3.获取数据库连接池对象，：通过工厂来获取，
	4获取连接
	
		 /*加载配置文件*/
        Properties pro = new Properties();
        InputStream is = 		druid.class.getClassLoader().getResourceAsStream("druid.properties");
        pro.load(is);
        /*获取连接池对象*/
        DataSource ds = DruidDataSourceFactory.createDataSource(pro);
        /*获取连接*/
        Connection connection = ds.getConnection();
        System.out.println(connection);
        
        
        定义工具类
        	  Connection connection =null;
        PreparedStatement preparedStatement = null;
        try {
            connection = jdbvutils.getConnection();
            String sql = "insert into student values(?,?)";
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setString(1,"孙悟空");
            preparedStatement.setInt(2,15);
            int i = preparedStatement.executeUpdate();
            System.out.println(i);
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {
            jdbvutils.close(preparedStatement,connection);
        }
        
        Spring template
        	1.导入五个包
        	2.创建jdbctemplate对象，依赖数据源Datesource
        	3.调用jdbctemplate方法来执行
        	
       JdbcTemplate jdbcTemplate = new JdbcTemplate(JdbcUtils.get);
        String sql = "updata ....?";
        int update = jdbcTemplate.update(sql, 3);
```

# 二十四. Java web

## 24.1服务器

```java
weblogic  oracle付费版  收费 大型
websphere ibm公司  收费 大型
Jboss  jboss  收费  大型
tomacat apache基金组织，中小型 javaee服务器  开源的
```

## 24.1 tomcat

```java
  目录结构 
   	bin  可执行文件
    conf  配置文件
    lib 依赖的 jar包
    logs 日志文件
    temp 临时文件
    webapps 存放项目的
    work 存放运行时的数据
    
    配置
    	1.直接将项目放到webapps下面
    	2.修改压缩改成war包,然后拖进去
    	3.配置conf/server.xml;
    	
    	静态项目
    	动态项目
    		--webinfo
    			--web.xml
    			--classse目录
    			--lib目录
    			
    			
   将tomcat继承到IDEA中，
```

## 24.2 servlet

```java
server applet  运行在服务器端的小程序
就是一个接口，接口定义了java类，被浏览器访问到的规则
	1.创建javaee项目，
	2.定义一个类，实现servlet接口
	3.实现接口的抽象方法
	4.配置
	
	
	web.xml
		   <!--配置servlet-->
                <servlet>
                    <servlet-name>demo1</servlet-name>
                    <servlet-class>servlet.demo.demo</servlet-class>
                </servlet>
                <!--映射-->
                <servlet-mapping>
                    <servlet-name>demo1</servlet-name>
                    <url-pattern>/demo1</url-pattern>
                </servlet-mapping>
                
      生命周期
      		init()  初始化 方法，在servlet被创建时候执行，只会执行一次
      		service()  每次servlet被访问执行
      		destory()  销毁方法，servlet被杀死时候执行
      		servlet()  用来获取配置对象
      		getservletinfo()  获取servlet() 信息
      
      
      servlet3.0注解配置
      		好处：支持注解配置，
      		在类上面使用 webservlet注解
      		
      		@webservlet(urlpatterns = "demo")
      
      servlet 体系结构
      		1.servlet  接口
      		2.genericservlet	抽象类
      			以后写直接结成这个抽象类就可以了
      		3.httpservlet	抽象类
      			用的比较多
      			对http协议的一种粉装，简化操作
      			复写doGet/doPost方法
      	配置
      		@webservlet({"demo1","demo2","demo3"})
      		三种配置
      			1./xxx
      			2./xxx/xxx  /user/demo4
      			3.*.do  *.dao   任何都可以访问
      		
```

## 24.3 request

```java
request继承体系
	servletrequest  接口
			继承
	httpservletrequest  接口
			实现
	requestfacade

request获取请求消息数据
	1.获取请求行数据
		获取请求方式  getMethod()
		虚拟目录	getcontextpath()
		servlet路径 getservletpath()
		获取请求参数	getqueryString()
		获取请求url getrequestURI()
		获取客户机ip地址	getremoteaddr()
		
		 protected void doGet(HttpServletRequest request, HttpServletResponse response)				{
        		String s = request.getQueryString();
        		System.out.println(s);
    		}
    2.获取请求头的数据
    	getHeader(name)  获取请求头的值 
    	getHeaderName()	 获取请求头名称
    	
    	防盗链
    	
    	 Enumeration<String> headName = request.getHeaderNames();
         while(headName.hasMoreElements()){
                String name = headName.nextElement();
                String value = request.getHeader(name);
             System.out.println(name+"-----"+value);
         }
    	得到
    	host-----localhost:8080
connection-----keep-alive
upgrade-insecure-requests-----1
user-agent-----Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.130 Safari/537.36
sec-fetch-user-----?1
accept-----text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
sec-fetch-site-----none
sec-fetch-mode-----navigate
accept-encoding-----gzip, deflate, br
accept-language-----zh-TW,zh;q=0.9,en-US;q=0.8,en;q=0.7
cookie-----Webstorm-c7ae48fb=ad1984c8-fa5b-4222-8441-e07386c40845; pgv_pvi=4967734272; JSESSIONID=3D36D24A77F95694E4E8330F59751CF5


	3.获取请求体
		只有POST请求有请求体
			1.获取流对象
			2.再从流中间获取数据
	4.获取请求参数
		getparameter()  根据参数名称获取参数值
		getparametervalues() 更具参数名称获取参数的数组
		getparameterName()  获取u所有请求的参数
		getparametermap()  获取所有键值对
			 1.String username = request.getParameter("username");
			 2.Map<String, String[]> parameterMap = request.getParameterMap();
                    Set<String> strings = parameterMap.keySet();
                    for (String i:strings){
                        System.out.print(i);
                        String[] strings1 = parameterMap.get(i);
                        for (String g:strings1){
                            System.out.println(g);
                        }
                    }
              中文方式乱码
              request.setCharacterEncoding("utf-8");
	5.请求转发
		一种在服务器内部的资源跳转方式
		A-B  转发
			第一种
				RequestDispatcher requestDispatcher = 		request  .getRequestDispatcher("/demo2");
       	 requestDispatcher.forward(request,response);
        	第二种
		1.浏览器地址栏路径没有发生变化
		2.服务器内部资源访问
		3.转发是一次请求，多个资源使用同一个请求
    6.共享数据
    	服务器内部共享数据
    		域对象：一个有作用范围的对象，可以在范围内共享数据
    		request域:代表一次请求的范围
    				1.setattribute(name,obj); 发送数据
    				2.getattribute(name) 获取数据
    				3.removerattribute(name) 移除
    	request.setAttribute("msg","hello!!!");
    	 Object ms = request.getAttribute("msg");
    7.获取servletcontext
    	getservletcontext();获取对象成功
    	
    8.Beanutils 工具类
    
    	简化数据封装
    	 //获取请求参数
        Map<String, String[]> parameterMap = request.getParameterMap();
        //创建user对象
        User loginUser = new User();
         //使用beanutils
        try {
            BeanUtils.populate(loginUser,parameterMap);
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }
       细节
                1.用于封装 javabean 标准的java类
                2.必须提供空参的构造器
                3。成员变量必须用private修饰
                4.提供getter setter类
                
         功能	
         		封装数据的，成员变量
```

## 24.4 response



```java
响应头
		Content-Type:服务器告诉客户端本次相应体数据格式和编码格式
		CONtent-disposition 服务器告诉客户端以什么样的格式打开响应体数据
				in-line 默认值
				attachment;filename=xxx 以附件形式打开响应体，文件下载
				
		状态码 1xx;服务器端开始接受客户端信息，但是没有接受完成，
		  2xx: 成功
		  3xx 重定向 302重定向 304访问缓存
		  4xx 客户端错误	404路径错误 405请求方式没有对应的方法
		  5xx 服务器端错误	500服务器内部出现异常，
相应行
	
响应体
	就是传输的数据
	
	
	设置头
		setheader()
	设置响应体
		获取输出流
		使用输入流，将数据输出到浏览器
		字符字节输出流	getwriter()
					getoutputwriter()
					
					
	重定向步骤
			1.设置状态码
			2.设置响应头
			  response.setStatus(302);
       		 response.setHeader("location","/demo2");
       		 
       		 优化
       		 	response.sendRedirect("/demo2")
       		 	
       		 	特点
       		 		1.转发地址栏路径不变，只能访问当前服务器下的资源，是一次请求
       		 		2.重定向的地址栏发生变化，重定向可以访问其他服务器的资源，重定向是两次请求
       		 		
       输出数据
       	1.获取字符输出流
       	2.输出数据
       		response.setHeader("content-type","text/html;charset=utf-8");
       			 PrintWriter writer = response.getWriter();
        		//设置字符集就可以
       			 writer.write("<h1>你好你好hello!!</h1>");
       			 
       			 
       			 输出字节流数据 hello.getbytes()
       			 
       	验证码
       	
       	ServletContent  代表整个web应用
       		1.获取mime类型，
       			在互联网通信的过程中的文件类型一种标准，
       				格式 大类型/小类型    text/html  image/jpeg
       				 ServletContext servletContext = request.getServletContext();
                    //定义一个文件类型
                    String filename = "a.jpg";
                    String mimeType = servletContext.getMimeType(filename);
       		2.域对象，共享数据
       			set/get/remove attribute
       			范围最大，所有用户的数据
       		3.获取文件服务器的真实路径
       			getrealpath("/b.txt")
       		
       		
       		处理中文文件的下载展示
       			使用浏览器编码类
       		
```

## 24.5 cookie

```java
一次会话中，共享数据，一次会话有多次请求
	1.可以发送多个cookie，默认情况下浏览器关闭cookie消失
		可以持久化保存  setmaxage();
	2.cookie能不能存中文，cookie的范围有多大 tomcat8以后
		不同服务器之间的cookie共享问题，一级域名相同即可
```

## 24.6 JSP入门

```java
java server page;
	既可以指定html标签，也可以定义java代码
	
	原理		本质上也是一个 servlet
		1.服务器解析请求消息，找到jsp页面，
		2.如果找到了，会将jsp转化为 .java文件
		3.会编译java文件 生成class文件
		4.由字节码文件提供访问
		
	脚本
		jsp声明java代码的方式，
		1.<%
			java代码 
			不在里面，就会编程字符串
			%>  
				定义在service方法中，可以定义变量
		2.<%!  代码 %> 定义成员变量，成员方法 在 java类的成员位置
		3.<%=  代码 %> 会输出到页面上，意思就是输出语句
		
	jsp内置对象
		在jsp中，不需要获取和创建对象，直接可以使用的对象
		jsp一共有9个内置对象
		1.request
		2.response
		3.out 将数据输出到页面上
```

## 24.7 session

```java
服务器端会话技术，将数据保存在服务器端的对象中
	1.获取 httpsession对象
		requsest.getsession();
	2.使用httpsession对象
		set/get/remove attribute()
		
		
	服务器如何确保再一次会话范围内，多次获取的session是同一个
		session id 用来实现
		
		细节
			1.客户端关闭后，再打开 两次sessionid 不一样，希望一样加一个cookie；键位sessionid，设置最大存活时间
			2.通过session的钝化，活化可以保存session，为同一个
			3.session默认失效时为 30分钟
			4.可以存储任意大小的
			
		和cookie的区别
			1.session没有大小限制
			2.session在服务器端，cookie存储在客户端
			3.session相对于安全一些
```

## 24.8 JSP深入

### 24.8.1指令

```java
作用
	配置jsp页面，导入资源文件
	格式
		<%@ 指令名称 属性值 = 1 属性值 = 2 %>
		分类
			page  配置jsp页面的
					设置响应体的的mime类型以及字符集
					设置jsp页面的编码
					导入java包
					errorpage 发生异常会自动跳转到指定页面
					iserrorpage 可以使用内置对象exception
			include 页面的包含导入页面的资源文件
					包含其他页面 分成几部分jsp互相包含
			tahlib	导入资源的
					导入便签库  jstl例如
					
		注释
			jsp  <%--  --%>
			
		内置对象
			1.pagecontext  当前页面共享数据 ，获取其他8个内置对象  
域对象前面四个2.request	   一次请求访问多个资源
			3.session		一次会话多个请求间
			4.application	多个用户间共享数据 唯一
			5.response		响应对象
			6.page			当前页面的对象
			7.out			输出对象，输出到页面上
			8.config		servlet的配置对象
			9.exception		异常对象
```

### 24.8.2 MVC

```java
M 模型   业务逻辑操作，查询数据库 					java对象
V 视图	调用模型，将视图展示，获取客户端的输入			servlet
C 控制器	视图展示								jsp

优点  
	耦合度降低，方便维护 ，分工协作
	重用性高
```

### 24.8.3 El表达式

```java
expression language  
	1.替换简化java代码的书写
	也可以忽略  page里面设置 isELignore = true
	语法
		${表达式}
		
	运算
		逻辑运算父  &&(and)  ||(or)   !(not)
		空运算符  empty 用于判断字符串，集合，数组对象是否为null或者长度为0
	获取值
		1.el表达式只能从域对象中获取值
		2.语法
			${ 域的名称.键的名称 }
			${ 键名 }  一次从最小的域中查找，找到位置
			
			获取对象
				1.对象 ${request.u.name}   u表示 实例化对象，name表示getname方法
				2.list集合 
						${域的名称.list}  打印集合
						${域的名称.list[0]} 获取第一个元素
				3.MAP集合
						${域的名称.键的名称.key名称}
						${域的名称.键的名称【“key名称”】}
			隐式对象：
				11个隐式对象
					pagecontext
```

### 24.8.4 JSTL

```java
java server tag library

	作用用于替换  java代码
		导入jar包
		<%@ taglib uri="" profix%>
		
		
		常用标签
			if		
				<c:if test="true"></c:if>
			choose  相当于switch语句
				<c:choose>
                    <c:when test=""></c:when>
                    <c:when test=""></c:when>
                </c:choose>
			foreach
			
				<c:forEach begin="1" end="10" var="i" step="1" varStatus="s">
                    ${i}<br>
                    ${s.index}
                    ${$.count}
                </c:forEach>
```

## 24.9 Filter

```java
过滤器
	当请求的时候，过滤器可以将一些请求拦截下来，完成一些特殊的功能
	作用
		一般完成通用的操作：登陆验证，登陆过后才能访问
		
		1.定义一个类，让他实现一个接口Filter，
		2.复写里面的方法，
		3.配置拦截路径
			1.webxml配置
				 <filter>
                    <filter-name>demo1</filter-name>
                    <filter-class>servlet.filter.hello</filter-class>
                </filter>
                <filter-mapping>
                    <filter-name>demo1</filter-name>
                    <url-pattern>/*</url-pattern>
                </filter-mapping>
			2.注解
				@WebFilter("/*")   访问所有资源之前都会拦截
				filterChain.doFilter(servletRequest,servletResponse);
			3.过滤器执行流程
			4.过滤器生命周期
				init 加载资源
				destroy 释放资源
			5.过滤器配置详情
				拦截路径配置
					1.资源路径  /index.jsp  只有访问index.jsp
					2.拦截目录  /user/*  访问user下的所有资源
					3.后缀名   *.jsp   访问所有jsp文件
					4./*     拦截所有资源
				拦截方式
					1.注解设置
						dispatchtypes属性
							1.request 默认值，浏览器直接请求
							2.forword	转发来访问资源
							3.include	包含访问资源
							4.error	错误跳转资源
							5.async	异步访问资源
			@WebFilter(value = "/*",dispatcherTypes = DispatcherType.REQUEST)
			6.过滤器链 配置多个过滤器
			
					注解按照类名字符串比较规则比较值小的先执行 a>b
					
					xml  mapping 谁在上面谁执行
```

## 24.10 Listener

```java
事件  	一件事情
事件源		一件事情发生的地方
监听器		 一个对象，一段代码
注册监听 	将前面三个绑定到一起，当事件源发生事情后，执行监听器代码

	servletContextListener 接口，去实现
	
	xml
		<listener>
            <listener-class>servlet.listener.Listener</listener-class>
        </listener>
```

## 24.11 ajax ，Json

```java
同步  客户端必须等待服务器的回应，，在等待的期间不能做其他操作
异步	客户端可以干其他的操作，不要等待服务器端的相应

Json	
	多用于存储交换信息的语法，进行数据的传输，比xml更加快速
	
	解析器
		//创建jackson核心对象
		
		1.java对象转 json
			ObjectMapper map = new OBjectMapper()
			1.map.writeValue(参数1，obj);
				File: 将对象转化为json字符串并且保存到文件中
				Writer 将对象转化为json字符串并且填充到字符输出流中
				OUTpoutstrem 将对象转化为json字符串并且填充到字节输出流中
			2.String json = mapper.weiteValueASString(person);
			
			注意
				1.@JsonIgnore	忽略该属性
					加载属性值上面
				2.@Jsonformat(pattern = "yyyy-MM-dd")  格式化属性
				
				复杂数据转化
					List  数组
					MAp  对象格式一致
				
		2.json转 java
			创建核心对象 OBjectmapper
			调用readvalue(json字符串，转化的类型)
```

