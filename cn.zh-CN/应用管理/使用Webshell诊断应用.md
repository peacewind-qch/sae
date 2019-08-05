# 使用Webshell诊断应用 {#concept_123414_zh .concept}

本文将先向您介绍 SAE 中的 Webshell 功能，以及 SAE 应用的网络环境（包括容器内的环境）等运维背景知识，然后在此基础上教您如何利用 Webshell 完成基本的运维需求。

## Webshell 简介 {#section_w2f_gw7_ah9 .section}

您可以通过阿里云控制台直接获取 ECS 的 Shell 来完成自己的运维需求。如果 ECS 内开启了 SSH 服务，且 ECS 存在弹性公网 IP，那么您也可以在本地通过 SSH 服务获取 ECS 的 Shell 完成运维需求。

由于 SAE 特殊的架构和网络环境，您暂时无法直接从本地通过 SSH 服务获取应用容器的 Shell。在 SAE 的场景中，容器是一个暂态的、供应用运行的环境，一般来说不需要进入运维。为了方便您进行线上问题定位排查，SAE 在控制台提供了一个简单的 Webshell，供您查看并调试自己的容器，操作入口如下图所示：

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/123414/cn_zh/1561705730643/webshell%E5%85%A5%E5%8F%A3.png)

打开 Webshell 后，您可以点击窗口右上角的全屏按钮将窗口全屏显示：

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/123414/cn_zh/1561706052658/webshell%E5%85%A8%E5%B1%8F.png)

SAE 默认给出的 Jar/War 类型应用的容器基础镜像主要是面向应用运行时，暂未提供冗余的排查工具。对于您自己的镜像，不需要在镜像中启动 SSH 服务，只需要带有可执行的`/bin/bash`即可，同时建议您带上所需的运维工具，方便排查。

**说明：** 目前 Webshell 不支持 Windows 镜像。

## 应用的网络环境 {#section_hkc_8ux_nai .section}

