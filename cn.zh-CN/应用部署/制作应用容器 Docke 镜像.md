# 制作应用容器 Docke 镜像 {#concept_98492_zh .concept}

Spring Cloud 或 Dubbo 框架下编译的应用War 包或 Jar 包，如果需要在 SAE 上以镜像方式部署，请参见本文将应用的War 包或 Jar 包制作为镜像并在 SAE 中发布。

## 注意事项 {#section_x77_afn_264 .section}

在制作应用镜像前，请查阅[镜像创建规约](#section_roq_3tb_2nt)并按照规约制作镜像。

## 创建标准 Dockerfile {#section_5vd_j7r_cxr .section}

[Dockerfile](https://docs.docker.com/engine/reference/builder/) 是以文本格式来快速创建自定义镜像的配置文件。

标准的[Dockerfile](https://docs.docker.com/engine/reference/builder/)描述了 SAE 创建应用运行环境所需的所有指令。

-   针对 War 包应用，该指令定义了对 JDK、Tomcat、War 包的下载、安装和启动等操作。
-   针对 Jar 包应用，该指令定义了对 JDK、Jar 包的下载、安装和启动等操作。

如下示例介绍如何制作不同框架应用镜像的 Dockerfile。

-   [HSF 应用的 Dockerfile 示例（基于 WAR 包）](#)
-   [HSF 应用的 Dockerfile 示例（基于 JAR 包）](#)
-   [Spring Cloud 或 Dubbo 应用的 Dockerfile 示例（基于 WAR 包）](#)
-   [Spring Cloud 或 Dubbo 应用的 Dockerfile 示例（基于 JAR 包）](#)

## HSF 应用的 Dockerfile 示例（基于 WAR 包） {#section_6sv_980_6vo .section}

``` {#codeblock_qzx_yc6_erq}
FROM centos:7
MAINTAINER 轻量级分布式应用服务 SAE 研发团队 
# 安装打包必备软件
RUN yum -y install wget unzip telnet
# 准备 JDK/Tomcat 系统变量
ENV JAVA_HOME /usr/java/latest
ENV CATALINA_HOME /home/admin/apache-tomcat-7.0.91
ENV ADMIN_HOME /home/admin
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/bin
RUN mkdir -p /home/admin
# 下载安装 JDK 7
RUN wget http://edas-hz.oss-cn-hangzhou.aliyuncs.com/agent/prod/files/jdk-7u80-linux-x64.rpm -O /tmp/jdk-7u80-linux-x64.rpm && \
    yum -y install /tmp/jdk-7u80-linux-x64.rpm && \
    rm -rf /tmp/jdk-7u80-linux-x64.rpm
# 下载安装Tomcat
RUN wget http://edas-hz.oss-cn-hangzhou.aliyuncs.com/apache-tomcat-7.0.91.tar.gz -O /tmp/apache-tomcat-7.0.91.tar.gz && \
    tar -xvf /tmp/apache-tomcat-7.0.91.tar.gz -C /home/admin && \
    rm /tmp/apache-tomcat-7.0.91.tar.gz && \
    chmod +x ${CATALINA_HOME}/bin/*sh

RUN mkdir -p ${CATALINA_HOME}/deploy/
# 下载部署 SAE 演示 WAR 包
RUN wget http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/hello-edas.war -O /tmp/ROOT.war && \
    unzip /tmp/ROOT.war -d ${CATALINA_HOME}/deploy/ROOT/ && \
    rm -rf /tmp/ROOT.war
# 设定 Tomcat 安装目录为容器启动目录，并采用 run 方式启动 Tomcat，在标准命令行输出 catalina 日志
WORKDIR $ADMIN_HOME
CMD ["catalina.sh", "run"]
			
```

## HSF 应用的 Dockerfile 示例（基于 JAR 包） {#section_58y_7mv_pfq .section}

``` {#codeblock_ad7_ez3_164}
FROM centos:7
MAINTAINER 轻量级分布式应用服务 SAE 研发团队 
# 安装打包必备软件
RUN yum -y install wget unzip telnet
# 准备 JDK/Tomcat 系统变量
ENV JAVA_HOME /usr/java/latest
ENV PATH $PATH:$JAVA_HOME/bin
ENV ADMIN_HOME /home/admin
# 下载安装 JDK 7
RUN wget http://edas-hz.oss-cn-hangzhou.aliyuncs.com/agent/prod/files/jdk-7u80-linux-x64.rpm -O /tmp/jdk-7u80-linux-x64.rpm && \
    yum -y install /tmp/jdk-7u80-linux-x64.rpm && \
    rm -rf /tmp/jdk-7u80-linux-x64.rpm
# 下载部署 SAE 演示 JAR 包
RUN mkdir -p /home/admin/app/ && \
         wget http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/hello-edas-0.0.1-SNAPSHOT.jar -O /home/admin/app/hello-edas-0.0.1-SNAPSHOT.jar
# 将启动命令写入启动脚本 start.sh
RUN mkdir -p /home/admin
RUN echo '$JAVA_HOME/bin/java -jar $CATALINA_OPTS /home/admin/app/hello-edas-0.0.1-SNAPSHOT.jar'> /home/admin/start.sh && chmod +x /home/admin/start.sh
WORKDIR $ADMIN_HOME
CMD ["/bin/bash", "/home/admin/start.sh"]
			
```

## Spring Cloud 或 Dubbo 应用的 Dockerfile 示例（基于 WAR 包） {#section_ope_ayt_l59 .section}

``` {#codeblock_d12_3fh_r8v}
FROM centos:7
MAINTAINER 轻量级分布式应用服务 SAE 研发团队

# 安装打包必备软件
RUN yum -y install wget unzip telnet

# 准备 JDK/Tomcat 系统变量
ENV JAVA_HOME /usr/java/latest
ENV CATALINA_HOME /home/admin/apache-tomcat-7.0.91
ENV ADMIN_HOME /home/admin
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/bin
RUN mkdir -p /home/admin

# 下载安装 OpenJDK 
RUN yum -y install java-1.8.0-openjdk-devel

# 下载安装 Tomcat
RUN wget http://edas-hz.oss-cn-hangzhou.aliyuncs.com/apache-tomcat-7.0.91.tar.gz -O /tmp/apache-tomcat-7.0.91.tar.gz && \
    tar -xvf /tmp/apache-tomcat-7.0.91.tar.gz -C /home/admin && \
    rm /tmp/apache-tomcat-7.0.91.tar.gz && \
    chmod +x ${CATALINA_HOME}/bin/*sh

RUN mkdir -p ${CATALINA_HOME}/deploy/

# 增加容器内中文支持
ENV LANG="en_US.UTF-8"

# 增强 Webshell 使⽤体验
ENV TERM=xterm

# 下载部署 SAE 演示 WAR 包
RUN wget http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/hello-edas.war -O /tmp/ROOT.war && \
    unzip /tmp/ROOT.war -d ${CATALINA_HOME}/deploy/ROOT/ && \
    rm -rf /tmp/ROOT.war

# 设定 Tomcat 安装目录为容器启动目录，并采用 run 方式启动 Tomcat，在标准命令行输出 catalina 日志
WORKDIR $ADMIN_HOME
CMD ["catalina.sh", "run"]
			
```

## Spring Cloud 或 Dubbo 应用的 Dockerfile 示例（基于 JAR 包） {#section_k3p_zr3_ert .section}

``` {#codeblock_0sx_mki_dx4}
FROM centos:7
MAINTAINER 轻量级分布式应用服务 SAE 研发团队 

# 安装打包必备软件
RUN yum -y install wget unzip telnet

# 准备 JDK/Tomcat 系统变量
ENV JAVA_HOME /usr/java/latest
ENV PATH $PATH:$JAVA_HOME/bin
ENV ADMIN_HOME /home/admin

# 下载安装 OpenJDK
RUN yum -y install java-1.8.0-openjdk-devel

# 下载部署 SAE 演示 JAR 包
RUN mkdir -p /home/admin/app/ && \
         wget http://edas-hz.oss-cn-hangzhou.aliyuncs.com/demo/1.0/hello-edas-0.0.1-SNAPSHOT.jar -O /home/admin/app/hello-edas-0.0.1-SNAPSHOT.jar

# 增加容器内中⽂支持
ENV LANG="en_US.UTF-8"

# 增强 Webshell 使⽤体验
ENV TERM=xterm

# 将启动命令写入启动脚本 start.sh
RUN mkdir -p /home/admin
RUN echo '$JAVA_HOME/bin/java -jar $CATALINA_OPTS /home/admin/app/hello-edas-0.0.1-SNAPSHOT.jar'> /home/admin/start.sh && chmod +x /home/admin/start.sh
WORKDIR $ADMIN_HOME
CMD ["/bin/bash", "/home/admin/start.sh"]
			
```

## 自定义设置 Dockerfile {#section_qba_0zs_05r .section}

通过编辑 Dockerfile 方式进行运行环境配置修改，如 JDK 版本替换、Tomcat 配置修改、更改运行时环境等操作。

-   更换 JDK 版本

    在标准 Dockerfile 文件中，请参见如下示例更换其他版本的 JDK。

    ``` {#codeblock_0vh_xh9_cwz}
    # 下载安装 JDK 8
    RUN wget http://edas-hz.oss-cn-hangzhou.aliyuncs.com/agent/prod/files/jdk-8u65-linux-x64.rpm -O /tmp/jdk-8u65-linux-x64.rpm && \
        yum -y install /tmp/jdk-8u65-linux-x64.rpm && \
        rm -rf /tmp/jdk-8u65-linux-x64.rpm
    							
    ```

-   在 Tomcat 启动参数中添加 SAE 运行时环境

    SAE 提供了 JVM 环境变量 `DEAS_CATALINA_OPTS` 包含运行所需的基本参数。此外 Ali-Tomcat 提供了自定义 JVM 参数配置选项 `JAVA_OPTS`，可以设置 Xmx Xms 等参数。 启动参数具体详情请参见[应用运行时环境变量](#table_ov7_c4w_96u) ，

    ``` {#codeblock_3zd_4an_wnr}
    # 设置 SAE 应用 JVM 参数
    ENV CATALINA_OPTS ${EDAS_CATALINA_OPTS}
    # 设置 JVM 参数
    ENV JAVA_OPTS="\
         -Xmx3550m \
         -Xms3550m \
         -Xmn2g \
         -Xss128k"
    							
    ```


## 在本地构建镜像 {#section_hyq_rbg_m4a .section}

从本地命令行进入 Dockerfile 所在的目录，执行 docker build 命令构建镜像：

``` {#codeblock_lsx_1ev_w7e}
docker build -t [标签名称，最好取应用名]:[版本号] .
或
docker build -t [标签名称，最好取应用名]:[版本号] -f /path/to/custom_dockerfile_name .  #假如您创建好的 Dockerfile 在其他位置或名称不为 Dockerfile 时适用。
```

列如：

``` {#codeblock_rll_7x3_ha5}
docker build -t hsf-provider:1.0.0 .
```

构建完成后，使用`docker images | grep <镜像标签名称>`命令查看本地编译好的镜像。

## 上传镜像到镜像仓库 {#section_2s2_m3a_gar .section}

上传本地编译好的镜像到[镜像仓库](https://cr.console.aliyun.com)，并在 SAE 中选择该镜像进行部署。

例如：推送镜像 registry.cn-hangzhou.aliyuncs.com/edas/demo-frontend-service:20181111 镜像到镜像仓库。

``` {#codeblock_e62_mv0_8y8}
docker push registry.cn-hangzhou.aliyuncs.com/edas/demo-frontend-service:20181111
				
```

## 镜像创建规约 {#section_roq_3tb_2nt .section}

通过 Dockerfile 制作自定义镜像时，须遵循以下规范及限制。

-   租户/加密信息

    SAE 应用用户鉴权与加密凭证的信息。

    |环境变量 Key|类型|描述|
    |--------|--|--|
    |tenantId|String|SAE 租户 ID|
    |accessKey|String|鉴权 Access Key ID|
    |secretKey|String|鉴权 Access Key Secret|

    |路径|类型|描述|
    |--|--|--|
    |/home/admin/.spas\_key/default|File|SAE 租户鉴权信息，包含上述 ENV 信息|

-   服务信息

    包含运行时所需连接的 SAE 域名、端口等信息。

    |环境变量 Key|描述|
    |--------|--|
    |EDAS\_ADDRESS\_SERVER\_DOMAIN|配置中心服务域名或 IP|
    |EDAS\_ADDRESS\_SERVER\_PORT|配置中心服务端口|
    |EDAS\_CONFIGSERVER\_CLIENT\_PORT|CS 服务端口|

-   应用运行时环境变量（强制）

    SAE 部署时会提供以下环境变量，为保证应用运行正常，请勿覆盖配置。

    |环境变量 Key|描述|
    |--------|--|
    |POD\_IP|POD IP|
    |EDAS\_APP\_ID|SAE 应用 ID|
    |EDAS\_ECC\_ID|SAE ECC ID|
    |EDAS\_PROJECT\_NAME|同 EDAS\_APP\_ID，用于调用链解析|
    |EDAS\_JM\_CONTAINER\_ID|同 EDAS\_ECC\_ID，用于调用链解析|
    |EDAS\_CATALINA\_OPTS|中间件运行时所需 CATALINA\_OPTS 参数|
    |CATALINA\_OPTS|同 EDAS\_CATALINA\_OPTS，默认 TOMCAT 启动参数|


