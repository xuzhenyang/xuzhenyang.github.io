---
title: "JUnit"
layout: page
date: 2018-09-07 11:24
---

# 测试异常

1. @Test

```
@Test(expected = IllegalArgumentException.class)
public void test() {
    //注：无法验证在具体某一行抛出异常
    //test code
}
```

2. ExpectedException

```
@Rule
public ExpectedException thrown = ExpectedException.none();

@Test
public void test() {
    //设置预期异常
    thrown.expect(IllegalArgumentException.class);
    thrown.expectMessage("参数不正确");
    //这里会抛出异常
    test.call();
}
```