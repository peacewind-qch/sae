# 绑定 SLB {#task_122997_zh .task}

在 SAE 中创建应用后，可以通过添加公网 SLB（Server Load Balancer，负载均衡） 实现公网访问，可以添加内网 SLB 实现同 VPC 内所有应用间互相访问。本文介绍如何对应用进行 SLB 绑定。

-   场景一：绑定已有 SLB
    -   在 SLB 控制台[创建 SLB 实例](https://help.aliyun.com/document_detail/86454.html)。
    -   在 SAE控制台[创建 SAE 应用](https://help.aliyun.com/document_detail/94541.html)。
    -   [上传已有 SSL 证书](https://help.aliyun.com/document_detail/90792.html)。
-   场景二：绑定新建 SLB
    -   在 SAE 控制台[创建 SAE 应用](https://help.aliyun.com/document_detail/94541.html)。
    -   [上传已有 SSL 证书](https://help.aliyun.com/document_detail/90792.html)。

**说明：** 

-   创建 SLB 实例前请了解其 [使用限制](https://help.aliyun.com/document_detail/32459.html)。
-   SLB 实例与 SAE 应用所在的实例必须属于同一个 VPC 内。

## 场景一：绑定已有 SLB {#section_o4k_wjl_tl3 .section}

1.  登录 [SAE 控制台](https://sae.console.aliyun.com)。
2.  在左侧导航树选择**Serverless 应用引擎** \> **应用列表**，并在应用列表页面单击具体应用名称。
3.  在应用详情页面的**基本信息** \> **应用访问设置**区域绑定 SLB。 添加公网 SLB 单击**添加公网 SLB 访问**；添加内网 SLB 单击**添加私网 SLB 访问**。本文以**添加公网 SLB 访问**为例。

    ![应用访问设置1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067673/156801247956572_zh-CN.png)

    **说明：** 绑定 SLB 前，请检查您的阿里云账户余额是否大于 100 元，SLB 额度（每个账户 50 个）是否已用满。账户余额不足或者 SLB 额度用满时，都会导致添加公网 SLB 失败。

    1.  单击**公网访问地址**所在行的**添加公网 SLB 访问**，开始添加公网 SLB。 

        ![添加公网SLB访问](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067673/156801247956535_zh-CN.png)

    2.  在添加公网 SLB 访问的**请选择 SLB**所在行的下拉列表中选择已有的 SLB。 

        **说明：** 复用已有 SLB 时，SAE 仅支持通过 SLB 控制台购买的 SLB实例，不能复用其它产品代购的 SLB，以防出现监听配置冲突。

    3.  配置 SLB 监听端口。 
        -   TCP协议：
            -   **SLB 端口**：公网 SLB 前端端口，通过该端口访问应用，可设置范围为1~65535。
            -   **容器端口**：进程监听端口。由程序定义，例如：Web 服务默认使用 8080 端口。
        -   HTTPS协议：
            -   **HTTPS 端口**：公网负载均衡前端端口，通过该端口访问应用，可设置范围为1~65535。
            -   **SSL证书**：SSL协议证书，在下拉菜单中选择已上传的SSL证书。
            -   **容器端口**：进程监听的端口。由程序定义，例如：Web服务默认使用 8080 端口。
    4.  单击**确认**，SLB 绑定完成。
4.  结果验证。 

    复制配置的SLB IP 及其端口，如 `192.168.0.184:80`，并在浏览器中输入地址并回车，即可分别进入各自的应用首页。

    如果 SLB 右侧未出现 IP 和端口信息，则表示绑定 SLB 失败，请[查看变更记录](cn.zh-CN/应用管理/查看变更记录.md#)，并修复失败原因。


## 场景二：绑定新建 SLB {#section_238_za6_1eu .section}

1.  登录 [SAE 控制台](https://sae.console.aliyun.com)。
2.  在左侧导航树选择**Serverless 应用引擎** \> **应用列表**，并在应用列表页面单击具体应用名称。
3.  在应用详情页面的**基本信息** \> **应用访问设置**区域绑定 SLB。 添加公网 SLB 单击**添加公网 SLB 访问**；添加内网 SLB 单击**添加私网 SLB 访问**。本文以**添加公网 SLB 访问**为例。

    ![应用访问设置1](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067673/156801247956572_zh-CN.png)

    **说明：** 

    -   绑定 SLB 后，用户能通过公网访问您的应用。系统会为您的应用自动购买一个公网 SLB 服务，按使用量计费。购买的 SLB 信息可以在[负载均衡控制台](https://slb.console.aliyun.com)查看。
    -   绑定 SLB 前，请检查您的阿里云账户余额是否大于 100 元，SLB 额度（每个账户 50 个）是否已用满。账户余额不足或者 SLB 额度用满时，都会导致添加公网 SLB 失败。
    1.  单击**公网访问地址**所在行的**添加公网 SLB 访问**，开始添加公网 SLB。 

        ![添加公网SLB访问](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067673/156801247956535_zh-CN.png)

    2.  在添加公网 SLB 访问的**请选择 SLB**所在行的下拉列表中选择**新建**。 选择新建之后系统自动进行**SLB 配额检查**和**账户余额检查**，检查通过后为应用自动购买全新的 SLB 实例，并在下方显示具体SLB信息。
    3.  配置 SLB 监听端口。 
        -   TCP协议：
            -   **SLB 端口**：公网 SLB 前端端口，通过该端口访问应用，可设置范围为1~65535。
            -   **容器端口**：进程监听端口。由程序定义，例如：Web 服务默认使用 8080 端口。
        -   HTTPS协议：
            -   **HTTPS 端口**：公网负载均衡前端端口，通过该端口访问应用，可设置范围为1~65535。
            -   **SSL证书**：SSL协议证书，在下拉菜单中选择已上传的SSL证书。
            -   **容器端口**：进程监听的端口。由程序定义，例如：Web服务默认使用 8080 端口。
    4.  单击**确认**，SLB 绑定完成。
4.  结果验证。 

    复制配置的SLB IP 及其端口，如 `192.168.0.184:80`，并在浏览器中输入地址并回车，即可分别进入各自的应用首页。

    如果 SLB 右侧未出现 IP 和端口信息，则表示绑定 SLB 失败，请[查看变更记录](cn.zh-CN/应用管理/查看变更记录.md#)，并修复失败原因。


## 其他操作 {#section_4dx_qfa_0r0 .section}

1.  修改 私网 SLB 访问设置
2.  在应用详情页面的**基本信息** \> **应用访问设置**区域，请依据网络需求单击**编辑私网 SLB 访问**或**编辑公网网 SLB 访问**。 

    ![编辑删除SLB](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067673/156801248057199_zh-CN.png)

3.  在弹出的编辑私网 SLB 访问或编辑公网 SLB 访问对话框，修改所需信息并单击**确认**。

1.  删除私网 SLB 访问设置
2.  在应用详情页面的**基本信息** \> **应用访问设置**区域，单击**删除私网 SLB 访问**或**删除公网 SLB 访问**。 

    ![编辑删除SLB](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1067673/156801248057199_zh-CN.png)

3.  单击**确认**，并在**删除私网SLB访问**或者**删除公网 SLB 访问**对话框中单击**确认**。

