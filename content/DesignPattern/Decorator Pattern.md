---
title: "Decorator Pattern"
layout: page
date: 2018-06-06 23:00
---

# 装饰器模式

装饰器模式 : 使用组合而不是继承，动态地为对象添加功能

在餐厅点汉堡包，需要配上肥仔快乐水和薯条

Java的I/O使用了装饰器，FilterInputStream就是抽象的装饰类

# 看代码

定义抽象组件以及具体组件：

```
//抽象组件
public abstract class Hamburger {
    String desc = "汉堡包";

    public String getDesc() {
        return desc;
    }

    public abstract double getPrice();
}

//具体对象
public class BigHamburger extends Hamburger {

    public BigHamburger() {
        desc = "大份汉堡";
    }

    @Override
    public double getPrice() {
        return 30;
    }
}
public class SmallHamburger extends Hamburger {

    public SmallHamburger() {
        desc = "小份汉堡";
    }

    @Override
    public double getPrice() {
        return 20;
    }
}
```

抽象装饰类：

```
public abstract class HamburgerDecorator extends Hamburger {
    public abstract String getDesc();
}
```

具体装饰类：

```
//肥仔快乐水！
public class Cola extends HamburgerDecorator {

    private Hamburger hamburger;

    //在构造器中引入被装饰者
    public Cola(Hamburger hamburger) {
        this.hamburger = hamburger;
    }

    @Override
    public String getDesc() {
        return hamburger.getDesc() + ",可乐";
    }

    @Override
    public double getPrice() {
        return hamburger.getPrice() + 8;
    }
}
public class Chips extends HamburgerDecorator {

    private Hamburger hamburger;

    public Chips(Hamburger hamburger) {
        this.hamburger = hamburger;
    }

    @Override
    public String getDesc() {
        return hamburger.getDesc() + ",薯条";
    }

    @Override
    public double getPrice() {
        return hamburger.getPrice() + 12;
    }
}

```

测试:

```
public class Main {
    public static void main(String[] args) {
        Hamburger hamburger1 = new BigHamburger();
        hamburger1 = new Cola(hamburger1);
        hamburger1 = new Chips(hamburger1);
        System.out.println("套餐:" + hamburger1.getDesc() + " | " + "价格:" + hamburger1.getPrice());
        Hamburger hamburger2 = new SmallHamburger();
        hamburger2 = new Cola(hamburger2);
        System.out.println("套餐:" + hamburger2.getDesc() + " | " + "价格:" + hamburger2.getPrice());
    }
}
```

```
套餐:大份汉堡,可乐,薯条 | 价格:50.0
套餐:小份汉堡,可乐 | 价格:28.0
```