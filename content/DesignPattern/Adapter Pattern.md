---
title: "Adapter Pattern"
layout: page
date: 2018-06-13 22:50
---

# 适配器模式

适配器模式 : 将一个类的接口，转换为客户期望的另一个接口。

此处指介绍对象适配器，Java不支持多继承，所以不介绍类适配器

# 看代码

目标接口：

```
public interface Target {
    void request();
}
```

适配器：

```
public class Adapter implements Target {

    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    @Override
    public void request() {
        //实现目标接口，并使用被适配对象的引用来转换实现
        System.out.println("可能是真的");
        adaptee.specificRequest();
    }
}
```

被适配的对象：

```
public class Adaptee {
    public void specificRequest() {
        System.out.println("我是假的");
    }
}
```

客户端只需要调用目标接口：

```
public class Client {
    public static void main(String[] args) {
        Target target = new Adapter(new Adaptee());
        target.request();
    }
}
```