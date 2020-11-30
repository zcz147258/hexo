---
title: Java基础
date:
updated:
type: "tags"
categories: Java
comments:
description: Java基础
keywords: Java基础
top_img: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=428108013,2443178233&fm=26&gp=0.jpg
cover: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=428108013,2443178233&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 一.基础知识点(面试题)

## 1.1String Stringbuilder Stringbuffer的区别

```java
str = 'hello'  +  'world'  需要开辟三次内存空间 不得不说这是对内存空间的极大浪费

和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象
StringBuffer类中的方法都添加了synchronized关键字

String：不可变字符串；
StringBuffer：可变字符串、效率低、线程安全；
StringBuilder：可变字符序列、效率高、线程不安全；

初始化上的区别，String可以空赋值，后者不行，报错

StringBuilder 类在 Java 5 中被提出，它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。

（1）如果要操作少量的数据用 String；
（2）多线程操作字符串缓冲区下操作大量数据 StringBuffer；
（3）单线程操作字符串缓冲区下操作大量数据 StringBuilder（推荐使用）。
```

## 1.2 Interger 和String类型转化

```java
//装箱就是自动将基本数据类型转换为包装器类型；拆箱就是自动将包装器类型转换为基本数据类型。

//将String类转化为Interger
在 Java 中要将 String 类型转化为 int 类型时,需要使用 Integer 类中的 parseInt() 方法或者 valueOf() 方法进行转换.

//方法一:Integer类的静态方法toString()
Integer a = 2;
String str = Integer.toString(a)

//方法二:Integer类的成员方法toString()
Integer a = 2;
String str = a.toString();

//方法三:String类的静态方法valueOf()
Integer a = 2;
String str = String.valueOf(a);
```



# 二.基础知识点2（基础整理）

## 2.1 Jdk 和 Jre

```java
JDK：java开发工具包
    先编译（编译器javec），后运行（解释器java）
JRE：java运行环境
    加载代码（加载器），校验代码（校验器），执行代码（解释器）
```

## 2.2数据类型

```java
1、基本数据类型：

    数值型：byte     1字节   8位   -128~127
        short    2字节   16位  -32768~32767
        int      4字节   32位  -2^31~2^31-1
        long     8字节   64位  2^63~2^63-1
    浮点类型：
        float    4字节   32位  
        double   8字节   64位
    字符型：char     2字节   16位   0~65535
    布尔型：boolean  true    false

2、引用类型：
    字符串 String、 类 class 、枚举 enum、接口interface
```

## 2.3变量

```java
1、数据类型划分：
    基本类型变量：数据的值
    引用类型变量：数据的地址
2、声明的位置划分：
    局部变量
    全局变量
        区别：
        1、默认值
            局部没有默认值，使用前必须初始化。
            全局有默认值，默认为0，不必须初始化。
        2、声明位置
            局部在方法内。
            全局在方法外类内。
        3、作用位置
            局部只能在自己声明的方法里。
            全局在整个类中
```

## 2.4位运算符

```java
与运算符  &
128 & 129 = 129
“a”的值是129，转换成二进制就是10000001，而“b”的值是128，转换成二进制就是10000000。根据与运算符的运算规律，只有两个位都是1，结果才是1，可以知道结果就是10000000，即128。

或运算符 |
或运算符用符号“|”表示，其运算规律如下
两个位只要有一个为1，那么结果就是1，否则就为0，

非运算符 ~
非运算符用符号“~”表示，其运算规律如下：
如果位为0，结果是1，如果位为1，结果是0，

异或运算符 ^
异或运算符是用符号“^”表示的，其运算规律是：
两个操作数的位中，相同则结果为0，不同则结果为1。

移位运算符
<<   左移运算符，将运算符左边的对象向左移动运算符右边指定的位数（在低位补0）
>>   "有符号"右移运算 符，将运算符左边的对象向右移动运算符右边指定的位数。使用符号扩展机制，也就是说，如果值为正，则在高位补0，如果值为负，则在高位补1.
>>>  "无符号"右移运算 符，将运算符左边的对象向右移动运算符右边指定的位数。采用0扩展机制，也就是说，无论值的正负，都在高位补0.

```

## 2.5多态

```java
    1、分类
        编译时多态：在编译过程中察觉的多态，重载，向上转型。
        运行时多态：在运行过程中察觉的多态，向下转型。
    2、向上转型、向下转型是在继承关系中，向下转型必须在向上转型的基之上。
    3、在继承关系中，父类的对象可以指向子类的实例，父类引用实体方法的时候，是调用子类重写以后的方法。
    4、向上转型
        父类的引用指向子类的实体
        父类类名 对象名=new 子类类();
        优点：减少重复代码，提高代码的复用性
        缺点:父类的引用无法调用子类特有的属性和方法
        解决方案：向下转型
    5、向下转型：
        子类对象的父类引用赋给子类
        子类类名 对象名=（子类类名）父类对象;
    6、 instanceof 判断左边的对象是否属于右边的类  对象名 instanceof 类名（子类类名）
    7、匿名对象
        new 类名（）  只有堆空间，没有栈空间，只能属于一次，为了节省代码。
```

## 2.6抽象abstract

