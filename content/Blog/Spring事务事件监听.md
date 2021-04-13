---
title: "Spring事务事件监听"
layout: page
date: 2019-04-06 15:21
---

Spring支持事件监听，实现ApplicationListener接口

```
@Component
public class MyListener 
        implements ApplicationListener<MyEvent> {
  
    public void onApplicationEvent(MyEvent event) {
        ...
    }
}
```

然后使用ApplicationEventPublisher发送事件

```
@Component
public class MyComponent {

    private final ApplicationEventPublisher publisher;
    
    @Autowired
    public MyComponent(ApplicationEventPublisher publisher) { ... }
    
    public void sendEvent(Something something) {
        this.publisher.publishEvent(new MyEvent(something)); 
    }

}
```

在Spring 4.1，使用@EventListener注解即可，可以搭配@Async注解实现异步任务

```
@Component
public class MyListener {
  
    @EventListener
    public void handleMyEvent(MyEvent event) {
        ...
    }
}
```

但是这样还不能满足需求，在有事务的场景下，例如，新增了配置，在数据库里插入一条配置数据，此时还没提交事务，但是已经发送并接收到了事件，导致没有查询到新增的配置。这就需要在事务提交的边缘试探（逃

Spring提供了@TransactionEventListener注解，使得事件的监听可以在事务的不同阶段执行。默认值为AFTER_COMMIT，即在事务提交后执行监听处理。

```
@Component
public class MyComponent {
  
  @TransactionalEventListener
  public void handleMyEvent(MyEvent<Something> myEvent) { 
    ...
  }

}
```

---

进阶：原理

---

注：

event是否需要继承ApplicationEvent?

@TransactionEventListener，默认在非事务情况下不执行

Spring4.2之后，ApplicationEventPublisher自动被注入到容器中，采用Autowired即可获取？

---

参考: [better-application-events-in-spring-framework-4-2](http://spring.io/blog/2015/02/11/better-application-events-in-spring-framework-4-2)
