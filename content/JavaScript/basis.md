---
title: "basis"
layout: page
date: 2018-01-02 15:24
---

# Promise

Promise是抽象异步处理对象以及对其进行各种操作的组件，Promise的功能是可以将复杂的异步处理轻松地进行模式化(必须按照接口规定的方法编写处理代码)

promise的三种状态：等待（pending）、已完成（fulfilled）、已拒绝（rejected）

then 方法每次都会创建并返回一个新的promise对象

Promise#catch 只是 promise.then(undefined, onRejected); 方法的一个别名

```
promise
    .then(taskA)
    .then(taskB)
    .catch(onRejected)
    .then(finalTask);
```

## 参考

[JavaScript Promise迷你书](http://liubin.org/promises-book/)

---

# 闭包

闭包: 返回的内部函数

函数外无法获得函数内的变量；闭包"封闭了外部状态"，(getName封闭了name)，外部状态的scope失效的时候，还有一份保留在内部

```
var Foo = function () {
    var name = 'fooname';
    var age = 12;
    this.getName = function () {
        return name;
    };
    this.getAge = function () {
        return age;
    };
};
var foo = new Foo();

foo.name;        //  => undefined
foo.age;         //  => undefined
foo.getName();   //  => 'fooname'
foo.getAge();    //  => 12
```