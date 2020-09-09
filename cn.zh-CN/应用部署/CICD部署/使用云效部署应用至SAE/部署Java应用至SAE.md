# 部署Java应用至SAE

本文以Java应用为例，介绍如何使用云效以镜像方式将应用部署至SAE。云效现已支持分批发布的发布策略。

-   [注册阿里云账号](https://help.aliyun.com/document_detail/37195.html)。
-   [将业务代码上传至阿里云Code](https://help.aliyun.com/document_detail/57904.html)。

    **说明：** 业务代码中须包含应用的Dockerfile文件，具体制作步骤请参见[制作应用容器Docker镜像](/cn.zh-CN/应用部署/制作应用容器Docker镜像.md)。

-   [将镜像文件上传至阿里镜像库](https://help.aliyun.com/document_detail/60997.html)。
-   [开通云效](https://rdc.aliyun.com)。

## 部署流程

![云效部署SAE（镜像方式）](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9818827951/p73926.png)

1.  如果您的应用已经部署在SAE上，则无需创建新的应用。如果第一次部署应用到SAE，则需要在SAE控制台创建应用，以便云效将业务代码推送到该应用中。
2.  在SAE创建应用完成后，需要在云效控制台创建对应的应用，应用的部署方式（例如JAR、WAR和镜像）两边需要一致。
3.  在云效控制台完成应用创建后，需要使用云效提供的流水线模板创建出应用集成发布的基础流水线。
4.  基础流水线创建完成后，需要更改流水线中的构建任务。例如：如果您在SAE控制台使用镜像部署应用，那么在该环节您需要将原流水线**构建**任务删掉，添加为供镜像方式部署使用的**Java镜像构建**。整个流水线运行后，本环节的构建产物将供部署环节发布使用。
5.  构建任务配置完成后，需要指定上环节（即构建任务环节）构建产物和应用的部署目的地，即应用在SAE上的区域和应用名称。整个流水线运行成功后，应用成功部署到SAE上。

## 步骤一：在SAE上创建应用

如果您是第一次使用SAE托管应用，需要预先在SAE上使用Demo应用创建相应的应用。

本文以镜像部署为例，具体操作请参见[在SAE控制台使用镜像部署应用](/cn.zh-CN/应用部署/控制台部署/在SAE控制台使用镜像部署应用.md)。

**说明：** 在SAE控制台创建应用时使用的部署方式（JAR、WAR和镜像），必须与在云效的流水线设置保持一致。简而言之，在SAE上使用镜像方式部署，那么在云效设置流水线时，构建环节必须是镜像相关配置。

![在SAE上创建应用](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9818827951/p73708.png)

## 步骤二：在云效配置应用基本信息

1.  登录[云效控制台应用列表页面](https://rdc.aliyun.com/appcenter/overview)。

2.  在菜单栏中选择**项目** \> **项目列表**，并在**项目列表**页面单击右上角的**新建项目**，然后在弹出的页面中设置项目信息，并单击**确定**。

    项目信息有**项目类型**、**项目名称**、**公开性**和**项目背景**等，请依据实际情况设置。

    ![在云效创建项目](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1157559951/p73719.png)

3.  在菜单栏中选择**研发** \> **应用**，并在**我的应用**页面中，单击左上角的**创建新应用**，然后在**创建新应用**对话框设置应用基本信息并单击**创建**。

    ![在云效创建应用](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1157559951/p73722.png)


## 步骤三：在云效使用模板构建基础流水线

1.  在菜单栏中选择**研发** \> **流水线**，在**流水线**页面单击右上角的**新建流水线**。

2.  在**新建流水线**页面设置**编程语言**和**流程模板**，并单击**下一步**。

    ![云效中设置流水线设置-变成语言和模板设置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9818827951/p73731.png)

    -   **编程语言**：选择**Java**。
    -   **模板**：选择**Java测试、构建**。
    **说明：** 如果您的应用编程语言非Java，请根据实际情况选择。

3.  在弹出的流水线配置页面中，进行代码库设置，并单击**下一步**。

    ![在云效设置代码库](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9818827951/p73738.png)

    -   代码库类型：选择**阿里云Code**。
    -   **代码仓库**：选择您的代码仓库地址。
    -   **分支**：选择代码分支。
    -   **别名**：代码的别名，后续用于执行组件代码克隆路径，使用数字、字母或下划线。
4.  在弹出的流水线配置页面中，设置流水线的基本信息如流水线名称、管理员等，并单击**创建**。

    ![云效构建基本流水线](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9818827951/p73753.png)


## 步骤四：在云效中配置构建任务

1.  在**编辑流水线**页面单击**构建**，在**阶段：构建**页面单击![删除按钮](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1157559951/p74753.png)。

    ![阶段：构建示意图](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1157559951/p74752.png)

2.  在**编辑流水线**页面单击![添加](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2157559951/p74261.png)，并在弹出的**阶段模板**中选择**Java镜像构建**。

    ![选择Java镜像构建示意图](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1157559951/p74756.png)

    ![添加Java镜像构建结果图](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1157559951/p74757.png)

3.  配置构建任务的基本信息。

    1.  在弹出的**阶段：新增阶段**面板中设置**阶段名称**和**流转配置**。

        ![修改构建01](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0918827951/p73760.png)

4.  配置构建任务的执行步骤。

    1.  单击**任务列表**中具体任务名称。

    2.  在**任务：Java构建Docker镜像并推送镜像仓**页面的**Docker镜像构建上传**区域，设置镜像信息。

        ![设置镜像信息](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0918827951/p73763.png)

        -   **步骤名称**：保持默认，也可以自定义。
        -   **区域**：Docker镜像文件所在的地域。
        -   **仓库**：Docker镜像文件所在地址。
        -   **标签**：Docker镜像Tag，支持固定参数例如1.0，或者动态参数$\{DATETIME\}。
        -   **Dockerfile路径**：Dockerfile相对于代码库根目录所在路径，如META/config/Dockerfile或Dockerfile。该文件云效会自动为您创建，无需自建。
        -   **ContextPath**：填写相对于代码根目录的路径，如target，如果不填则为Dockerfile文件所在目录。
        -   **组件出参**：为本构建环节产生的结果文件，供部署环节使用。

## 步骤五：在云效部署应用至SAE

步骤一所创建应用不包含您的任何业务代码，在本环节将应用代码推送至SAE上，即将SAE上的应用升级为含有您业务代码的应用。

**说明：** 云效现已支持分批发布的发布策略，详情参见[步骤4](#step_config_deploy_job)。

1.  在**编辑流水线**页面的**阶段**区域中，单击![添加](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2157559951/p74261.png)。

2.  在**阶段模板**面板中选择**部署到 SAE**。

    ![在云效部署环节选择部署SAE模板](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7028827951/p73766.png)

3.  单击新增的流水线阶段，在右侧面板上设置阶段的基本信息，并单击**任务列表**下的**部署到 SAE**。

    ![在云效设置流水线中部署任务](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0918827951/p73767.png)

4.  在**任务：部署到SAE**面板中配置部署任务。

    ![在云效设置部署信息](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0918827951/p73768.png)

    -   **任务名称**：自定义的任务名称。不可超过20个字符。
    -   **区域**：选择步骤一所创建的应用所在地域。
    -   **SAE应用**：选择步骤一所创建的应用。
    -   **构建产物**：为步骤四中**组件出参**产生的结果。
    -   **发布策略**：可选择**分批发布**或**灰度发布**。
    -   **分批方式**：可选择**手动确认**或**自动确认**。例如，如需在完成第一批发布时先观察发布结果再决定后续操作，则可选择**手动确认**。
    -   **灰度台数**：要执行灰度发布的机器数量。

        **说明：** 此字段仅在**发布策略**为**灰度发布**时显示。

    -   **发布批次**：发布分批的数量。
    -   **分批等待时间**：相邻发布批次之间的等待时间。
5.  配置完毕后，单击页面右上角的**保存**和**运行**。

    ![云效部署结果](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0918827951/p73769.png)

    云效开始按照配置的流水线工作，最终将应用部署至SAE。


## 结果验证

-   方法一：

    云效显示部署成功后，在SAE控制台查看应用的变更记录，是否产生应用重新部署的变更记录。

    ![云效部署后在SAE产生变更记录](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1918827951/p73771.png)

-   方法二：

    云效显示部署成功后，在SAE控制台查看应用的基本信息，查看镜像地址是否与在云效中设置相同。

    ![在云效部署后SAE应用信息](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/1918827951/p73772.png)


## 常见问题

-   如何使用云效以JAR或者WAR包方式部署应用到SAE？
    1.  在SAE控制台以JAR或者WAR包方式创建应用。
    2.  在[步骤四：在云效中配置构建任务](#section_b0x_asc_bqh)的步骤2中构建**阶段模板**选择**Java JAR/WAR包构建**，并在弹出的任务步骤设置页面中，依据提示设置JAR或者WAR包构建物信息。
    3.  [设置部署阶段任务并将应用至SAE](#section_l5l_3bo_rb7)。
-   其他编程语言如何使用云效将应用部署到SAE？

    在流水线构建任务环节，您选择所需的编程语言模板，具体部署操作请参见[部署Node.js应用至SAE](/cn.zh-CN/最佳实践/使用云效部署应用至SAE/部署Node.js应用至SAE.md)和[部署Golang应用至SAE](/cn.zh-CN/最佳实践/使用云效部署应用至SAE/部署Golang应用至SAE.md)。

    ![云效支持的编程语言](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5694688951/p73774.png)

-   除Java应用外其他编程语言的应用想要部署在SAE上，在SAE创建应用时使用那种部署方式（JAR、WAR和镜像）？

    使用**镜像方式**。使用云效部署时，切记您应用程序代码中须包含应用的Dockerfile文件。


## 更多信息

-   在SAE部署完成后，您可以对应用进行更新、扩缩容、启停、删除应用等生命周期管理操作，具体操作方式请参见[管理应用生命周期](/cn.zh-CN/应用管理/管理应用生命周期.md)。
-   在SAE部署完成后，您可以对应用进行自动弹性伸缩、SLB绑定和批量启停等提升应用性能的操作，具体操作方式请参见以下文档：
    -   [绑定SLB](/cn.zh-CN/应用管理/绑定SLB/为应用绑定SLB.md)
    -   [配置弹性伸缩策略](/cn.zh-CN/应用管理/配置弹性伸缩策略.md)
    -   [一键启停应用](/cn.zh-CN/应用管理/一键启停应用.md)
    -   [配置管理](/cn.zh-CN/应用管理/配置管理/配置管理概述.md)
    -   [变更实例规格](/cn.zh-CN/应用管理/变更实例规格.md)
-   在SAE部署完成后，您还可以对应用进行日志管理、监控管理、应用事件查看和变更记录查看等聚焦应用运行状态的操作，具体操作方式请参见以下文档：
    -   [日志管理](/cn.zh-CN/日志管理/查看实时日志.md)
    -   [监控管理](/cn.zh-CN/监控管理/基础监控.md)
    -   [应用事件查看](/cn.zh-CN/应用管理/查看应用事件.md)
    -   [变更记录查看](/cn.zh-CN/应用管理/查看变更记录.md)
    -   [使用Webshell诊断应用](/cn.zh-CN/应用管理/使用 Webshell 诊断应用.md)

## 问题反馈

如果您在使用SAE过程中有任何疑问，欢迎您扫描下面的二维码加入钉钉群进行反馈。

![SAE钉钉群2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5885359951/p72048.png)

