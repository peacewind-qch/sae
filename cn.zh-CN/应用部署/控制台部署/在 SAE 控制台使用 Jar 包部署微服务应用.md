# 在 SAE 控制台使用 Jar 包部署微服务应用 {#concept_97761_zh .concept}

SAE 是面向应用的 Serverless PaaS 平台，向上抽象了应用的概念，您可以无需管理和维护集群与服务器，只需专注于设计和构建应用程序，将其部署在 SAE。本文介绍如何在 SAE 控制台使用 Jar 包部署微服务应用。

SAE 应用的部署方式可参考以下表格。

|应用举例|部署方式|参考开发文档|
|----|----|------|
|原生 Spring Cloud|WAR、JAR、镜像|[将 Spring Cloud 应用托管到 SAE](https://help.aliyun.com/document_detail/123013.html)|
|原生 Dubbo|WAR、JAR、镜像|[将 Dubbo 应用托管到 SAE](https://help.aliyun.com/document_detail/123021.html)|
|HSF|WAR、JAR、镜像|/|
|多语言应用|镜像|/|

## 前提条件 {#section_cyn_arn_twp .section}

-   [创建专有网络 VPC](https://help.aliyun.com/document_detail/110363.html#creatVPCInEDASServerless)。
-   有环境隔离需求，请[创建命名空间](https://help.aliyun.com/document_detail/110363.html#creatNamespaceInEDASServerless)。

## 应用 Demo 下载 {#section_daq_hh0_21n .section}

本文以 Demo 应用演示在 SAE 控制台使用 Jar 包部署微服务应用。

-   下载服务提供者应用 Demo : [service-provider](http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/spring-boot-provider-1.0-SNAPSHOT.jar)
-   下载服务消费者应用 Demo：[service-consumer](http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/spring-boot-consumer-1.0-SNAPSHOT.jar)

## 创建服务提供者 {#section_49q_eyv_gn0 .section}

此服务提供者提供了一个简单的 echo 服务，并将自身注册到服务发现中心。

1.  登录 [SAE 控制台](https://sae.console.aliyun.com)。
2.  在左侧导航树选择**轻量级分布式应用服务** \> **应用列表**，进入应用列表页面，单击右上角**创建应用**。
3.  在**应用基本信息**页签内，设置应用相关信息，配置完成后单击**下一步：应用部署配置**。

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/120281/cn_zh/1561951749953/%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A81.png)

    -   **应用名称**：输入应用名称。允许数字，字母，下划线以及中划线组合，仅允许字母开头，最大长度 36 个字符。
    -   **命名空间**：在下拉菜单中选择创建好的命名空间。
    -   **VPC 网络**：在下拉菜单中选择VPC 和 vswitch 。
    -   **应用实例数**：选择要创建的实例个数。
    -   **实例规格**：单击**请选择**，在选择实例规格页面内选择实例的 **CPU** 和 **Memory** 规格。
    -   **应用描述**：填写应用的基本情况，输入的描述信息不超过100个字符。
4.  在应用部署配置页面，选择 **Jar 包部署**，依据页面指示进行配置。完成设置后单击**确认创建**。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/Serverless/Serverless_console-JAR-deploy.png)

    -   **应用运行环境**：使用 Springboot 或 Dubbo 的用户，应用运行环境请选择标准Java应用运行环境；使用 HSF 的用户，应用运行环境请选择EDAS-Container-XXX。
    -   **Java环境**：选择 Open JDK7 或 Open JDK8。

    -   **文件上传方式**：选择上传 Jar 包或Jar 包地址。

-   上传 Jar 包：下载 [service-provider](http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/spring-boot-provider-1.0-SNAPSHOT.jar) ，下载完成后单击**选择文件**，选择下载完毕的 Jar 包 [service-provider](http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/spring-boot-provider-1.0-SNAPSHOT.jar) 并上传。
-   Jar 包地址：右键单击 [service-provider](http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/spring-boot-provider-1.0-SNAPSHOT.jar) 并选择**复制链接地址**，将该地址输入在**Jar 包地址**栏中。
**说明：** 应用部署程序包名仅允许字母、数字，及中划线\( - \)、下划线\( \_ \)两个特殊符号。

    -   **版本**：设置版本（如：1.1.0），不建议用时间戳作为版本号。
    -   **启动命令设置**（可选）：参照[如何设置 Jar 启动命令](https://help.aliyun.com/document_detail/100337.html)配置。
    -   **环境变量设置**：参照[如何设置环境变量](https://help.aliyun.com/document_detail/96560.html)配置。
    -   **Hosts 绑定设置**（可选）：参照[如何设置 Hosts 绑定](https://help.aliyun.com/document_detail/100335.html)配置。
    -   **应用健康检查**（可选）：参照[如何设置应用健康检查](https://help.aliyun.com/document_detail/96713.html)配置。
5.  在创建完成页面单击**应用详情页**，进入应用详情页查看应用的基本信息和实例部署信息。在**实例部署信息**页签查看实例的运行状态，如果**运行状态**显示为绿色的 Running，表示应用部署成功。

## 创建服务消费者 {#section_q0d_24d_6pi .section}

参照[创建服务提供者](#section_49q_eyv_gn0)步骤创建服务消费者。

1.  在应用列表页面右上角单击**创建应用**。
2.  在应用基本信息页面，输入应用相关信息，然后单击**下一步：应用部署配置**。
    -   **应用名称**：输入应用名称，此名称须与服务提供者的应用名称不能相同。

        应用名称命名规则：允许数字，字母，下划线以及中划线组合，且仅允许字母开头，最大长度 36 个字符。

    -   **命名空间**：选择与服务提供者相同的命名空间。
    -   **VPC 网络**：在下拉菜单中选择与服务提供者相同的 VPC 和 vswitch。
    -   **应用实例数**：选择要创建的实例个数。
    -   **实例规格**：单击**请选择**，在选择实例规格页面内选择实例的 **CPU** 和 **Memory** 规格。当完成选择后会在应用基本信息页面显示所选择的规格。
    -   **应用描述**：填写应用的基本情况，输入的描述信息不超过100个字符。
3.  在应用部署配置页面，选择 Jar 包部署，单击**确认创建**。

-   **Java 环境**：选择 JDK7 或 JDK8。
-   **文件上传方式**：选择上传 Jar 包或Jar 包地址。

-   上传 Jar 包：下载 [service-provider](http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/spring-boot-provider-1.0-SNAPSHOT.jar) ，下载完成后单击**选择文件**，选择下载完毕的 Jar 包 [service-provider](http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/spring-boot-provider-1.0-SNAPSHOT.jar) 并上传。
-   Jar 包地址：右键单击 [service-provider](http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/spring-boot-provider-1.0-SNAPSHOT.jar) 并选择**复制链接地址**，将该地址输入在**Jar 包地址**栏中。
**说明：** 应用部署程序包名仅允许字母、数字，及中划线\( - \)、下划线\( \_ \)两个特殊符号。

-   **版本**：设置版本（如：1.1.0），不建议用时间戳作为版本号。
-   **启动命令设置**（可选）：参照[如何设置 Jar 启动命令](https://help.aliyun.com/document_detail/100337.html)配置。
-   **环境变量设置**：参照[如何设置环境变量](https://help.aliyun.com/document_detail/96560.html)配置。
-   **应用健康检查**（可选）：参照[如何设置应用健康检查](https://help.aliyun.com/document_detail/96713.html)配置。

## 服务调用验证 {#section_xfd_o3l_016 .section}

1.  在左侧导航栏选择**轻量级分布式应用服务** \> **应用列表**，进入应用列表页面。在应用列表中找到所创建的服务提供者和服务消费者应用，单击相应的应用名称进入应用详情页。查看服务列表和实时日志验证应用成功发布并互相调用。
2.  在左侧导航栏单击**服务列表**，可以分别查看应用发布和消费服务。
    -   服务提供者可以在**发布的服务**页签查看到所发布的服务。

        ![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/Severless/service-provider-service-list.png)

    -   服务消费者可以在**消费的服务**页签查看到所消费的服务。

        ![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/Severless/service-consumer-service-list.png)

3.  给服务消费者应用[绑定一个公网SLB](https://help.aliyun.com/document_detail/113305.html)，使用绑定后生成的公网IP登录该应用，并开启服务调用。
4.  进入服务消费者应用，在左侧导航树选择**应用监控** \> **应用总览**，查看看调用服务的请求数据。

## 更多信息 {#section_tp6_x4b_0j2 .section}

-   使用 SAE 创建应用后，可以进行更新、扩缩容、启停应用监控和删除应用等管理操作，具体操作方式请参见[应用生命周期管理](https://help.aliyun.com/document_detail/113076.html)。

-   在SAE中创建应用后，可以通过添加公网 SLB 实现公网访问，添加内网 SLB 实现同 VPC 内所有节点够能通过私网负载均衡访问您的应用，具体操作方式请参见[绑定SLB](https://help.aliyun.com/document_detail/113305.html)。


## 更多信息 {#section_wj7_2u2_133 .section}

-   在 SAE 部署应用后，可以进行更新、扩缩容、启停应用监控和删除应用等管理操作，具体操作请参见[应用生命周期管理](https://help.aliyun.com/document_detail/113076.html)。
-   在 SAE 中部署应用后，可通过添加公网 SLB 实现公网访问；添加内网 SLB 实现同 VPC 内所有节点够能通过私网负载均衡访问应用，具体操作请参见[绑定SLB](https://help.aliyun.com/document_detail/113305.html)。

## 问题反馈 {#section_dza_pfj_h5j .section}

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

