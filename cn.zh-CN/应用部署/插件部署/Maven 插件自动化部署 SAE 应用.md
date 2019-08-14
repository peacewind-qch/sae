# Maven 插件自动化部署 SAE 应用 {#concept_110639_zh .concept}

SAE 应用除通过控制台方式进行应用部署，还可使用应用开发工具进行部署。本节介绍如何通过 Maven 的 toolkit-maven-plugin 插件进行自动化部署。此方式适用于有应用开发经验用户。

## 自动化部署 {#section_hyw_lyq_yrn .section}

通过 toolkit-maven-plugin 插件自动化部署应用的流程：添加插件依赖，配置插件，构建部署。

1.  添加插件依赖。

    在 pom.xml 文件中增加如下所示的插件依赖。

    ``` {#codeblock_eys_2az_iy3 .language-xml}
    <build>
        <plugins>
            <plugin>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>toolkit-maven-plugin</artifactId>
                <version>1.0.2</version>
            </plugin>
        </plugins>
    </build>
    							
    ```

2.  配置插件

    配置插件主要包含账号配置，打包配置及部署配置。如果需要更多自定义配置项可参考[打包参数](#)和[部署参数](#)进行设置。

    1.  账号配置

        在打包工程的根目录下创建文件格式为 `YAML` 的账号配置文件，命名为`toolkit_profile.yaml`并填入如下信息：

        ``` {#codeblock_zug_ow2_oxf .language-yaml}
        regionId:        #应用所在区域，如北京为`cn-beijing`，上海为`cn-shanghai`，杭州为`cn-hangzhou`。
        accessKeyId:     #访问阿里云资源的AK
        accessKeySecret: #访问阿里云资源的SK
        									
        ```

    2.  打包配置

        在打包工程的根目录下创建文件格式为 `YAML` 的打包配置文件。如果打包工程为 Maven 的子模块，则需要在子模块的目录下创建该文件，并命名为`toolkit_package.yaml`，填入如下信息：

        ``` {#codeblock_6h8_95a_oy0 .language-yaml}
        apiVersion: V1
        kind: AppPackage
        spec:
        packageType: #应用部署包类型，支持War、FatJar、Image三种格式。
        packageUrl:  #如果应用部署包类型为War或FatJar，可填入此字段，不填则使用当前maven构建的包进行部署。
        imageUrl:    #如果部署包类型为Image，可填入此字段；Image类型也可以在本地构建Docker镜像进行部署，请参考打包文件参数章节设置相关参数。
        									
        ```

    3.  部署配置

        在打包工程的根目录下创建文件格式为 `YAML` 的部署文件，命名为`toolkit_deploy.yaml`，并填入如下信息：

        ``` {#codeblock_zgx_ww4_cqx .language-yaml}
        apiVersion: V1
        kind: AppDeployment
        spec:
        type: serverless
        target:
         appId:        #部署应用的ID，如果配置了appId则无需配置namespaceId和appName
         namespaceId:  #命名空间，如不清楚appId，可使用此命名空间及应用名称进行部署
         appName:      #应用名称，如不清楚appId，可使用此应用名称及命名空间进行部署
        									
        ```

3.  构建部署

    进入`pom.xml`所在的目录（如果部署 Maven 子模块，则进入子模块`pom.xml`所在的目录），执行如下命令：

    ``` {#codeblock_jey_pkp_4if .language-shell}
    mvn clean package toolkit:deploy -Dtoolkit_profile=toolkit_profile.yaml -Dtoolkit_package=toolkit_package.yaml -Dtoolkit_deploy=toolkit_deploy.yaml
    							
    ```

    命令参数含义为：

    -   `toolkit:deploy`：在打包完成后进行应用部署。
    -   `-Dtoolkit_profile`：指定账号配置文件。如果账号文件跟 `pom.xml` 在同一个目录下，且名字为`.toolkit_profile.yaml`（注意：文件名最前面有个小数点），可不填此参数，插件会自动获取。
    -   `-Dtoolkit_package`: 指定打包文件。如果打包文件跟 `pom.xml` 在同一个目录下，且名字为`.toolkit_package.yaml`（注意：文件名最前面有个小数点），可不填此参数，插件会自动获取。
    -   `-Dtoolkit_deploy`: 指定部署文件。如果部署文件跟 `pom.xml` 在同一个目录下，且名字为`.toolkit_deploy.yaml`（注意：文件名最前面有个小数点），可不填此参数，插件会自动获取取。
    执行该打包命令后，系统显示如下结果，当回显信息中显示“BUDILD SUCCESS”表示部署成功。

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/110639/cn_zh/1552453792195/1537957243390-51f79f1a-b03f-4d7e-b0bb-4fa242ceb003.jpeg)