```java
作用：节省代码，提高代码的复用性
1、抽象类格式：访问权限修饰符   abstract class 类名{}
2、抽象方法格式：访问权限修饰符  abstract 返回值类型  方法名(形式参数列表);
注意：
    1、如果一个类里有抽象方法，那么这个类必须声明成抽象类。
    2、一个类里面可以没有抽象方法，可以有非抽象方法，
    3、类继承抽象类：
        把子类也用abstract修饰，变成抽象类。
        子类重写父类的抽象的方法
    4、抽象类不能创建对象。
    5、抽象类可以有构造方法，在创建子类的时候，super隐式调用父类的构造方法，将父类的属性和方法放到子类的对象空间里。
    6、在继承你关系中，子类能够继承抽象类的各种属性和方法，除了私有的和构造方法。
    7、只有公开的才可以和abstract连用，static final private 都不可以。
        static属于类方法，不允许覆盖，abstract必须被覆盖。final不能被重写。
 
 抽象和接口的区别
 1、关键字：抽象类 abstract      接口interface
2、抽象类继承 extends         接口实现 implements
3、子类继承抽象类和          实现类实现接口的格式不同
4、接口中只有全局变量和抽象方法        抽象类中有各种属性和方法
5、抽象类只能单继承              接口可以多实现
6、抽象类的子类只能继承一个父类    实现类可以实现多个接口，并且还可以继承父类
7、抽象类的作用：提高代码的复用性   接口的作用：1、规范代码2、提高代码的拓展新
```

## 2.7模式

```java
1、单例模式

    分类：懒汉式、饿汉式

    1、构造方法私有化
    2、在本类中创建本类对象
    3、保证对象的唯一性final
    4、给外界提供得到对象的方法 static
    5、在多线程中，饿汉式安全，懒汉式不安全

2、简单工厂模式

    批量创建对象

    1 创建工厂类 : 创建对象的方法
    2 果汁类 是所有种类果汁的父类
    3 在工厂类的方法中返回果汁类
    4 根据测试类中传递的字符串判断到底返回哪种果汁
    5 测试类通过工厂类返回果汁对象

3、建造者模式 

    内部类使用场景
    目的：静态内部类创建外部类对象
    1、 创建外部类，在其中创建一个静态内部类
    2、静态内部类中写属性，构造方法和set get方法
    3、静态内部类中写一个方法，必须返回外部类对象
    4、 给外部类创建对象，传递参数。

4、装饰者模式
    1、在处理流中使用
    2、子类重写父类的方法,提高父类方法的功能及效率
    3、为了尽可能减少重复代码,在重写的方法中用父类的对象调用父类原来的方法
    4、得到父类对象可以通过将父类对象作为子类属性,通过子类构造方法传递父类对象
```

## 2.8 数组及常用算法

```java
1、声明：

  int a[];  int []b;
2、初始化：
    动态初始化：1、a=new int[2]; int[0]=1;...
    动态初始化：2、b=new b[]{3,4};
    静态初始化：int [] c={5,6};

3、数组常用的方法：
    排序：Array.sort();
    查找：Array.binarySearch();
    打印：Array.toString();
    复制：Array.copyof();
4、常用操作

    1、冒泡排序
    for(int i=0;i<a.length-1;i++){//控制外循环的次数
        for(int j=0;j<a.length-1-i;j++){//控制内循环次数，比外循环少一次，与下一个比较
            if(a[j]>a[j+1]){
                int temp=a[j];
                a[j]=a[j+1];
                a[j+1]=temp;
            }
        }
    }

    2、选择排序

    for (int i = 0; i < a.length-1; i++) {
        int k=i;
        for (int j = i; j < a.length-1; j++) {
            if (a[k]>a[j+1]) {
                k=j+1;
            }
        }
        if(i!=k){
            int temp=a[i];
            a[i]=a[k];
            a[k]=temp;
        }
    }

    3、顺序查找

    public static int find(int []b,int a){
    for (int i = 0; i < b.length; i++) {
        if (a==b[i]) {
            return i;
        }
    }
    return -1;
    }
    4、二分查找
    public static int find(int b[],int a){
    int max=b.length-1;
    int min=0;
    for (int i = 0; i < b.length; i++) {
        int midle=(max+min)/2;
        if(a==b[midle]){
            return midle;
        }else if(a>b[midle]){
           min=midle+1;
        }else if(a<b[midle]){
            max=midle-1;
        }
    }
return -1;

}
```

# 三. Java常用类

## 3.1拆箱装箱

```java
1、装箱：把基本数据类型转成包装类类型。

2、拆箱：把包装类类型转成基本数据类型。

3、为什么要包装类？

    八种基本数据类型不满足面向对象的思想，不包括属性和方法。如果给基本数据类型添加功能，只能创建其包装类，将方法和属性封装进去。
    jdk5.0以后出现了自动拆箱，装箱。

4、Integer支持字符串，但字符串必须是数字。Integer integer3=new Integer("2");
   compareTo();     比较大小，大返回整数，小于返回负数，相等返回0
   toBinaryString();    将十进制数转成二进制，返回String字符串的表现形式
   toHexString();   将十进制转成十六进制
   toOctalString(); 将十进制转成八进制
   toString();      将int类型数据转成String字符串
   Integer.valueOf();   将int转成integer类型对象
   new Integer();   将int转成integer类型对象
   parseInt();      将Integer转成int
   intValue();      将Integer转成int
```

## 3.2 String字符串

