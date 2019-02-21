---
layout:     post
title:      SpringCloud 概述
subtitle:   History Blogs @ 2019/2/19
date:       2019-02-19
author:     baby joker
categories:	SpringCloud
tags:	SpringCloud
---
　　SpringCloud 概述及其常用组件




---
## 微服务？ Martin Fowler
　　就目前而言，对于微服务业界并没有一个统一的、标准的定义  
　　但通常而言，微服务架构是一种架构模式或者说是一种架构风格，**它提倡将歹意应用程序华为成一组小的服务**，每个服务运行在其自己的独立**进程中**，服务之间相互协调、相互配合，为用户提供最终价值。服务之间采用轻量级的通信机制互相沟通（通常使用的是基于HTTP的RestfulAPI）。每个服务都围绕着具体业务进行构建，并且能够被独立的部署到生产环境、类生产环境。另外，应尽量避免统一的、集中式的服务管理机制，对于具体的一个服务而言，应根据业务上下文，选择合适的语言、工具对其进行构建，可以有一个非常轻量级的集中式管理来协调这些业务，可以使用不同的语言来编写服务，也可以使用不同的数据存储。

## 微服务核心
　　微服务化的核心就是将传统的一站式应用根据业务拆分成一个个的服务，彻底地去耦合，每一个微服务提供单个业务功能的服务，一个服务做一件事，从技术的角度看就是一种小而独立的处理过程，类似进程的概念，能够自行单独启动或者销毁，拥有自己独立的数据库

## 微服务优点
　　1.每个服务足够内聚，足够小，代码容易理解，这样能聚焦一个指定的业务功能或业务需求  
　　2.开发简单、开发效率高，一个服务就专职的做好一件事  
　　3.微服务能够被小团队单独开发，2~5人即可  
　　4.微服务是低耦合的，属于具有功能意义的服务，无论在开发还是部署阶段都是独立的  
　　5.可以使用不同语言进行开发  
　　6.易于与第三方集成，微服务允许容易且灵活的方式集成自动部署，通过持续集成工具（jenkins，Hudson，bamboo）  
　　7.微服务易于被单独开发人员理解、修改、维护。  
　　8.容易融合最新技术  
　　9.**微服务只是业务逻辑的代码，不会和HTML，CSS或者其他界面组件混合。**  
　　10.**每个微服务都有自己的存储能力，可以用自己的数据库**

## 微服务缺点
　　1.开发人员需要处理分布式系统的复杂性  
　　2.多服务运维的难度（随着服务的增加，运维的压力将逐渐增大）  
　　3.系统部署依赖  
　　4.服务间通信成本  
　　5.数据一致性  
　　6.系统集成测试  
　　7.性能监控。。。

## 常见微服务技术栈

| 微服务功能          | 使用技术                                                     | 备注 |
| ------------------- | ------------------------------------------------------------ | ---- |
| 服务开发            | Springboot、Spring、SpringMVC                                |      |
| 服务配置与管理      | Netflix的Archaius、阿里的Diamond                             |      |
| 服务注册于发现      | Eureka、Consul、Zookeeper                                    |      |
| 服务调用            | Rest、RPC、gRPC                                              |      |
| 服务熔断器          | Hystrix、Envoy                                               |      |
| 负载均衡            | Ribbon、Nginx                                                |      |
| 声明式服务调用      | Feign                                                        |      |
| 消息队列            | Kafka、RabbitMQ、ActiveMQ                                    |      |
| 服务配置管理        | SpringCloud Config、Chef                                     |      |
| 服务路由（API网关） | Zuul                                                         |      |
| 服务监控            | Zabbix、Nagios、Metrics、Spectator                           |      |
| 链路追踪            | Zipkin、Brave、Dapper                                        |      |
| 服务部署            | Docker、OpenStack、Kubernetes                                |      |
| 数据流操作开发包    | Spring Cloud Stream（封装与Redis、RabbitMQ、Kafka等发送接收消息） |      |
| 事件消息总线        | Spring Cloud Bus                                             |      |
| ...                 |                                                              |      |


