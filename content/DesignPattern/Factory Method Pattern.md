---
title: "Factory Method Pattern"
layout: page
date: 2018-05-31 23:46
---

# 工厂方法模式

明天就是六一儿童节了，工厂要忙着生产很多糖果

工厂方法模式 : 父类中所需要用到的的对象，推迟到在子类中进行实例化

# 看代码

对工厂和对象进行抽象：

```
//抽象的工厂接口
public abstract class CandyCreator {
    public Candy getCandy(String name) {
        Candy candy = createCandy(name);
        candy.make();
        candy.pack();
        return candy;
    }
    //工厂方法
    abstract Candy createCandy(String name);
}
//抽象的物件
public abstract class Candy {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    abstract void make();
    abstract void pack();
}

```

定义具体的工厂和物件：

```
public class LollipopCreator extends CandyCreator {
    @Override
    Candy createCandy(String name) {
        Candy lollipop = new Candy() {
            @Override
            void make() {
                System.out.println("制作棒棒糖");
            }

            @Override
            void pack() {
                System.out.println("打包棒棒糖");
            }
        };
        lollipop.setName(name);
        return lollipop;
    }
}
```

调用工厂：

```
public class Main {
    public static void main(String[] args) {
        CandyCreator candyCreator = new LollipopCreator();
        Candy candy = candyCreator.getCandy("棒棒糖");
        System.out.println(candy.getName() + "制作完成");
    }
}
```