```java
==                  比较地址
.equals()               比较内容
.equalsIgnoreCase()         忽略大小写比较是否相同
.charAt();              字符串截取出指定的下标开始
.compareTo()                比较大小
.compareToIgnore()          忽略大小比较
.concat()               将参数字符串连接到指定字符串后面
.contains()             是否包含参数字符串
.startsWith()               以指定前缀开头
.endsWith()             以指定后缀结尾
.indexOf("/")               第一次出现
.indexOf("/", 3)            指定位置开始索引
.lastIndexOf("/")           最后一次出现
.substring(string11.lastIndexOf("/")+1);截取指定位置
.substring(string11.lastIndexOf("/")+1, string11.lastIndexOf("."));//截取字符串，指定开始位置和结束位置
.replace('a', 'b')          替换指定字符串，替换所有的
.toUpperCase()              全部转为大写
.toLowerCase()              全部转成小写
.trim()                 去掉字符串前后的空格，中间的去不掉
```

## 3.3 StringBuffer

```java
.append("abckjc");          追加
.insert(2, "mmm");          插入
.delete(2, 4);              删除，参数1是起始下标，参数2是结束下标，左闭右开
.reverse();             逆顺反转
   
   String         长度不可变
  StringBuffer   长度可变   线程安全        速度慢
  StringBuilder  长度可变   线程不安全   速度快
```

## 3.4 Charcter

```java
.isLetter('a');     判断是否为字母
.isLetter('a');     判断是否为小写字母
isUpperCase('A');   判断是否为大写字母
toLowerCase('D');   将大写字母转成小写字母  如果本身是小写字母 则转换完还是小写字母
toUpperCase('f');   将字母专程为大写字母
```

## 3.5正则表达式

```java
字符类

[abc]       a、b、c其中任意一个
[^abc]      除了a、b、c中的任意一个
[a-zA-Z]     a-z或A-Z范围中的任意一个
[a-zA-Z0-9]  a-z A-Z 0-9 其中任意一个
[……]         可以自己定义范围

预定字符类

\d   数字0-9
\D   非数字0-9
\s   空白字符：[ \t\n\x0B\f\r]
\S   非空白字符：\s
\w   单词字符：[a-zA-Z_0-9]
\W   非单词字符\w

数量词

？     一次或者一次也没有
*      0次到多次
+      一次或者多次
{n}    恰好n次
{n,}   至少n次
{n,m}  至少n次但不超过m次
 .matches();    匹配是否适合
 .spil();   拆分
```

## 3.6时间相关的类

```java
1、Date类
    .getTime();计算毫秒
    
2、SimpleDateFormat类  格式化时间
    .format();返回的是String字符串

3、Calendar接口  日历字段之间的转换提供了一些方法
    .get(Calendar.YEAR);
    .get(Calendar.MONTH);// 默认是当前月份减一    从0开始的  
    .get(Calendar.DAY_OF_MONTH);
    .get(Calendar.DAY_OF_WEEK);
        Calendar calendar = Calendar.getInstance();
    Date date = calendar.getTime();

4、Runtime运行时时间
    .freeMemory(); 当前的系统剩余空间

5、System.exit(0);退出程序，参数是0 是正常退出
   System.gc();调用垃圾回收器 ，不一定能够起来 ，只是起到一个促进的作用
```

# 四.集合

```java
数组：长度固定，数据类型相同

集合：长度不固定，数据类型可以不同，只能存对象
collection  
List           Set         
ArrayList      HashSet
LinkedList     TreeSet
Vector		   LinkedHashSet ==> 1、有序不重复
 
Map
HashMap
TreeMap
```

## 4.1 Collection

```

```

## 4.2 List

```java
List：元素是有序的，元素可以重复。因为该集合体系有索引。
        |--ArrayList：底层的数据结构使用的是数组结构。特点：查询速度很快。但是增删稍慢。线程不同步。
        |--LinkedList：底层使用的是链表数据结构。特点：增删速度很快，查询稍慢。
        |--Vector：底层是数组数据结构。线程同步。被ArrayList替代了。

ArrayList：
    增：add();addAll(0,list2);
    获取：get(1)；
    修改：set();
    截取：subList(0, 2);左闭右开

LinkedList：
    增：addFirst(); addLast();      jdk1.6后  offFirst(); offLast();
    获取：getFirst(); getLast();              peekFirst(); peekLast();
    删除：removeFirst(); removeLast();        pollFirst(); pollLast();
    压栈：push();
    弹栈：pop();

    逆序输出：linkedList.descendingIterator()
```

## 4.3 Set

```java
Set：元素是无序（存入和取出的顺序不一定一致），元素不可以重复。     
       |--HashSet：底层数据结构是哈希表。线程不同步。 保证元素唯一性的原理：判断元素的hashCode值是否相同。如果相同，还会继续判断元素的equals方法，是否为true。
       |--TreeSet：可以对Set集合中的元素进行排序。默认按照字母的自然排序。底层数据结构是二叉树。保证元素唯一性的依据：compareTo方法return 0。
       Set集合的功能和Collection是一致的

1、HashSet： 哈希表
    1、可以通过元素的两个方法，hashCode和equals来完成保证元素唯一性。如果元素的HashCode值相同，才会判断equals是否为true。
    如果元素的hashCode值不同，不会调用equals。
    
    2、hashcode是内存地址通过一定运算的到的int类型的数值。返回值是int类型的数据，各个属性的hash值。 相加
    3、hashcode值相同,也不一定是同一个对象 
    4、调用hashcode方法可以帮助去过滤调用完全不可能相同的 对象,提高执行效率
    5、equals最终确定两个对象是否相同的

    @Override
    public int hashCode() {
        // TODO Auto-generated method stub
        int code=name==null?0:name.hashCode();
        return code;
    }

    @Override
    public boolean equals(Object obj) {
        // TODO Auto-generated method stub
        if(obj==this){
            return true;
        }
        if (obj==null) {
            return false;
        }
        if (obj instanceof Person) {
            Person person=(Person)obj;
            if (this.name.equals(person.name)) {
                return true;
            }
    }
    return false;
}

linkedHashSet  1、有序不重复

TreeSet：红黑树
```

