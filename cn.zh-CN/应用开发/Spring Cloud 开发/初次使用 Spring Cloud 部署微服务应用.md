# 初次使用 Spring Cloud 部署微服务应用 {#concept_123010_zh .concept}

初次使用原生 Spring Cloud 部署微服务应用时，您需在本地程序中添加依赖配置实现服务注册与发现，并在本地测试调用结果后，将服务提供者和消费者分别部署到 SAE。

-   下载 [Maven](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/App-develop/apache-maven-3.6.0-bin.tar.gz) 并设置环境变量。
-   下载最新版本的 [Nacos Server](https://github.com/alibaba/nacos/releases)，并按以下步骤启动 Nacos Server。
    1.  解压下载的 Nacos Server 压缩包。
    2.  进入`nacos/bin`目录，执行如下命令启动 Nacos Server。
        -   Linux/Unix/Mac 系统：执行命令`sh startup.sh -m standalone`。
        -   Windows 系统：双击执行`startup.cmd`文件。

## 步骤一：获取 Demo {#section_70c_jbp_31o .section}

-   [service-provider 下载\>\>](http://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/demo/nacos-service-provider.zip)
-   [service-consumer 下载\>\>](http://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/demo/nacos-service-consumer.zip)

## 步骤二：创建服务提供者 {#section_35x_xhp_9bs .section}

在本地创建命名为`nacos-service-provider`的Spring Cloud 工程，修改 pom 依赖，开启服务注册与发现，并将注册中心指定为 Nacos Server。

1.  创建名为 nacos-service-provider 的 Maven 工程。
2.  添加 pom 依赖。

    在 `pom.xml` 文件中添加依赖：

    ``` {#codeblock_qzq_y8s_4tj .language-xml}
        <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>2.1.4.RELEASE</version>
            <relativePath/>
        </parent>
    
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
                <version>0.9.0.RELEASE</version>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
            </dependency>
        </dependencies>
    
        <dependencyManagement>
            <dependencies>
                <dependency>
                    <groupId>org.springframework.cloud</groupId>
                    <artifactId>spring-cloud-dependencies</artifactId>
                    <version>Greenwich.SR1</version>
                    <type>pom</type>
                    <scope>import</scope>
                </dependency>
            </dependencies>
        </dependencyManagement>
    
        <build>
            <plugins>
                <plugin>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-maven-plugin</artifactId>
                </plugin>
            </plugins>
        </build>
    							
    ```

    Spring Cloud Alibaba 版本说明：

    -   示例中使用的版本为 Spring Cloud Greenwich ，对应 Spring Cloud Alibaba 版本为 0.9.0.RELEASE。
    -   如果使用 Spring Cloud Finchley 版本，对应 Spring Cloud Alibaba 版本为 0.2.2.RELEASE。
    -   如果使用 Spring Cloud Edgware 版本，对应 Spring Cloud Alibaba 版本为 0.1.2.RELEASE。（Spring Cloud Edgware 版本的生命周期即将在 2019 年 8 月结束，不推荐使用这个版本开发应用。）
3.  开启服务注册与发现。
    1.  在`src\main\java`下创建命名为`com.aliware.sae`的 Package。
    2.  在 Package`com.aliware.sae`中创建服务提供者的启动类`ProviderApplication`，并添加以下代码，其中`@EnableDiscoveryClient`注解表明此应用需开启服务注册与发现功能。

        ``` {#codeblock_ylx_ro5_n29 .language-java}
            package com.aliware.edas;
        
            import org.springframework.boot.SpringApplication;
            import org.springframework.boot.autoconfigure.SpringBootApplication;
            import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
        
            @SpringBootApplication
            @EnableDiscoveryClient
            public class ProviderApplication {
        
                public static void main(String[] args) {
                    SpringApplication.run(ProviderApplication.class, args);
                }
            }
        
        								
        ```

4.  提供 Echo 服务。

    在 Package`com.aliware.edas`中创建`EchoController`，指定 URL mapping 为 \{/echo/\{String\}\}，指定 HTTP 方法为 GET，方法参数从 URL 路径中获得，回显收到的参数。

    ``` {#codeblock_ocr_0mr_0zp}
    
    package com.aliware.edas;
    
    import org.springframework.web.bind.annotation.PathVariable;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;
    import org.springframework.web.bind.annotation.RestController;
    
    @RestController
    public class EchoController {
        @RequestMapping(value = "/echo/{string}", method = RequestMethod.GET)
        public String echo(@PathVariable String string) {
            return string;
        }
    }
    
    							
    ```

5.  修改配置。

    在`src\main\resources`路径下创建文件`application.properties`，并在该文件中添加以下配置，指定 Nacos Server 的地址。

    ``` {#codeblock_z9z_hr5_4vo}
    xml
    spring.application.name=service-provider
    server.port=18081
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
    
    							
    ```

    其中`127.0.0.1`为 Nacos Server 的IP地址。如果您的 Nacos Server 部署在另外一台机器，则需要修改成对应的 IP 地址。如果有其它需求，可以参考[配置项参考](#section_xbv_n1o_n1b)在`application.properties`文件中增加配置。

6.  查询应用服务。
    1.  执行`nacos-service-provider`中`ProviderApplication`的`main`函数，启动应用。

    2.  登录本地启动的 Nacos Server 控制台`http://127.0.0.1:8848/nacos`（本地 Nacos 控制台的默认用户名和密码均为 `nacos`），在左侧导航栏中选择**服务管理** \> **服务列表**，可以看到服务列表中已经包含了`service-provider`，且在详情中可以查询该服务的详情。

## 步骤三：创建服务消费者 {#section_en7_2ca_8r4 .section}

在本地创建名为`nacos-service-consumer` Spring Cloud 工程。修改 pom 依赖，开启服务注册与发现，将注册中心指定为 Nacos Server。添加配置，使消费者在 RestTemplate 和 FeignClient 这两个客户端去调用服务提供者。

1.  创建 nacos-service-consumer 工程命名为`nacos-service-consumer`的 Maven 工程。
2.  添加 pom 依赖。

    在`pom.xml`文件中添加以下依赖。

    ``` {#codeblock_hi0_36y_0cw .language-xml}
    <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>2.1.4.RELEASE</version>
            <relativePath/>
        </parent>
    
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
                <version>0.9.0.RELEASE</version>
            </dependency>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
            </dependency>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-starter-openfeign</artifactId>
            </dependency>
        </dependencies>
    
        <dependencyManagement>
            <dependencies>
                <dependency>
                    <groupId>org.springframework.cloud</groupId>
                    <artifactId>spring-cloud-dependencies</artifactId>
                    <version>Greenwich.SR1</version>
                    <type>pom</type>
                    <scope>import</scope>
                </dependency>
            </dependencies>
        </dependencyManagement>
    
        <build>
            <plugins>
                <plugin>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-maven-plugin</artifactId>
                </plugin>
            </plugins>
        </build>
    						
    ```

3.  开启服务注册与发现。

    与服务提供者 `nacos-service-provider` 相比，除了开启服务注册与发现外，还需要添加两项配置才能使用 RestTemplate 和 FeignClient 这两个客户端：

    1.  在`src\main\java`下创建命名为 `com.aliware.sae`的Package。
    2.  在 Package`com.aliware.sae`中配置 RestTemplate 和 FeignClient。
        1.  在 Package`com.aliware.edas` 中创建一个接口类`EchoService`，添加`@FeignClient`注解，并配置对应的 HTTP URL 地址及 HTTP 方法。

            ``` {#codeblock_66h_g1z_ffi .language-java}
            package com.aliware.edas;
            
            import org.springframework.cloud.openfeign.FeignClient;
            import org.springframework.web.bind.annotation.PathVariable;
            import org.springframework.web.bind.annotation.RequestMapping;
            import org.springframework.web.bind.annotation.RequestMethod;
            
            @FeignClient(name = "service-provider")
            public interface EchoService {
                @RequestMapping(value = "/echo/{str}", method = RequestMethod.GET)
                String echo(@PathVariable("str") String str);
            }
            										
            ```

        2.  在 Package `com.aliware.edas` 中创建启动类`ConsumerApplication`并添加相关配置。

            -   使用 `@EnableDiscoveryClient` 注解启用服务注册与发现。
            -   使用 `@EnableFeignClients` 注解激活 FeignClient。
            -   添加 `@LoadBalanced` 注解将 RestTemplate 与服务发现集成。
            ``` {#codeblock_hdf_alx_unc .language-java}
            package com.aliware.edas;
            
            import org.springframework.boot.SpringApplication;
            import org.springframework.boot.autoconfigure.SpringBootApplication;
            import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
            import org.springframework.cloud.client.loadbalancer.LoadBalanced;
            import org.springframework.cloud.openfeign.EnableFeignClients;
            import org.springframework.context.annotation.Bean;
            import org.springframework.web.client.RestTemplate;
            
            @SpringBootApplication
            @EnableDiscoveryClient
            @EnableFeignClients
            public class ConsumerApplication {
            
                @LoadBalanced
                @Bean
                public RestTemplate restTemplate() {
                    return new RestTemplate();
                }
            
                public static void main(String[] args) {
                    SpringApplication.run(ConsumerApplication.class, args);
                }
            }
            
            										
            ```

4.  创建 Controller。

    在 Package `com.aliware.edas` 中创建类 `TestController` 以演示和验证服务发现功能。

    ``` {#codeblock_5nn_css_rje}
    
    package com.aliware.edas;
    
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.PathVariable;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;
    import org.springframework.web.bind.annotation.RestController;
    import org.springframework.web.client.RestTemplate;
    
    @RestController
    public class TestController {
    
        @Autowired
        private RestTemplate restTemplate;
        @Autowired
        private EchoService echoService;
    
        @RequestMapping(value = "/echo-rest/{str}", method = RequestMethod.GET)
        public String rest(@PathVariable String str) {
            return restTemplate.getForObject("http://service-provider/echo/" + str,
                    String.class);
        }
    
        @RequestMapping(value = "/echo-feign/{str}", method = RequestMethod.GET)
        public String feign(@PathVariable String str) {
            return echoService.echo(str);
        }
    
    }
    
    
    						
    ```

5.  修改配置。

    在`src\main\resources`路径下创建文件`application.properties`，在`application.properties`中添加如下配置，指定 Nacos Server 的IP地址。

    ``` {#codeblock_3k4_55y_z4f}
    
    spring.application.name=service-consumer
    server.port=18082
    spring.cloud.nacos.discovery.server-addr=127.0.0.1:8848
    
    						
    ```

    其中`127.0.0.1:8848`为 Nacos Server 的地址。如果您的 Nacos Server 部署在另外一台机器，则需要修改成对应的地址。如果有其它需求，可以参考[配置项参考](#section_xbv_n1o_n1b)在`application.properties`文件中增加配置。

6.  查询应用服务。
    1.  执行`nacos-service-consumer` 中 `ConsumerApplication` 的 `main` 函数，启动应用。
    2.  登录本地启动的 Nacos Server 控制台 `http://127.0.0.1:8848/nacos`（本地 Nacos 控制台的默认用户名和密码同为 nacos），在左侧导航栏中选择**服务管理** \> **服务列表** ，可以看到服务列表中已经包含了`service-consumer`，且在详情中可以查询该服务的详情。

## 步骤四：查看调用结果 {#section_o4a_y7i_8uu .section}

在本地测试消费者对提供者的服务调用结果。启动服务，查看调用结果。

-   **Linux/Unix/Mac 系统**：执行`curl http://127.0.0.1:18082/echo-rest/rest-rest`和`curl http://127.0.0.1:18082/echo-feign/feign-rest`。
-   **Windows系统**：在浏览器中输入`http://127.0.0.1:18082/echo-rest/rest-rest`和`http://127.0.0.1:18082/echo-feign/feign-rest`。

## 步骤五：将应用部署到 SAE {#section_n29_frh_8uw .section}

在本地完成应用的开发和测试后，便可将应用打包并部署到 SAE。部署应用的详细步骤请参见[部署应用概述](https://help.aliyun.com/document_detail/113181.htm)。

**说明：** 

-   SAE 暂不支持创建空应用，故第一次部署需在控制台完成。
-   如果使用 JAR 包部署，在应用部署配置时选择**应用运行环境**为标准 Java 应用运行环境。
-   如果使用 WAR 包部署，在应用部署配置时**应用运行环境**为apache-tomcat-XXX。

当您将应用部署到 SAE 时，SAE 服务注册中心会以更高优先级去设置 Nacos Server 服务端地址和服务端口，以及 namespace、access-key、secret-key、context-path 信息。您无需进行任何额外的配置，原有的配置内容可以选择保留或删除。

## 结果验证 {#section_3xr_rzv_z0t .section}

1.  为[步骤五：将应用部署到 SAE](#section_n29_frh_8uw)中部署的消费者服务应用[绑定公网 SLB](https://help.aliyun.com/document_detail/113305.html)，在浏览器输入配置好的公网访问地址，进入应用首页。
2.  在应用首页发起调用请求，然后登录 SAE 控制台，进入消费者应用详情页面，在左侧导航栏选择**应用监控** \> **应用总览**，查看服务调用数据总览。

    当能够监测到调用数据则说明服务调用成功。


## 配置项参考 {#section_xbv_n1o_n1b .section}

|配置项|Key|默认值|说明|
|---|---|---|--|
|服务端地址|spring.cloud.nacos.discovery.server-addr|无|Nacos Server 启动监听的 IP 地址和端口。|
|服务名|spring.cloud.nacos.discovery.service|$\{spring.application.name\}|给当前的服务命名。|
|网卡名|spring.cloud.nacos.discovery.network-interface|无|当 IP 未配置时，注册的 IP 为此网卡所对应的 IP 地址。如果此项也未配置，则默认取第一块网卡的地址。|
|注册的 IP 地址|spring.cloud.nacos.discovery.ip|无|优先级最高。|
|注册的端口|spring.cloud.nacos.discovery.port|-1|默认情况下不用配置，系统会自动探测。|
|命名空间|spring.cloud.nacos.discovery.namespace|无|常用场景之一是不同环境的注册的区分隔离，例如开发测试环境和生产环境的资源（如配置、服务）隔离等。|
|Metadata|spring.cloud.nacos.discovery.metadata|无|使用 Map 格式配置，用户可以根据自己的需要自定义一些和服务相关的元数据信息。|
|集群|spring.cloud.nacos.discovery.cluster-name|DEFAULT|配置成 Nacos 集群名称。|
|接入点|spring.cloud.nacos.discovery.enpoint|UTF-8|地域的某个服务的入口域名，通过此域名可以动态地拿到服务端地址，此配置在部署到 SAE 时无需填写。|
|是否集成 Ribbon|ribbon.nacos.enabled|true|一般不需要修改。|

## 更多信息 {#section_cew_oka_iu3 .section}

-   更多关于 Spring Cloud Alibaba Nacos Discovery 的信息请参见：[Spring Cloud Alibaba Nacos Discovery](https://github.com/spring-cloud-incubator/spring-cloud-alibaba/wiki/Nacos-discovery)。
-   如果您在本地开发了依赖 Eureka、Consul、ZooKeeper 等组件实现的服务注册与发现的 Spring Cloud 应用，将该应用修改依赖配置并部署至 SAE 的相关操作请参见：[将 Spring Cloud 应用托管到 SAE](https://help.aliyun.com/document_detail/123013.html)。

