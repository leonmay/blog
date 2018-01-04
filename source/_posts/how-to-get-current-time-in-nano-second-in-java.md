---
title: How to get current time in nano second in Java
date: 2018-01-01 21:05:00
tags: java
category: technology
toc: true
---
#### background
最近做的一个project，利用serial number表征数据的state，所以需要一个serial number的build function。  
业务需求不再过多介绍，需要mark一下踩过的坑，做一些简单的介绍和总结，希望和同我一样的java小白，能有所收获吧。

#### serial number
serial number/code，也就是流水号或者是序列号。  
[serial code](https://en.wikipedia.org/wiki/Serial_code)应用领域很广，但最主要的作用都是一样的，都是用来表示唯一性的，生成原则是基于不同的[number scheme](https://en.wikipedia.org/wiki/Numbering_scheme)。但是基本上serial number都包含一定的意义（数据库的自增键可能作用更单一），比如通信的IMEI、IMSI，产品中的ISBN、ISSN都可以区分地域，通信中也有不少自定义的serial number会使用time+product+incr_number的方式。
上面提到的project其实也是为了区分唯一性，同时需要表示数据的新旧状态，自然而然就想到了使用time。

#### todo
最初的方案是使用当前的毫秒值+自增序列构造，虽然能够实现功能，但是由于自增序列会影响current time的意义，所以并不是很合适，如果使用自增序列取模，那又可能会影响新旧状态的准确性。so，自然而然，想到了使用更细粒度的时间戳，刚好java的系统库中有nanoTime方法，完美，但是问题也随后而来。

#### nanoTime vs currentTimeMillis
发现问题是在测试的时候，序列号的十进制表示是从33xx起，而不是15xx(UTC Time)，简单的测试和查看了之后，发现问题出在nanoTime，关于nanoTime和currentTimeMillis的区别，万能的www上有太多说明，java的函数介绍也有说明，简单而言，nanoTime由于有越界的可能，设计之初也是使其相对值有意义(好比说指针可以相减，不能求和)，currentTimeMillis能表示系统当前时间。

#### get current time in nano second
问题找到了，就是如何去处理，目前也是简单的使用满足需求的方案（不是最优方案）去实现。
简单而言就是在服务初始化时先定义其实的nanotime和millistime，实际调用是返回哨兵位时间以及累加值
```
public static class StartTime {
public static final long startMillis = System.currentTimeMillis();
public static final long startNano = System.nanoTime();
}

return (System.nanoTime() - startNano) + startMillis * 1000 * 1000;
```
当然上面的例子也是有越界的风险，但是对于需求不影响，也就不再去纠结了

#### fundation
再使用调用方法是要好好看文档，不能想当然，有好的想法也希望可以联系[我](leon.may.yq@gmail.com)