## 4.4 Map

```java
  1）该集合存储键值对，一对一对往里存
  2）要保证键的唯一性
 Map
        |--Hashtable：底层是哈希表数据结构，不可以存入null键null值。该集合是线程同步的。JDK1.0，效率低。
        |--HashMap：底层是哈希表数据结构。允许使用null键null值，该集合是不同步的。JDK1.2，效率高。
        |--TreeMap：底层是二叉树数据结构。线程不同步。可以用于给Map集合中的键进行排序。
    初始容量16，加载因子0.75
        Map和Set很像。其实Set底层就是使用了Map集合。
    1、添加
        Vput(K key,V value);//添加元素，如果出现添加时，相同的键，那么后添加的值会覆盖原有键对应值，并put方法会返回被覆盖的值。
        voidputAll(Map <? extends K,? extends V> m);//添加一个集合
    2、删除
        clear();//清空
        Vremove(Object key);//删除指定键值对
    3、判断
        containsKey(Objectkey);//判断键是否存在
        containsValue(Objectvalue)//判断值是否存在
        isEmpty();//判断是否为空

    4、获取
         Vget(Object key);//通过键获取对应的值
         size();//获取集合的长度

1、HashMap
    HashSet底层封装HashMap，所以HashSet中的规律都是用于HashMap的键。值允许重复，允许多个null，键只允许一个null
    如果自定义类作为键，需要重写hashcode的和equals方法，保证事物唯一性。如果作为值，则不重写

    @Override
    public int hashCode() {
        // TODO Auto-generated method stub
        int code=name==null?0:name.hashCode();
        int code2=age;
        int code3=sex.hashCode();
        return code+code2+code3;
    }

    @Override
    public boolean equals(Object obj) {
        // TODO Auto-generated method stub
        if (this==obj) {
            return true;        
        }
        if (obj==null) {
            return false;
        }
        if (obj instanceof Person) {
            Person person=(Person) obj;
            if (this.name.equals(person.name)) {
                if(this.age==person.age){
                    if (this.sex.equals(person.sex)) {
                        return true;
                    }
                }   
            }
        }
        return false;
    }

2、TreeMap

    1、自然排序
        public int compareTo(Person o) {
        // TODO Auto-generated method stub
        if (this.age<o.age) {
            return 1;
        }else if (this.age>o.age) {
            return -1;
        }else {
            CollationKey collationKey=Collator.getInstance().getCollationKey(this.name);
            CollationKey collationKey2=Collator.getInstance().getCollationKey(o.name);
            return collationKey.compareTo(collationKey2);
        }
    }

    2、定制排序
    单独写一个类
        public class GirlCom implements Comparator<Girl> {
        @Override
        public int compare(Girl o1, Girl o2) {
        // TODO Auto-generated method stub
        if(o1.age>o2.age){
            return 1;
        }else if(o1.age<o2.age){
            return -1;
        }else {
            if(o1.weight>o2.weight){
                return 1;
            }else if(o1.weight<o2.weight){
                return -1;
            }else {
                CollationKey collationKey=Collator.getInstance().getCollationKey(o1.name);
                CollationKey collationKey2=Collator.getInstance().getCollationKey(o2.name);
                return collationKey.compareTo(collationKey2);   
                    }
                }
            }
        }



    调用格式：TreeMap< Girl,String > treeMap=new TreeMap< Girl,String>(new GirlCom());   
    
    
   2.Hashtable  如果自定义类作为键，则重写compato方法，如果作为值，则不重写
   3.遍历集合的方式：
   
  	1、keySet();只得出来值
    Set<String> set = map.keySet();//键的集合
    //1、迭代
    Iterator<String> iterator = set.iterator();
    while (iterator.hasNext()) {
        String key = iterator.next();
        System.out.println(map.get(key));
    }

    //2、fore
    for (String string2 : set) {
        System.out.println(map.get(string2));// String2是键
    }

2、entrySet();键-值对方式
    Set<Entry<String, String>>  set2=map.entrySet();
    //迭代
    Iterator<Entry<String, String>> iterator3=set2.iterator();
    while (iterator3.hasNext()) {
        Entry<String, String> kEntry=iterator3.next();
         System.out.println(kEntry);
    }

    //fore
    for (Entry<String, String> entry : set2) {
        System.out.println(entry);
    }
```

# 五.Java IO

## 5.1 File类

