# IntelliJ IDEA 插件快速部署 SAE 应用 {#concept_110665_zh .concept}

Alibaba Cloud Toolkit for IntelliJ IDEA（下文简称 Cloud Toolkit）是一个免费的 IDE 插件，帮助阿里云用户更高效的使用阿里云。

您只需注册或使用一个已有的阿里云账号，即可免费下载 Cloud Toolkit。下载完成后，您可以将该插件安装到 IntelliJ IDEA 中。

当您在本地完成应用程序的开发、调试及测试后，通过该插件即可轻松将应用程序部署到阿里云。目前支持将应用部署到 ECS、EDAS、SAE 或容器服务 Kubernetes。

本文档将向您介绍如何在 IntelliJ IDEA 中安装 Cloud Toolkit，并使用 Cloud Toolkit 快速部署 SAE 应用。

## 前提条件 {#section_kj4_fwb_lwf .section}

-   下载并安装 [JDK 1.8 或更高版本](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。
-   下载并安装 [IntelliJ IDEA \(2018.3 或更高版本\)](https://www.jetbrains.com/idea/download/)。

**说明：** 因 JetBrains 插件市场官方服务器在海外，如遇访问缓慢无法下载安装的，请加入文末交流群，向 Cloud Toolkit 产品运营获取离线包安装。


## 安装 Cloud Toolkit {#section_wei_ien_29a .section}

1.  启动 IntelliJ IDEA。
2.  在 IntelliJ IDEA 中安装插件。
    -   Mac 系统：进入 Preference 配置页面，选择左边的 Plugins，在右边的搜索框里输入 Alibaba Cloud Toolkit ，并单击**Install** 安装。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/Install-Intellij-Idea-MAC.jpg)

    -   Windows 系统：进入 **Plugins** 选项，搜索 Alibaba Cloud Toolkit，并单击**Install**安装。

        ![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/edas-cloudtoolkit-installconfig-Windows.png)

3.  在 IntelliJ IDEA 中插件安装成功后，重启IntelliJ IDEA，您可以在工具栏看到 Alibaba Cloud Toolkit 的图标（![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/aliyun%20logo.png)）。

## 配置 Cloud Toolkit 账号 {#section_af7_cvg_5e7 .section}

在安装完 Alibaba Cloud Toolkit 后，您需使用 Access Key ID 和 Access Key Secret 来配置 Cloud Toolkit 的账号。

1.  启动 IntelliJ IDEA。
2.  单击 Alibaba Cloud Toolkit 的图标![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/aliyun%20logo.png)），在下拉列表中单击 **Preference…**，进入设置页面，在左侧导航栏单击 **Alibaba Cloud Toolkit** \> **Accounts** 。
3.  在 Accounts 界面中设置**Access Key ID** 和 **Access Key Secret**，然后单击 **OK**。

    ![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/Config-Idea-Cloud-Toolkit-Account.png)

    -   如果您已经注册过阿里云账号，在 Accounts 界面中单击 **Get existing AK/SK**，进入阿里云登录页面。用已有账号登录后，跳转至安全信息管理页面，获取 **Access Key ID** 和 **Access Key Secret**。

    -   如果您还没有阿里云账号，在 Accounts 界面中单击单击 **Sign up**，进入阿里云账号注册页面，注册账号。注册完成后按照上述方式获取 **Access Key ID** 和 **Access Key Secret**。


## 部署应用到 SAE {#section_gr5_2i7_x0j .section}

目前支持使用 Cloud Toolkit 插件将应用通过 WAR包、JAR包或Image部署到 SAE。

1.  在 IntelliJ IDEA 上单击 Alibaba Cloud Toolkit 的图标（![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/aliyun%20logo.png)），在下拉列表中单击 **Deploy to EDAS Serverless**。
2.  在 Deploy to EDAS Serverless 的运行配置页面，配置应用部署参数。然后单击 **Apply** 保存设置。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/Serverless/Serverless_CloudToolkit_DeploytoServerless1.png)

    1.  在配置页面中根据您的实际需求选择应用的 Region、Namespace、Application 。
        -   Region：应用所在地域。
        -   Namespace：应用所在命名空间。
        -   Application：应用名称。
    2.  设置构建方式。
        -   **Maven Build**：选择 Maven Build 方式来构建应用时，系统会默认添加一个 Maven 任务来构建部署包。如果您需要部署一个子模块，请参考 部署多模块工程 章节来增加相应的Maven任务。
        -   **Upload File**：选择 Upload File 方式来构建应用时，选择上传您的 WAR 包或者 JAR 包，然后进行部署。
        -   **Image**: 选择 Image 方式来构建应用时，需要填入一个镜像地址，然后进行部署。
    **说明：** 如果您还没有在 SAE 上创建 SAE 应用，在对话框右上角单击 **Create Serverless Application on EDAS Console…**，跳转到 SAE 控制台创建 SAE 应用。创建应用的步骤请参考[在 SAE 部署一个 Java Web 应用](https://help.aliyun.com/document_detail/94541.html)。

3.  单击 **Run** 执行上面步骤的运行配置，IntelliJ IDEA 的 Console 区域会打印部署日志。您可以根据日志信息检查部署结果。

## 管理 Maven 构建任务 {#section_ee6_wqu_5l8 .section}

在 IntelliJ IDEA 中安装的 Cloud Toolkit 内可以部署 Maven 的构建任务。您也可以在 Deploy to EDAS Serverless 的配置页面的 **Before launch** 区域来添加、删除、修改和移动 Maven 构建任务。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/Serverless/Serverless_CloudToolkit_DeploytoServerless-manageMaven-1.png)

在添加 Maven 构建任务编辑框中，您可以单击右侧的文件夹按钮选择当前工程的所有可用模块，并在 Command line 中编辑构建命令。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/add-maven-in-Intellij-Idea.png)

## 部署多模块工程 {#section_69n_ve3_noh .section}

实际工作中碰到的大部分 Maven 工程都是多模块的，各个项目模块可以独立开发，其中某些模块又可能会使用到其他的一些模块的功能，这样的项目工程就是多模块工程。

如果您的工程项目为 Maven 多模块工程并且想部署工程中的某子模块，那么需要保证 EDAS Serverless Deployment 配置页面中的 **Before launch** 中的 Maven 构建任务中最后一个任务为该子模块的构建任务。（如不了解如何管理 Maven 构建任务，请参考上面的[管理 Maven 构建任务](#) 小节）

例如：当前 CarShop 工程存在如下子模块：

carshop

-   itemcenter-api
-   itemcenter
-   detail

其中，itemcenter 和 detail 为子模块，且都依赖于 itemcenter-api 模块，现在想部署 itemcenter 模块，应该怎么做？只需要在配置页面中的 Before launch 中增加如下两个 Maven 任务即可：

1.  增加一个在父工程 carshop 中执行 `mvn clean install` 的 Maven 任务；
2.  增加一个在子模块 itemcenter 中执行 `mvn clean package` Maven 任务。

**说明：** 需要保证子模块的 Maven 任务为 Before launch 中最后的构建任务。

## 问题反馈 { .section}

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

