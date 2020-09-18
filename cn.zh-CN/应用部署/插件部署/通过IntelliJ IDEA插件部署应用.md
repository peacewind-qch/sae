---
keyword: [ACT部署应用, Alibaba Cloud Toolkit for IntelliJ IDEA]
---

# 通过IntelliJ IDEA插件部署应用

除了通过SAE控制台进行应用部署，您还可以通过Alibaba Cloud Toolkit for IntelliJ IDEA（简称Cloud Toolkit）插件部署应用。

1.  下载并安装[JDK1.8或更高版本](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。
2.  下载并安装[IntelliJ IDEA（2018.3或更高版本）](https://www.jetbrains.com/idea/download/)。

    **说明：** 由于JetBrains插件官方服务器设立在海外，如果因访问缓慢导致无法下载安装，请加入文末交流群，从Cloud Toolkit产品运营部获取离线安装包。

3.  [在IntelliJ IDEA中安装和配置Cloud Toolkit]()。

Cloud Toolkit是阿里巴巴提供的免费IDE插件。您可以注册或使用已有的账号免费下载Cloud Toolkit，下载完成后，将其安装在IntelliJ IDEA中。

在本地完成应用程序的开发、调试及测试后，您可以通过本插件将应用程序快速部署到SAE。

## 部署应用到SAE

Cloud Toolkit插件目前仅支持将应用以WAR包、JAR包或镜像方式部署到SAE。

1.  在IntelliJ IDEA界面左侧的**Project**区域中右键单击待部署的工程名，在快捷菜单中选择**Alibaba Cloud** \> **Deploy to SAE...**。

2.  在**Deploy to SAE**对话框，配置应用部署参数，配置完成后单击**Apply**保存设置。

    ![配置部署信息](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2802900061/p96724.png)

    参数说明如下：

    |参数|说明|
    |--|--|
    |Region|选择应用所在地域。|
    |Namespace|选择应用所在命名空间。|
    |Application|选择应用名称。|
    |Build|    -   **Maven Build**：Maven Build方式构建应用，默认添加Maven任务构建部署包。如果需要部署子模块，请参见[使用IntelliJ IDEA部署多模块工程中的子模块]()。
    -   **Upload File**：JAR包或者WAR包构建应用，上传WAR包或者JAR包后部署应用。
    -   **Image**：镜像方式构建应用，需要设置镜像地址后部署应用。
    -   **Gradle Build**：暂不支持。 |

3.  在**Deploy to SAE**对话框，单击**Advanced**，在**Advanced**区域配置应用高级参数。

    **说明：** 如果您未配置高级参数，部署时将默认使用[SAE控制台](https://sae.console.aliyun.com/)上的值。

    ![Advanced设置](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/2802900061/p166425.png)

    参数说明如下：

    |类型|参数|示例值|说明|
    |--|--|---|--|
    |部署JAR包|Package Version|1.0.1|部署的应用版本号。|
    |JDK|Open JDK 8|部署的应用依赖的JDK版本。|
    |Web Container|apache-tomcat-7.0.91|部署的应用依赖的Tomcat版本。|
    |启动命令设置|Jar Start Options|custom-option|JAR包启动应用选项。应用默认启动命令如下：    ```
$JAVA_HOME/bin/java $JarStartOptions -jar $CATALINA_OPTS "$package_path" $JarStartArgs
    ``` |
    |Jar Start Args|custom-args|JAR包启动应用参数。应用默认启动命令如下：    ```
$JAVA_HOME/bin/java $JarStartOptions -jar $CATALINA_OPTS "$package_path" $JarStartArgs
    ``` |
    |发布策略设置|Update Strategy|\{"type":"GrayBatchUpdate","batchUpdate":\{"batch":2,"releaseType":"auto","batchWaitTime":1\},"grayUpdate":\{"gray":1\}\}|部署策略，可参考以下示例：    -   示例1：灰度1台+后续分2批+自动分批+分批间隔1分钟

        ```
{"type":"GrayBatchUpdate","batchUpdate":{"batch":2,"releaseType":"auto","batchWaitTime":1},"grayUpdate":{"gray":1}}
        ```

    -   示例2：分2批发布+自动分批+分批间隔0分钟

        ```
{"type":"BatchUpdate","batchUpdate":{"batch":2,"releaseType":"auto","batchWaitTime":0}}
        ``` |
    |Hosts绑定设置|Custom Host Alias|\[\{"hostName":"samplehost","ip":"127.0.0.1"\}\]|容器内自定义Host映射。|
    |应用健康检查设置|Liveness|\{"exec":\{"command":\["sleep","5s"\]\},"initialDelaySeconds":10,"timeoutSeconds":11\}|容器健康检查，健康检查失败的容器将被杀死并恢复。目前仅支持容器内下发命令的方式：    ```
{"exec":{"command":["sleep","5s"]},"initialDelaySeconds":10,"timeoutSeconds":11}
    ``` |
    |Readiness|\{"exec":\{"command":\["sleep","6s"\]\},"initialDelaySeconds":15,"timeoutSeconds":12\}|应用启动状态检查，多次健康检查失败的容器将被杀死并重启。不通过健康检查的容器将不会有SLB流量进入。|
    |部署设置|Min Ready Instances|1|应用的最小存活实例数。|
    |Batch Wait Time|10|分批发布等待时间，单位为秒。|
    |环境变量设置|Envs|\[\{"name":"envtmp","value":"0"\}\]|容器环境变量参数。|

4.  单击**Run**。

    您可以通过以下两种方式证明应用已部署成功：

    -   IntelliJ IDEA的**Console**区域打印的运行日志中显示`BUILD SUCCESS`。
    -   [SAE控制台](https://sae.console.aliyun.com/)上的应用变更记录显示**执行成功**。

## 管理Maven构建任务

在**Deploy to SAE**页面的**Before launch**区域，您可以对Maven构建任务执行添加、删除、修改和移动操作。

![管理Maven构建任务](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3802900061/p166430.png)

1.  在IntelliJ IDEA界面左侧的**Project**中右键单击待部署的工程名，在快捷菜单中选择**Alibaba Cloud** \> **Deploy to SAE...**。

2.  在**Deploy to SAE**页面的**Before launch**区域，管理Maven任务。

    -   添加任务
        1.  单击**Before launch**区域右侧的![添加Maven任务](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/7281610061/p166693.png)，在下拉框中选择**Run Maven Goal**。
        2.  在**Select Maven Goal**对话框中，选择当前工程可用的模块，在**Command line**区域中输入构建命令。

            ![添加Maven任务对话框](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9731610061/p166696.png)

        3.  单击**OK**。
    -   删除任务：选择需要删除的任务，单击**Before launch**区域右侧的![删除Maven任务](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9731610061/p166698.png)。
    -   修改任务：选择需要修改的任务，单击**Before launch**区域右侧的![编辑Maven任务](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9731610061/p166700.png)，在**Select Maven Goal**对话框中修改任务信息，单击**OK**。
    -   移动任务：选择需要移动的任务，单击**Before launch**区域右侧的![移动Maven任务1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9731610061/p166701.png)或![移动Maven任务2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/9731610061/p166702.png)，调整任务顺序。

## 部署多模块工程

多模块工程是各个模块独立开发，模块之间存在调用关系的项目工程。Cloud Toolkit可以用于部署多模块工程中的某个子模块的场景。

如果您需要部署多模块Maven工程的子模块，您需要在**Deploy to SAE**页面的**Before launch**区域中，将待部署的子模块任务设置为最后执行，具体操作请参见[使用IntelliJ IDEA部署多模块工程中的子模块]() 。

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