```java
1、File类
    创建：File file = new File(路径字符串);
    .exists();文件是否存在
    .delete();删除文件
    .getPath();路径
    .isFile());是文件吗
    .isDirectory();是目录吗
    .getName();名称
    .getAbsolutePath();绝对路径
    .lastModified()；最后修改时间
    .length();文件大小，不能判断目录/文件夹
    .getParent();父路径，得到指定目录的前一级目录
    .getAbsoluteFile();得到文件绝对路径文件
    
    创建：文件
    .createNewFile();创建文件
    .mkdir();创建一层文件夹
    .mkdirs();创建多层文件夹
    File(String path)              通过将给定路径名字符串转换为抽象路径名来创建一个新 File 实例
    File(String path,String child) 根据 parent 抽象路径名和 child 路径名字符串创建一个新 File 实例。
    File(File file,String child)
list()                    返回一个字符串数组，这些字符串目录中的文件和目录。
list(FileNameFilter)      返回一个字符串数组，这些字符串指满足指定过滤器的文件和目录。
listFiles                 返回一个抽象路径名数组，这些路径名目录中的文件。
listFiles(FileNameFilter) 返回抽象路径名数组，这些路径名满足指定过滤器的文件和目录。
```

## 5.2 IO流

```java
按流分向：
    输入流：从数据源到程序中的流   
    输出流：从程序到数据源的流
按数据传输的单位：
    字节流：以字节为单位传输数据的流
    字符流：以字符为单位传输数据的流
按功能分：
    节点流：直接与数据源打交道的流
    处理流：不直接与数据源打交道，与其他流打交道
    
                字节流                       字符流
输入流      InputStream  超类，抽象类       Reader 超类，抽象类
输出流       OutputStream 超类，抽象类       Write  超类，抽象类

流
	read() 一个字节一个字节的读  返回值是读取到得数据的int表现形式   
	read(byte[])  把字节读取到数组中   返回 的是读取到的个数 返回：读入缓冲区的字节总数，如果因为已经到达文件末尾而没有更多的数据，则返回 -1。
	read(byte[],int offset,int length) 指定的数组中偏移的个数  指定的数组的下标  存储数据的长度
	
字节流
	FileInputStream   字节流 输入流 节点流 直接操作文件的
	read();
	read(byte[]);
	read(byte[],off,,len);   （byte[]接受数据，返回值！=-1）

    FileOutputStream  字节流 输出流 节点流
    write(int);
    write(byte[]);
    write(bute[],off,len);
	
	//读取操作
    File file = new File("E:\ceshi.wmv");// 源文件
    File file2 = new File("E:\aaa\ceshi.wmv");// 目标文件
    // 1、创建流对象
    FileInputStream fis = new FileInputStream(file);
    FileOutputStream fos = new FileOutputStream(file2);
    // 2、读取文件
    byte[] bs = new byte[1024];
    int num = 0;
    while ((num = fis.read(bs)) != -1) {
    fos.write(bs);
    }
    // 3、刷新
    fos.flush();
    // 4、关闭流     
    
字符流
        FileReader        字符流 输入流 节点流
        read(char[]);            （char[]接收数据，返回值！=-1）
        FileWriter        字符流 输出流 节点流
        write(char,offset,length);
        循环读取判断 ！=-1
	//读取文件
    File file=new File("E:\22.txt");
    File file2=new File("E:\aa\22.txt");
    FileReader fileReader=new FileReader(file);
    FileWriter fileWriter=new FileWriter(file2);
    char [] ch=new char[4];
    int num=0;
    while((num=fileReader.read(ch))!=-1){
    fileWriter.write(ch,0,num);
    }
    fileWriter.flush();
	关闭流
```

## 5.3缓存流

```java
   BufferedInoutStream   字节流 输入流 处理流    （byte[]接受数据，返回值！=-1） 
   BufferedOutputStream  字节流 输出流
   BufferedReader        字符流 输入流           （String接受数据，返回值！=null）resdLine();
   BufferedWriter        字符流 输出流
   
       readLine();读取一行，返回值String 循环读取判断 ！=null
       newLine();换行
       \r\n换行
            
	//读取文件
    BufferedInputStream bis=new BufferedInputStream(new FileInputStream(new File("E:\ceshi.wmv")));
    BufferedOutputStream bos=new BufferedOutputStream(new FileOutputStream(new File("E:\aa\ceshi.wmv")));
    byte []bs=new byte[1024];
    int num=0;
    long time=System.currentTimeMillis();
    while((num=bis.read(bs))!=-1){
        bos.write(bs,0,num);
    }
    bos.flush();

    关闭流
```

## 5.4 转化流

```java
  字节转字符   InputStreamReader   继承自Reader （String接收数据，返回值！=null）
  字符转字节   OutputStreamWriter  继承自Wriiter
	
	//转化
    BufferedReader bufferedReader=new BufferedReader(new InputStreamReader(new FileInputStream( new File("E:\ceshi.wmv"))));
    BufferedWriter bufferedWriter=new BufferedWriter(new OutputStreamWriter(new FileOutputStream(new File("E:\aa\demo\ceshi.wmv"))));
    String string=null;
    while((string=bufferedReader.readLine())!=null){
        bufferedWriter.write(string);
    }
    bufferedWriter.flush();
    //关闭流
```

## 5.5对象流序列化

