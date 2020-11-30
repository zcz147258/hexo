---
title: Java8
date:
updated:
type: "tags"
categories: Java
comments:
description: Java8
keywords: Java8
top_img: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2286041472,790384686&fm=26&gp=0.jpg
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2286041472,790384686&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.lambda表达式

本质为函数式接口的实现,如果一个接口只声明了一个抽象方法,那么成为这个接口为函数式接口

```java
@Test
    public void test(){

        Runnable r1 = new Runnable() {
            public void run() {
                System.out.println("run!!!!!!!");
            }
        };
        r1.run();

        Runnable r2 = () -> System.out.println("run111!!!!!!!");
        r2.run();
    }

 @Test
    public void test1(){
        Comparator<Integer> com = new Comparator<Integer>() {
            @Override
            public int compare(Integer o1,Integer o2) {
                return Integer.compare(o1,o2);
            }
        };

        int compare = com.compare(2,5);
        System.out.println(compare);

        //lambda1 类型推断
        Comparator<Integer> com1 = (o1,o2) -> Integer.compare(o1,o2);
        int compare1 = com.compare(3,1);
        System.out.println(compare1);

        //lambda2方法引用写法
        Comparator<Integer> com2 = Integer::compare;
        int compare2 = com.compare(8,10);
        System.out.println(compare2);
    }
```

java内置4大函数式接口

```java
消费型接口 Consumer<T>     viod accept(T t)
供给型接口 Supplier<T>     T get()
函数型接口 Function(T,R)   R apply(T t)
断定型接口 Predicate<T>    boolean test(T t)

//消费型接口
 @Test
    public void test(){
        happyTime(500, new Consumer<Double>() {
            @Override
            public void accept(Double aDouble) {
                System.out.println("价格为："+aDouble);
            }
        });

        happyTime(400,money ->  System.out.println("价格为："+money));
    }

    public void happyTime(double money, Consumer<Double> con){
        con.accept(money);
    }

//断定型接口
public class LambdaTest2 {
    @Test
    public void test() {

        List<String> list = Arrays.asList("北京", "西安", "上海", "南京", "天津", "东京");
//        List<String> filterStrs = filterString(list, new Predicate<String>() {
//            @Override
//            public boolean test(String s) {
//                return s.contains("京");
//            }
//        });
//        System.out.println(filterStrs);

        List<String> filterStrs = filterString(list, s -> s.contains("京"));
        System.out.println(filterStrs);
    }
    //根据给定的规则，过滤字符串，
    public List<String> filterString(List<String> list, Predicate<String> pre){
        ArrayList<String> filterList = new ArrayList<>();
        for (String s: list) {
            if(pre.test(s)){
                filterList.add(s);
            }
        }
        return filterList;
    }
}
```

# 2.方法引用

```java
/**
 * 当要传递给lambda体的操作 已经有实现的方法了 ，可以使用方法引用
 * 对象::非静态方法
 * 类::静态方法
 * 类::非静态方法
 * 要求 ： 接口中的抽象方法的形参列表和返回值类型和方法引用的形参列表和返回值相同
 */
public class demo1 {

    //情况1  对象 :: 实例方法
    //Consumer 中的 void accept(T t)
    //printStream中的 void println(T t)
    @Test
    public void test(){
        Consumer<String> con = str -> System.out.println(str);
        con.accept("北京");

        PrintStream ps = System.out;
        Consumer<String> con1 = ps::println;
        con1.accept("上海");
    }

    /**
     * Supplier中的 T get()
     * Employee 中的String getName()
     */
    public void test2(){
    }
}

@Test
    public void test3(){
        Function<Double,Long> func1 = new Function<Double, Long>() {
            @Override
            public Long apply(Double aDouble) {
                return Math.round(aDouble);
            }
        };
        Long apply = func1.apply(0.8);
        System.out.println(apply);


        Function<Double,Long> func2 =  Math :: round;

        Long apply1 = func2.apply(0.4);
        System.out.println(apply1);
    }

 @Test
    public void test4(){
        Comparator<String> com1 = (s1,s2) ->s1.compareTo(s2);
        System.out.println(com1.compare("abc","abd"));


        Comparator<String> com2 = String::compareTo;
        System.out.println(com2.compare("abd","dasdas"));
    }

    @Test
    public void test5(){
        BiPredicate<String,String> pre1 = (s1,s2) -> s1.equals(s2);
        System.out.println(pre1.test("abc","abc"));

        BiPredicate<String,String> pre2 = String::equals;
        System.out.println(pre1.test("abc","abcd"));
    }
```

# 3.Stream Api

```
Stream是处理集合的关键抽象概念 它可以指定你希望对集合进行的操作，可以执行非常复杂的查找，过滤，映射数据等操作
Stream主要是用来进行计算
Collection 是一种静态的内存数据结构,而Stream是有关计算的

注意
Stream自己不会存储元素
Stream不会改变源对象 相反 他们会返回一个持有结果的新Stream。
Stream操作是延迟执行 这意味着他们会等到需要结果才执行
```

