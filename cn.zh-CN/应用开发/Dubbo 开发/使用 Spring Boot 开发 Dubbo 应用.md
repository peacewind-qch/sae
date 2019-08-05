# 使用 Spring Boot 开发 Dubbo 应用 {#concept_122997_zh .task}

如果您只有简单的 Java 基础和 Maven 经验，而不熟悉 Dubbo，您可以从零开始开发 Dubbo 服务，并使用 SAE 服务注册中心实现服务注册与发现。

-   下载、启动及配置轻量级配置中心。

    为了便于本地开发，SAE 提供了含有 SAE 服务注册中心基本功能的轻量级配置中心。基于轻量级配置中心开发的应用无需修改任何代码和配置就可以部署到云端的 SAE 中。

    请您参考 [配置轻量级配置中心](https://help.aliyun.com/document_detail/44163.html) 进行下载、启动及配置。推荐使用最新版本。

-   下载 [Maven](http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz) 并设置环境变量（本地已安装的可略过）。

SAE 服务注册中心实现了 Dubbo 所提供的 SPI 标准的[注册中心扩展](http://dubbo.apache.org/zh-cn/docs/dev/impls/registry.html)，能够完整地支持 Dubbo 服务注册、[路由规则](http://dubbo.apache.org/zh-cn/docs/user/demos/routing-rule.html)、[配置规则功能](http://dubbo.apache.org/zh-cn/docs/user/demos/config-rule.html)。

SAE 服务注册中心能够完全代替 ZooKeeper 和 Redis，作为您 Dubbo 服务的注册中心。同时，与 ZooKeeper 和 Redis 相比，还具有以下优势：

-   SAE 服务注册中心为共享组件，节省了您运维、部署 ZooKeeper 等组件的机器成本。
-   SAE 服务注册中心在通信过程中增加了鉴权加密功能，为您的服务注册链路进行了安全加固。
-   SAE 服务注册中心与 SAE 其他组件紧密结合，为您提供一整套的微服务解决方案。

全新场景使用 Spring Boot 开发 Dubbo 应用有两种主要的方式：

-   使用 xml 开发
-   使用 Spring Boot 的注解方式开发

使用 xml 方式请参考 [将 Dubbo 应用托管到 SAE](https://help.aliyun.com/document_detail/97471.html)。文本档介绍如何使用 Spring Boot 的注解方式开发 Dubbo 服务。

Spring Boot 使用极简的配置能够快速搭建基于 Spring 的 Dubbo 服务，相比 xml 的开发方式，开发效率更高。

## 步骤1：创建服务提供者 {#section_tqn_dbd_a2v .section}

1.  创建名为`spring-boot-dubbo-provider` Maven 工程，命。
2.  在`pom.xml`文件中添加所需的依赖。 

    这里本文以 Spring Boot 2.0.6.RELEASE 为例。

    ``` {#codeblock_5un_bpl_z5y .language-xml}
        <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.0.6.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba.boot</groupId>
            <artifactId>dubbo-spring-boot-starter</artifactId>
            <version>0.2.0</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba.edas</groupId>
            <artifactId>edas-dubbo-extension</artifactId>
            <version>1.0.6</version>
        </dependency>
    
    </dependencies>
    						
    ```

    如果您需要选择使用 Spring Boot 1.x 的版本，请使用 Spring Boot 1.5.x 版本，对应的 com.alibaba.boot:dubbo-spring-boot-starter 版本为 0.1.0。

    **说明：** Spring Boot 1.x 版本的生命周期即将在 2019 年 8 月 结束，推荐使用新版本开发您的应用。

3.  开发 Dubbo 服务提供者。 Dubbo 中服务都是以接口的形式提供的。
    1.  在`src/main/java`路径下创建 package `com.alibaba.sae.boot`。
    2.  在`com.alibaba.sae.boot`下创建名为`IHelloService` 接口（interface） ，其中包含了 `SayHello` 方法。 

        ``` {#codeblock_wl6_5eg_0gv .language-java}
        package com.alibaba.sae.boot;
        public interface IHelloService {
        String sayHello(String str);
        }
        								
        ```

    3.  在`com.alibaba.sae.boot`下创建名为`IHelloServiceImpl`类，实现此接口。 

        ``` {#codeblock_p2o_g7g_436 .language-java}
        package com.alibaba.sae.boot;
        import com.alibaba.dubbo.config.annotation.Service;
        @Service
        public class IHelloServiceImpl implements IHelloService {
        public String sayHello(String name) {
          return "Hello, " + name + " (from Dubbo with Spring Boot)";
         }
        }
        								
        ```

        **说明：** 这里的 Service 注解是 Dubbo 提供的一个注解类，类的全名称为：**com.alibaba.dubbo.config.annotation.Service** 。

4.  配置 Dubbo 服务 
    1.  在 `src/main/resources`路径下创建`application.properties`或`application.yaml`文件，并将其打开。
    2.  在`application.properties`或`application.yaml`中添加如下配置。 

        ``` {#codeblock_fsk_kdz_s5p .language-properties}
        # Base packages to scan Dubbo Components (e.g @Service , @Reference)
        dubbo.scan.basePackages=com.alibaba.sae.boot
        dubbo.application.name=dubbo-provider-demo
        dubbo.registry.address=edas://127.0.0.1:8080
        								
        ```

        **说明：** 

        -   以上三个配置没有默认值，必须要给出具体的配置。
        -   `dubbo.scan.basePackages`的值为开发代码中含有`com.alibaba.dubbo.config.annotation.Service`和`com.alibaba.dubbo.config.annotation.Reference`注解所在的包。多个包之间用逗号隔开。
        -   `dubbo.registry.address`的值前缀必须以 edas:// 开头，后面的 IP 地址和端口是轻量版配置中心。
5.  开发并启动 Spring Boot 入口类`DubboProvider`。 

    ``` {#codeblock_wng_8gy_oyg .language-java}
        package com.alibaba.sae.boot;
    
        import org.springframework.boot.SpringApplication;
        import org.springframework.boot.autoconfigure.SpringBootApplication;
    
        @SpringBootApplication
        public class DubboProvider {
    
            public static void main(String[] args) {
    
                SpringApplication.run(DubboProvider.class, args);
            }
    
        }
    						
    ```

6.  登录[轻量版配置中心控制台](http://127.0.0.1:8080)，在左侧导航栏中单击**服务列表**，查看提供者列表。 可以看到服务提供者里已经包含了`com.alibaba.sae.boot.IHelloService`，且可以查询该服务的服务分组和提供者 IP。

## 步骤2：创建服务消费者 {#section_uoo_50c_564 .section}

1.  创建名为`spring-boot-dubbo-consumer` Maven 工程。
2.  在`pom.xml`文件中添加相关依赖。 

    本文以 Spring Boot 2.0.6.RELEASE 为例。

    ``` {#codeblock_q5x_mra_qdo .language-xml}
        <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.0.6.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba.boot</groupId>
            <artifactId>dubbo-spring-boot-starter</artifactId>
            <version>0.2.0</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba.edas</groupId>
            <artifactId>edas-dubbo-extension</artifactId>
            <version>1.0.6</version>
        </dependency>
    
    </dependencies>
    						
    ```

    如果您需要选择使用 Spring Boot 1.x 的版本，请使用 Spring Boot 1.5.x 版本，对应的 com.alibaba.boot:dubbo-spring-boot-starter 版本为 0.1.0。

    **说明：** Spring Boot 1.x 版本的生命周期即将在 2019 年 8 月 结束，推荐使用新版本开发您的应用。

3.  开发 Dubbo 消费者 
    1.  在`src/main/java`路径下创建 package `com.alibaba.sae.boot`。
    2.  在`com.alibaba.sae.boot`下创建名为`IHelloService`接口（interface） ，里面包含了 `SayHello` 方法。 

        ``` {#codeblock_oew_8ok_sl3 .language-java}
        package com.alibaba.sae.boot;
        
        public interface IHelloService {
         String sayHello(String str);
        }
        								
        ```

4.  开发 Dubbo 服务调用。 

    例如需要在 Controller 中调用一次远程 Dubbo 服务，开发的代码如下所示。

    ``` {#codeblock_rz3_p5w_9jo .language-java}
    package com.alibaba.sae.boot;
    
    import com.alibaba.dubbo.config.annotation.Reference;
    import org.springframework.web.bind.annotation.PathVariable;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    
    @RestController
        public class DemoConsumerController {
    
            @Reference
            private IHelloService demoService;
    
            @RequestMapping("/sayHello/{name}")
            public String sayHello(@PathVariable String name) {
                return demoService.sayHello(name);
            }
        }
    							
    ```

    **说明：** 这里的 Reference 注解是 com.alibaba.dubbo.config.annotation.Reference 。

5.  在`application.properties/application.yaml`配置文件中新增以下配置： 

    ``` {#codeblock_l7s_f2b_pb0 .language-properties}
    dubbo.application.name=dubbo-consumer-demo
    dubbo.registry.address=edas://127.0.0.1:8080
    						
    ```

    **说明：** 

    -   以上两个配置没有默认值，必须要给出具体的配置。
    -   `dubbo.registry.address`的值前缀必须是以 edas:// 开头，后面的 IP 地址和端口是轻量版配置中心。
6.  开发并启动 Spring Boot 入口类`DubboConsumer`。 

    ``` {#codeblock_b6c_4li_y1g .language-java}
    package com.alibaba.sae.boot;
    
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    
    @SpringBootApplication
    public class DubboConsumer {
    
        public static void main(String[] args) {
    
            SpringApplication.run(DubboConsumer.class, args);
        }
    
    }
    						
    ```

7.  登录[轻量版配置中心控制台](http://127.0.0.1:8080)，在左侧导航栏中单击**服务列表**，再在服务列表页面选择**调用者列表** ，查看调用者列表。 可以看到包含了`com.alibaba.sae.boot.IHelloService`，且可以查看该服务的服务分组和调用者 IP。

## 步骤3：结果验证 {#section_6cw_737_6na .section}

-   本地验证。

    `curl http://localhost:17080/sayHello/SAE`

    `Hello, SAE (from Dubbo with Spring Boot)`

-   在 SAE 中验证。

    `curl http://localhost:8080/sayHello/SAE`

    `Hello, SAE (from Dubbo with Spring Boot)`


## 步骤4：部署到 SAE {#section_bg4_wxr_up5 .section}

1.  分别在`DubboProvider`和`DubboConsumer`的`pom.xml`文件中添加如下配置，然后执行 mvn clean package 将本地的程序打成可执行的 JAR 包。 

    ``` {#codeblock_dbu_e7c_zjt .language-xml}
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

2.  根据您要部署的集群类型，参考[应用部署概述](https://help.aliyun.com/document_detail/113181.html)部署应用。