```java
   ObjectInputStream    readObject();
   ObjectOutputStream   writeObject(Object obj);

   1、用对象流去存储对象的前提是 将对象序列化 实现接口Serializable
   2、序列化和反序列化（将对象持久化储存）
    将对象转成字节叫序列化
    将字节转成对象叫反序列化
   3、序列化ID，帮助区分版本，可写可不写。
   4、transient修饰不想被序列化的属性，存储默认值
	
	//操作
    Person person =new Person("秋秋", 22);
    Person person2=new Person("菜菜", 21);
    ObjectOutputStream objectOutputStream=new ObjectOutputStream(new FileOutputStream(new File("a.txt")));
    objectOutputStream.writeObject(person);
    objectOutputStream.writeObject(person2);
    objectOutputStream.flush();
    if (objectOutputStream!=null) {
        objectOutputStream.close();
    }

    ObjectInputStream objectInputStream=new ObjectInputStream(new FileInputStream(new File("a.txt")));
        Person person3=(Person) objectInputStream.readObject();
        System.out.println(person3);
        Person person4=(Person) objectInputStream.readObject();
        System.out.println(person4);
        if (objectInputStream!=null) {
            objectInputStream.close();          
        }

  数据包装流（了解）字节流，读取字节

       DataInputStream
       DataOutputStream
       1、新增了很多读取和写入基本数据类型的方法
       2、读取的顺序和写入的顺序一样，否则数据内容会和存入时的不同

        DataOutputStream dataOutputStream = new DataOutputStream(new FileOutputStream(new File("b.txt")));
        dataOutputStream.writeInt(22);
        dataOutputStream.writeLong(34567);
        dataOutputStream.writeBoolean(true);
        dataOutputStream.flush();
        if (dataOutputStream != null) {
            dataOutputStream.close();
        }

    DataInputStream dataInputStream = new DataInputStream(new FileInputStream(new File("b.txt")));
    System.out.println(dataInputStream.readInt());
    System.out.println(dataInputStream.readLong());
    System.out.println(dataInputStream.readByte());
    if (dataInputStream != null) {
        dataInputStream.close();
    }
```

# 六.多线程

## 6.1创建线程的方式

```java
    1、创建一个类继承Thread
    2、重写run方法
    3、创建线程对象
    4、启动线程
    5、Thread.currentThread().getName()，哪个线程调用，名字就是哪个现成的名字
      getName()；super调用父类的getName()，被赋值谁的名字，就打印谁的名字

        
	//操作
    main方法：
    Test2 test=new Test2("一号窗口");test.start();
        Test2 test2=new Test2("二号窗口");test2.start();

    class Test2 extends Thread{
        String name;
        int ticket=10;
         public Test2(String name) {
            super(name);
            this.name = name;
        }
        public void run() {
            while (true) {
                if (ticket>0) {
                    ticket--;
                    System.out.println(Thread.currentThread().getName()+"还剩下"+ticket);
                }else {
                    break;}
            }
        }

    共享资源操作相同
    1、共享资源类实现Runable接口
    2、重写run方法
    3、创建共享资源对象
    4、创建线程对象，将共享资源对象添加到线程中
    5、启动线程
    main方法：
    Test3 test3=new Test3();
    Thread thread=new Thread(test3);
    Thread thread2=new Thread(test3);
    thread.start();
    thread2.start();
    
    class Test3 extends Thread{
        String name;
        int ticket=10;
         public Test2(String name) {
            super(name);
            this.name = name;
        }
        public void run() {
            while (true) {
                if (ticket>0) {
                    ticket--;
                    System.out.println(Thread.currentThread().getName()+"还剩下"+ticket);
                }else {
                    break;}
            }
        }

    贡献资源操作不相同
    1、贡献资源作为一个单独的类
    2、由多个操作去实现Runable接口
    3、把共享资源作为多个操作类的属性
    4、创建线程对象，将共享资源对象添加到线程中
    5、启动线程

    main方法：
    Card card=new Card();
    Boyfriend boyfriend=new Boyfriend(card);
    Girlfriend girlfriend=new Girlfriend(card);
    Thread thread=new Thread(boyfriend);
    Thread thread2=new Thread(girlfriend);
    thread.start();
    thread2.start();
    class Card{
        double money;
    }
    
    class Boyfriend implements Runnable{
        Card card;
        public Boyfriend(Card card){
            this.card=card;
        }
        @Override
        public void run() {
        // TODO Auto-generated method stub
            for (int i = 0; i < 5; i++) {
                card.money+=500;
                System.out.println(Thread.currentThread().getName()+"存500-剩余金额"+card.money);
            }
        }
    }

    class Girlfriend implements Runnable{
        Card card;
        public Girlfriend(Card card){
            this.card=card;
        }
        @Override
        public void run() {
        // TODO Auto-generated method stub
            for (int i = 0; i < 5; i++) {
                card.money-=500;
                System.out.println(Thread.currentThread().getName()+"取500，剩余金额"+card.money);
            }
        }
    }
```

## 6.2 run start区别

```java
run没有开辟新的栈空间，没有新线程，都是主线程在执行
start开辟了新的栈空间，在新的栈空间启动run()方法
```

## 6.3线程的调度

```java
setPriority();分配优先级，默认5,最低1，最高10
.join();插队，阻塞指定的线程等到另一个线程完成以后再继续执行
    .sleep();需要设置睡眠时间
    .yield();礼让，当执行到这个方法时，会让出cpu时间，立马变成可执行状态
sleep和pield的区别：
         sleep                 yeild
        线程进入被阻塞的状态   线程转入暂停执行的状态
```

## 6.4打断线程

```java
1、用标记，当终止线程时，会执行完run方法
2、stop()方法，不建议使用，会执行不到特定的代码
3、interrupt()，只能中断正在休眠的线程，通过抛异常的方法中断线程的终止。
    InputStream inputStream=System.in;
    int m=inputStream.read();
    myThread2.interrupt();//通过外界输入打断  
    
    
    线程的状态
    新建    就绪   执行   死亡  阻塞
```

