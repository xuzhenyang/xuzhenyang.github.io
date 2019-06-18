---
title: "Web认证与SSO"
layout: page
date: 2019-02-17 10:49
---

在互联网的上古时期，网页大多都是静态页面，HTTP协议是无状态的，每次请求都是相对独立，返回相同的响应。

随着互联网的发展，网页有了动态交互的内容，不同用户需要看到各自的内容，网站就需要管理会话，来识别不同的用户，返回不同的信息。

## Cookie/Session

这时候就有一个解决方案，用户在系统登录后，服务端生成一个随机的会话标识（session id），并将这个session id返回给客户端，一般保存在浏览器的Cookie里，客户端在之后的请求里带上这个id，服务端就能识别用户。

session信息只保存在单机上，如果有多个登录服务集群，可以使用session粘连来保证获取到统一服务器上的session。但是如果某台服务挂了，这台服务上的用户session全都会失效，使用session复制能够解决，但也很麻烦。

随着系统的扩大，甚至有多系统集群，登录服务的压力也会急剧增加。上述方案不利于登录服务的水平扩展，可以采用memcache集中保存session信息，但是也增加了单点失败的风险，一单出现问题，所有用户都要重新登录。

Cookie还有跨域的限制。

## Token

上述的验证、session保存都在服务端，是不是可以把验证信息保存在客户端？

使用加密算法，将用户信息做数据签名，服务端同样用算法和密钥签名一次，比较验证签名数据即可。这样就不需要额外存储认证信息，利用计算时间来换取空间。

![](https://user-gold-cdn.xitu.io/2019/1/3/168127bc43a44ad3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

当然token里保存的信息是明文的，不能存储敏感信息，而且token无法被强制过期。

## SSO

![](https://bbsmax.ikafan.com/static/L3Byb3h5L2h0dHAvaW1hZ2VzMjAxNS5jbmJsb2dzLmNvbS9ibG9nLzY0MDYzMi8yMDE3MDIvNjQwNjMyLTIwMTcwMjE0MDAzMDEwMjg1LTU3NDg4MTk3MC5wbmc=.jpg)