## 更多配置项 {#section_cr2_4vo_awr .section}

1.  打包参数

    打包文件支持的参数如下所示：

    ``` {#codeblock_cdu_63g_szj .language-yaml}
    apiVersion: V1
    kind: AppPackage
    spec:
      packageType:  #应用部署包类型，支持War、FatJar、Image。
      imageUrl:     #镜像地址，Image包类型应用可填入。
      packageUrl:   #包地址，War、FatJar类型应用可填入。
      build:
        docker:
           dockerfile:        #Docker镜像构建文件。如您希望在本地构建镜像部署，需填入此字段。
           imageRepoAddress:  #阿里云镜像仓库地址。如您希望在本地构建镜像部署，需填入此字段。
           imageTag:          #镜像Tag。如您希望在本地构建镜像部署，需填入此字段。
           imageRepoUser:     #阿里云镜像仓库用户名。如您希望在本地构建镜像部署，需填入此字段。
           imageRepoPassword: #阿里云镜像仓库密码。如您希望在本地构建镜像部署，需填入此字段。
        oss:
           bucket:      #目标存储桶名称。如您希望使用自定义的oss仓库存储部署包，需填入此字段。
           key:         #oss自定义路径。如您希望使用自定义的oss仓库存储部署包，需填入此字段。
           accessKeyId: #oss账号。如您希望使用自定义的oss仓库存储包，需填入此字段。
           accessKeySecret: #oss密码。如您希望使用自定义的oss仓库存储包，可填入此字段。
    						
    ```

2.  部署参数

    部署文件支持的参数如下所示：

    ``` {#codeblock_0f0_0iy_rah .language-yaml}
    apiVersion: V1
    kind: AppDeployment
    spec:
      type: serverless
      target:
        appName:     #应用名称
        namespaceId: #应用所在命名空间
        appId:       #应用ID。插件会使用此应用进行部署，如未填入则使用namespaceId和appName来查找应用进行部署。
      version: #部署版本号，默认使用日时分秒格式
      jdk:     #部署的包依赖的 JDK 版本，JDK 支持版本为 Open JDK 7 和 Open JDK 8。镜像不支持。
      webContainer:  #部署的包依赖的 Tomcat 版本，WebContainer 支持 apache-tomcat-7.0.91。镜像不支持。
      batchWaitTime: #分批等待时间。
      command:       #镜像启动命令。该命令必须为容器内存在的可执行的对象。例如: sleep。设置该命令将导致镜像原本的启动命令失效。
      commandArgs: #镜像启动命令参数。上述启动命令所需参数。
        - 1d
      envs:    #容器环境变量参数
        - name: envtmp0
          value: '0'
        - name: envtmp1
          value: '1'
      customHostAlias:  #容器内自定义host映射
        - hostName: 'samplehost1'
          ip: '127.0.0.1'
        - hostName: 'samplehost2'
          ip: '127.0.0.1'
      jarStartOptions:  #Jar包启动应用选项
      jarStartArgs:     #Jar包启动应用参数
      liveness:   #容器健康检查，健康检查失败的容器将被杀死并恢复。
        exec:
          command:
            - sleep
            - 1s
        initialDelaySeconds: 5
        timeoutSeconds: 11
      readiness:  #应用启动状态检查，多次健康检查失败的容器将被杀死并重启。不通过健康检查的容器将不会有 SLB 流量进入。
        exec:
          command:
            - sleep
            - 1s
        initialDelaySeconds: 5
        timeoutSeconds: 11
      minReadyInstances: 1  #最小存活实例数。在滚动升级过程中或者滚动升级失败，可用实例数都将尽可能不小于该值，为 0 则不限制。弹性扩缩容的范围不应该小于该值，否则将触发异常。
    						
    ```


