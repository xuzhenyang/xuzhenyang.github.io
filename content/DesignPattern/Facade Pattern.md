---
title: "Facade Pattern"
layout: page
date: 2018-06-13 22:50
---

# 外观模式

外观模式 : 提供一个统一的接口，用来访问系统中的其他接口。

例如FacadeService类里组合了AService、BService、CService，提供了一个高层接口，调用其他Service的接口来实现功能。

定义的高层接口，让子系统更容易使用，收拢并减少耦合。