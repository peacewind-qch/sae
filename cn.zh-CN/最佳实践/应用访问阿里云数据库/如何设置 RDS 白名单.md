# 如何设置 RDS 白名单 {#concept_1426363 .concept}

创建 SAE 应用之后，如果你需要访问 RDS 数据库，需要设置 RDS 白名单。

## 背景信息 {#section_vb2_pes_xiw .section}

不同场景下，白名单设置的内容不同。本文我们将从以下两个场景来分别说明白名单设置的相关操作。

-   [场景一：应用访问本 VPC 内的 RDS 数据库](#section_03m_fax_xys)
-   [场景二：应用跨 VPC 或跨 Region 访问 RDS 数据库](#section_oig_j0g_gkw)

## 场景一：应用访问本 VPC 内的 RDS 数据库 {#section_03m_fax_xys .section}

1.  登录 [RDS 管理控制台](https://rdsnext.console.aliyun.com/)。
2.  在控制台页面左上角，选择实例所在地域。

    **说明：** 目前 SAE 仅开放了**华北 2 （北京）**和**华东 1 （杭州）**地域，故请选择**华北 2 （北京）**或**华东 1 （杭州）**地域。

3.  在左侧导航栏单击**实例列表**，然后在**云数据管理**的**基本信息**页签单击具体实例名称。
4.  在实例基本信息页面左侧导航栏中单击**数据安全性**。
5.  在数据安全性页面的**白名单设置**页签中，单击 default 区域右侧的**修改**按钮。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067696/156721889953763_zh-CN.png)

6.  在弹出的对话框中，将 SAE 应用所在的 VPC 网络的网段地址配置在白名单输入框中。
    1.  登录 [VPC 控制台](https://vpc.console.aliyun.com/)，在专有网络列表中找到应用所在的 VPC，单击该 VPC 的名称进入专有网络详情页面。
    2.  复制应用所在的 VPC 的IPv4网段。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067696/156721889953768_zh-CN.png)

    3.  在**组内白名单设置**框中粘贴该 VPC 的 IPv4 网段地址，然后单击**确定**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067696/156721889953770_zh-CN.png)

7.  在完成以上设置后，您的 SAE 应用就能访问本 VPC 内的 RDS 数据库了。

## 场景二：应用跨 VPC 或跨 Region 访问 RDS 数据库 {#section_oig_j0g_gkw .section}

不同 VPC 和不同 Region 之间逻辑上完全隔离，故常规情况下不能跨 VPC 和跨 Region 访问 RDS 数据库。若您的应用想跨 VPC 或跨 Region 访问 RDS 数据库，请按照下面步骤进行相关配置。

1.  前提准备

    参考 [SAE 应用如何访问公网](https://help.aliyun.com/document_detail/100317.html)购买 **NAT 网关**和**弹性公网 IP 组合包**并保证 SAE 应用可以访问公网。

2.  设置白名单

    1.  参考[场景一：应用访问本 VPC 内的 RDS 数据库](https://help.aliyun.com/document_detail/100272.html?spm=a2c4g.11186623.6.620.41294c37xokiXo#AccessTheRDSWithinTheSameVPC)步骤 1~5 进入修改白名单分组对话框。
    2.  在修改白名单分组对话框中，将 SAE 应用购买的弹性公网 IP 配置在白名单输入框中。
        1.  登录 [VPC 控制台](https://vpc.console.aliyun.com/)，在左侧导航栏单击 **NAT 网关**，复制应用实例所配置的**弹性公网 IP**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067696/156721889953780_zh-CN.png)

        2.  在**组内白名单**设置框中粘贴该 VPC 的 **弹性公网 IP**地址，然后单击**确定**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067696/156721889953781_zh-CN.png)

    3.  在完成以上设置后，您的 SAE 应用就能跨 VPC、跨 Region 访问 RDS 数据库了。

