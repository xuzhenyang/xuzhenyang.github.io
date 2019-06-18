---
title: "Builder Patternn"
layout: page
date: 2018-03-11 22:17
---

# Builder模式

找对象很难吗？找不到的话自己new一个吧，多new几个也行！

emmm...这个要胸大，那个要腿长，脑壳疼

试试Builder模式吧

# 别bb 看代码

将女朋友的构造器私有化，内置Builder类来构建各个参数

```
public class Girlfriend {
    //一定要有名字!
    private final String name;
    private String face;
    private String boobs;
    private String leg;

    private Girlfriend(GirlfriendBuilder builder) {
        this.name = builder.name;
        this.face = builder.face;
        this.boobs = builder.boobs;
        this.leg = builder.leg;
    }

    public static class GirlfriendBuilder {
        private String name;
        private String face;
        private String boobs;
        private String leg;

        public GirlfriendBuilder(String name) {
            this.name = name;
        }

        public GirlfriendBuilder face(String face) {
            this.face = face;
            return this;
        }

        public GirlfriendBuilder boobs(String boobs) {
            this.boobs = boobs;
            return this;
        }

        public GirlfriendBuilder leg(String leg) {
            this.leg = leg;
            return this;
        }

        public Girlfriend build() {
            return new Girlfriend(this);
        }
    }

    @Override
    public String toString() {
        return "Girlfriend{" +
                "name='" + name + '\'' +
                ", face='" + face + '\'' +
                ", boobs='" + boobs + '\'' +
                ", leg='" + leg + '\'' +
                '}';
    }
}
```

当你需要女朋友的时候，可以非常语义化地进行定制

```
public class Main {

    public static void main(String[] args) {
        Girlfriend girlfriendA = new Girlfriend.GirlfriendBuilder("17岁白丝JK").boobs("贫乳").leg("白丝").build();
        Girlfriend girlfriendB = new Girlfriend.GirlfriendBuilder("网红妹").face("瓜子脸").boobs("大胸").leg("大长腿").build();
        System.out.println(girlfriendA);
        System.out.println(girlfriendB);
    }
}
```

emmmmm...

```
Girlfriend{name='17岁白丝JK', face='null', boobs='贫乳', leg='白丝'}
Girlfriend{name='网红妹', face='瓜子脸', boobs='大胸', leg='大长腿'}
```

---

# 参考

[设计模式之Builder模式]("https://www.jianshu.com/p/e2a2fe3555b9")