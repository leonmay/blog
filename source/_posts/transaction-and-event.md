---
title: Transaction And Event
date: 2016-09-21 12:05:00
tags: base
category: technology
toc: true
---
### 1. 事务(Transaction)
#### 概念
事务(Transaction)是访问并可能更新数据库中各种数据项的一个程序执行单元(unit)。事务通常由高级数据库操纵语言或编程语言（如SQL，C++或Java）书写的用户程序的执行所引起，并用形如begin transaction和end transaction语句（或函数调用）来界定。事务由事务开始(begin transaction)和事务结束(end transaction)之间执行的全体操作组成。
例如：在关系数据库中，一个事务可以是一条SQL语句，一组SQL语句或整个程序。
引申概念： [事务隔离级别](http://baike.baidu.com/link?url=fpM8ILJdEiN56LiN-A4SGPj4SACkYbmajnWrisEE-rTjdSIp39jCvOAfx2m2auDHnaFg8OL1mwOKGpv7P6TVSq)； [脏读、幻读、不可重复读](http://zhidao.baidu.com/link?url=ZspEzixPNiHJ1K6DqncQfqrU9cupapGAs5kYOq1jpE2Jwg1cxiazEuVm9sAHYGx4gEgRN56sADS-3AWuPqkyHS6gT3FF3sheOKhW5VgbA3G)
#### 特性
事务是恢复和并发控制的基本单位。
事务应该具有4个属性：原子性、一致性、隔离性、持久性。这四个属性通常称为ACID特性。
原子性（atomicity）。一个事务是一个不可分割的工作单位，事务中包括的诸操作要么都做，要么都不做。
一致性（consistency）。事务必须是使数据库从一个一致性状态变到另一个一致性状态。一致性与原子性是密切相关的。
隔离性（isolation）。一个事务的执行不能被其他事务干扰。即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰。
持久性（durability）。持久性也称永久性（permanence），指一个事务一旦提交，它对数据库中数据的改变就应该是永久性的。接下来的其他操作或故障不应该对其有任何影响。

### 2. 事件(Event)
#### 构成要素
（1）事件源：指能触发事件的对象，有时又称为事件的发送者和或事件的发布者。
（2）侦听器：指能接收到事件消息的对象。
（3）事件处理程序：当事件发生时对事件进行处理，又称事件函数或事件方法，包含事件处理程序的对象称为事件的接受者，又称事件的订阅者。
#### 概念
事件有系统事件和用户事件。系统事件由系统激发，如时间每隔24小时，银行储户的存款日期增加一天。用户事件由用户激发，如用户点击按钮，在文本框中显示特定的文本。事件驱动控件执行某项功能。
触发事件的对象称为事件发送者；接收事件的对象称为事件接收者。
#### C#中事件机制的工作过程如下：
（1）将实际应用中需通过事件机制解决的问题对象注册到相应的事件处理程序上，表示今后当该对象的状态发生变化时，该对象有权使用它注册的事件处理程序。
（2）当事件发生时，触发事件的对象就会调用该对象所有已注册的事件处理程序。

