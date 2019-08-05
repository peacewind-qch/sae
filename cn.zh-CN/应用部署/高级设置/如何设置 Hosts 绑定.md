# 如何设置 Hosts 绑定 {#concept_100335_zh .concept}

SAE 应用在创建、部署时均可设置 Hosts 绑定。通过向实例的 etc/hosts 文件中添加条目，做到在应用实例级别覆盖对主机名的解析。Hosts 绑定设置可以在 SAE 应用实例创建或者重新部署后生效。

示例一：使用 ECS 的时候，Eureka 服务器的地址使用本地 Host 解析成域名 discovery1 和 discovery2 。当您使用 SAE 以后，您可直接在应用创建和应用部署页面修改本地 Host。

示例二：您可以在 hosts 文件添加额外的条目，例如将 foo.local、bar.local 解析为 127.0.0.1，将 foo.remote、 bar.remote 解析为 10.1.2.3。

## 操作步骤 {#section_w5v_k7o_e73 .section}

1.  登录 [SAE 控制台](https://sae.console.aliyun.com)。
2.  在左侧导航栏单击**应用列表**，在应用列表页面右上角单击**创建应用**。
3.  绑定 Hosts。

    -   **新创建应用**：在应用基本信息页签内，设置新建应用相关信息，然后单击**下一步：应用部署配置**。在应用部署配置页面，您可以展开 **Hosts 绑定设置**页签并输入 Hosts 配置项。

    -   **已创建应用**：在控制台左侧导航栏单击**应用列表**，在应用列表内选择您需添加或者更新 Hosts 的应用，在应用详情页右上角单击**部署应用**，在部署应用页面您可以新增或者更改 Hosts 配置。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/serverless-HOSTS-BINGING.png)

4.  应用创建或者重新部署完成后，您的 Hosts 配置即可生效，您就可以通过域名访问应用了。

