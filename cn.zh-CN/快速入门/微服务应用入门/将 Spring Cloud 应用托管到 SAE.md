# 将 Spring Cloud 应用托管到 SAE {#concept_123013_zh .concept}

您在本地开发了依赖 Eureka、Consul、ZooKeeper 等组件实现的服务注册与发现的 Spring Cloud 应用。若您想将该应用部署至 SAE，需要将服务注册与发现的组件的依赖和配置替换成 Spring Cloud Alibaba Nacos Discovery，无需修改任何业务代码，可将应用部署到 SAE 并进行 SAE微服务管理。

## 背景信息 {#section_2mg_bjh_eho .section}

Spring Cloud Alibaba Nacos Discovery 实现了 Spring Cloud Registry 的标准接口与规范，与 Spring Cloud 接入 Eureka、Consul、ZooKeeper 等组件实现服务注册与发现的方式一致。

使用开源版本 Spring Cloud Alibaba Nacos Discovery 开发的应用部署到 SAE 上，可以享受商业版的 SAE 服务注册中心的优势和能力。

商业版的 SAE 服务注册中心，与 Nacos、Eureka 和 Consul 相比，具有以下优势：

-   共享组件，节省了您部署、运维 Nacos、Eureka 或 Consul 的成本。
-   对服务注册和发现的调用均进行了链路加密，保护您的服务安全性，无需担心服务被未授权的应用发现。
-   SAE 服务注册中心与 SAE 其他组件紧密结合，为您提供一套完整的微服务解决方案，包括环境隔离、平滑上下线、灰度发布等。

## 前提条件 {#section_mnz_qe1_2k7 .section}

