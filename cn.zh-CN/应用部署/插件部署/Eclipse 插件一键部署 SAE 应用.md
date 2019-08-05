# Eclipse 插件一键部署 SAE 应用 {#concept_1375315 .concept}

Alibaba Cloud Toolkit for Eclipse（下文简称 Cloud Toolkit）是一个免费的 IDE 插件，帮助阿里云用户更高效的使用阿里云。您只需注册或使用一个已有的阿里云账号，即可免费下载 Cloud Toolkit。下载完成后，您可以将该插件安装到 Eclipse 中。

当您在本地完成应用程序的开发、调试及测试后，通过该插件即可轻松将应用程序部署到阿里云。目前支持将应用部署到 ECS、EDAS、SAE 或容器服务 Kubernetes。

本文档将向您介绍如何在 Eclipse 中安装 Cloud Toolkit，并使用 Cloud Toolkit 快速部署一个应用到 SAE。

## 前提条件 {#section_tdu_qpz_0ii .section}

-   下载并安装 [JDK 1.8 或更高版本](http://java.com/zh_CN/download/)
-   下载并安装适用于 Java EE 开发人员的 [Eclipse IDE、4.5.0（代号：Mars）或更高版本](http://www.eclipse.org/downloads/)

## 安装 Cloud Toolkit {#section_z0u_c2d_e1s .section}

1.  启动 Eclipse。
2.  在菜单栏中选择**Help** \> **Install New Software**
3.  在 Available Software 对话框的 **Work with** 文本框中输入 Cloud Toolkit for Eclipse 的 URL
4.  在下图所示的列表区域中勾选需要的组件 Alibaba Cloud Toolkit Core 和 Alibaba Cloud Toolkit Deployment Tools，并在下方 Details 区域中不勾选 Connect all update sites during install to find required software。完成组件选择之后，单击**Next**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156500226853391_zh-CN.png)

5.  按照 Eclipse 安装页面的提示，完成后续安装步骤。

    **说明：** 安装过程中可能会出现没有数字签名对话框，选择Install anyway即可。

6.  Cloud Toolkit 插件安装完成后，重启 Eclipse，您可以在工具栏看到 Alibaba Cloud Toolkit 的图标。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156500226853395_zh-CN.png)


## 配置 Cloud Toolkit 账号 {#section_l7z_kaq_d1n .section}

您需使用 Access Key ID 和 Access Key Secret 来配置 Cloud Toolkit 的账号。

1.  启动 Eclipse。
2.  在工具栏单击 Alibaba Cloud Toolkit 图标右侧的下拉按钮，在下拉菜单中单击 **Alibaba Cloud Preference…**。
3.  在 Preference \(Filtered\) 对话框的左侧导航栏中单击 **Accounts**。
4.  在 Accounts 界面中设置 Access Key ID 和 Access Key Secret，然后单击 **OK**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156500226853416_zh-CN.png)

    -   如果您已经注册过阿里云账号，在 Accounts 界面中单击 **Manage existing Acount**，进入阿里云登录页面。用已有账号登录后，跳转至安全信息管理页面，获取 Access Key ID 和 Access Key Secret。
    -   如果您还没有阿里云账号，在 Accounts 界面中单击单击 **Sign up**，进入阿里云账号注册页面，注册账号。注册完成后按照上述方式获取 Access Key ID 和 Access Key Secret。

## 将应用部署到 SAE {#section_84s_27c_ccc .section}

目前支持使用 Cloud Toolkit 插件将应用通过 WAR 包、JAR 包和 Image 部署到 SAE。

1.  在 Eclipse 界面左侧的 Package Explorer 中右键单击您的应用工程名，在弹出的下拉菜单中选择**Alibaba Cloud** \> **Deploy to EDAS Serverless…**
2.  在 Deploy to EDAS Serverless 对话框根据您的实际需求选择应用的 Region、Namespace、Application，设置部署方式，然后单击 **Deploy**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156500226953440_zh-CN.png)

    应用信息说明：

    -   **Region**：应用所在地域。
    -   **Namespace**：应用所在命名空间。
    -   **Application**：应用名称。
    **说明：** 如果您还没有在 SAE 上创建应用，在对话框右上角单击 **Create Serverless Application on EDAS Console…**，跳转到 SAE 控制台创建应用。创建应用的步骤请参考[在 SAE 部署一个 Java Web 应用](https://help.aliyun.com/document_detail/94541.html)

3.  部署开始后，Eclipse 的 Console 区域会打印部署日志。您可以根据日志信息检查部署结果。

## 终止 Cloud Toolkit 插件运行 {#section_exb_s0x_xsx .section}

在插件运行过程中，如果想停止插件运行，可以在 Progress 页面终止 EDAS-deploy 进程。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067665/156500226953449_zh-CN.png)

## 问题反馈 {#section_w8o_tsp_kji .section}

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

