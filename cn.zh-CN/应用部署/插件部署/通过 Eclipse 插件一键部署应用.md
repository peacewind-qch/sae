# 通过 Eclipse 插件一键部署应用 {#concept_1375315 .concept}

SAE 应用除通过控制台方式进行应用部署，还可以通过 Alibaba Cloud Toolkit for Eclipse 插件部署应用。此方式适用于有应用开发经验的用户。

## 背景信息 {#section_qe2_6gg_32z .section}

Alibaba Cloud Toolkit for Eclipse（本文简称 Cloud Toolkit）为阿里巴巴提供的免费 IDE 插件。注册或使用已有阿里云账号免费下载 Cloud Toolkit。下载完成后，将其安装在 IntelliJ IDEA 中。

在本地完成应用程序的开发、调试及测试后，通过本插件将应用程序快速部署到阿里云。目前仅支持将应用部署到 ECS、EDAS、SAE 或容器服务 Kubernetes。

## 前提条件 {#section_tdu_qpz_0ii .section}

-   下载并安装 [JDK 1.8 或更高版本](http://java.com/zh_CN/download/)
-   下载并安装适用于 Java EE 开发的 [Eclipse IDE、4.5.0（代号：Mars）或更高版本](http://www.eclipse.org/downloads/)

## 安装 Cloud Toolkit {#section_z0u_c2d_e1s .section}

1.  启动 Eclipse。
2.  在菜单栏中选择**Help** \> **Install New Software**。
3.  在 Available Software 对话框的 **Work with** 文本框中，输入 Cloud Toolkit for Eclipse 的 URL。
4.  在下图所示的列表区域中勾选需要的组件 **Alibaba Cloud Toolkit Core** 和 **Alibaba Cloud Toolkit Deployment Tools**，并在下方 Details 区域中去勾选 **Connect all update sites during install to find required software** ，取消勾选后单击**Next**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156721856553391_zh-CN.png)

5.  按照 Eclipse 安装页面的提示，完成后续安装步骤。

    **说明：** 安装过程中提示没有数字签名对话框，请选择 **Install anyway**。

6.  Cloud Toolkit 插件安装完成后，重启 Eclipse。重启后在工具栏显示 Alibaba Cloud Toolkit 图标。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156721856553395_zh-CN.png)


## 配置 Cloud Toolkit 账号 {#section_l7z_kaq_d1n .section}

安装 Cloud Toolkit 完成后，需要使用 Access Key ID 和 Access Key Secret 配置 Cloud Toolkit 账号。

1.  启动 Eclipse。
2.  在工具栏 Cloud Toolkit 图标右侧下拉菜单中选择 **Alibaba Cloud Preference…** \> **Alibaba Cloud Tooll** \> **Accounts**。
3.  在 Accounts 界面中设置 **Access Key ID** 和 **Access Key Secret**并单击 **OK**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156721856553416_zh-CN.png)

    -   已有阿里云账号，在 Accounts 界面中单击 **Get existing AK/SK**，进入并登录阿里云登录页面，系统自动跳转至安全信息管理页面，获取 **Access Key ID** 和 **Access Key Secret**。
    -   没有阿里云账号，在 Accounts 界面中单击 **Sign up**，进入阿里云账号注册页面并完成注册。注册完成后并获取 **Access Key ID** 和 **Access Key Secret**。


## 将应用部署到 SAE {#section_84s_27c_ccc .section}

Cloud Toolkit 插件目前仅支持将应用以 WAR包、JAR包或Image部署到 SAE。

1.  在 Eclipse 界面左侧的 Package Explorer 中选择创建的应用工程名，并在弹出的下拉菜单中选择**Alibaba Cloud** \> **Deploy to EDAS Serverless…**。
2.  在 Deploy to EDAS Serverless 对话框中，依据需求选择应用的 **Region**、**Namespace**、**Application**，并设置部署方式，配置完成后单击 **Deploy**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156721856553440_zh-CN.png)

    应用信息说明：

    -   **Region**：应用所在地域。
    -   **Namespace**：应用所在命名空间。
    -   **Application**：应用名称。
3.  部署过程中，Eclipse 的 Console 区域回显应用的部署日志，依据日志信息检查部署结果。

## 终止 Cloud Toolkit 插件运行 {#section_exb_s0x_xsx .section}

在插件运行过程中，现场需要插件运行，请在 Progress 页面终止 EDAS-deploy 进程。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156721856653449_zh-CN.png)

## 问题反馈 {#section_w8o_tsp_kji .section}

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

