---
title: "Abstract Factory Pattern"
layout: page
date: 2018-05-30 23:09
---

# 抽象工厂模式

抽象工厂模式 : 将所需创建对象的家族抽象为接口，需要时，调用具体工厂的callback来生成对应的对象

当产品只有一种时，抽象工厂变成工厂方法；当产品有多种类型时，工厂方法模式变为抽象工厂。

# 看代码

对工厂和对象进行抽象：

```
//抽象的工厂接口
public interface CarFactory {
    Wheel createWheel();
    CarBody createCarBody();
}
//抽象的物件
public interface Wheel {
    String getSize();
}
public interface CarBody {
    String getColor();
}
```

定义具体的工厂和物件：

```
//具体的工厂
public class AudiCarFactory implements CarFactory {
    @Override
    public Wheel createWheel() {
        return new BigWheel();
    }

    @Override
    public CarBody createCarBody() {
        return new BlackCarBody();
    }
}
public class FerrariCarFactory implements CarFactory {
    @Override
    public Wheel createWheel() {
        return new SmallWheel();
    }

    @Override
    public CarBody createCarBody() {
        return new RedCarBody();
    }
}
//具体的物件
public class BigWheel implements Wheel {
    @Override
    public String getSize() {
        return "轮框都是16寸";
    }
}
public class SmallWheel implements Wheel {
    @Override
    public String getSize() {
        return "轮框都是12寸";
    }
}
public class BlackCarBody implements CarBody {
    @Override
    public String getColor() {
        return "酷炫黑";
    }
}
public class RedCarBody implements CarBody {
    @Override
    public String getColor() {
        return "法拉利红";
    }
}
```

调用工厂：

```
public class Main {
    public static void main(String[] args) {
        System.out.println("---生产奥迪---");
        Wheel audiWheel = new AudiCarFactory().createWheel();
        System.out.println("轮子:" + audiWheel.getSize());
        CarBody audiBody = new AudiCarFactory().createCarBody();
        System.out.println("车身:" + audiBody.getColor());
        System.out.println("---生产法拉利---");
        Wheel ferrariWheel = new FerrariCarFactory().createWheel();
        System.out.println("轮子:" + ferrariWheel.getSize());
        CarBody ferrariBody = new FerrariCarFactory().createCarBody();
        System.out.println("车身:" + ferrariBody.getColor());
    }
}
```