## 3.1生成Stream

```java
/**
 * 生成Stream
 */
public class test {

    /**
     * 集合获取
     */
    public void test1(){
        List<String> list = new ArrayList<>();
        //返回一个顺序流
        list.stream();
        //返回一个并行流
        list.parallelStream();
    }

    /**
     * 数组获取
     */
    public void test2(){
        int[] arr = new int[]{1,2,3,4,5,6};
        IntStream stream = Arrays.stream(arr);
    }

    /**
     * 通过Stream的of
     */
    public void test3(){
        Stream<Integer> integerStream = Stream.of(1, 2, 3, 4, 5);
    }

    /**
     * 无限流
     * 造数据
     */
    @Test
    public void test4(){
        //迭代
        Stream.iterate(0,t -> t + 2).limit(10).forEach(System.out::println);

        //生成
        Stream.generate(Math::random).limit(10).forEach(System.out::println);
    }


}

```

## 3.2筛选切片

```java
/**
 * 筛选和切片
 */
public class middle {

    @Test
    public void test(){
        int[] arr = new int[]{5,6,6,4,5,9,11};
        IntStream stream = Arrays.stream(arr);
//        过滤  filter
//        截断流 limit
//        跳过元素 skip
//        筛选 通过流生成的元素去重 hahCode和equals 去除重复元素
        stream.filter(e -> e % 2 ==0)
                .skip(2)
                .limit(2)
                .forEach(System.out::println);

        //筛选去重
        IntStream stream1 = Arrays.stream(arr);
        stream1.distinct().forEach(System.out::println);
    }
}
```

## 3.3映射

```java
/**
 * 映射
 * map
 * flatmap
 */
public class test3 {
    @Test
    public void test(){
        List<String> str = Arrays.asList("aa", "bb", "cc", "dd");

        //map  接受一个函数作为参数  将元素进行转化或者提取信息
        str.stream().map(e -> e.toUpperCase()).forEach(System.out::println);

        //flatmap 将流中的每个值转化成另一个流，然后把流进行返回
//        str.stream().map(test3::fromStringToStream).forEach(e->e.forEach(System.out::println));
        str.stream().flatMap(test3::fromStringToStream).forEach(System.out::println);
    }

    public static Stream<Character> fromStringToStream(String str){
        ArrayList<Character> list = new ArrayList<>();
        for (Character chars : str.toCharArray()) {
            list.add(chars);
        }
        return list.stream();
    }
}
```

## 3.4排序

```java
/**
 * 排序
 */
public class sort {

    @Test
    public void test(){
        List<Integer> list = Arrays.asList(12, 43, 66, 25, 88, 65, 98, 11, 23, 12);
        //自然排序
        list.stream().sorted().forEach(System.out::println);

        //自定义排序
        list.stream().sorted((e1,e2)->{
            return Integer.compare(e2,e1);
        }).forEach(System.out::println);
    }
}
```

## 3.5终止

```java
/**
 * 终止操作 forEach也可以
 */
public class end {

    @Test
    public void test(){
        List<Integer> list = Arrays.asList(12, 43, 66, 25, 88, 65, 98, 11, 23, 12);
        //全部匹配
        boolean b = list.stream().allMatch(e -> e > 20);

        //部分匹配
        boolean b1 = list.stream().anyMatch(e -> e > 20);

        //是否没有
//        boolean b2 = list.stream().noneMatch();

        //第一个元素
        Optional<Integer> first = list.stream().findFirst();

        //返回任意元素
        Optional<Integer> any = list.parallelStream().findAny();

        //求总数
        long count = list.stream().filter(e -> e > 50).count();

        //求最大值
//        list.stream().max(e -> e.getSalary());
        System.out.println(count);
    }
}
```

## 3.6归约

```java
/**
 * reduce
 * 归约
 */
public class reduce {

    @Test
    public void test(){
        //求和
        List<Integer> list = Arrays.asList(1,2,3,4,5,6,7,8,9,10);
        Integer sum = list.stream().reduce(8, Integer::sum);
        System.out.println(sum);
    }
}
```

## 3.7收集

```java
**
 * 收集  对流进行收集
 */
public class collect {

    @Test
    public void test(){
        List<Integer> list = Arrays.asList(12, 43, 66, 25, 88, 65, 98, 11, 23, 12,88);

        List<Integer> collect = list.stream().filter(e -> e > 20).collect(Collectors.toList());
        Set<Integer> collect1 = list.stream().filter(e -> e > 20).collect(Collectors.toSet());
        System.out.println(collect);
        System.out.println(collect1);
    }
}
```

# 4.Options类

```
为了解决空指针异常
是一个容器类
```

```java
public class test {

    @Test
    public void test1(){
        Optional<Girl> girl = Optional.of(new Girl());
        System.out.println(girl);
    }

    @Test
    public void test2(){
        Optional<Girl> girl = Optional.ofNullable(new Girl());
        System.out.println(girl);
    }
}
```

