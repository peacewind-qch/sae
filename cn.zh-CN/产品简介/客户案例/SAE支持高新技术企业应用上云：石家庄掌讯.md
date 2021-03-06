# SAE支持高新技术企业应用上云：石家庄掌讯

SAE能帮助企业极速上云，将微服务应用平滑地迁移到SAE平台上，不涉及任何代码和业务逻辑的修改，并能通过灵活的应用启停来降低资源使用成本。本文以高新技术企业应用石家庄掌讯为例，介绍SAE在支持企业应用上云方面的成功案例。

石家庄掌讯信息技术有限公司是一家提供企业信息化咨询、创新型软件产品、电商代运营服务，标准化管理、快速发展的高新技术企业。当前公司正处于企业互联网市场突破转型重要阶段，希望将更多精力转移到业务创新，以提升开发和交付效率，降低试错成本。因此选择一套低门槛开箱即用的持续交付、快速部署和运维平台尤为重要。

## 业务痛点

石家庄掌讯面临以下业务痛点：

-   组织、人员权限管理复杂。
-   工程实践、流程规范不容易复用，代码质量无法保证。
-   FTP手工发布效率慢。
-   缺少专职运维人员和微服务改造实战经验，研发运维效率不高。
-   测试开发环境和生产环境的闲置计算资源较多。

## 为什么选择SAE

-   SAE采用阿里云完善的权限管理机制，按需分配权限，降低企业信息安全风险。
-   SAE采用Serverless架构，屏蔽了底层IaaS运维和K8s细节，并且与FaaS形态的Serverless产品不同，无需修改编程模型和改造代码即可直接使用。
-   SAE支持多种部署应用的方式，支持微服务以及多语言应用快速上云，且无需自建监控系统，提供了开箱即用的应用监控能力，极大提升了交付效率。
-   SAE提供丰富的功能和服务，包括应用发布、应用管理、服务治理、自动弹性、一键启停应用和应用监控等。
-   SAE支持基于CPU、内存使用率等监控指标自动触发扩缩容，也支持定时弹性，这种灵活的弹性策略既能轻松应对流量高峰，也真正做到了按需使用，节省了非打卡时段的闲置成本。

## 解决方案

石家庄掌讯解决方案逻辑图如下。

![石家庄掌讯解决方案逻辑图](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1018469951/p164195.png)

方案实施如下：

-   网络准备。

    石家庄掌讯有一定的网络要求，需要在部署前创建VPC，详情参见[创建VPC](/cn.zh-CN/快速入门/准备工作.md)。

-   环境隔离。

    石家庄掌讯对安全要求性较高，可在SAE中以命名空间进行逻辑隔离，详情参见[创建命名空间](/cn.zh-CN/快速入门/准备工作.md)。

-   部署上云。

    SAE内置服务注册中心，提供WAR、JAR和镜像三种便捷上云方式，降低了技术门槛，详情参见[应用部署概述](/cn.zh-CN/应用部署/应用部署概述.md)。

-   应用访问。

    石家庄掌讯部署在SAE后，需要配置SLB以实现公网访问，详情参见[为应用绑定SLB](/cn.zh-CN/应用管理/绑定SLB/为应用绑定SLB.md)和[部署在SAE上的应用如何访问公网](/cn.zh-CN/最佳实践/应用访问公网/部署在SAE上的应用如何访问公网.md)。

-   应用管理。

    SAE提供了应用生命周期管理、应用实例查看、网关路由、一键启停、弹性伸缩等功能，详情参见[应用管理概述](/cn.zh-CN/应用管理/应用管理概述.md)。

    -   开发环境和测试环境，可以使用一键启停功能来批量停止闲置应用，减少资源浪费，详情参见[一键启停应用](/cn.zh-CN/应用管理/一键启停应用.md)。
    -   针对应用的业务潮汐特性，无需规划容量，利用定时弹性伸缩功能即可从容应对，详情参见[配置弹性伸缩策略](/cn.zh-CN/应用管理/配置弹性伸缩策略.md)。
    -   针对应用的请求分发需求，可以通过网关路由功能实现，详情参见[为应用配置网关路由](/cn.zh-CN/应用管理/配置网关路由/为应用配置网关路由.md)。
-   应用监控。
    -   CPU、内存、负载和网络等基础监控，详情参见[基础监控](/cn.zh-CN/监控管理/基础监控.md)。
    -   应用总请求量、平均响应时间等应用健康指标监控，详情参见[应用总览](/cn.zh-CN/应用监控/控制台功能/应用总览.md)。
    -   堆内存指标、非堆内存指标、直接缓冲区指标、内存映射缓冲区指标、GC（垃圾收集）累计详情和JVM线程数等JVM指标监控，详情参见[JVM监控](/cn.zh-CN/应用监控/控制台功能/应用详情/JVM 监控.md)。
    -   CPU、内存、Disk（磁盘）、Load（负载）、网络流量和网络数据包等主机指标监控，详情参见[t152241.md\#](/cn.zh-CN/应用监控/控制台功能/应用详情/主机监控.md)。
    -   SQL分析、异常分析、错误分析、链路上下游和接口快照等接口调用监控，详情参见[应用接口调用监控](/cn.zh-CN/应用监控/控制台功能/应用接口调用监控.md)。

## 开通SAE

单击下方按钮可立即前往SAE开通页面。

