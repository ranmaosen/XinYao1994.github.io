---
layout:     post
title:      Session Token相关区别
subtitle:   History Blogs @ 2019/11/21
date:       2019-11-21
author:     baby joker
categories:	Java
tags:	Session Token
---
　　为什么要有session的出现、session的生成方式、session的弊端

​		为什么会有token出现、token的生成方式、token优点

​		token和session的区别









### 1. 为什么要有session的出现 ##

​		由于网络中http协议本身是无状态协议，这样，无法确定你的本次请求和上次请求是不是你发送的。如果要进行类似论坛登录相关的操作，根本实现不了。

### 2. session生成方式

​		浏览器第一次访问服务器，服务器会创建一个session，然后同时为该session生成一个唯一的会话key，也就是sessionId，然后将sessionId与对应的session分别作为key与value保存到缓存中，也可以持久化到数据库中，然后服务器再把sessionId以cookie的形式发送给客户端。这样浏览器下次访问时，会直接带着cookie中的sessionId。然后服务器根据sessionId找到对应的session进行匹配；

​		还有一种是浏览器禁用了cookie或者不支持cookie，这种可以通过URL重写的方式发送到服务器。

​		简单来说，用户访问时说自己是张三，他可能欺骗你，我们在服务器保存张三的信息，给他一个id，让他下次用id直接访问。

### 3. 为什么有token的出现

​		首先session的存储需要一定的空间，其次session的传递一般都是通过cookie来传递，或者url重写的方式；而token在服务器是可以不需要存储用户信息的，而token的传递方式也不限于cookie传递，当然token也是可以保存起来的。

### 4. token的生成方式

​		浏览器第一次访问服务器根据传过来的唯一标识userId，服务器会通过一些算法（如常用的HMAC-SHA256算法，然后加一个秘钥）生成一个token，然后通过BASE64编码一下之后将这个token发给客户端，同时将这个token保存起来，下次请求时带上这个token，服务器再次收到请求后，然后会用相同的算法和秘钥去验证token，如果通过则执行业务操作，不通过则返回不通过消息。

### 5. token和session的区别

​		①	token和session其实都是为了身份验证，session一般翻译为“会话”，而token翻译为“令牌”。

​		②	session服务器会保存一份，可能保存在缓存、文件、数据库；同样session和token都有过期时间一说，都需要管去管理过期时间；

​		③	其实token和session的问题是一种时间与空间的博弈问题，session是空间换时间，token是时间换空间。这两者选择要看具体情况而定。

​		④	session和token都是“客户端存储”，“每次访问携带”，但token很容易设计为自包含的，也就是说**后端不需要记录什么东西，每次一个无状态请求，每次解密验证，每次当场得出合法/非法结论。**这一切判断依据除了固化在的CS两端一些逻辑之外，整个信息都是自包含的。这才是真正的无状态。而sessionId一般都是一段随机字符串，需要到后端去检索id的有效性。万一服务器重启导致内存里的session不见了，或者redis服务器挂了将无法继续。

​		⑤	token从设计上必须通过get参数或者post参数提交，一般是不允许保存在cookies当中的，容易产生csrf漏洞。

​		⑥	session_id和token的作用比较相似，但说session一般既包括客户端中的session_id，也包括服务端内存或数据库中保存的session数据，另外session一般只标识会话，用户身份的信息是间接保存在session数据中的，登录之前也有session，登出甚至换身份登录之后session_id可以保持不变，而token一般跟用户身份有一一对应关系，登出之后token就失效

​		**session方案：**发你一个身份证，上面只有一个id。每次办事去后台查询id是否有效。

​		**token方案：**发你一张加密身份证，上面都是信息。拿出卡片即意味着“自己人”。

### 6. session的弊端

​		①	服务器压力增大：通常session都是存储在内存中，每个用户认证之后都会讲session数据保存在服务器中，而当用户量增大时，服务器压力将增大。

​		②	CSRF跨站伪造请求攻击：session是基于cookie进行用户识别的，cookie被截获，用户就会很容易受到跨站请求伪造的攻击。

​		③	扩展性不强：session存在服务器缓存，也即内存，是不共享的，用户第一次访问为服务器a，第二次访问为服务器b，此时不能判断用户为“未登录状态

### 7. token优点

​		①	无状态：服务端不存储状态，多服务器需要session同步信息。

​		②	存储简单：可以使用浏览器的localStorge等，app也可以使用自带数据库存储字符串。而且不会出现cookie跨域问题。

​		③	携带信息：token可以用JWT来携带部分不敏感信息，比如userId等，服务器只需解密token即可获得。