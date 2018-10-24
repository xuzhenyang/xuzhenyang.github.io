---
title: "Proxy Pattern"
layout: page
date: 2018-07-24 22:30
---

# 代理模式

为另一个对象提供一个替身或占位符以控制对这个对象的访问

绘制图片的时候，可以使用proxy实现懒加载，绘制的时候再从url获取图片

也可以使用proxy实现对象访问的控制等

# 看代码

定义图形接口:

```
public interface Graphics {
    void draw();
}
```

图片和图片的代理都实现图形接口:

```
public class Image implements Graphics {

    public Image(String url) {
        System.out.println("从" + url + "获取图片");
    }

    @Override
    public void draw() {
        System.out.println("绘制图形");
    }
}

public class ImageProxy implements Graphics {

    private Graphics image; //持有图形对象的引用
    private String url;

    public ImageProxy(String url) {
        this.url = url;
    }

    @Override
    public void draw() {
        if (image == null) {
            image = new Image(url); //绘制的时候才加载图片
        }
        image.draw();
    }
}
```

绘制图片的实现:

```
public class Painter {
    private Graphics image;

    public Painter() {
        image = new ImageProxy("http://test.com/test");
    }

    void paint() {
        System.out.println("先做一些事");
        image.draw();
        System.out.println("画完了");
    }
}

public class Main {
    public static void main(String[] args) {
        new Painter().paint();
    }
}
```

结果:

```
先做一些事
从http://test.com/test获取图片
绘制图形
画完了
```