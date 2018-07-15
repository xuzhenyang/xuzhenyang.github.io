---
title: "Simple Factory Pattern"
layout: page
date: 2018-05-29 22:39
---

# 简单工厂模式

很简单的工厂模式

简单工厂模式 : 封装创建对象的逻辑

# 看代码

定义对象：

```
public class Product {
    private String name;
    private String price;
    private String type;

    public Product(String name, String price, String type) {
        this.name = name;
        this.price = price;
        this.type = type;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPrice() {
        return price;
    }

    public void setPrice(String price) {
        this.price = price;
    }

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }

    @Override
    public String toString() {
        return "Product{" +
                "name='" + name + '\'' +
                ", price='" + price + '\'' +
                ", type='" + type + '\'' +
                '}';
    }
}
```

定义工厂，用静态方法封装创建对象的逻辑：

```
public class SimpleFactory {
    public static Product createProduct(String type) {
        if ("food".equals(type)) {
            return new Product("Oreo", "10元", "food");
        }
        else if ("drink".equals(type)) {
            return new Product("Cola", "3元", "drink");
        }
        else {
            return null;
        }
    }
}
```

调用工厂：

```
public class Main {
    public static void main(String[] args) {
        System.out.println("---生产食物---");
        System.out.println(SimpleFactory.createProduct("food"));
        System.out.println("---生产饮料---");
        System.out.println(SimpleFactory.createProduct("drink"));
    }
}
```