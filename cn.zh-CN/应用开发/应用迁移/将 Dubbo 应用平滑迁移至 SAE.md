# 将 Dubbo 应用平滑迁移至 SAE {#concept_123004_zh .concept}

如果您的 Dubbo 应用已经部署在阿里云上，当前需要将应用迁移至SAE，请参考本文将应用平滑迁移到 SAE 中，并实现基本的服务注册与发现。如果您的 Dubbo 应用还未部署到阿里云，请提交工单或联系 SAE 技术支持人员为您提供完整的上云及迁移到 SAE 方案。

## 迁移流程 {#section_vjb_6gf_r14 .section}

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

## 迁移方案 {#section_l0c_pd6_6xe .section}

迁移应用有两种方案，切流迁移、双注册和双订阅迁移方案。两种方案均可保证应用正常运行不中断情况下完成平滑迁移。

**说明：** 本文将主要介绍双注册和双订阅方案。

-   切流迁移方案

    使用 Dubbo 将原有的服务注册中心同步到 SAE ConfigServer，开发全新的应用部署到 SAE，通过 SLB 和域名配置进行切流。

    选择此方案，请参考[将 Dubbo 应用托管到 SAE](https://help.aliyun.com/document_detail/97471.html) 开发应用。

-   双注册和双订阅迁移方案

    双注册和双订阅迁移方案指在应用迁移时同时接入两个注册中心（原有注册中心和 SAE 注册中心），以保证已迁移的应用和未迁移的应用之间可相互调用。

    双注册和双订阅平滑迁移方案架构图如下：

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/108540/cn_zh/1559801367562/edas-appDev-Dubbo-app-migration-multiRegis-archi.gif)

    -   已迁移的应用和未迁移的应用之间可以互相发现，从而实现互相调用，保证了业务的连续性。
    -   使用方式简单，仅需要添加依赖，并修改极少代码，实现双注册和双订阅。
    -   支持查看消费者服务调用列表的详情，实时地查看到迁移的进度。
    -   支持在不重启应用的情况下，动态地变更服务注册的策略和服务订阅的策略，只需要重启一次应用就可以完成迁移。

## 迁移第一个应用 {#section_1dq_z94_ks0 .section}

1.  选择迁移需求优先级最高的应用。

    建议从最下层 Provider 开始迁移。如果调用链路太复杂难分析，可以任意选一应用进行迁移。

2.  在应用程序中添加依赖并修改配置 \(双注册、双订阅\)。
    1.  在`pom.xml`文件中添加 `edas-dubbo-migration-bom` 依赖。

        ``` {#codeblock_ctn_wic_ta2}
            <dependency>
                    <groupId>com.alibaba.edas</groupId>
                    <artifactId>edas-dubbo-migration-bom</artifactId>
                    <version>2.6.5.1</version>
                    <type>pom</type>
                </dependency>
        							
        ```

    2.  在 `application.properties` 中添加SAE注册中心的IP地址。

        ``` {#codeblock_c0i_77o_tzd}
        dubbo.registry.address = edas-migration://30.5.124.15:9999?service-registry=edas://127.0.0.1:8080,zookeeper://172.31.20.219:2181&reference-registry=zookeeper://172.31.20.219:2181&config-address=127.0.0.1:8848
        							
        ```

        **说明：** 如果是非 Spring Boot 应用，在 dubbo.properties 或者对应的 Spring 配置文件中进行设置。

        -   `edas-migration://30.5.124.15:9999` 

            多注册中心的头部可以不做修改，启动的时候，如果日志级别是为WARN 及以下，系统可能会上报WARN 的日志，因为 Dubbo 会对 IP 和端口进行校验，请忽略该日志。

        -   `service-registry`是服务的注册中心地址，支持服务的多注册中心，可以注入多个注册中心地址。每个注册中心均采用标准的 Dubbo 注册中心格式；多个用`,`分隔。 示例中172.31.20.219 为ZooKeeper 地址，现场配置时请使用真实地址和端口。
        -   `reference-registry`是服务订阅的注册中心地址，支持多注册或者注册到未迁移前的注册中心。
        -   `config-address`是动态推送的地址。
    3.  其他修改。

        对于非 Spring Boot 的 Spring 应用，需要将`com.alibaba.edas.dubbo.migration.controller.EdasDubboRegistryRest`添加到您的扫描路径中。

