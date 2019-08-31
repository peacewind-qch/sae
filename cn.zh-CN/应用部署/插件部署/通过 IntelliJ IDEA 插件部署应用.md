# 通过 IntelliJ IDEA 插件部署应用 {#concept_110665_zh .concept}

SAE 应用除通过控制台方式进行应用部署，还可通过 Alibaba Cloud Toolkit for IntelliJ IDEA 插件部署应用。此方式适用于有应用开发经验的用户。

## 背景信息 {#section_83g_upp_y06 .section}

Alibaba Cloud Toolkit for IntelliJ IDEA（本文简称 Cloud Toolkit）为阿里巴巴提供的免费 IDE 插件。注册或使用已有阿里云账号免费下载 Cloud Toolkit。下载完成后，将其安装在 IntelliJ IDEA 中。

在本地完成应用程序的开发、调试及测试后，通过本插件将应用程序快速部署到阿里云。目前仅支持将应用部署到 ECS、EDAS、SAE 或容器服务 Kubernetes。

## 前提条件 {#section_kj4_fwb_lwf .section}

-   下载并安装 [JDK 1.8 或更高版本](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。
-   下载并安装 [IntelliJ IDEA \(2018.3 或更高版本\)](https://www.jetbrains.com/idea/download/)。

**说明：** 由于 JetBrains 插件官方服务器设立在海外，如果因访问缓慢导致无法下载安装，请加入文末交流群，从 Cloud Toolkit 产品运营部获取离线安装包。


## 安装 Cloud Toolkit {#section_wei_ien_29a .section}

1.  启动 IntelliJ IDEA。
2.  在 IntelliJ IDEA 中安装插件。
    -   Mac 系统：进入 Preference 配置页面，选择左边的 Plugins，在右边的搜索框里输入 Alibaba Cloud Toolkit ，并单击**Install** 安装。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/Install-Intellij-Idea-MAC.jpg)

    -   Windows 系统：进入 **Plugins** 选项，搜索 Alibaba Cloud Toolkit，并单击**Install**安装。

        ![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/edas-cloudtoolkit-installconfig-Windows.png)

3.  插件安装成功后，重启 IntelliJ IDEA，在工具栏显示 Cloud Toolkit 图标（![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/aliyun%20logo.png)）。

## 配置 Cloud Toolkit 账号 {#section_af7_cvg_5e7 .section}

安装 Cloud Toolkit 完成后，需要使用 Access Key ID 和 Access Key Secret 配置 Cloud Toolkit 账号。

1.  启动 IntelliJ IDEA。
2.  单击 Cloud Toolkit 图标![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/aliyun%20logo.png)，在下拉列表中单击 **Preference…**，在设置页面左侧导航栏选择 **Alibaba Cloud Toolkit** \> **Accounts** 。
3.  在 Accounts 界面中设置**Access Key ID** 和 **Access Key Secret**，并单击 **OK**。

    ![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/Config-Idea-Cloud-Toolkit-Account.png)

    -   已有阿里云账号，在 Accounts 界面中单击 **Get existing AK/SK**，进入并登录阿里云登录页面，系统自动跳转至安全信息管理页面，获取 **Access Key ID** 和 **Access Key Secret**。
    -   没有阿里云账号，在 Accounts 界面中单击 **Sign up**，进入阿里云账号注册页面并完成注册。注册完成后并获取 **Access Key ID** 和 **Access Key Secret**。


## 部署应用到 SAE {#section_gr5_2i7_x0j .section}

Cloud Toolkit 插件目前仅支持将应用以 WAR包、JAR包或Image部署到 SAE。

1.  在 IntelliJ IDEA 上单击 Cloud Toolkit 图标![](http://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/aliyun%20logo.png)，并在下拉列表中选择 **Deploy to EDAS Serverless**。
2.  在 Deploy to EDAS Serverless 运行配置页面，配置应用部署参数。配置完成后单击 **Apply** 保存设置。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/Serverless/Serverless_CloudToolkit_DeploytoServerless1.png)

    1.  在配置页面中根据需求选择应用的 Region、Namespace、Application 。

        Region：应用所在地；Namespace：应用所在命名空间；Application：应用名称。

    2.  设置构建方式。
        -   **Maven Build**：选择 Maven Build 方式构建应用，系统默认添加 Maven 任务构建部署包。如果需要部署子模块，具体操作请参见[部署多模块工程](#section_69n_ve3_noh)增加相应的 Maven 任务。
        -   **Upload File**：选择 Upload File 方式构建应用，上传待部署的 WAR 包或者 JAR 包并进行部署。
        -   **Image**：选择 Image 方式构建应用，注入镜像地址并进行部署。
3.  单击 **Run** ，IntelliJ IDEA 的 Console 区域打印部署应用运行日志。您可以根据日志信息检查部署结果。

## 管理 Maven 构建任务 {#section_ee6_wqu_5l8 .section}

在 Deploy to EDAS Serverless 配置页面的 **Before launch** 区域，可以对进行 Maven 构建任务添加、删除、修改和移动等管理操作。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/Serverless/Serverless_CloudToolkit_DeploytoServerless-manageMaven-1.png)

在添加 Maven 构建任务编辑框中，单击右侧的文件夹按钮并选择当前工程所有可用模块，在 Command line 中输入构建命令。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/DeveloperTool/add-maven-in-Intellij-Idea.png)

## 部署多模块工程 {#section_69n_ve3_noh .section}

Maven 工程为多模块开发模式，各个模块独立开发，模块之前存在调用关系，这样的项目工程称为多模块工程。

需要部署多模块 Maven 工程的子模块，在 EDAS Serverless Deployment 配置页面的 **Before launch** 中，将待部署的子模块任务设置为最后执行，如何设置具体操作请参见[管理 Maven 构建任务](#) 。

例如：当前 CarShop 工程存在如下子模块：

carshop

-   itemcenter-api
-   itemcenter
-   detail

其中，itemcenter 和 detail 为子模块，且都依赖于 itemcenter-api 模块。现在需要部署 itemcenter 模块，则在配置页面中 Before launch 中增加如下两个 Maven 任务。

1.  在父工程 carshop 中增加执行 `mvn clean install` 的 Maven 任务。
2.  在子模块 itemcenter 中增加执行 `mvn clean package`的 Maven 任务。

**说明：** 确保子模块的 Maven 任务为 Before launch 最后执行的构建任务。

## 问题反馈 {#section_iay_ywy_u78 .section}

如果您在使用 SAE 过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/Serverless-client-group.png)

