# 将 Spring Cloud 框架应用平滑迁移至 SAE {#concept_123003_zh .concept}

如果您的 Spring Cloud 集群（包含多个应用）已经部署在阿里云上，当前需要将应用迁移至SAE，请参考本文将应用平滑迁移到 SAE 中，并实现基本的服务注册与发现。如果您的 Spring Cloud 集群还未部署到阿里云，请提交工单或联系 SAE 技术支持人员为您提供完整的上云及迁移到 SAE 方案。

## 迁移流程 {#section_mxn_ktz_blk .section}

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/120424/cn_zh/1559210531885/edas-appDev-springCloud-app-migration-archi.png)

1.  （必选）迁移应用

    迁移的应用通常是无状态的，需要先进行应用迁移。

2.  （可选）迁移 SLB 或修改域名配置

    在应用迁移完成后，您还需要迁移 SLB 或修改域名配置。

    -   SLB
        -   如果您的应用在迁移之前已经使用 SLB，应用迁移后可以复用该 SLB。您可以根据您的实际需求选择绑定 SLB 的策略，详情请参见 [SLB 绑定概述](https://help.aliyun.com/document_detail/108135.html)。
        -   如果您的应用在迁移之前没有使用 SLB，建议在迁移完入口应用（如上图所示的 API Gateway）后，为该应用创建并绑定一个新的 SLB。
        -   迁移应用的方案中，推荐使用双注册和双订阅方案，以节约ECS 成本。如果由于某种原因（如原 ECS 端口被占用）不能复用之前的 ECS，则需要采用切流迁移方案，添加新的 ECS用于应用迁移。在应用迁移完成后，依据迁移前应用是否使用SLB，选择复用 SLB 或创建 SLB 并绑定到迁移后应用。
    -   域名

        -   如果迁移后的应用可以复用 SLB，则域名配置无需修改。
        -   如果迁移后的应用需要创建新的 SLB 并绑定，则需要在域名中添加新的 SLB 配置，详情请参见[域名 DNS 修改](https://help.aliyun.com/document_detail/54157.html)，并删除原来不再使用的 SLB。
3.  （可选）迁移存储和消息队列

    -   如果应用迁移前已经部署在阿里云上，同时存储和消息队列同样使用了阿里云相关产品（如 RDS、MQ 等），则应用迁移完成后，迁移前的存储和消息队列无需迁移。
    -   如果应用迁移前没有部署在阿里云上，请提交工单或联系 SAE 技术支持人员为您提供完整的上云及迁移到 SAE 方案。

本文以 Demo 应用演示平滑迁移。Demo下载 [Provider Demo](https://edas-network-connect.oss-cn-beijing.aliyuncs.com/dubbo-edas-demo-zk-provider.zip) , [Consumer Demo](https://edas-network-connect.oss-cn-beijing.aliyuncs.com/dubbo-edas-demo-zk-consumer.zip)。

## 迁移方案 {#section_gzk_otd_zst .section}

迁移应用有两种方案，切流迁移、双注册和双订阅迁移方案。两种方案均可保证应用正常运行不中断情况下完成平滑迁移。

**说明：** 本文将主要介绍双注册和双订阅方案。

-   切流迁移方案

    使用 Spring Cloud Alibaba 将原有的服务注册中心切换到 Nacos。开发一套新的应用部署到 SAE，最后通过 SLB 和域名配置来进行切流。

    如果您选择此方案，那您可以参考[将 Spring Cloud 应用托管到 SAE](https://help.aliyun.com/document_detail/72618.html)开发应用，不需要再阅读迁移应用的后续内容，只需要关注本文末尾的[迁移风险点和技术支持](#)。

-   双注册和双订阅迁移方案

    双注册和双订阅迁移方案指在应用迁移时同时接入两个注册中心（原有注册中心和 SAE 注册中心），以保证已迁移的应用和未迁移的应用之间可相互调用。

    双注册和双订阅平滑迁移方案架构图如下：

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/108540/cn_zh/1559801367562/edas-appDev-Dubbo-app-migration-multiRegis-archi.gif)

    -   已迁移的应用和未迁移的应用之间可以互相发现，从而实现互相调用，保证了业务的连续性。
    -   使用方式简单，仅需要添加依赖，并修改极少代码，实现双注册和双订阅。
    -   支持查看消费者服务调用列表的详情，实时地查看到迁移的进度。
    -   支持在不重启应用的情况下，动态地变更服务注册的策略和服务订阅的策略，只需要重启一次应用就可以完成迁移。

## 迁移第一个应用 {#section_16u_xia_bhd .section}

1.  选择迁移需求优先级最高的应用。

    建议从最下层 Provider 开始迁移。如果调用链路太复杂难分析，可以任意选一应用进行迁移。

2.  步骤二：在应用程序中添加依赖并修改配置 。
    1.  在`pom.xml`文件中添加 `spring-cloud-starter-alibaba-nacos-discovery` 依赖。

        ``` {#codeblock_9sz_hfg_mf2}
        <dependency>
             <groupId>org.springframework.cloud</groupId>
             <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
             <version>{相应的版本}</version>
         </dependency>
        							
        ```

    2.  在 `application.properties` 中添加 nacos-server 的IP地址。

        ``` {#codeblock_48b_6zv_9pn}
        spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
        							
        ```

    3.  Spring Cloud 默认依赖中只能引入一个注册中心，存在多个注册中心时，启动会异常。如果需要至支持多注册，添加依赖 `edas-sc-migration-starter`。

        ``` {#codeblock_smg_e74_kqi}
        <dependency>
             <groupId>com.alibaba.edas</groupId>
             <artifactId>edas-sc-migration-starter</artifactId>
             <version>1.0.2</version>
         </dependency>
        							
        ```

    4.  Ribbon 是实现负载均衡组件，应用从多个注册中心订阅服务，需要修改 Ribbon 配置。在应用启动的主类中，将 RibbonClients 默认配置修改为 `MigrationRibbonConfiguration`。

        假设原有的应用主类启动代码如下：

        ``` {#codeblock_a09_ynv_njk}
        @SpringBootApplication
         public class ConsumerApplication {
             public static void main(String[] args) {
                 SpringApplication.run(ConsumerApplication.class, args);
             }
         }
        								
        ```

        修改后应用主类启动代码如下

        ``` {#codeblock_s5s_59r_izt}
        @SpringBootApplication
         @RibbonClients(defaultConfiguration = MigrationRibbonConfiguration.class)
         public class ConsumerApplication {
             public static void main(String[] args) {
                 SpringApplication.run(ConsumerApplication.class, args);
             }
         }
        								
        ```

        **说明：** 

        在本地修改应用或者应用部署到 SAE 后，如果对应用有其它控制需求（如注册到哪些注册中心或从哪些注册中心订阅），可以通过 Spring Cloud Config 或 Nacos Config 进行动态的配置调整，无需重启应用，调整配置请参考[动态调整服务注册和订阅方式](#)。

        通过 Spring Cloud Config 或 Nacos Config 进行动态配置调整，需要在其应用中添加配置管理依赖和修改配置，使用 Spring Cloud Config 请参考开源文档，使用 Nacos Config 请参考[实现配置管理](https://help.aliyun.com/document_detail/100003.html)。

3.  步骤四：将应用部署到 SAE 中

    根据实际需求将应用部署到 ECS 集群或容器服务 Kubernetes 集群中，具体操作请参见[部署应用概述](https://help.aliyun.com/document_detail/94757.html)。

    -   迁移前已使用 ECS，迁移后将 ECS 导入到 SAE 中，具体操作请参见[导入 ECS](https://help.aliyun.com/document_detail/57453.html) 。

        **说明：** 在导入 ECS 时如果系统提示需要转化后导入，请备份重要数据。

    -   如果需要创建新的 ECS、集群等资源，请在原有 VPC 内创建，保证迁移前后应用网络互通，实现应用平滑迁移。

        ECS、集群等资源创建，具体请参见[创建资源](https://help.aliyun.com/document_detail/87742.html)。

    -   在数据库、缓存、消息队列等产品中为新 ECS 配置 IP 白名单等，确保应用所依赖的第三方组件正常访问。
4.  结果验证
    1.  观察业务运行是否正常。
    2.  查看服务订阅监控。

        如果应用开启了 Spring Boot Actuator 监控功能，请访问 Actuator 查看此应用订阅的各服务的 RibbonServerList 信息。Actuator 地址如下：

        -   Spring Boot 1.x 版本：[http://ip:port/dubboRegistry](http://ip:port/dubboRegistry)
        -   Spring Boot 2.x 版本：[http://ip:port/actuator/dubboRegistry](http://ip:port/actuator/dubboRegistry)
        metaInfo 中 serverGroup 字段表示此节点的服务注册中心。

        ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/120424/cn_zh/1559123295576/edas-appDev-springCloud-app-migration-actuator.png)


## 迁移其它所有应用 {#section_ira_o0d_oc0 .section}

依照[迁移第一个应用](cn.zh-CN/应用开发/应用迁移/将 Dubbo 应用平滑迁移至 SAE.md#section_1dq_z94_ks0)，依次将所有应用迁移到 SAE。

## 清理迁移配置 {#section_o8m_8n9_6ug .section}

迁移完成后，删除原有的注册中心配置和迁移过程专用的依赖`edas-sc-migration-starter`。

`edas-sc-migration-starter` 迁移专用的 starter，长期使用对业务的稳定性没有影响，对于 Ribbon 负载均衡实现有一定的局限性，建议在迁移完毕后删除，并在业务量较小的时间段内进行分批重启应用。

-   动态调整服务注册和订阅方式

    应用迁移过程中，可以通过 SAE 配置管理功能动态变更服务注册和订阅方式。

-   动态调整服务订阅

    系统默认订阅策略是从所有注册中心订阅，并对数据进行聚合。

    您可以通过 SAE 的配置管理修改`spring.cloud.edas.migration.subscribes`属性，选择具体的注册中心订阅数据。

    ``` {#codeblock_7pw_4qj_3c5}
    spring.cloud.edas.migration.subscribes=nacos,eureka # 同时从 Eureka 和 Nacos 订阅服务
    
     spring.cloud.edas.migration.subscribes=nacos        # 只从 Nacos 订阅服务
    						
    ```

-   动态变更服务注册

    系统默认订阅策略是从所有注册中心订阅。

    您可以通过 SAE 的配置管理来调整服务注册中心。

    通过修改`spring.cloud.edas.migration.registry.excludes`属性关闭指定的注册中心。

    ``` {#codeblock_y1b_g6k_445}
    spring.cloud.edas.migration.registry.excludes=   #默认值为空，注册到所有的服务注册中心
    
     spring.cloud.edas.migration.registry.excludes=eureka   #关闭 Eureka 的注册
    
     spring.cloud.edas.migration.registry.excludes=nacos,eureka   #关闭 Nacos 和 Eureka 的注册
    						
    ```

    应用运行时如需要动态修改服务注册策略，可使用 Spring Cloud 配置管理功能在运行时修改此属性。


## 迁移问题咨询 { .section}

迁移过程中遇到异常情况，申请加入钉钉群进行咨询。

**说明：** 为了更好的服务您，请申请时备注公司名与阿里云账号。

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/120424/cn_zh/1559210237205/edas-appDev-springCloud-app-migration-actuator-dingdinggroup.png)

