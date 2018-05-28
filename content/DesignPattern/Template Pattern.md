---
title: "Template Pattern"
layout: page
date: 2018-03-07 22:45
---

# 模板模式

有点饿了，想吃点东西

喝牛奶和吃饼干，可能没什么区别吧，对于饿的人来说。

如果有一些共同的流程步骤，试试模板模式吧。

模板负责控制流程，模板的实现类只需要关注每个步骤的细节。

# 别bb 看代码

吃东西的流程：

```
public abstract class EatFood {
    //拿吃的
    protected abstract void getFood();
    //拆包
    protected abstract void unwrap();
    //吃
    protected abstract void eat();
    //完整流程
    public void eatFood() {
        getFood();
        unwrap();
        eat();
    }
}
```

喝牛奶的细节：

```
public class DrinkMilk extends EatFood {
    @Override
    protected void getFood() {
        System.out.println("从冰箱里拿牛奶");
    }

    @Override
    protected void unwrap() {
        System.out.println("打开牛奶盒");
    }

    @Override
    protected void eat() {
        System.out.println("喝掉它！");
    }
}
```

吃奥利奥的细节：

```
public class EatOreo extends EatFood {
    @Override
    protected void getFood() {
        System.out.println("去小卖部买了奥利奥");
    }

    @Override
    protected void unwrap() {
        System.out.println("撕开包装");
    }

    @Override
    protected void eat() {
        System.out.println("扭一扭 泡一泡 舔一舔");
    }
}
```

开吃吧！

```
public class Main {

    public static void main(String[] args) {
        EatFood drinkMilk = new DrinkMilk();
        EatFood eatOreo = new EatOreo();
        drinkMilk.eatFood();
        System.out.println("---");
        eatOreo.eatFood();
    }
}
```

```
从冰箱里拿牛奶
打开牛奶盒
喝掉它！
---
去小卖部买了奥利奥
撕开包装
扭一扭 泡一泡 舔一舔
```