3.  步骤三：本地验证

    此处以动态配置的方式为例。

    1.  准备工作

        已完成[ZooKeeper下载](http://mirror.bit.edu.cn/apache/zookeeper/zookeeper-3.4.14/zookeeper-3.4.14.tar.gz)、[轻量配置中心配置](https://help.aliyun.com/document_detail/44163.html)、[Nacos下载及启动](https://nacos.io/zh-cn/docs/quick-start.html)。

    2.  检查服务是否成功注册。
        -   登录轻量配置中心，在服务提供者列表中查看对应的服务。
        -   登录 ZooKeeper，查看服务注册和消费信息。
    3.  （可选） 登录 Nacos，配置服务注册信息。

**说明：** 如果不需要动态配置的话，无需执行此步骤。

|参数|配置及操作|
|--|-----|
|DataId|设置为dubbo.registry.config。|
|Group|设置对应 Dubbo 应用的名称applicationName，如 dubbo-migration-demo-server。 配置信息是应用维度，所以应用名不能重复。|
|配置内容| -   应用级别

    ``` {#codeblock_y9u_uiv_h9g .language-properties}
dubbo.reference.registry=edas://127.0.0.1:8080   ##注册服务的注册中心
dubbo.service.registry=edas://127.0.0.1:8080,zookeeper:127.0.0.1:2181   ##订阅服务的注册中心
																
    ```

-   实例 IP 级别

    ``` {#codeblock_pnx_w8r_ihx .language-properties}
169.254.15.86.dubbo.reference.registry=edas://127.0.0.1:8080,zookeeper:127.0.0.1:2181
169.254.15.86.dubbo.service.registry=edas://127.0.0.1:8080
																
    ```

 集群验证时建议先验证实例 IP 级别，再验证整个应用验证。

 |

    4.  查看迁移后应用调用是否正常，查看注册中心的注册订阅关系。

        -   Spring Boot 1.x 版本：http://ip:port/dubboRegistry
        -   Spring Boot 2.x 版本：http://ip:port/actuator/dubboRegistry
        ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/108540/cn_zh/1559805546095/edas-appDev-dubbo-app-migration-validation.png)

4.  步骤四：将应用部署到 SAE 中

    根据实际需求将应用部署到 ECS 集群或容器服务 Kubernetes 集群中，具体操作请参见[部署应用概述](https://help.aliyun.com/document_detail/94757.html)。

    -   迁移前已使用 ECS，迁移后将 ECS 导入到 SAE 中，具体操作请参见[导入 ECS](https://help.aliyun.com/document_detail/57453.html) 。

        **说明：** 在导入 ECS 时如果系统提示需要转化后导入，请备份重要数据。

    -   如果需要创建新的 ECS、集群等资源，请在原有 VPC 内创建，保证迁移前后应用网络互通，实现应用平滑迁移。

        ECS、集群等资源创建，具体请参见[创建资源](https://help.aliyun.com/document_detail/87742.html)。

    -   在数据库、缓存、消息队列等产品中为新 ECS 配置 IP 白名单等，确保应用所依赖的第三方组件正常访问。
5.  结果验证
    1.  观察业务运行是否正常。
    2.  查看服务订阅监控。

        如果应用开启了 Spring Boot Actuator 监控功能，请访问 Actuator 查看此应用订阅的各服务的 RibbonServerList 信息。Actuator 地址如下：

        -   Spring Boot 1.x 版本：http://ip:port/dubboRegistry
        -   Spring Boot 2.x 版本：http://ip:port/actuator/dubboRegistry
        ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/108540/cn_zh/1559805546095/edas-appDev-dubbo-app-migration-validation.png)

        `dubbo.orig.**`表示应用中配置的注册中心信息。

        `dubbo.effective.**`表示生效的注册中心信息。


## 迁移其它所有应用 {#section_5xq_fgq_84y .section}

依照[迁移第一个应用](#section_1dq_z94_ks0)，依次将所有应用迁移到 SAE。

## 清理迁移配置 {#section_1kt_ykm_zhj .section}

迁移完成后，删除原有的注册中心配置和迁移过程专用的依赖`edas-dubbo-migration-bom`。

修改对应的注册中心地址\(即删除 ZooKeeper 的配置\)，保证 Consumer、Provider 仅从 SAE 订阅。

-   方式一：动态配置

    请参考[本地验证](#)中的方法进行修改。

-   方式二：手动修改

    所有的应用修改完成后，修改应用的注册中心地址，将订阅的地址改为 SAE ConfigServer。

    ``` {#codeblock_xd2_xdw_72q}
    dubbo.registry.address = edas-migration://30.5.124.15:9999?service-registry=edas://127.0.0.1:8080,zookeeper://172.31.20.219:2181&reference-registry=edas://127.0.0.1:8080&config-address=127.0.0.1:8848
    					
    ```

    `reference-registry`的`zookeeper://172.31.20.219:2181`改为`edas://127.0.0.1:8080`。修改完成之后，即可部署应用。

    ``` {#codeblock_xgv_krg_p6k}
    dubbo.registry.address = edas://127.0.0.1:8080
    						
    ```

    **说明：** 当应用迁移完成之后，如果不再使用`ZooKeeper`，需要从注册中心配置中删除`zookeeper://172.31.20.219:2181`


应用重启请选择业务量较小时间段分批进行。

## 迁移问题咨询 {#section_j0w_bue_kpf .section}

迁移过程中遇到异常情况，申请加入钉钉群进行咨询。

**说明：** 为了更好的服务您，请申请时备注公司名与阿里云账号。

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/120424/cn_zh/1559210237205/edas-appDev-springCloud-app-migration-actuator-dingdinggroup.png)