SAE 应用处于您自己购买的阿里云 VPC 内。SAE 还额外提供了一层中间件服务调用隔离的手段：命名空间。命名空间与 VPC 内的 VSwitch 是绑定关系，一个命名空间对应一个 VSwitch，一个 VSwitch 可以对应多个命名空间（关于 VPC 的原理和产品介绍，请参见[VPC 基础架构](https://help.aliyun.com/document_detail/34221.html)）。简单来讲，VPC 内的 IP 地址为局域网地址，不同 VPC 内的 2 层以上数据包无法路由到目的地。命名空间主要用于中间件逻辑隔离，不同命名空间内的应用在中间件层面是隔离的，如服务发现和配置下发等。

鉴于 VPC 的产品特性和当前的 SAE 的产品特性，容器无法直接触达 VPC 外的服务（阿里云产品除外，如 OSS、镜像服务等）。在没有额外配置的情况下，您的容器运行在网络“孤岛”环境。

容器无法触达公网的代码示例：

![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/123414/cn_zh/1561708585549/webshell-docker.png)

基于以上网络情况的介绍，您应该可以明白为什么您无法直接触达自己的容器了。

容器内需要访问公网服务，可以通过购买 NAT，并配置 VPC 内 VSwitch 的 SNAT 规则即可，详见[应用如何访问公网](https://help.aliyun.com/document_detail/100317.html)。SNAT 规则可以让 VPC 内地址访问公网地址，从而使用公网暴露的服务，获取到公网的资源。

## 构建镜像的方法 {#section_xzw_5zj_4i1 .section}

基于阿里云容器镜像服务，SAE 集成了为您构建和管理镜像的功能。用于构建的基础镜像为 `centos:7`，在此基础上为您配置好了时区、语言与编码方式、Open JDK 运行环境。

容器存在的目的是为了让应用运行起来，SAE 不可能以占用所有用户运行时资源为代价，集成过多的工具。因此，若您对容器内工具有需求，建议自行构建镜像（构建方法请参见[制作应用镜像](../../../../cn.zh-CN/应用部署/制作应用镜像.md#)），或者按需从 OSS 拉取。

## 诊断应用 {#section_as2_dqj_n53 .section}

线上容器的运维一般是不必要的。如果您确定需要进入容器进行运维，请务必了解您的操作对线上业务的风险：对于单点应用，您的行为可能导致容器 OOM，从而导致分钟级别的业务中断，而对于多点部署的业务，上述现象可能造成业务秒级中断。

SAE 应用的诊断一般从这两个方面入手：常规检查和上传搜集的日志。

-   常规检查

    常规检查的方法比较多，以 Java 应用为例，一般是检查进程、线程以及 JVM 的健康状态。

    -   首先执行命令`ps -ef | grep java`检查您的 Java 进程是否还存在。这里必须特别说明的是，容器内一般需要使用主进程启动您的应用，这样一旦您的应用被 kill 掉，容器也会退出，SAE 会将退出的容器重新启动，防止业务中断。
    -   如果进程不见了，可以执行命令`dmesg | grep -i kill`查看 OOM 相关日志。如果存在日志，那么说明您的应用进程被 kill 掉了，接着检查工作目录下`hs_err_pid{PID}.log`日志文件，定位具体的原因。
    -   Java 类型应用的在线分析可以使用阿里巴巴开源软件 Arthas 解决，建议在测试镜像中集成 Arthas 工具进行常规诊断。Arthas 可以很方便地实时查看类加载情况，观察方法出入参，环境变量等。

**说明：** 

接入 Arhas前，需要先打通公网。

您可以执行以下命令下载并运行 Arthas：

``` {#codeblock_w8d_f32_2l5 .language-java}
wget https://alibaba.github.io/arthas/arthas-boot.jar
java -jar arthas-boot.jar
											
```

-   日志上传

    受限于容器内工具的匮乏，推荐的方案是将容器内搜集到的日志上传到云端，然后下载到本地进行分析。SAE 暂时没有提供容器内日志的下载功能，这里给出一种基于阿里云 OSS 服务的解决方案。OSS 打通了阿里云生态几乎所有的网络环境，您几乎可以在任何网络环境下上传以及下载 OSS 上的文件。

    利用 OSS 服务上传并下载日志的操作方法如下：

    1.  在容器内部[安装 OSS 命令行工具](https://help.aliyun.com/document_detail/50452.html)。

        ``` {#codeblock_qdg_hzp_6f9 .language-java}
        ## 以64位centos系统，root下
        ## 没有打通公网的情况下可以选择在本地下载，然后将这个文件上传到 oss，然后取 oss 的 vpc 内地址进行下载
        wget http://gosspublic.alicdn.com/ossutil/1.5.0/ossutil64
        chmod 755 ossutil64
        								
        ```

    2.  配置您的 OSS 命令行工具，附上当前地域 VPC 内的 [endpoint](https://help.aliyun.com/document_detail/31837.html)（VPC 内的上传不需要打通公网，也不消耗公网带宽流量，更加经济），并填写用于接收上传文件的账号的 [AccessKey](https://help.aliyun.com/document_detail/53045.html)，然后查看已经创建的 Bucket，来检查您的 OSS 服务是否可用。

        ``` {#codeblock_7ip_m6d_ndp .language-java}
        ## 请先确保账号（不必是当前账号，任意开通阿里云oss服务的账号均可）已开通 OSS 服务
        ## 按照提示配置您的 AK SK endpoint信息，ststoken 不需要填写
        ./ossutil64 config
        ## 检查账号是否可用，如果报错则配置错误，如果没有bucket，则建议前往oss控制台创建，命令行工具也支持创建
        ./ossutil64 ls
        ## 这里创建一个模拟的日志文件，用于上传
        echo "Hello" > edas-app.log
        ./ossutil64 cp edas-app.log {bucket-address，例如：oss://test-bucket，可以从上述命令"./ossutil64 ls"中查看}
        								
        ```

    3.  从 OSS 控制台或其他工具中找到您的日志文件，下载到本地，并使用您熟悉的工具进行分析。

