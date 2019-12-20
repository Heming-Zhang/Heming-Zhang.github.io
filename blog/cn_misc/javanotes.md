---
layout: notes
section-type: notes
title: Java 一些零碎知识点
category: cn_misc
---

* TOC
{:toc}
---

## 类的高级特性

### 1.包
* Java包的命名规则是全部使用小写字母
* 包名冲突问题可以通过使用域名的反向来命名，因为域名是独一无二的，则自然不会发生冲突

### 2.异常
* 捕捉异常：经常使用try, catch, finally 模块来捕捉
* 在catch模块中，可以干脆写catch(Exceptionn e)，因为如果是NullPointerException写Arithmetic Exception就捕捉不到
* Java常见异常：
* ClassCastException 类型转换异常
* ClassNotFoundException 未找到相应类异常
* ArithmeticException 算术异常
* 异常的catch需要遵循一定的次序，如果将Exception放在前面，则会优先catch这些异常，后面的ArithmeticException和MyException都不能继续下去了。
* Java中的RuntimeException
![](.//pictures/JavaException.jpg)

### 3.集合类
* java.util包中提供了一些集合类，这些集合类又被称为容器。集合类与数组的不同之处是，数组的长度是固定的，集合的长度是可变的；数组用来存放基本类型的数据，集合用来存放对象的引用。常用的集合有List集合、Set集合和Map集合，其中List与Set继承了Collection接口，各接口还提供了不同的实现类。

![](.//pictures/Collection2.png)

Tips：三目运算符(?:)
```
int a = 2;
int b = 3;
int c = 1;
int result = (a<c)?b:c;
```
上面的例子中，最终result的数值应该是1
* List集合
* Set集合，一般来说，在JDBC中使用ResultSet作为容器来承装数据库中查询结果，最后再使用get方法取出每个字段中的值；但如果在通常的应用中，set若需要同时读取对象时，需要创建接口CompareTo来重载方法
* Map集合，其没有继承Collection接口，提供的是key到value的映射。Map中不能包含相同的key，每个key只能映射一个value。