## 典型场景示例 {#section_iym_867_g0l .section}

典型部署场景及相关配置示例。

-   场景一：本地构建War（或FatJar）包进行部署

    假设您在北京环境有 WAR（或 FatJar）类型的 SAE 应用，期望本地构建 WAR（或 FatJar）进行部署。打包配置和部署配置如下所示。

    -   打包文件：

        ``` {#codeblock_go7_qrn_70q .language-yaml}
        apiVersion: V1
        kind: AppPackage
        spec:
          packageType: War
        									
        ```

    -   部署文件：

        ``` {#codeblock_4t9_urs_vvq .language-yaml}
        apiVersion: V1
        kind: AppDeployment
        spec:
          type: serverless
          target:
            appId:  #应用ID。插件会使用此应用进行部署，如未填入则使用namespaceId和appName来查找应用进行部署。
            namespaceId:  #【可选】命名空间，如不清楚appId，可使用此命名空间及应用名称进行部署
            appName:      #【可选】应用名称，如不清楚appId，可使用此命名空间及应用名称进行部署
        									
        ```

-   场景二：使用已有镜像地址部署镜像类型应用

    假设您在北京环境有一个镜像类型应用，期望使用已有的镜像（registry.cn-beijing.aliyuncs.com/test/gateway:latest ）部署应用。打包配置和部署配置如下所示。

    -   打包文件：

        ``` {#codeblock_2n3_6tj_yo1 .language-yaml}
        apiVersion: V1
        kind: AppPackage
        spec:
          packageType: Image
          imageUrl: registry.cn-beijing.aliyuncs.com/test/gateway:latest
        									
        ```

    -   部署文件：

        ``` {#codeblock_zjv_fhs_2jq .language-yaml}
        apiVersion: V1
        kind: AppDeployment
        spec:
          type: serverless
          target:
            appId:  #应用ID。插件会使用此应用进行部署，如未填入则使用namespaceId和appName来查找应用进行部署。
            namespaceId:  #【可选】命名空间，如不清楚appId，可使用此命名空间及应用名称进行部署
            appName:      #【可选】应用名称，如不清楚appId，可使用此命名空间及应用名称进行部署
        									
        ```

-   场景三：本地构建镜像上传至仓库并部署应用

    假设您在北京环境有镜像类型应用，期望在本地编译并构建为镜像，并上传到阿里云镜像仓库进行部署，打包配置和部署配置如下所示。

    -   打包文件：

        ``` {#codeblock_6bm_rj8_rog .language-yaml}
        apiVersion: V1
        kind: AppPackage
        spec:
          packageType: Image
          build:
            docker:
               dockerfile: Dockerfile #指定Dockerfile
               imageRepoAddress:      #镜像仓库地址
               imageTag:              #镜像Tag
               imageRepoUser:         #镜像仓库用户名
               imageRepoPassword:     #镜像仓库密码
        									
        ```

    -   部署文件：

        ``` {#codeblock_zyc_qlw_akm .language-yaml}
        apiVersion: V1
        kind: AppDeployment
        spec:
          type: serverless
          target:
            appId:  #应用ID。插件会使用此应用进行部署，如未填入则使用namespaceId和appName来查找应用进行部署。
            namespaceId:  #【可选】命名空间，如不清楚appId，可使用此命名空间及应用名称进行部署
            appName:      #【可选】应用名称，如不清楚appId，可使用此命名空间及应用名称进行部署
        									
        ```


