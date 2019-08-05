# 初次使用 Dubbo 构建微服务应用 {#concept_123020_zh .concept}

当您初次使用原生 Dubbo 构建微服务应用时，您需在本地完成添加依赖和配置管理等操作，然后将应用部署到 SAE，然后实现微服务应用的服务注册与发现，并查看服务调用关系。

## 背景信息 {#section_alp_qf8_86q .section}

如果您完全不了解 Dubbo，详细阅读本文后，您将了解如何通过 `sae-dubbo-extension` 实现 Dubbo 应用的服务注册与发现，以及实现消费者对提供者的服务调用。

SAE 目前支持的 Dubbo 版本为 2.5.3 到 2.7.0：

-   如果您使用的 Dubbo 版本为 2.5.3 ~ 2.6.x，对应的 `sae-dubbo-extension` 的版本为 1.0.6。
-   如果您使用的 Dubbo 版本为 2.7.0，对应的 `sae-dubbo-extension` 的版本改成 2.0.2。

SAE 服务注册中心实现了 Dubbo 所提供的 SPI 标准的[注册中心扩展](http://dubbo.apache.org/zh-cn/docs/dev/impls/registry.html)，能够完整地支持 Dubbo 服务注册、[路由规则](http://dubbo.apache.org/zh-cn/docs/user/demos/routing-rule.html)、[配置规则](http://dubbo.apache.org/zh-cn/docs/user/demos/config-rule.html)功能。

SAE 服务注册中心能够完全代替 ZooKeeper 和 Redis，作为您 Dubbo 服务的注册中心。同时，与 ZooKeeper 和 Redis 相比，还具有以下优势：

-   SAE 服务注册中心为共享组件，节省了您运维、部署 ZooKeeper 等组件的机器成本。
-   SAE 服务注册中心在通信过程中增加了鉴权加密功能，为您的服务注册链路进行了安全加固。
-   SAE 服务注册中心与 SAE 其他组件紧密结合，为您提供一整套的微服务解决方案。

## 准备工作 {#section_9ed_e3o_2h4 .section}

-   下载、启动并配置轻量级配置中心。

    为了便于本地开发，SAE 提供了包含 SAE 服务注册中心基本功能的轻量级配置中心。基于轻量级配置中心开发的应用无需修改任何代码和配置就可以部署到 SAE 中。

    请您参考[配置轻量级配置中心](https://help.aliyun.com/document_detail/44163.html)进行下载、启动及配置。推荐使用最新版本。

-   下载 Maven 并设置环境变量（如已安装可跳过）。

## 步骤一：获取 Demo {#section_1qv_xc9_nny .section}

[sae-dubbo-demo 下载](http://edas-public.oss-cn-hangzhou.aliyuncs.com/install_package/demo/edas-dubbo-demo.zip)

## 步骤二：创建服务提供者 {#section_ane_4lv_ck5 .section}

在本地创建一个提供者应用工程，添加依赖，配置服务注册与发现，并将注册中心指定为 SAE 轻量级配置中心。

1.  使用 IDE（如 IDEA 和 Eclipse）创建一个 Maven 工程。
2.  在 Maven 工程中的`pom.xml`文件中添加 **dubbo** 和 **sae-dubbo-extension** 依赖，版本分别为 2.6.2 和 1.0.6。

    ``` {#codeblock_aou_m8q_qj8 .language-xml}
        <dependencies>
             <dependency>
                 <groupId>com.alibaba</groupId>
                 <artifactId>dubbo</artifactId>
                 <version>2.6.2</version>
             </dependency>
    
             <dependency>
                 <groupId>com.alibaba.sae</groupId>
                 <artifactId>sae-dubbo-extension</artifactId>
                 <version>1.0.6</version>
             </dependency>
        </dependencies>
    					
    ```

3.  开发 Dubbo 服务提供者。

    Dubbo 中服务是以接口的形式提供。

    1.  在`src/main/java`路径下创建名为`com.alibaba.sae` package 。
    2.  在`com.alibaba.sae`下创建名为 `IHelloService`接口（interface） ，包含 `SayHello` 方法。

        ``` {#codeblock_sog_gop_4ab}
          package com.alibaba.sae;
        
          public interface IHelloService {
              String sayHello(String str);
          }
        							
        ```

    3.  在`com.alibaba.sae`下创建名为`IHelloServiceImpl`类，用来实现此接口。

        ``` {#codeblock_r59_gbc_tzy}
          package com.alibaba.sae;
        
          public class IHelloServiceImpl implements IHelloService {
              public String sayHello(String str) {
                  return "hello " + str;
              }
          }
        							
        ```

4.  配置 Dubbo 服务。

    1.  在 `src/main/resources`路径下创建 `provider.xml`文件并打开。
    2.  在`provider.xml`中，添加 Spring 相关的 XML NameSpace（xmlns） 和 XML Schema Instance（xmlns:xsi），以及 Dubbo 相关的 NameSpace（xmlns:dubbo） 和 Scheme Instance（xsi:schemaLocation）。

``` {#codeblock_fxz_y8m_98f}
  <beans xmlns="http://www.springframework.org/schema/beans"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
     xsi:schemaLocation="http://www.springframework.org/schema/beans
     http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
     http://code.alibabatech.com/schema/dubbo
     http://code.alibabatech.com/schema/dubbo/dubbo.xsd"> 
								
```

    3.  在 `provider.xml` 中将接口和实现类展现为 Dubbo 服务。

        ``` {#codeblock_3iq_i22_whr}
          <dubbo:application name="demo-provider"/>
        
          <dubbo:protocol name="dubbo" port="28082"/>
        
          <dubbo:service interface="com.alibaba.sae.IHelloService" ref="helloService"/>
        
          <bean id="helloService" class="com.alibaba.sae.IHelloServiceImpl"/>
        							
        ```

    4.  在 `provider.xml` 中将注册中心指定为 SAE 轻量级配置中心。

        其中 127.0.0.1 为轻量级配置中心的地址，如果您的轻量级配置中心部署在另外一台机器，则需要修改成对应的 IP 地址。由于轻量级配置中心不支持修改端口，所以端口必须使用 8080。

        ``` {#codeblock_s1z_9ox_abu}
          <dubbo:registry id="sae" address="sae://127.0.0.1:8080"/>
        							
        ```

5.  启动服务。
    1.  在 `com.alibaba.sae`中创建类 Provider，并按下面的代码在 Provider 的 main 函数中加载 Spring Context，将配置好的 Dubbo 服务展现。

        ``` {#codeblock_neo_20v_p4o .language-java}
        package com.alibaba.sae;
        
        import org.springframework.context.support.ClassPathXmlApplicationContext;
        
        public class Provider {
            public static void main(String[] args) throws Exception {
                ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext(new String[] {"provider.xml"});
                context.start();
                System.in.read();
            }
        }
        							
        ```

    2.  执行 Provider 的 main 函数，启动服务。
6.  登录轻量级配置中心控制台 `http://127.0.0.1:8080`，在左侧导航栏中单击**服务列表** ，查看提供者列表。在列表中可以看到服务提供者已经包含了 `com.alibaba.sae.IHelloService`，且可以查询该服务的**服务分组**和**提供者 IP**。

## 步骤三：创建服务消费者 {#section_3hc_hxc_jrw .section}

在本地创建一个消费者应用工程，添加依赖，添加订阅服务的配置。

1.  创建 Maven 项目并引入依赖。

    具体操作请参见[步骤二：创建服务提供者](#section_ane_4lv_ck5)的[步骤1](#)～[步骤2](#)。

2.  开发 Dubbo 服务。

    Dubbo 中服务是以接口的形式提供。

    1.  在`src/main/java`路径下创建名为`com.alibaba.sae`的package 。
    2.  在`com.alibaba.sae`下创建名为`IHelloService`接口（interface） ，其中包含了 `SayHello` 方法。

**说明：** 通常在单独的模块中定义接口供其他程序调用，服务提供者和服务消费者都通过 Maven 依赖来调用此模块。本文档从易操作和便于理解角度出发，服务提供者和服务消费者分别创建了两个完全相同的接口，现场实际开发过程中不推荐创建两个相同接口。

        ``` {#codeblock_umm_bn1_s96}
          package com.alibaba.sae;
        
          public interface IHelloService {
              String sayHello(String str);
          }
        							
        ```

3.  配置 Dubbo 服务。

    1.  在 `src/main/resources`路径下创建 `consumer.xml`文件并打开。
    2.  在`consumer.xml`中，添加 Spring 相关的 XML NameSpace（xmlns） 和 XML Schema Instance（xmlns:xsi），以及 Dubbo 相关的 NameSpace（xmlns:dubbo） 和 Scheme Instance（xsi:schemaLocation）。

        ``` {#codeblock_n2k_osn_n7w}
          <beans xmlns="http://www.springframework.org/schema/beans"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xmlns:dubbo="http://code.alibabatech.com/schema/dubbo"
             xsi:schemaLocation="http://www.springframework.org/schema/beans
             http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
             http://code.alibabatech.com/schema/dubbo
             http://code.alibabatech.com/schema/dubbo/dubbo.xsd"> 
        							
        ```

    3.  在 `consumer.xml` 中添加如下配置，订阅 Dubbo 服务。

        ``` {#codeblock_mec_75v_fxn}
          <dubbo:application name="demo-consumer"/>
        
          <dubbo:registry id="sae" address="sae://127.0.0.1:8080"/>
        
          <dubbo:reference id="helloService" interface="com.alibaba.sae.IHelloService"/>
        							
        ```

4.  启动、验证服务。

    1.  在`com.alibaba.sae`下创建类 Consumer，并按下面的代码在 Consumer 的 main 函数中加载 Spring Context，订阅并消费 Dubbo 服务。

        ``` {#codeblock_si9_s7n_qhs .language-java}
            package com.alibaba.sae;
        
            import org.springframework.context.support.ClassPathXmlApplicationContext;
        
            import java.util.concurrent.TimeUnit;
        
            public class Consumer {
                public static void main(String[] args) throws Exception {
                    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext(new String[] {"consumer.xml"});
                    context.start();
                    while (true) {
                        try {
                            TimeUnit.SECONDS.sleep(5);
                            IHelloService demoService = (IHelloService)context.getBean("helloService");
                            String result = demoService.sayHello("world");
                            System.out.println(result);
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        							
        ```

    2.  执行 Consumer 的 main 函数，启动服务。
5.  验证创建结果。
    1.  启动后，控制台不断地输出 `hello world`，表示服务消费成功。
    2.  登录轻量级配置中心控制台 `http://127.0.0.1:8080`，在左侧导航栏中选择**服务列表** \> **调用者列表**，在调用者列表显示 `com.alibaba.sae.IHelloService`，且可以查看该服务的**服务分组**和**调用者 IP**。

## 步骤四：部署到 SAE {#section_k16_bpf_t6x .section}

1.  分别在 Provider 和 Consumer 的 pom.xml 文件中添加如下配置，然后执行 mvn clean package 将本地的程序打成可执行的 JAR 包。

    -   Provider

        ``` {#codeblock_09v_8u5_mja .language-xml}
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
                           <configuration>
                               <classifier>spring-boot</classifier>
                               <mainClass>com.alibaba.sae.Provider</mainClass>
                           </configuration>
                       </execution>
                   </executions>
               </plugin>
         </plugins>
        </build>
        							
        ```

    -   Consumer

        ``` {#codeblock_ev0_3m4_59d .language-xml}
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
                           <configuration>
                               <classifier>spring-boot</classifier>
                               <mainClass>com.alibaba.sae.Consumer</mainClass>
                           </configuration>
                       </execution>
                   </executions>
               </plugin>
         </plugins>
        </build>
        							
        ```

2.  参考[部署微服务应用到 SAE](https://help.aliyun.com/document_detail/97761.html)部署应用。

## 更多信息 {#section_3oq_e3j_von .section}

您还可以[使用 Spring Boot 开发 Dubbo 应用](https://help.aliyun.com/document_detail/97761.html)。

