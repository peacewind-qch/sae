# 绑定 SLB {#concept_113305_zh .concept}

在 SAE 中创建应用后，可以通过添加公网 SLB 实现公网访问，添加内网 SLB 实现同 VPC 内所有节点够能通过私网负载均衡访问您的应用。

## 前提条件 {#section_rr8_w9t_fgg .section}

在 SAE 控制台上给应用绑定 SLB 时您需先参考[使用限制](https://help.aliyun.com/document_detail/32459.html)创建负载均衡实例和创建应用，并且 SLB 实例和 SAE 应用所在的实例必须属于同一个 VPC。

-   已在 SLB 控制台[创建负载均衡实例](https://help.aliyun.com/document_detail/86454.html)。
-   已在 SAE 控制台[创建 SAE 应用](https://help.aliyun.com/document_detail/94541.html)。

## 绑定 SLB 到应用 {#section_tcj_tmb_6qh .section}

1.  [登录 SAE 控制台](http://sae.console.aliyun.com)。

2.  在左侧导航栏，单击**应用列表**，在页面单击具体应用名称。

3.  在应用详情页面的**基本信息** \> **应用访问设置**区域，单击**公网访问地址**右侧的**添加公网 SLB 访问**。
4.  在**添加公网 SLB 访问**对话框中，设置负载均衡参数，然后单击**确认**完成配置。

**说明：** 

-   绑定 SLB 后，用户能通过公网访问您的应用。系统会为您的应用自动购买一个公网 SLB 服务，按使用量计费。购买的 SLB 信息可以在[负载均衡控制台](https://slb.console.aliyun.com)查看。

-   绑定 SLB 前，请检查你的阿里云账户余额是否大于 100 元，SLB 额度（每个账户 50 个）是否已用满。账户余额不足或者 SLB 额度用满时，都会导致添加公网 SLB 失败。

![添加公网SLB访问](https://aliware-images.oss-cn-hangzhou.aliyuncs.com/EDAS/Serverless/Serverless-AppDeploy-addSLB.png)

-   **SLB 端口**：公网负载均衡前端端口，通过该端口访问应用，可设置范围为1~65535。
-   **容器端口**容器端口：进程监听的端口。一般由程序定义，比如：Web 服务默认使用 8080 端口。
-   **网络协议**：默认为 TCP，不可更改。

## 结果验证 {#section_yi1_1l9_7yv .section}

复制配置的负载均衡的 IP 及端口，如 `192.168.0.184:80`，在浏览器中粘贴地址并回车，即可分别进入各自的应用首页。

如果负载均衡右侧未出现 IP 和端口信息，则表示绑定负载均衡失败，请进入变更记录查看变更详情，根据变更记录排查并修复失败原因。

