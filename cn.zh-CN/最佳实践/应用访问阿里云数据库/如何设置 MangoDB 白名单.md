# 如何设置 MangoDB 白名单 {#task_1426493 .task}

创建 SAE 应用之后，如果你需要访问 MangoDB 数据库，需要设置 MangoDB 白名单。

不同场景下，白名单设置的内容不同。本文我们将从以下两个场景来分别说明白名单设置的相关操作。

-   [场景一：应用访问本 VPC 内的 MangoDB 数据库](#section_vwv_u7o_gmg)
-   [场景二：应用跨 VPC 或跨 Region 访问 MangoDB 数据库](#section_c5x_y9m_a4m)

## 场景一：应用访问本 VPC 内的 MangoDB 数据库 {#section_vwv_u7o_gmg .section}

1.  登录 [MangoDB 管理控制台](https://mongodb.console.aliyun.com/)。
2.  在控制台页面左上角，选择实例所在地域。 

    **说明：** 目前 SAE 现已开放了**华北 2 （北京）**、**华东 1 （杭州）**、**华东 2 （上海）**和**华南 1 （深圳）**地域。

3.  在左侧导航栏单击**副本集实例列表**或**分片集群实例列表**，找到目标实例，单击实例名称。
4.  在实例基本信息页面的左侧导航栏中，选择**数据安全性** \> **白名单设置**
5.  在 **default** 分组右侧的**操作**列选择**手动修改**。 

    ![mangodb白名单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067698/156773736953799_zh-CN.png)

6.  在弹出的对话框中，将 SAE 应用所在的 VPC 网络的网段地址配置在白名单输入框中。 
    1.  登录 [VPC 控制台](https://vpc.console.aliyun.com/)，在专有网络列表中找到应用所在的 VPC，单击该 VPC 的名称进入专有网络详情页面。
    2.  复制应用所在的 VPC 的 IPv4 网段。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067696/156773736953768_zh-CN.png)

    3.  在**允许访问IP名单**设置框中粘贴该 VPC 的 IPv4 网段地址，然后单击**确定**。 

        ![mangodb修改白名单/手动修改](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067698/156773736953801_zh-CN.png)

7.  在完成以上设置后，您的 SAE 应用就能访问本 VPC 内的 MangoDB 数据库了。

## 场景二：应用跨 VPC 或跨 Region 访问 MangoDB 数据库 {#section_c5x_y9m_a4m .section}

不同 VPC 和不同 Region 之间逻辑上完全隔离，故常规情况下不能跨 VPC 和跨 Region 访问 MangoDB 数据库。若您的应用想跨 VPC 或跨 Region 访问 MangoDB 数据库，请按照下面步骤进行相关配置。

1.  前提准备
2.  参考 [SAE 应用如何访问公网](https://help.aliyun.com/document_detail/100317.html)购买NAT 网关和弹性公网 IP 组合包并保证 SAE 应用可以访问公网。

1.  设置白名单
2.  参考[场景一：应用访问本 VPC 内的 MangoDB 数据库](#section_vwv_u7o_gmg)步骤 1~5 进入修改白名单分组对话框。
3.  在修改白名单分组对话框中，将 SAE 应用购买的弹性公网 IP 配置在白名单输入框中。 
    1.  登录 [VPC 控制台](https://vpc.console.aliyun.com/)，在左侧导航栏单击**NAT 网关**，复制应用实例所配置的**弹性公网 IP**。 

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/serverless-nat-gateway-ip.png)

    2.  在**允许访问IP名单**设置框中粘贴该**VPC 的 弹性公网 IP**地址，然后单击**确定**。 

        ![mangodb修改白名单/手动修改](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067698/156773736953801_zh-CN.png)

4.  在完成以上设置后，您的 SAE 应用就能跨 VPC、跨 Region 访问 MangoDB 数据库了。

