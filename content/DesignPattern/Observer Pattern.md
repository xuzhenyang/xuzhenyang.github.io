---
title: "Observer Pattern"
layout: page
date: 2018-06-05 23:30
---

# 观察者模式

观察者模式 : 定义对象的一对多依赖，一个对象状态改变，所有依赖者都会收到通知更新

数据中心更新数据时，通知各个监听的子系统更新数据

Java内置Observer接口及Observable类

# 看代码

定义观察者接口及主题接口：

```
//观察者接口
public interface Observer {
    void update(Data data);
}
//主题接口
public interface Subject {
    void registerObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}
//数据类
public class Data {
    private int x;
    private int y;
    private int z;

    //省略构造器、getter、setter、toString
    ...
}
```

实现数据中心及观察者：

```
//数据中心
public class DataCenter implements Subject {
    private Data data;
    private List<Observer> observers;

    public DataCenter() {
        observers = new ArrayList<Observer>();
    }

    public void setData(Data data) {
        this.data = data;
        notifyObservers();
    }

    @Override
    public void registerObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(data);
        }
    }
}

//子系统
public class FirstSystem implements Observer {
    @Override
    public void update(Data data) {
        System.out.println("1th System update : " + data.toString());
    }
}
public class SecondSystem implements Observer {
    @Override
    public void update(Data data) {
        System.out.println("2nd System update : " + data.toString());
    }
}
```

测试：

```
public class Main {
    public static void main(String[] args) {
        DataCenter dataCenter = new DataCenter();
        System.out.println("初始化dataCenter...");
        FirstSystem firstSystem = new FirstSystem();
        dataCenter.registerObserver(firstSystem);
        System.out.println("注册firstSystem");
        dataCenter.setData(new Data(1, 2, 3));
        SecondSystem secondSystem = new SecondSystem();
        dataCenter.registerObserver(secondSystem);
        System.out.println("注册secondSystem");
        dataCenter.setData(new Data(1, 2, 4));
        dataCenter.removeObserver(secondSystem);
        System.out.println("移除secondSystem");
        dataCenter.setData(new Data(2, 4, 6));
    }
}
```