# Java基础知识

## java标识符
用于给java程序中的变量、类、方法等命名的符号。

* 遵循以下规则
  * 标识符可以由字母、数字、下划线（_）、美元符（$）组成，但不能包含 @、%、空格等其它特殊字符，不能以数字开头。譬如：123name 就是不合法滴
  * 标识符不能是 Java 关键字和保留字（ Java 预留的关键字，以后的升级版本中有可能作为关键字），但可以包含关键字和保留字。如：不可以使用 void 作为标识符，但是 Myvoid 可以
  * 标识符是严格区分大小写的。 所以涅，一定要分清楚 imooc 和 IMooc 是两个不同的标识符哦！
  *  标识符的命名最好能反映出其作用，做到见名知意。

## java中的数据类型

* 数据类型
  * 基本数据类型
    * 数值型：byte|1  short|2  int|4  long|8  float|4  double|8
    * 字符型 char|2 
    * 布尔型 boolean|1 `理论上占1bit，1/8字节，实际处理按1byte处理`
  * 引用数据类型 类(class) 接口(interface) 数组

java 自动类型转换  强制类型转换(大-->小)

[![自动类型转换](base/images/自动类型转换.png)](https://www.cnblogs.com/ljdblog/p/6253799.html "跳转说明")

java中的条件运算符，也称为 “三元运算符”

语法形式：布尔表达式 ？ 表达式1 ：表达式2

```java
    String str = (8>5) ? "8大于5" : "8不大于5";
    Sysout.out.println(str);
```

![符号有限级](base/images/java_fhyxj.png)

## java常用的3种循环

```java
while(判断条件){
    循环操作
}
```

```java
do{
    循环操作
}while(判断条件);
```

```java
for(循环变量初始条件;循环条件;循环变量变化){
    循环操作
}
```
还有`foreach`等遍历操作

`break` 结束循环

`continue` 的作用是跳过循环体中剩余的语句执行下一次循环。

## 数组

```java
int[] score = {76,81,90,72};
```

jquery在线API http://jquery.cuishifeng.cn/index.html

lambda表达式

匿名内部类
```java
new 需要实现的接口() | 父类构造器()
{
    //需要实现的方法或重载父类的方法
}
```

docker run -d --hostname my-rabbit --name rabbit -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin -p 15672:15672 -p 5672:5672 -p 25672:25672 -p 61613:61613 -p 1883:1883 rabbitmq:management

lambda使用方法注意
Lambda表达式只支持函数式接口  也就是只有一个抽象方法的接口