## 6.5同步

```java
发生在两个以两个以上的线程中
解决代码的重复问题
优点：提高了线程中数据的安全性
缺点：降低了执行效率

 1、同步代码块
synchronized（锁）{同步代码块}
注意：锁分任意锁和互斥锁，锁是对象，琐是唯一的。        

 2、同步方法
public synchroinzed 返回值类型 方法名（）{同步代码}

 3、在共享资源中：
    线程操作相同，琐是this
        synchronized (this) {// 同步代码块，包含同步代码块。任意锁，互斥锁。
            if (ticket > 0) {
                System.out.println(Thread.currentThread().getName() + "---" + ticket--);
            } else {
                break;
            }
        }

    线程操作不相同，琐是共享资源对象
        synchronized (card) {
            card.setMoney(card.getMoney() + 1000);
            System.out.println("Boy+1000---" + card.getMoney());
        }

 4、在同步方法中：

    共享资源，线程操作相同，资源类中的锁是this
    共享资源，线程操作不相同，资源类中的锁也是this

        public synchronized void input(){
            money+=100;
            System.out.println("input+100----"+money);
    }
    
    
  5.在静态方法同步
  在静态方法中同步：懒汉式
  	同步代码块，琐是类.class

同步方法，锁也是类.class

    public  static LazyInstance getInstance(){
        if (instance==null) {
            synchronized (LazyInstance.class) {
                if (instance==null) {
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        // TODO Auto-generated catch block
                        e.printStackTrace();
                    }
                    instance=new LazyInstance();
                }
            System.err.println(instance.hashCode());
            }
            }       
        return instance;
    }
    
    
    经典例子
    面包类：class Bread{属性和构造方法}
	超市类：class Market{
        Bread[] breads=new Bread[];//超市里有面包数组
        int index=-1;//一开始没有面包，下标为-1；
        public synchronized void sale(){
            if(index<=-1){////如果没有没有面包，就等待添加
                this.wait();
                }
            ////如果有面包，就打印面包信息
            System.out.println("消费面包"+breads[index].id+breads[index].name+breads[index].price);
            index--;//面包减少一个
            this.notify();唤醒添加线程
            }

        public synchronized vide add（Bread bread）{
            if(index>=4){
                this.wait();
                }
            indenx++;//面包下标＋1，存入下一面包位置中
            breads[index]=bread;//给数组中的面包赋值
            System.out.println("添加面包"+breads[index].id+breads[index].name+breads[index].price); 
            this.notify();//唤醒销售线程
            }

工厂类：实现Runnable接口：
        将超市类作为属性
        添加构造方法
        重写run方法，调用超市类add方法

顾客类：实现Runnable接口：
        将超市类作为属性
        添加构造方法
        重写run方法，调用超市类sale方法
```

# 七.网络编程

```java
tcp udp

tcp
	    面向连接，数据安全可靠，效率偏低，传输数据大小无限制
udp
		面向无连接，数据安全不可靠，执行效率高，数据大小不超过64kb
 		注意：tcp和udp只是传输协议，只是设定了规范，真正传输的数据ip协议。

        ip协议：将数据从源传递到目的地
        ipv4:32位
        ipv6:128位
        ipconfig 查看ip相关信息
        ping 查看指定ip或者地址能不能连通
```

## 7.1 ip编程

```java
    1、InetAddress，  没有构造方法，只能通过自己的静态方法创建对象
    2、getLocalHost()，   返回值是InetAddress，得到本机的主机名和地址
    3、getByName(ip),    返回值是InetAddress，有参数，可以写ip，网址，得到指定的主机
    4、getHostAddress(), 得到主机的地址
    5、getHostName()，    得到指定的主机名
```

## 7.2 TCP编程

```java
    客户端：
        1、创建socket对象，指定ip地址和端口号
        2、需要从socket中得到OutputStream
            聊天配合字符流输入流使用，直接转换输入输出即可
            文件配合字节流使用，字节流读，socket输出。
        3、将想要发送的数据写入到OutputStream中。flush    
        4、关闭流关闭socket  

    服务器：
        1、创建ServerSocket对象，指定端口号
        2、serversocket.accep()，返回一个Socket对象（客户端发过来的socket）
         接收客户端发送的数据，如果没有接收到，阻塞程序的运行

        3、从Socket中得到InputStream流，将数据从流中读取出来
            聊天配合字符输出流使用。
            文件配合字节输出流使用，socket读，字节流输出。
        4、展示/写入到另外的地方
        5、关闭流，关闭Socket  

    聊天：
    聊天客户端：
        Socket socket=new Socket("127.0.0.1", 65499);
        OutputStream outputStream=socket.getOutputStream();
        BufferedWriter bufferedWriter=new BufferedWriter(new OutputStreamWriter(outputStream));
        InputStream inputStream=socket.getInputStream();
        BufferedReader bufferedReader=new BufferedReader(new InputStreamReader(inputStream));
        Scanner scanner=new Scanner(System.in);
        while (true) {
            System.out.println("客户端：");
            String string=scanner.next();
            bufferedWriter.write(string);
            bufferedWriter.newLine();
            bufferedWriter.flush();
            if (string.equals("拜拜")) {
                break;
            }
            //接收数据
            String string2=null;
                string2=bufferedReader.readLine() ;
                System.out.println("服务器回复："+string2);
                }  
        //关闭流和socket

    聊天服务器：
        ServerSocket serverSocket=new ServerSocket(65499);
        System.out.println("服务器等待中。。。");
        Socket socket=serverSocket.accept();
        InputStream inputStream=socket.getInputStream();
        Scanner scanner=new Scanner(System.in);
        BufferedReader bufferedReader=new BufferedReader(new InputStreamReader(inputStream));
        OutputStream outputStream=socket.getOutputStream();
        BufferedWriter bufferedWriter=new BufferedWriter(new OutputStreamWriter(outputStream));
        String string=null;
        while (true) {
         string=bufferedReader.readLine();
         System.out.println("客户端说"+string);
         if (string.equals("拜拜")) {
                break;
            }
         System.out.println("服务器回复：");
         String string2=scanner.next();
         bufferedWriter.write(string2);
         bufferedWriter.newLine();
         bufferedWriter.flush();
        }

        //关闭各种流和socket等
```

