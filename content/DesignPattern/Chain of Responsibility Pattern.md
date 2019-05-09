---
title: "Chain of Responsibility Pattern"
layout: page
date: 2018-03-11 22:17
---

# 责任链模式

小明参加中国有西瓜，blablabla念了一段经后，三位导师要依依点评

# 别bb 看代码

需要一个导师的抽象类，持有下一位导师的引用，以及抽象方法

```
public abstract class Judge {
    private Judge next;

    Judge setNext(Judge judge) {
        this.next = judge;
        return this.next;
    }

    void tryNext() {
        if (next != null) {
            next.comment();
        }
    }

    abstract void comment();
}

```

以及三位导师的实现类

```
public class JudgeA extends Judge {
    @Override
    void comment() {
        System.out.println("A : 我觉得OK");
        tryNext();
    }
}

public class JudgeB extends Judge {
    @Override
    void comment() {
        System.out.println("B : 我觉得不行");
        tryNext();
    }
}

public class JudgeC extends Judge {
    @Override
    void comment() {
        System.out.println("C : 阿岳真的很严格");
        tryNext();
    }
}
```

好了导师们可以开始嘴炮了

```
public class Main {

    public static void main(String[] args) {
        Judge judgeA = new JudgeA();
        judgeA.setNext(new JudgeB()).setNext(new JudgeC());
        judgeA.comment();
    }
}

```

那么问题来了，小明到底行不行？

```
A : 我觉得OK
B : 我觉得不行
C : 阿岳真的很严格
```

---

注：责任链可以是如上链状相连，也可以在第三方集中顺序执行