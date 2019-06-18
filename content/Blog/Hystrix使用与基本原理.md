---
title: "Hystrix使用与基本原理"
layout: page
date: 2019-06-18 18:12
---
## 基本使用

继承HystrixCommand，在构造器里配置参数

```
public class QueryOrderIdCommand extends HystrixCommand<Integer> {
    private final static Logger logger = LoggerFactory.getLogger(QueryOrderIdCommand.class);
    private OrderServiceProvider orderServiceProvider;

    public QueryOrderIdCommand(OrderServiceProvider orderServiceProvider) {
        super(Setter.withGroupKey(HystrixCommandGroupKey.Factory.asKey("orderService"))
                .andCommandKey(HystrixCommandKey.Factory.asKey("queryByOrderId"))
                .andCommandPropertiesDefaults(HystrixCommandProperties.Setter()
                        .withCircuitBreakerRequestVolumeThreshold(10)//至少有10个请求，熔断器才进行错误率的计算
                        .withCircuitBreakerSleepWindowInMilliseconds(5000)//熔断器中断请求5秒后会进入半打开状态,放部分流量过去重试
                        .withCircuitBreakerErrorThresholdPercentage(50)//错误率达到50开启熔断保护
                        .withExecutionTimeoutEnabled(true))
                .andThreadPoolPropertiesDefaults(HystrixThreadPoolProperties
                        .Setter().withCoreSize(10)));
        this.orderServiceProvider = orderServiceProvider;
    }

    @Override
    protected Integer run() {
        return orderServiceProvider.queryByOrderId();
    }

    @Override
    protected Integer getFallback() {
        return -1;
    }
}
```

调用Command执行请求即可

```
@Test
public void testQueryByOrderIdCommand() {
    Integer r = new QueryOrderIdCommand(orderServiceProvider).execute();
    logger.info("result:{}", r);
}
```

## 运行流程

![](https://raw.githubusercontent.com/wiki/Netflix/Hystrix/images/hystrix-command-flow-chart.png)

## 配合Dubbo统一封装对外请求