## 当前各大IT公司用的微服务架构有哪些？  
　　1.阿里Dubbo、HSF  
　　2.京东JSF  
　　3.新浪微博Montan  
　　4.当当DubboX

## 选择Spring Cloud微服务架构原因
  
　　1.整体解决方案和框架成熟度  
　　2.社区热度  
　　3.可维护性   
　　4.学习容易  

## 什么是Spring Cloud
　　SpringCloud，基于SpringBoot提供了一整套微服务解决方案，包括服务注册与发现、配置中心、链路监控、服务网关、负载均衡、熔断器等组件，除了基于Netflix的开源组件做高度抽象封装之外，还有一些选型中立的开源组件  
　　SpringCloud利用SpringBoot的开发便利性巧妙地简化了分布式系统基础设施的开发，SpringCloud为开发人员提供了快速构建的分布式系统工具，包括**配置管理、服务发现、熔断器、路由、微代理、事件总线、全局锁、决策精选、分布式会话**等，它们都可以利用SpringBoot的开发风格进行一键部署  
　　SpringBoot并没有重复制造轮子，它只是将目前各家公司开发的比较成熟、经得起实际考研的服务框架组合起来，通过SpringBoot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者一套**简单易懂、易于部署和易于维护的分布式系统开发包**  
　　一句话总结：**SpringCloud是分布式微服务架构下的一站式解决方案**

## SpringCloud与SpringBoot关系

　　SpringBoot专注于便捷开发单体微服务  
　　SpringCloud是关注全局的微服务协调治理框架，它将SpringBoot开发的一个个单体微服务整合并进行管理，为各个微服务之间提供**配置管理、服务发现、断路器、路由、微代理、事件总线、全局锁、决策精选、分布式会话等集成服务**  
　　SpringBoot可以不使用SpringCloud独立开发项目，但SpringCloud离不开SpringBoot的支持
## SpringCloud与Dubbo对比 
　　
| null         | Dubbo         | SpringCloud         |
| ------------ | ------------- | ------------------- |
| 服务注册中心 | ZooKeeper     | Eureka              |
| 服务调用方式 | RPC           | REST API            |
| 服务监控     | Dubbo-monitor | Spring Boot Admin   |
| 断路器       | 不完善        | Hystrix             |
| 服务网关     | 无            | Zuul                |
| 分布式配置   | 无            | Spring Cloud Config |
| 服务跟踪     | 无            | Spring Cloud Sleuth |
| 消息总线     | 无            | Spring Cloud Bus    |
| 数据流       | 无            | Spring Cloud Stream |
| 批量任务     | 无            | Spring Cloud Task   |
 
 
　　**最大的区别**：SpringCloud抛弃了Dubbo的RPC通信，采用的是基于HTTP的REST方式  
　　严格的来说，这两种方式各有优劣。虽然从一定程度上来说，SpringCloud牺牲了服务调用的性能，但也能避免原生RPC带来的问题。而且Rest相比RPC更加灵活，服务提供方和调用方依赖的只依靠“一纸契约”，不存在代码级别的强依赖，在快速演化的微服务环境下更加合适

　　**品牌机与组装机的区别**  
　　SpringCloud的功能更加强大，组件更多，涵盖面更广，能够与Spring Framework、Spring Boot、Spring Data、Spring Batch等其他Spring项目完美融合  
　　使用Dubbo各个环节选择自由度很高，需要自己进行整合与兼容性测试才能保证稳定  
　　**社区活跃度对比**：Dubbo停止了5年左右的更新，虽于2017.07重启，对于技术发展的新需求，需要由开发者自行拓展升级，对于很多想要采用微服务架构的中小软件公司/组织并不太划算（没有强大的技术修改Dubbo源码、整合周边形成一整套结局方案、线上未知的风险性）  SpringCloud活动更频繁   
　　**定位区别：**Dubbo的定位是一款RPC框架，而SpringCloud是微服务架构下的一站式解决方案
## to be continued  -> (12/51)
