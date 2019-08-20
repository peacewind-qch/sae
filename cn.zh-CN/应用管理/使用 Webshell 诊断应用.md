# 使用 Webshell 诊断应用 {#concept_123414_zh .concept}

本文将先向您介绍 SAE 的 Webshell 功能，以及 SAE 应用的网络环境（包括容器内的环境）等运维背景知识，并在此基础上教您如何利用 Webshell 完成基本的运维需求。

## Webshell 简介 {#section_w2f_gw7_ah9 .section}

您可以通过阿里云控制台直接获取 ECS 的 Shell 来完成运维需求。如果 ECS 内开启了 SSH 服务，且 ECS 存在弹性公网 IP，那么在本地可以通过 SSH 服务获取 ECS 的 Shell 完成运维需求。

在 SAE 的场景中，容器是一个暂态的、供应用运行的环境，通常不需要进行运维。为了方便进行线上问题定位、排查，SAE 在控制台提供了简易版 Webshell，供您查看并调试自己的容器。操作入口如下图所示：

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/123414/cn_zh/1561705730643/webshell%E5%85%A5%E5%8F%A3.png)

打开 Webshell 后，您可以单击窗口右上角的全屏按钮，将窗口全屏显示。

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/123414/cn_zh/1561706052658/webshell%E5%85%A8%E5%B1%8F.png)

SAE 应用容器的基础镜像是面向运行时的，暂态的，因此您的镜像，不需要在镜像中启动 SSH 服务，仅需要带有可执行的`/bin/bash`即可，同时建议您带上所需的运维工具，方便排查。

**说明：** 目前 Webshell 不支持 Windows 镜像。

## 应用的网络环境 {#section_hkc_8ux_nai .section}

SAE 应用置于自建的 VPC 网络，并提供了命名空间功能，可以将中间件层面的服务调用进行逻辑隔离。命名空间与 VPC 内的 VSwitch 为绑定关系，一个命名空间仅能对应一个 VSwitch，一个 VSwitch 可以对应多个命名空间。即 VPC 内的 IP 地址为局域网地址，不同 VPC 内应用间无法访问。命名空间主要用于中间件逻辑隔离，不同命名空间内的应用在中间件层面是隔离的，如服务发现和配置下发等。

**说明：** VPC 的原理和产品介绍，具体内容请参见[VPC 基础架构](https://help.aliyun.com/document_detail/34221.html)。

鉴于 VPC 的产品特性和当前的 SAE 的产品特性，容器无法直接触达 VPC 外的服务（阿里云产品除外，如 OSS、镜像服务等）。在没有额外配置的情况下，您的容器运行在网络“孤岛”环境。从而从另一方面阐述了为什么用户无法直接触达 SAE 应用容器。

容器无法触达公网的代码示例：

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/123414/cn_zh/1561708585549/webshell-docker.png)

容器内如果需要访问公网服务，须购买 NAT，并在 VPC 内 配置 VSwitch 的 SNAT 规则，具体操作请参见[应用如何访问公网](https://help.aliyun.com/document_detail/100317.html)。

SNAT 规则可以让 VPC 内地址访问公网地址，从而能够调用公网显露的服务，获取公网资源。

## 构建镜像的方法 {#section_xzw_5zj_4i1 .section}

基于阿里云容器镜像服务，SAE 集成了镜像构建和管理镜像的功能。用于构建的基础镜像为 `centos:7`，并为您配置了时区、语言与编码方式、Open JDK 运行环境等运行环境。

容器存在的目的是为了让应用运行起来，SAE 不可能以占用所有用户运行资源为代价，集成过多的工具。因此，若您对容器内工具有更多需求，请参见[制作应用镜像](../../../../cn.zh-CN/应用部署/制作应用容器 Docke 镜像.md#)内容自行构建镜像或者按需从 OSS 获取。

## 诊断应用 {#section_as2_dqj_n53 .section}

通常线上容器运维不必要。如果您需要进入容器并进行运维，存在一定的业务风险

-   单点应用业务：可能导致容器 OOM，从而导致分钟级别的业务中断。
-   多点部署业务：可能导致业务秒级中断。

SAE 应用的诊断有常规检查和上传搜集的日志两种方式。

-   常规检查

    常规检查方法众多。以 Java 应用为例，有进程检查、线程以及 JVM 的健康状态检查。

    -   执行命令`ps -ef | grep java`检查应用的 Java 进程是否存在。

        **说明：** 容器内通常使用主进程启动应用，如果应用被 kill 掉，则容器也会退出，SAE 自动将退出的容器重新启动，防止业务中断。

        如果进程不存在，请执行`dmesg | grep -i kill`命令检查 OOM 日志。如果日志存在，表示应用的进程被 Kill 掉，需要检查工作目录下`hs_err_pid{PID}.log`日志文件，并定位具体原因。

    -   Java 类型应用在线分析还可以使用阿里巴巴开源软件 Arthas，建议在测试镜像中集成 Arthas 工具进行常规诊断。Arthas 能够实时查看 Java 类加载情况，方便观察方法出参、入参和环境变量等。

        **说明：** 

        接入 Arhas前，请先链接公网。

        您可以执行以下命令下载并运行 Arthas：

        ``` {#codeblock_gfz_606_9rb .language-java}
        wget https://alibaba.github.io/arthas/arthas-boot.jar
        java -jar arthas-boot.jar
        										
        ```

-   日志上传

    由于容器内工具匮乏，推荐将容器内搜集到的日志上传到云端，并下载到本地进行分析。

    目前 SAE 没有容器内日志下载功能，由于OSS 服务连通阿里云下所有网络环境，推荐使用阿里云 OSS 服务进行日志上传下载。

    通过 OSS 服务上传并下载日志的操作方法如下：

    1.  在容器内部[安装 OSS 命令行工具](https://help.aliyun.com/document_detail/50452.html)。

        ``` {#codeblock_qdg_hzp_6f9 .language-java}
        ## 以64位centos系统，root下
        ## 没有打通公网的情况下可以选择在本地下载，然后将这个文件上传到 oss，然后取 oss 的 vpc 内地址进行下载
        wget http://gosspublic.alicdn.com/ossutil/1.5.0/ossutil64
        chmod 755 ossutil64
        								
        ```

    2.  配置所需的 OSS 命令行工具，并附上当前地域 VPC 内的 [endpoint](https://help.aliyun.com/document_detail/31837.html)，填写用于接收上传文件的账号的 [AccessKey](https://help.aliyun.com/document_detail/53045.html)，查看已经创建的 Bucket，检查您的 OSS 服务是否可用。

        ``` {#codeblock_7ip_m6d_ndp .language-java}
        ## 请确保账号（不必是当前账号，任意开通阿里云oss服务的账号均可）已开通 OSS 服务
        ## 按照提示配置您的 AK SK endpoint信息，ststoken 无需填写
        ./ossutil64 config
        ## 检查账号是否可用，如果报错则配置错误，如果没有bucket，则建议前往oss控制台创建，命令行工具也支持创建
        ./ossutil64 ls
        ## 这里创建一个模拟的日志文件，用于上传
        echo "Hello" > edas-app.log
        ./ossutil64 cp edas-app.log {bucket-address，例如：oss://test-bucket，可以从上述命令"./ossutil64 ls"中查看}
        								
        ```

    3.  从 OSS 控制台或其他工具中找到您的日志文件，下载到本地，并使用您熟悉的工具进行分析。

