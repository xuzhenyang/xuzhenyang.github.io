---
title: "Strategy Pattern"
layout: page
date: 2018-05-28 23:15
---

# 策略模式

小明有一关老是打不过，大哥给了小明三个锦囊妙计，让小明打开试试

策略模式 : 封装具体的算法，客户端可以根据需要替换算法，而不用关心算法的具体实现。

# 看代码

封装锦囊：

```
public interface Kit {
    //Just do it !
    //照着锦囊上写的做就对了
    void doIt();
}
```

锦囊妙计的具体实现：

```
public class KitA implements Kit {
    @Override
    public void doIt() {
        System.out.println("上去就是干");
    }
}
public class KitB implements Kit {
    @Override
    public void doIt() {
        System.out.println("不要慌 去叫大哥来");
    }
}
public class KitC implements Kit {
    @Override
    public void doIt() {
        System.out.println("快跑啊！");
    }
}
```

小明只要拆开就能用：

```

public class XiaoMing {
    private Kit kit;

    public XiaoMing(Kit kit) {
        this.kit = kit;
    }

    public void openKit() {
        kit.doIt();
    }
}


```

不行就读档换一个锦囊试试...

```
public class Main {
    public static void main(String[] args) {
        XiaoMing xiaoMing;
        System.out.println("---小明读取存档---");
        xiaoMing = new XiaoMing(new KitA());
        xiaoMing.openKit();
        System.out.println("---小明读取存档---");
        xiaoMing = new XiaoMing(new KitB());
        xiaoMing.openKit();
        System.out.println("---小明读取存档---");
        xiaoMing = new XiaoMing(new KitC());
        xiaoMing.openKit();
    }
}
```

结果：

```
---小明读取存档---
上去就是干
---小明读取存档---
不要慌 去叫大哥来
---小明读取存档---
快跑啊！
```