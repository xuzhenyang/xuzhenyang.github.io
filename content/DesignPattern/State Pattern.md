---
title: "State Pattern"
layout: page
date: 2018-07-15 20:30
---

# 状态模式

允许对象在内部状态改变时改变它的行为，对象看起来好像修改了它的类。

类图和策略模式一样，策略模式，context主动指定策略；对象模式，context的状态随时间流逝而改变。

# 看代码

定义红绿灯的状态:

```
public interface State {
    void change(Light light);
}

public class RedState implements State {
    @Override
    public void change(Light light) {
        try {
            System.out.println("现在是红灯 请等待10秒");
            TimeUnit.SECONDS.sleep(10);
            light.setState(new GreenState());
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class YellowState implements State {
    @Override
    public void change(Light light) {
        try {
            System.out.println("现在是黄灯 请等待3秒");
            TimeUnit.SECONDS.sleep(3);
            light.setState(new RedState());
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class GreenState implements State {
    @Override
    public void change(Light light) {
        try {
            System.out.println("现在是绿灯 请等待5秒");
            TimeUnit.SECONDS.sleep(5);
            light.setState(new YellowState());
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

定义红绿灯context:

```
public class Light {
    private State state = new RedState();

    public void setState(State state) {
        this.state = state;
    }

    void change() {
        state.change(this);
    }
}
```

测试:

```
public class Main {
    public static void main(String[] args) {
        Light light = new Light();
        while (true) {
            light.change();
        }
    }
}
```

结果:

```
现在是红灯 请等待10秒
现在是绿灯 请等待5秒
现在是黄灯 请等待3秒
现在是红灯 请等待10秒
现在是绿灯 请等待5秒
现在是黄灯 请等待3秒
现在是红灯 请等待10秒
...
```