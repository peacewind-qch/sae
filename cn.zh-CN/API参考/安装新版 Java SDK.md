# 安装新版 Java SDK {#concept_34917_zh .concept}

相较于旧版 Java SDK 直接开放下载，阿里云新版 Java SDK 采用了 Maven 的方式分发。为方便统一管理，阿里云所有的 Java SDK 均统一在同一个 Maven 项目中。

## 下载 Maven 软件 {#section_34m_tu8_y4j .section}

访问 [Maven 官方下载页面](http://maven.apache.org/download.cgi) 下载对应操作系统的 Maven 软件。Checksum 文件可供您校验下载文件是否正确无误。以下截图来自于 Windows 7 64 位操作系统，使用环境是 Eclipse Luna。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/156456103313402_zh-CN.png)

## 安装 Java SDK {#section_dg4_vvm_2gb .section}

1.  打开 [Java SDK 下载页面](http://develop.aliyun.com/sdk/java)，将阿里云的 SDK 存放的 Maven 库加入到 Maven 软件中。
2.  找到之前下载的 Maven 压缩包并解压，将下列 Maven 库信息添加到 conf 文件夹下的 settings.xml 文件中。

    ``` {#codeblock_41m_d2y_puk}
    <repositories>
        <repository>
            <id>sonatype-nexus-staging</id>
            <name>Sonatype Nexus Staging</name>
            <url>https://oss.sonatype.org/service/local/staging/deploy/maven2/</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
            <snapshots>
        </repository>
    </repositories>
    ```

3.  通过以下任一方式创建 Maven 项目：

-   方式一：在 Eclipse 添加一个 Maven 项目。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/156456103413404_zh-CN.png)

-   方式二：将已有的项目转换为 Maven 项目。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10054/156456103413405_zh-CN.jpg)

4.  打开 Maven 项目下的 pom.xml 文件，将 dependency 加入 Maven 项目中。您可以根据自身需要添加不同的依赖。

    **说明：** aliyun-java-sdk-core需设置为4.3.2版本。

    ``` {#codeblock_oem_1g0_59j}
    <dependencies>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-core</artifactId>
            <version>4.3.2</version>
        </dependency>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-sae</artifactId>
            <version>1.0.0</version>
        </dependency>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-yundun</artifactId>
            <version>2.1.3</version>
        </dependency>
        <dependency>
            <groupId>com.aliyun</groupId>
            <artifactId>aliyun-java-sdk-slb</artifactId>
            <version>2.0.0-rc1</version>
        </dependency>
    </dependencies>
    ```

5.  保存更改。Maven Dependencies 中会自动下载并加入 .jar 后缀的相应阿里云 SDK。

## 区分旧版 SDK 与新版 SDK {#section_mh1_q51_bgm .section}

若您使用的是旧版 SDK，建议您切换为新版 SDK，获取最新功能。通过下表中的 SDK 参数，可以识别 SDK 版本。

|对比项|旧版 SDK|新版 SDK|
|:--|:-----|:-----|
|如何提交请求|execute\(\)|getAcsResponse\(\)|
|如何存放 AccessKey 和 AccessKeySecret 的类|AliyunClient|IClientProfile|
|如何存放凭据对象|new DefaultAliyunClient\(APIUrl, Access Key, Access Key Secret\)|DefaultProfile.getProfile\(RegionId, Access Key, Access Key Secret\)|
|包名前缀|com.aliyun.api|com.aliyuncs|

