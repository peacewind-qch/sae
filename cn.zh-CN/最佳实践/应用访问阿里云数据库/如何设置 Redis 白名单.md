# 如何设置 Redis 白名单 {#concept_118771_zh .concept}

创建 SAE 应用之后，如果你需要访问 Redis 数据库，需要设置 Redis 白名单。

## 背景信息 {#section_h5n_b6f_x9b .section}

不同场景下，白名单设置的内容不同。本文我们将从以下两个场景来分别说明白名单设置的相关操作。

-   [场景一：应用访问本 VPC 内的 Redis 数据库](#section_59c_tnp_u0r)
-   [场景二：应用跨 VPC 或跨 Region 访问 Redis 数据库](#section_l5k_wik_8b6)

## 场景一：应用访问本 VPC 内的 Redis 数据库 {#section_59c_tnp_u0r .section}

1.  登录 [Redis 管理控制台](https://kvstorenext.console.aliyun.com)。
2.  在控制台页面左上角，选择实例所在地域。

    **说明：** 目前 SAE 仅开放了**华北 2 （北京）**和**华东 1 （杭州）**地域，故请选择**华北 2 （北京）**或**华东 1 （杭州）**地域。

    **说明：** 目前 SAE 现已开放了**华北 2 （北京）**、**华东 1 （杭州）**、**华东 2 （上海）**和**华南 1 （深证）**区域。

3.  在左侧导航栏单击**实例列表**，然后单击具体实例名称。
4.  在实例信息页面左侧的导航栏中单击**白名单设置**。
5.  单击 default 区域框右侧的**修改**。

    ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/118771/cn_zh/1557833503965/redis%E6%88%AA%E5%9B%BE.png)

6.  在弹出的对话框中，将 SAE 应用所在的 VPC 网络的网段地址配置在白名单输入框中。
    1.  登录 [VPC 控制台](https://vpc.console.aliyun.com)，在专有网络列表中找到应用所在的 VPC，单击该 VPC 的名称进入专有网络详情页面。
    2.  复制应用所在的 VPC 的 IPv4 网段。

        ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/serverless-app-vpc-ip-details.png)

    3.  在**组内白名单**设置框中粘贴该 VPC 的 IPv4 网段地址，然后单击**确定**。

        ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/118771/cn_zh/1557833529558/%E4%BF%AE%E6%94%B9%E7%99%BD%E5%90%8D%E5%8D%951.png)

7.  在完成以上设置后，您的 SAE 应用就能访问本 VPC 内的 Redis 数据库了。

## 场景二：应用跨 VPC 或跨 Region 访问 Redis 数据库 {#section_l5k_wik_8b6 .section}

不同 VPC 和不同 Region 之间逻辑上完全隔离，故常规情况下不能跨 VPC 和跨 Region 访问 Redis 数据库。若您的应用想跨 VPC 或跨 Region 访问 Redis 数据库，请按照下面步骤进行相关配置。

1.  前提准备

    参考[应用如何访问公网](cn.zh-CN/最佳实践/应用访问公网/应用如何访问公网.md#) 购买 NAT 网关和弹性公网 IP 组合包并保证 SAE 应用可以访问公网。

2.  设置白名单
    1.  参考[场景一：应用访问本 VPC 内的 Redis 数据库](#section_59c_tnp_u0r)步骤 1~5 进入修改白名单分组对话框。
    2.  在修改白名单分组对话框中，将 SAE 应用购买的弹性公网 IP 配置在白名单输入框中。
        1.  登录 [VPC 控制台](https://vpc.console.aliyun.com)，在左侧导航栏单击 **NAT 网关**，复制应用实例所配置的**弹性公网 IP**。

            ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/serverless-nat-gateway-ip.png)

        2.  在**组内白名单**设置框中粘贴该 VPC 的 弹性公网 IP地址，然后单击**确定**。

            ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/118771/cn_zh/1557833550267/%E4%BF%AE%E6%94%B9%E7%99%BD%E5%90%8D%E5%8D%952.png)

    3.  在完成以上设置后，您的 SAE 应用就能跨 VPC、跨 Region 访问 Redis 数据库了。


