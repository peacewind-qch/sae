# 在 SAE 控制台使用镜像部署应用 {#concept_97675_zh .concept}

SAE 是面向应用的 Serverless PaaS 平台，向上抽象了应用的概念，您可以无需管理和维护集群与服务器，只需专注于设计和构建应用程序，将其部署在 SAE。本文介绍如何在 SAE 控制台使用镜像部署应用。

SAE 支持通过镜像部署 SAE 应用，进行应用管理。

SAE 应用的部署方式可参考以下表格。

|应用举例|部署方式|参考开发文档|
|----|----|------|
|原生 Spring Cloud|WAR、JAR、镜像|[将 Spring Cloud 应用托管到 SAE](https://help.aliyun.com/document_detail/123013.html)|
|原生 Dubbo|WAR、JAR、镜像|[将 Dubbo 应用托管到 SAE](https://help.aliyun.com/document_detail/123021.html)|
|HSF|WAR、JAR、镜像|/|
|多语言应用|镜像|/|

## 前提条件 {#section_5th_epm_m58 .section}

1.  [创建专有网络 VPC](https://help.aliyun.com/document_detail/110363.html#creatVPCInEDASServerless)。
2.  [创建命名空间](https://help.aliyun.com/document_detail/110363.html#creatNamespaceInEDASServerless)。
3.  [制作应用镜像](https://help.aliyun.com/document_detail/98492.html)。

## 创建 SAE 应用 {#section_wwi_jgi_33h .section}

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
4.  在应用部署配置页面，选择 **镜像**，依据页面指示进行配置。完成设置后单击**确认创建**。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/serverless-app-image-development.png)

-   **配置镜像**：在镜像列表的下拉框内选择您所创建的镜像，镜像选中后会在配置镜像后面显示您所选择的镜像。
-   **启动命令设置**（可选）：参照[如何设置 Jar 启动命令](https://help.aliyun.com/document_detail/100337.html)配置。
-   **环境变量设置**：参照[如何设置环境变量](https://help.aliyun.com/document_detail/96560.html)配置。
-   **Hosts 绑定设置**：参照[如何设置 Hosts 绑定](https://help.aliyun.com/document_detail/100335.html)配置。
-   **应用健康检查**（可选）：参照[如何设置应用健康检查](https://help.aliyun.com/document_detail/96713.html)配置。
5.  进入应用详情页面，查看应用的基本信息和实例部署信息。

## 更新应用 {#section_7o6_8fh_b08 .section}

SAE 应用创建过程已经实现了应用部署，故**部署应用**主要用于更新应用，对运行环境变量、镜像配置和启动命令等配置项进行修改。

1.  在应用列表中，单击采用镜像部署的 SAE 应用名称，进入应用详情页面。
2.  在页面右上角单击**部署应用**。
3.  在部署应用页面，重新选择镜像，修改**最小存活实例数**，并可以修改配置启动命令、环境变量和健康检查等高级设置选项，然后单击**确认**。
4.  应用升级过程时，您可以在应用详情页面上方单击**查看详情**进入到变更详情页面，查看部署流程和执行日志。部署完成后，**执行状态**变为 Running则表示更新成功。

## 结果验证 {#section_bv5_gfw_yd2 .section}

应用发布后，通过查看实例运行状态或登录负载均衡配置网址两种方式验证应用已成功发布。

-   查看应用实例运行状态。

    在应用详情页中**实例部署信息**页签查看实例的运行状态。如果**执行状态**显示为绿色的 **Running**或者 **Completed**，表示应用发布成功。

-   配置公网负载均衡并访问应用。

    应用发布过程中或发布后，可以根据实际需要，通过配置负载均衡 SLB 在指定范围内开放应用，以便其它应用访问。

    负载均衡包括两类：

    -   **私网负载均衡**：在应用所在的 VPC 内提供应用的访问入口，保证应用能被同 VPC 内的其它应用访问。
    -   **公网负载均衡**：为该应用自动购买一个公网 SLB 服务，保证该应用能被公网中的其它应用访问。
    配置公网 SLB 访问和配置私网 SLB 访问的步骤相同，本文以配置公网 SLB 访问为例。

    1.  在应用详情页**基本信息**页签的**应用访问设置**区域，单击**添加公网 SLB 访问**。
    2.  在**添加公网 SLB 访问**对话框中设置 SLB 的侦听规则，负载均衡服务侦听规则中定义了如何将请求转发给后端服务器。一个负载均衡实例至少添加一个侦听。设置完侦听参数后单击**确定**。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/serverless-app-add-SLB.png)

        -   **SLB 端口**：公网负载均衡前端端口，通过该端口访问应用，可设置范围为1~65535。
        -   **容器端口**：进程侦听的端口。一般由程序定义，比如：Web 服务默认使用 8080 端口；MySQL 服务默认使用 3306 端口。
        -   **网络协议**：默认为 TCP，不可配置。
        **说明：** 请勿在服务均衡管理控制台上删除该侦听，否则将影响应用访问。

    3.  复制配置的 SLB IP 及端口，加上应用部署包的名称，如 39.106.245.40/80/image，在浏览器的地址中输入并回车，即可进入应用。

## 更多信息 {#section_42w_ydx_dow .section}

-   在 SAE 部署应用后，可以进行更新、扩缩容、启停应用监控和删除应用等管理操作，具体操作请参见[应用生命周期管理](https://help.aliyun.com/document_detail/113076.html)。
-   在 SAE 中部署应用后，可通过添加公网 SLB 实现公网访问；添加内网 SLB 实现同 VPC 内所有节点够能通过私网负载均衡访问应用，具体操作请参见[绑定SLB](https://help.aliyun.com/document_detail/113305.html)。

## 问题反馈 {#section_5qd_eh5_ctt .section}

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

