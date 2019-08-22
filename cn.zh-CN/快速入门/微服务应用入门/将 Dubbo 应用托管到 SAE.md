# 将 Dubbo 应用托管到 SAE {#task_1426493 .task}

如果需要将一个原生 Dubbo 应用托管到 SAE，只需在本地应用程序中修改服务注册与发现组件的依赖和服务注册中心配置，无需修改任何代码，可将原生 Dubbo 应用部署到 SAE，实现服务注册、发现及调用。

-   参考[配置轻量级配置中心](https://help.aliyun.com/document_detail/44163.html)下载轻量配置中心将其启动并进行host配置。

    **说明：** 为了便于本地开发，SAE 提供了一个包含了 SAE 服务注册中心基本功能的轻量级配置中心。基于轻量级配置中心开发的应用无需修改任何代码和配置就可以部署到云端的 SAE 中。推荐使用最新版本。

-   匹配相应的Dubbo 版本。

    SAE 目前支持的 Dubbo 版本为 2.5.3~2.7.0。

    -   如果您使用的 Dubbo 版本为 2.5.3~2.6.x，对应的 edas-dubbo-extension 的版本为 1.0.6。
    -   如果您使用的 Dubbo 版本为 2.7.0，对应的 edas-dubbo-extension 的版本为 2.0.2。

## 操作步骤 {#section_vwv_u7o_gmg .section}

1.  本地开发 Dubbo 应用使用的注册中心为 ZooKeeper，在本地开发时需要将依赖由 ZooKeeper 替换为 SAE 注册中心，并在配置文件中将 ZooKeeper 的配置修改为 SAE 注册中心。
    1.  修改依赖和配置 
        1.  在应用程序的`pom.xml`文件中将注册中心的依赖由 ZooKeeper 修改为 SAE 注册中心。

            原生 Dubbo 应用中的注册中心为 ZooKeeper，依赖如下：

            ``` {#codeblock_kc0_quh_228}
            <dependency>
                    <groupId>org.apache.dubbo</groupId>
                    <artifactId>dubbo-dependencies-zookeeper</artifactId>
                    <version>${dubbo.version}</version>
                    <type>pom</type>
            </dependency>
            ```

            需要修改为 SAE 注册中心。

            ``` {#codeblock_7dc_6za_k70 .language-xml}
            <dependency>
                    <groupId>com.alibaba.edas</groupId>
                    <artifactId>edas-dubbo-extension</artifactId>
                    <version>2.0.1</version>
            </dependency>
            											
            ```

        2.  在`src/main/resources`路径下的配置文件（如application.properties）中将 ZooKeeper 的配置修改为 SAE 注册中心。

            之前的配置为 ZooKeeper 的地址：

            `dubbo.registry.address = zookeeper://127.0.0.1:2181`

            修改为 SAE 注册中心的地址：

            `dubbo.registry.address = edas://127.0.0.1:2181`

2.  本地验证 
    1.  启动应用。
    2.  在本地打开浏览器，访问本地轻量配置中心控制台（http://127.0.0.1:8080）。
    3.  在左侧导航栏单击**服务列表**，在服务列表页面的**提供者列表**和**调用者列表**中分别查看是否存在 Provider 和 Consumer 应用。
    4.  依据应用的业务逻辑，检查应用的注册中心由 ZooKeeper 替换为 SAE 注册中心后，其服务是否能够调用成功。
3.  将应用部署到 SAE 
    1.  在应用的`pom.xml`文件中添加如下配置，然后执行 mvn clean package 将本地的程序打成可执行的 JAR 包。 

        ``` {#codeblock_4dk_xnv_x29}
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

