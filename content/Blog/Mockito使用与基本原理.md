---
title: "Mockito使用与基本原理"
layout: page
date: 2019-06-17 21:42
---

## 什么是Mockito

Mockito是用于Java的模拟测试框架，可以Mock外部依赖来方便测试

## 基本使用

### 创建与配置Mock

使用mock方法来创建Mock对象

```
// 使用 mock 静态方法创建 Mock 对象.
List mockedList = mock(List.class);
Assert.assertTrue(mockedList instanceof List);

// mock 方法不仅可以 Mock 接口类, 还可以 Mock 具体的类型.
ArrayList mockedArrayList = mock(ArrayList.class);
Assert.assertTrue(mockedArrayList instanceof List);
Assert.assertTrue(mockedArrayList instanceof ArrayList);
```

创建完Mock对象后，可以配置其行为

```
List mockedList = mock(List.class);

// 设置行为
// 当调用 mockedList.add("one") 时, 返回 true
when(mockedList.add("one")).thenReturn(true);
// 当调用 mockedList.size() 时, 返回 1
when(mockedList.size()).thenReturn(1);

Assert.assertTrue(mockedList.add("one"));
// 因为我们没有定制 add("two"), 因此返回默认值, 即 false.
Assert.assertFalse(mockedList.add("two"));
Assert.assertEquals(mockedList.size(), 1);

Iterator i = mock(Iterator.class);
when(i.next()).thenReturn("Hello,").thenReturn("Mockito!");
String result = i.next() + " " + i.next();
//assert
Assert.assertEquals("Hello, Mockito!", result);
```

### Mock与Spy的区别

Mock对象只是目标类型的空壳实例，所有的行为可以被跟踪；而Spy对象是对具体实例的封装，可以调用实例的正常方法

## 基本原理

Mock本质上是一个Proxy代理模式的应用。

Proxy模式，是在对象提供一个proxy对象，所有对真实对象的调用，都先经过proxy对象，然后由proxy对象根据情况，决定相应的处理，它可以直接做一个自己的处理，也可以再调用真实对象对应的方法。

所以Mockito本质上就是在代理对象调用方法前，用stub的方式设置其返回值，然后在真实调用时，用代理对象返回起预设的返回值。

---

参考:[Mockito的使用及原理及分析](https://zhuanlan.zhihu.com/p/28983008)
