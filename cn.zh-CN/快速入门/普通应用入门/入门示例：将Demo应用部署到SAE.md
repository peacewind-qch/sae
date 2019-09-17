# 入门示例：将Demo应用部署到SAE {#concept_1340338 .concept}

本文介绍如何将 SAE 所提供网页应用 Demo（用 Java 编写，已打成 WAR 包）部署到 SAE，并通过配置公网 SLB 来实现该应用的公网访问。通过该入门示例，可以帮助您初步了解 SAE 应用托管功能。

## 步骤一：开通服务 {#section_wh1_awk_e55 .section}

选择服务开通方式。

-   在产品官网开通
    1.  登录[阿里云主页](http://www.aliyun.com/)，在菜单栏选择**产品** \> **云计算基础** \> **弹性计算** \> **Serverless** \> **Serverless 应用引擎**，进入 SAE 的产品主页。
    2.  在 SAE 的产品主页上，单击**立即开通**进入服务开通页面，请根据提示完成服务开通。
-   在产品控制台开通
    1.  登录 [SAE 控制台](https://sae.console.aliyun.com/)。
    2.  在欢迎页面单击**立即开通**，根据提示完成服务开通。

## 步骤二：创建 VPC {#section_5us_yyf_njr .section}

SAE 需要通过[专有网络（VPC）](https://www.aliyun.com/product/vpc)构建安全隔离的网络环境。

如何创建 VPC具体请参见[搭建专有网络](https://help.aliyun.com/document_detail/65430.html)。

**说明：** 如果您已经创建过 VPC，则可在创建 SAE 应用时，在 **VPC 网络**所在行中的同步按钮 ，将已有的 VPC 同步到 SAE 中。

## 步骤三：将 Demo 应用部署到 SAE {#section_dx6_izr_v9p .section}

为了方便您快速熟悉在 SAE 部署应用，SAE 提供了 Demo 应用供您进行实践操作。该 Dmoe 应用为 SAE 欢迎网页程序，提供 WAR 包和 JAR 包两种方式。本示例教程以 WAR 包方式部署为例。

1.  [下载 Demo 应用](http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/hello-sae.war)。
2.  创建 SAE 应用并部署。

    部署 Demo 应用到 SAE 上。

    1.  登录 [SAE 控制台](https://sae.console.aliyun.com/)，在左侧导航树选择**Serverless 应用引擎** \> **应用列表**。

        **说明：** 若您是开通 SAE 服务后第一次登录控制台，系统会提示您先授权 SAE 访问您的云资源。您只需在安全授权提示对话框中单击**立即授权**，然后在继而出现的云资源访问授权对话框中单击**同意授权**，完成手机验证即可。

    2.  在应用列表页面单击**创建应用**，并在**应用基本信息**页签内设置应用相关信息。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1227549/156871827260491_zh-CN.png)

        -   **应用名称**：输入应用名称。在本示例教程中，请输入my-sae。
        -   **命名空间**：在下拉菜单中选择默认。该示例教程以最简单的场景为例，因此不设环境隔离的要求，您选择默认命名空间即可。
        -   **VPC 网络**：
            1.  先单击右侧的同步按钮 ，将已创建的 VPC 同步到 SAE 中。

                该过程大概需要耗时 3 分钟左右，请您耐心等待。若您在下拉选项中能够看到已创建的 VPC 和 VSwitch，则说明同步成功。

            2.  在下拉菜单中选择要将应用部署到的**VPC** 和要使用的 **VSwitch** 。
        -   **应用实例数**：选择要需要部署的应用实例。在该示例教程中实例数以 1 个为例。
        -   **实例规格**：单击**请选择**勾选所需的实例规格类型。

            实例规格类型以 CPU 和 Memory 进行划分。在该示例教程中，选择最低规格通用型 2。

        -   **应用描述**：输入简短文字描述该应用的基本情况。在此您可以输入“用于入门练习的示例应用”。
    3.  单击**下一步：应用部署配置**，并在应用部署配置页面，选择**应用部署方式**为**War 包部署** ，并按照页面指示进行配置，完成设置后单击**下一步：确认价格**。

        ![war包部署](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067637/156871827252900_zh-CN.png)

        -   **应用运行环境**：本示例Demo 应用为简单的欢迎页Java程序 应用，建议选择 EDAS-Container 3.5.5。

            **说明：** 对于 Spring 或 Dubbo 应用请选择apache-tomcat-xxx ；对于 HSF 应用请选择 EDAS-Container-XXX。

        -   **Java环境**：本示例Demo 应用为简单的欢迎页Java程序应用，建议选择 Open JDK 7 或 Open JDK 8 。

            **说明：** 在正式部署时，请正确选择开发应用时使用的JDK版本。

        -   **文件上传方式**：选择 **上传War包**。
        -   **时区设置**：选择当前应用所在时区，如UTC+8。
        -   **上传 War 包**：单击**选择文件**，上传已下载的 Demo 应用安装包。
        -   **版本**：设置版本号，本示例中 Dome 应用版本为 1.0。
        -   **环境变量设置**、**Hosts 绑定设置**、**应用健康检查**和**日志收集规设置**：本示例不涉及环境变量配置、Hosts 绑定、应用健康检查和日志收集，无需配置。
    4.  在确认价格页签查看您所创建应用的详细信息以及配置费用情况，并单击**确认创建**。
    5.  在创建完成页签，单击提示信息中的**应用详情页**链接，进入my-sae的应用详情页面。

        **说明：** my-sae 为[应用基本信息设置](#)中设置的应用名称。

    6.  单击**实例部署信息**页签，如果看到**运行状态**列显示为绿色 Running，表示应用部署成功。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067637/156871827252906_zh-CN.png)

        **说明：** 应用部署大概需要1～2两分钟，请您耐心等待。


## 步骤四：添加公网 SLB {#section_3ga_mbq_kc2 .section}

应用部署成功后需要为其添加公网 SLB 才能被通过公网被访问。SAE 会自动帮您代购 SLB 服务，按量计费，您只需配置应用的监听端口。

1.  在my-sae的应用详情页面，单击**基本信息**页签。
2.  在**应用访问设置**区域框，单击**公网访问地址**一栏的添加公网SLB访问。
3.  在弹出的**添加公网 SLB 访问**对话框中选择已有的 SLB，并配置默认监听端口。设置**SLB 端口** 为80，设置**容器端口**为8080。

    ![绑定SLB](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067673/156871827256535_zh-CN.png)

    **说明：** 

    -   SAE 支持新建 SLB，本文示例中以复用原有 SLB 为例。
    -   SAE 支持 TCP 协议监听和 HTTPS 监听，本文示例中以 TCP 协议监听为例。
4.  单击**确定**。

添加公网 SLB 需要极短的几秒钟。添加完成后，您可以在**应用详情页**的公网访问地址一栏看到该公网 SLB 的 IP 和端口 。

## 步骤五：通过公网访问 Demo 应用 {#section_5rq_h64_c4z .section}

根据**公网访问地址**栏显示的公网 SLB 的 IP 和端口，在浏览器中按http://slbip:port/的格式输入地址并回车，可以看到 Demo 应用的首页。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067637/156871827252949_zh-CN.png)