## 7.3 UDP编程

```java
    客户端：
        1、创建套接字对象，DatagramSocket，不需要指定端口号和地址
            （聊天配合字符输入流），文件配合字节输入流
        2、创建数据报包对象DatagramPacket，使用四个参数，指定数据，数据长度，地址，端口号。
        3、send发放发送数据
        4、关闭socket

    服务器：
        1、创建套接字对象DatagramSocket，指定端口号
        2、创建数据报包对象DatagramPacket，用两个参数的。指定数据和数据长度。
        3、receice()接收数据，如果接受不到，阻塞程序。
        4、根据数据报包进行一系列需要的操作

    聊天：
    客户端：
        DatagramSocket datagramSocket=new DatagramSocket();
        BufferedReader bufferedReader=new BufferedReader(new InputStreamReader(System.in));
        while (true) {
            System.out.println("客户端--：");
            String string2=bufferedReader.readLine();
            DatagramPacket datagramPacket=new DatagramPacket(string2.getBytes(), string2.getBytes().length, InetAddress.getLocalHost(),65496);
            datagramSocket.send(datagramPacket);
            if (string2.equals("拜拜")) {
                break;
            }
        byte []buf=new byte[1024];
        DatagramPacket datagramPacket2=new DatagramPacket(buf, buf.length);
        datagramSocket.receive(datagramPacket2);
        String string=new String(datagramPacket2.getData(), 0, datagramPacket2.getLength());
        System.out.println("服务器--"+string);
        }

    服务器：
        DatagramSocket datagramSocket = new DatagramSocket(65496);
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        System.out.println("客户端已准备");
        byte[] buf = new byte[1024];
        while (true) {
            DatagramPacket datagramPacket = new DatagramPacket(buf, buf.length);
            datagramSocket.receive(datagramPacket);
            String string = new String(datagramPacket.getData(), 0, datagramPacket.getLength());
            if (string.equals("拜拜")) {
                break;
            }

        System.out.println("我说~~"+string);
        //回复数据
        System.out.println("你说~~：");
        String string3 = bufferedReader.readLine();
        DatagramPacket datagramPacket2 = new DatagramPacket(string3.getBytes(), string3.getBytes().length,
       InetAddress.getLocalHost(), datagramPacket.getPort());
        if (string3.equals("拜拜")) {
            break;
        }
        datagramSocket.send(datagramPacket2);
        }
```

# 八.反射

```java
1、反射：
    反射是将类中的属性，方法，构造方法等解剖成一个个小的对象，并且能够调用
2、为什么使用反射：
    在一个类中，可以创建另外一个类的对象，调用其的属性和方法，无论那个类是否被创建了。
3、如何使用反射：
    类
    Class class=Class.forName(包名.类名)，每一个类都有唯一的一个类对象，这个类对象可以的得到类中的所有信息。
    
    构造方法
    class.getConstructor(null);     得到无参构造方法，返回Constructor
    class.getConstructor(String.clss,int.class);得到有参构造方法，返回Constructor
    constructor2.newInstance("曹菜菜",21); 返回Object类型的对象
    class.getConstructors();        得到所有构造方法，返回Constructor[]数组

	方法
    getMethod();                得到普通的方法，返回Method，指定方法名
    class1.getMethod("eat", null);      无参、无返回值、非私有的方法。
    class1.getMethod("play", String.class); 有参、无返回值。非私有方法。参数一，方法名。参数
    
二，参数类型.class
    method(n).invoke(object,null);      方法的执行，参数一是对象，参数二是传的参数值。
    getMethods();               得到子类和父类所有普通的方法，返回Method[]数组
    class1.getDeclaredMethod("sleep", null);得到私有的方法
    method6.setAccessible(true);
    class1.getDeclaredMethods();        得到自己类的所有方法，包括私有的，返回Method[]

	属性
    getFields();                得到public所有属性，返回Field[]
    getFileld("name");          得到public属性，返回Field,指定属性名
    field3.set(object5, "菜菜");
    Object object6 = field3.get(object5);
    getDeclareFields();         得到所有属性，包括私有的，返回Field[]
    getDeclareField();          得到属性，包括私有的，指定属性名，返回Field

4、反射的优点
    1、提高了java程序的灵活性和扩展性，降低了耦合性，提高了自适应的能力
    2、允许程序创建和控制任何类的对象，无需提前编码目标类

5、反射的缺点
    1、性能问题
    2、代码维护问题    
```