下载最新版本的 [Nacos Server](https://github.com/alibaba/nacos/releases)，并按以下步骤启动 Nacos Server。

1.  解压已下载的 Nacos Server 压缩包。
2.  进入`nacos/bin`目录，启动 Nacos Server。
    -   Linux/Unix/Mac 系统：执行命令`sh startup.sh -m standalone`。
    -   Windows 系统：双击执行`startup.cmd`文件。

## 步骤一：获取 Demo {#section_mli_6ez_15p .section}

eureka-service-provider和eureka-service-consumer是SAE提供的2个 Demo ，二者均为已经接入 Eureka 服务注册与发现的 Spring Cloud 应用，您需要下载到本地完成后续操作。

-   [eureka-service-provider 下载\>\>](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/SAE/eureka-service-provider.zip)
-   [eureka-service-consumer 下载\>\>](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/SAE/eureka-service-consumer.zip)

## 步骤二： provider 应用侧操作 {#section_amv_fb6_zqo .section}

将原来的应用托管到 SAE 中，需要在 provider 应用程序中添加 pom 依赖，并指定 Nacos Server 的IP地址。

1.  添加 pom 依赖。

    打开 provider 应用的 pom.xml 文件中，将 `spring-cloud-starter-netflix-eureka-client` 替换成为`spring-cloud-starter-alibaba-nacos-discovery`，并设置 nacos server 的版本信息。

    替换前：

    ``` {#codeblock_gl8_bc5_ue3 .language-xml}
    <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
    							
    ```

    替换后：

    ``` {#codeblock_s1u_2tx_za7 .language-xml}
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        <version>0.9.0.RELEASE</version>
    </dependency>
    							
    ```

    **说明：** 

    -   本示例中使用的版本为 Spring Cloud Greenwich，对应 `spring-cloud-starter-alibaba-nacos-discovery` 版本为 `0.9.0.RELEASE`。
    -   如果您使用的是 Spring Cloud Finchley 版本，对应 `spring-cloud-starter-alibaba-nacos-discovery` 版本为 `0.2.2.RELEASE`。
    -   如果使用的是 Spring Cloud Edgware 版本，对应 `spring-cloud-starter-alibaba-nacos-discovery` 版本为 `0.1.2.RELEASE`。（Spring Cloud Edgware 版本将在 2019 年 8 月结束生命周期，不推荐使用该版本进行应用开发。）
2.  指定 Nacos Server 的IP地址。

    打开`src\main\resources`路径下的文件`application.properties`，指定 Nacos Server 的IP地址。

    修改前：

    ``` {#codeblock_bu7_jbw_k3c .language-xml}
    spring.application.name=service-provider
    server.port=18081
    eureka.client.serviceUrl.defaultZone=http://127.0.0.1:8761/eureka/
    							
    ```

    修改后：

    ``` {#codeblock_irf_tsp_a61 .language-xml}
    spring.application.name=service-provider
    server.port=18081
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
    							
    ```

    其中`127.0.0.1`为 Nacos Server 的 IP 地址。如果您的 Nacos Server 部署在另外一台机器，则需要修改成对应的 IP 地址。如果有其它需求，可以参考[配置项参考](#section_07h_l2l_rvu)在`application.properties`文件中增加所需配置。

3.  查询应用服务。
    1.  执行`nacos-service-provider`中`ProviderApplication`的`main`函数，启动应用。
    2.  登录本地启动的 Nacos Server 控制台`http://127.0.0.1:8848/nacos`，在左侧导航栏中选择**服务管理** \> **服务列表** ，可以看到服务列表中包含了`service-provider`，且在详情中可以查询该服务的详情。

**说明：** 本地 Nacos 控制台的默认用户名和密码均为 `nacos`。


## 步骤三： consumer 应用侧操作 {#section_k3x_qbt_5ca .section}

将原来的应用托管到 SAE 中，需要在 consumer 应用程序中添加 pom 依赖，并指定 Nacos Server 的IP地址。

1.  添加 pom 依赖。

    在 consumer应用的 `pom.xml` 文件中，将 `spring-cloud-starter-netflix-eureka-server` 替换成 `spring-cloud-starter-alibaba-nacos-discovery`，并设置 nacos server 的版本。

    替换前：

    ``` {#codeblock_omb_g4s_po2 .language-xml}
    <dependency>
       <groupId>org.springframework.cloud</groupId>
       <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
    							
    ```

    替换后：

    ``` {#codeblock_bsk_cia_tgl .language-xml}
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        <version>0.9.0.RELEASE</version>
    </dependency>
    							
    ```

    **说明：** 

    -   本示例中使用的版本为 Spring Cloud Greenwich，对应 `spring-cloud-starter-alibaba-nacos-discovery` 版本为 `0.9.0.RELEASE`。
    -   如果您使用的是 Spring Cloud Finchley 版本，对应 `spring-cloud-starter-alibaba-nacos-discovery` 版本为 `0.2.2.RELEASE`。
    -   如果使用的是 Spring Cloud Edgware 版本，对应 `spring-cloud-starter-alibaba-nacos-discovery` 版本为 `0.1.2.RELEASE`。（Spring Cloud Edgware 版本将在 2019 年 8 月结束生命周期，不推荐使用该版本进行应用开发。）
2.  修改配置。

    打开`src\main\resources`路径下的文件`application.properties`，指定 Nacos Server 的IP地址。

    修改前 ：

    ``` {#codeblock_hb6_pkh_06p .language-xml}
    spring.application.name=service-consumer
    server.port=18082
    eureka.client.serviceUrl.defaultZone=http://127.0.0.1:8761/eureka/
    							
    ```

    修改后：

    ``` {#codeblock_bnv_vx7_2op .language-xml}
    spring.application.name=service-consumer
    server.port=18082
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
    							
    ```

    其中`127.0.0.1`为 Nacos Server 的IP地址。如果您的 Nacos Server 部署在另外一台机器，则需要修改成对应的 IP 地址。如果有其它需求，可以参考[配置项参考](#section_07h_l2l_rvu)在`application.properties`文件中增加配置。

3.  查询应用服务。
    1.  执行`eureka-service-provider`中`ConsumerApplication.java`，启动应用。
    2.  登录本地启动的 Nacos Server 控制台`http://127.0.0.1:8848/nacos`，在左侧导航栏中选择**服务管理** \> **服务列表** ，可以看到服务列表中已经包含了`service-consumer`，且在详情中可以查询该服务的详情。

**说明：** 本地 Nacos 控制台的默认用户名和密码均为 `nacos`。


## 步骤四：查看调用结果 {#section_50j_4lj_dn9 .section}

在本地测试消费者对提供者的服务调用结果。启动服务，执行 `IP + port / echo-rest / 自定义变量` 或 `IP + port / echo-feign / 自定义变量` 查看调用结果。

-   Linux/Unix/Mac 系统：执行`curl http://127.0.0.1:18082/echo-rest/{自定义变量}`或`curl http://127.0.0.1:18082/echo-feign/{自定义变量}`。

-   Windows系统：在浏览器中输入`http://127.0.0.1:18082/echo-rest/{自定义变量}`或`http://127.0.0.1:18082/echo-feign/{自定义变量}`。


## 步骤五：将应用部署到 SAE {#section_9di_2ge_kgj .section}

1.  在应用的pom.xml文件中添加如下配置，然后执行 mvn clean package命令将本地的程序编译成可执行的 JAR 包。

    ``` {#codeblock_lv3_vo2_519 .language-xml}
    <build>
         <plugins>
             <plugin>
                 <groupId>org.springframework.boot</groupId>
                 <artifactId>spring-boot-maven-plugin</artifactId>
                 <executions>
                     <execution>
                         <goals>
                             <goal>repackage</goal>
                         </goals>
                     </execution>
                 </executions>
             </plugin>
         </plugins>
     </build>
    					
    ```

2.  参照[部署微服务应用到 SAE](https://help.aliyun.com/document_detail/97761.html)，分别将在[步骤二： provider 应用侧操作](#section_amv_fb6_zqo)和[步骤二： provider 应用侧操作](#section_amv_fb6_zqo)修改依赖配置后的两个应用包部署至 SAE。

**说明：** 

-   SAE 暂不支持创建空应用，故第一次部署需在控制台完成。
-   如果使用 JAR 包部署，在应用部署配置时**应用运行环境**必需选择标准 Java 应用运行环境 。
-   如果使用 WAR 包部署，在应用部署配置时**应用运行环境**必需选择apache-tomcat-XXX 。
    当您将应用部署到 SAE 时，SAE 服务注册中心会以高优先级去自动设置 Nacos Server 服务端地址和服务端口，以及 namespace、access-key、secret-key、context-path 等信息。您无需进行任何额外的配置，原有的配置内容可以选择保留或删除。


## 步骤六：结果验证 {#section_dn7_4p2_y1v .section}

1.  为 consumer 应用[绑定公网 SLB](https://help.aliyun.com/document_detail/113305.html)，并在浏览器键入所设置的公网访问地址，进入应用首页。
2.  在应用首页发起调用请求，然后登录 SAE 控制台，进入消费者应用详情页面。
3.  在左侧导航栏选择**应用监控** \> **应用总览**，查看服务调用数据总览。当能够监测到调用数据则说明服务调用成功。

## 配置项参考 {#section_07h_l2l_rvu .section}

|配置项|Key|默认值|说明|
|---|---|---|--|
|服务端地址|spring.cloud.nacos.discovery.server-addr|无|Nacos Server 启动监听的 IP 地址和端口。|
|服务名|spring.cloud.nacos.discovery.service|$\{spring.application.name\}|给当前的服务命名。|
|网卡名|spring.cloud.nacos.discovery.network-interface|无|当 IP 未配置时，注册的 IP 为此网卡所对应的 IP 地址。如果此项也未配置，则默认取第一块网卡的地址。|
|注册的 IP 地址|spring.cloud.nacos.discovery.ip|无|优先级最高|
|注册的端口|spring.cloud.nacos.discovery.port|-1|默认情况下不用配置，系统会自动探测。|
|命名空间|spring.cloud.nacos.discovery.namespace|无|常用场景之一是不同环境的注册的区分隔离，例如开发测试环境和生产环境的资源（如配置、服务）隔离等。|
|Metadata|spring.cloud.nacos.discovery.metadata|无|使用 Map 格式配置，用户可以根据自己的需要自定义一些和服务相关的元数据信息。|
|集群|spring.cloud.nacos.discovery.cluster-name|DEFAULT|配置成 Nacos 集群名称。|
|接入点|spring.cloud.nacos.discovery.enpoint|UTF-8|地域的某个服务的入口域名，通过此域名可以动态地拿到服务端地址，此配置在部署到 EDAS 时无需填写。|
|是否集成 Ribbon|ribbon.nacos.enabled|true|一般不需要修改|

更多关于 Spring Cloud Alibaba Nacos Discovery 的信息请参见开源版本的 [Spring Cloud Alibaba Nacos Discovery](https://github.com/spring-cloud-incubator/spring-cloud-alibaba/wiki/Nacos-discovery) 文档。

