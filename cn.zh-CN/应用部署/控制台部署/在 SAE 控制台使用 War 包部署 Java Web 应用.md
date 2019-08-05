# 在 SAE 控制台使用 War 包部署 Java Web 应用 {#concept_94541_zh .concept}

SAE 是面向应用的 Serverless PaaS 平台，向上抽象了应用的概念，您可以无需管理和维护集群与服务器，只需专注于设计和构建应用程序，将其部署在 SAE。本文介绍如何在 SAE 控制台使用 War 包部署 Java Web 应用。

在 SAE 中部署应用的方式可参考以下表格。

|应用举例|部署方式|参考开发文档|
|----|----|------|
|原生 Spring Cloud|WAR、JAR、镜像|[将 Spring Cloud 应用托管到 SAE](https://help.aliyun.com/document_detail/123013.html)|
|原生 Dubbo|WAR、JAR、镜像|[将 Dubbo 应用托管到 SAE](https://help.aliyun.com/document_detail/123021.html)|
|HSF|WAR、JAR、镜像|/|
|多语言应用|镜像|/|

## 前提条件 {#section_nt6_dmy_cb0 .section}

-   [创建专有网络 VPC](https://help.aliyun.com/document_detail/110363.html#creatVPCInEDASServerless)。
-   有环境隔离需求，请[创建命名空间](https://help.aliyun.com/document_detail/110363.html#creatNamespaceInEDASServerless)。

## 创建 SAE 应用 {#section_gz1_4vd_795 .section}

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
4.  在应用部署配置页面，选择**应用部署方式**选择 **War 包部署**，依据页面指示进行配置。完成设置后单击**确认创建**。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/Serverless/Serverless_console-WAR-deploy.png)

    -   **应用运行环境**：使用 Springboot 或 Dubbo 的用户，应用运行环境请选择apache-tomcat-XXX；使用 HSF 的用户，应用运行环境请选择EDAS-Container-XXX。
    -   **Java环境**：选择 Open JDK 7 或 Open JDK 8。
    -   **文件上传方式**：可选择上传 War 包或War 包地址。
        -   **上传 War 包**：单击**选择文件**，选择待部署 War 包。
        -   **War 包地址**：输入 War 包的存放地址。

            **说明：** 应用部署程序包名仅允许字母、数字，及中划线\( - \)、下划线\( \_ \)两个特殊符号。

    -   **版本**：设置版本（如：1.1.0），不建议用时间戳作为版本号。
    -   **环境变量设置**：参照[如何设置环境变量](https://help.aliyun.com/document_detail/96560.html)配置。
    -   **Hosts 绑定设置**：参照[如何设置 Hosts 绑定](https://help.aliyun.com/document_detail/100335.html)配置。
    -   **应用健康检查**（可选）：参照[如何设置应用健康检查](https://help.aliyun.com/document_detail/96713.html)配置。
5.  进入**应用详情**页，查看应用的基本信息和实例部署信息。

## 结果验证 {#section_5k1_g42_lgt .section}

在**应用详情**页的**实例部署信息**页签查看实例的运行状态。如果**运行状态**显示为绿色的 Running或者 Completed，表示应用部署成功。

## 更多信息 {#section_kzv_6vf_whc .section}

-   在 SAE 部署应用后，可以进行更新、扩缩容、启停应用监控和删除应用等管理操作，具体操作请参见[应用生命周期管理](https://help.aliyun.com/document_detail/113076.html)。
-   在 SAE 中部署应用后，可通过添加公网 SLB 实现公网访问；添加内网 SLB 实现同 VPC 内所有节点够能通过私网负载均衡访问应用，具体操作请参见[绑定SLB](https://help.aliyun.com/document_detail/113305.html)。

## 问题反馈 {#section_l65_t3d_dxm .section}

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

