# 如何设置 Hosts 绑定 {#concept_100335_zh .concept}

SAE 支持应用实例级别的实例，通过 Host 绑定对主机名进行解析，方便应用实例通过主机名进行访问。

## 操作步骤 {#section_w5v_k7o_e73 .section}

1.  登录 [SAE 控制台](https://sae.console.aliyun.com)。
2.  在左侧导航树选择**轻量级分布式应用服务** \> **应用列表**，在应用列表页面右上角单击**创建应用**。
3.  在应用的应用基本信息页签内，设置应用相关信息并单击**下一步：应用部署配置**。
4.  在应用部署配置页面，展开 **Hosts 绑定设置**页签并输入 Host 配置项。

    如果当前应用已经部署在 SAE，请参见[部署和升级应用](../../../../cn.zh-CN/应用管理/应用生命周期管理.md#section_3qn_6i4_g2p)修改 Host 绑定。

    ![](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/edas/EDAS-Serverless/serverless-HOSTS-BINGING.png)

5.  应用部署完成后，所设置的 Hosts 配置生效，可以通过域名访问应用。

