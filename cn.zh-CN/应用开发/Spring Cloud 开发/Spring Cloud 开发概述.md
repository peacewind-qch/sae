# Spring Cloud 开发概述 {#concept_122998_zh .concept}

SAE 支持原生 Spring Cloud 微服务框架，在该框架下开发的应用只需添加依赖和修改配置，即可获取 SAE 企业级的应用托管、应用治理、监控报警和应用诊断等能力，实现代码零代码量应用迁移。

Spring Cloud 提供了简化应用开发的一系列标准和规范。这些标准和规范包含了服务发现、负载均衡、熔断、配置管理、消息事件驱动、消息总线等，同时 Spring Cloud 还在这些规范的基础上，提供了服务网关、全链路跟踪、安全、分布式任务调度和分布式任务协调的实现。

目前业界比较流行的 Spring Cloud 具体实现有 Spring Cloud Netflix、Spring Cloud Consul、Spring Cloud Gateway、Spring Cloud Sleuth 等，最近由阿里巴巴中间件开源的 Spring Cloud Alibaba 也是业界中受关注度很高的另一种实现。

如果您已经使用 Spring Cloud Netflix、Spring Cloud Consul 等 Spring Cloud 组件开发的应用，可以直接部署到 SAE 正常运行并获得应用托管能力，同时还可以不修改任何一行代码直接使用 SAE 所提供的高级监控功能，实现全链路跟踪、监控报警和应用诊断等监控功能。

如果您的 Spring Cloud 应用想使用 SAE 中更多的服务治理相关的功能，那么您需要将您的 Spring Cloud 组件替换为 Spring Cloud Alibaba 中的组件或增加 Spring Cloud Alibaba 组件。

## 兼容性说明 {#section_avu_j97_cvf .section}

SAE 目前支持 Spring Cloud Greenwich、Spring Cloud Finchley 和 Spring Cloud Edgware 三个版本。Spring Cloud、Spring Boot 和 Spring Cloud Alibaba 及各组件的版本对应关系请参见[版本配套关系说明](#section_2vw_cs7_oqi)。

Spring Cloud 功能 、开源实现及 SAE 兼容性如下表所示：

|Spring Cloud 功能|开源实现|SAE 兼容性|
|---------------|----|-------|
|通用功能|服务注册与发现| -   Netflix Eureka
-   Consul Discovery

 |兼容且提供替换组件|
|负载均衡|Netflix Ribbon|兼容|
|服务调用| -   Feign
-   RestTemplate

 |兼容|
|配置管理| -   Config Server
-   Consul Config

 |兼容且提供替换组件|
|服务网关| -   Spring Cloud Gateway
-   Netflix Zuul

 |兼容|
|链路跟踪|Spring Cloud Sleuth|兼容且提供替换组件|
|消息驱动 Spring Cloud Stream| -   RabbitMQ binder
-   Kafka binder

 |兼容且提供替换组件|
|消息总线 Spring Cloud Bus| -   RabbitMQ
-   Kafka

 |兼容且提供替换组件|
|安全|Spring Cloud Security|兼容|
|分布式任务调度|Spring Cloud Task|兼容|
|分布式协调|Spring Cloud Cluster|兼容|

## 版本配套关系说明 {#section_2vw_cs7_oqi .section}

Spring Cloud、Spring Boot 和 Spring Cloud Alibaba 及 SAE 提供的商业化组件的版本配套关系如下表所示。

|Spring Cloud|Spring Boot|Spring Cloud Alibaba|
|------------|-----------|--------------------|
|ANS|ACM|SchedulerX|
|Greenwich|2.1.x|0.9.0.RELEASE|
|Finchley|2.0.x|0.2.2.RELEASE|
|Edgware|1.5.x|0.1.2.RELEASE|

**说明：** Spring Cloud Alibaba Nacos Discovery 和 Spring Cloud Alibaba Nacos Config 分别 ANS 和 ACM 对应的开源组件。

