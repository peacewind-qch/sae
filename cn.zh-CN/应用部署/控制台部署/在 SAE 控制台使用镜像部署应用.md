# 在 SAE 控制台使用镜像部署应用 {#concept_97675_zh .concept}

应用开发完成后，可以将您的应用部署到 SAE 进行托管。本文介绍如何在 SAE 控制台使用镜像部署应用。

## 背景信息 {#section_n05_8a3_ymc .section}

SAE 支持通过镜像部署 SAE 应用，进行应用管理。

SAE 应用的部署方式如下表所示。

|应用举例|部署方式|参考开发文档|
|----|----|------|
|原生 Spring Cloud|WAR、JAR、镜像|[将 Spring Cloud 应用托管到 SAE](https://help.aliyun.com/document_detail/123013.html)|
|原生 Dubbo|WAR、JAR、镜像|[将 Dubbo 应用托管到 SAE](https://help.aliyun.com/document_detail/123021.html)|
|HSF|WAR、JAR、镜像|/|
|多语言应用|镜像|/|

## 前提条件 {#section_5th_epm_m58 .section}

1.  [创建 VPC](../cn.zh-CN/快速入门/准备工作.md#section_xrz_zr9_py3)
2.  [创建命名空间](../cn.zh-CN/快速入门/准备工作.md#section_cu5_k9p_xuf)
3.  [制作应用镜像](https://help.aliyun.com/document_detail/98492.html)

## 创建 SAE 应用 {#section_wwi_jgi_33h .section}

1.  登录 [SAE 控制台](https://sae.console.aliyun.com)。
2.  在左侧导航树选择**Serverless 应用引擎** \> **应用列表**，并在应用列表页面单击右上角**创建应用**。
3.  在**应用基本信息**页签内，设置应用相关信息，配置完成后单击**下一步：应用部署配置**。

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/120281/cn_zh/1561951749953/%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A81.png)

    -   **应用名称**：输入应用名称。允许数字，字母，下划线以及中划线组合，仅允许字母开头，最大长度 36 个字符。
    -   **命名空间**：在下拉菜单中选择创建好的命名空间。
    -   **VPC 网络**：在下拉菜单中选择VPC 和 vswitch 。
    -   **应用实例数**：选择要创建的实例个数。
    -   **实例规格**：单击**请选择**，在选择实例规格页面内选择实例的 **CPU** 和 **Memory** 规格。
    -   **应用描述**：填写应用的基本情况，输入的描述信息不超过100个字符。
4.  在应用部署配置页面，选择 **镜像**，依据页面指示进行配置。完成设置后单击**确认创建**。

    ![镜像部署](../DNSAE19102359/../DNICMS19102088/images/56820_zh-CN.png)

    -   **配置镜像**：在镜像列表的下拉框内选择您所创建的镜像，镜像选中后会在配置镜像后面显示您所选择的镜像。
    -   **启动命令设置**（可选）：请参见[如何设置启动命令](../cn.zh-CN/应用部署/高级设置/如何设置启动命令.md#)配置。
    -   **环境变量设置**（可选）：请参见[如何设置环境变量](https://help.aliyun.com/document_detail/96560.html)配置。
    -   **Hosts 绑定设置**（可选）：请参见[如何设置 Hosts 绑定](https://help.aliyun.com/document_detail/100335.html)配置。
    -   **应用健康检查**（可选）：请参见[如何设置应用健康检查](https://help.aliyun.com/document_detail/96713.html)配置。
    -   **日志收集设置**（可选）：请参见[如何设置日志收集](https://help.aliyun.com/document_detail/133987.html)配置。
5.  进入应用详情页面，查看应用的基本信息和实例部署信息。

## 更新应用 {#section_7o6_8fh_b08 .section}

**部署应用**主要用于更新应用，对运行环境变量、镜像配置、启动命令和日志收集等配置项进行修改。

1.  在应用列表中，单击采用镜像部署的 SAE 应用名称，进入应用详情页面。
2.  在页面右上角单击**部署应用**。
3.  在部署应用页面，重新选择镜像，修改**最小存活实例数**，并依据现场需要修改配置启动命令、环境变量和健康检查等高级设置选项，配置完成后单击**确认**。
4.  应用升级过程时，您可以在应用详情页面上方单击**查看详情**，在变更详情页面查看部署流程和执行日志。部署完成后，如果**执行状态**为 Running，表示应用更新成功。

## 结果验证 {#section_bv5_gfw_yd2 .section}

应用发布后，通过如下两种方式验证应用的发布结果。

-   查看应用实例运行状态。

    在应用详情页中**实例部署信息**页签查看实例的运行状态。如果**执行状态**显示为绿色的 **Running**或者 **Completed**，表示应用发布成功。

-   配置公网负载均衡并访问应用。

    应用发布过程中或发布后，根据实际需要，通过配置负载均衡 SLB 在指定范围内开放应用，以便其它应用访问。

    负载均衡包括如下两类：

    -   **私网负载均衡**：在应用所在的 VPC 内提供应用的访问入口，保证应用能被同 VPC 内的其它应用访问。
    -   **公网负载均衡**：为该应用自动购买公网 SLB 服务，保证该应用能被公网中的其它应用访问。
    配置公网 SLB 访问和配置私网 SLB 访问的步骤相同，具体操作请参见[绑定 SLB](../cn.zh-CN/应用管理/绑定 SLB.md#)。SLB 绑定完成后，在浏览器输入由 SLB IP 、端口及应用部署包名组成的访问地址并访问，如 39.106.245.40/80/image，即可进入应用。


## 更多信息 { .section}

-   使用 SAE 创建应用后，可以进行更新、扩缩容、启停应用监控和删除应用等管理操作，具体操作方式请参见[应用生命周期管理](https://help.aliyun.com/document_detail/113076.html)。
-   在SAE中创建应用后，可以进行弹性自动伸缩，具体操作方式请参见[配置弹性伸缩](https://help.aliyun.com/document_detail/134120.html)。
-   在SAE中创建应用后，可以通过添加公网 SLB 实现公网访问，添加内网 SLB 实现同 VPC 内所有节点够能通过私网负载均衡访问您的应用，具体操作方式请参见[绑定SLB](https://help.aliyun.com/document_detail/113305.html)。

## 问题反馈 { .section}

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![问题反馈](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

