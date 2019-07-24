# API概览 {#doc_961104 .concept}

轻量级分布式应用服务提供以下相关API接口。

## 命名空间和VPC {#section_yod_yrl_pkt .section}

|API|描述|
|---|--|
|[CreateNamespace](cn.zh-CN/API参考/命名空间和VPC/CreateNamespace.md)|创建命名空间|
|[DeleteNamespace](cn.zh-CN/API参考/命名空间和VPC/DeleteNamespace.md)|删除命名空间|
|[DescribeNamespace](cn.zh-CN/API参考/命名空间和VPC/DescribeNamespace.md)|查询命名空间详细信息|
|[DescribeNamespaces](cn.zh-CN/API参考/命名空间和VPC/DescribeNamespaces.md)|查询命名空间列表|
|[UpdateNamespace](cn.zh-CN/API参考/命名空间和VPC/UpdateNamespace.md)|更新命名空间信息|
|[DescribeNamespaceList](cn.zh-CN/API参考/命名空间和VPC/DescribeNamespaceList.md)|获取命名空间列表|

## 应用信息 {#section_eet_l1e_8lv .section}

|API|描述|
|---|--|
|[DescribeApplicationConfig](cn.zh-CN/API参考/应用信息/DescribeApplicationConfig.md)|获取应用配置信息。|
|[DescribeRegions](cn.zh-CN/API参考/应用信息/DescribeRegions.md)|使用 DescribeRegions 查询可用地域。|
|[DescribeInstanceLog](cn.zh-CN/API参考/应用信息/DescribeInstanceLog.md)|获取实例日志|
|[DescribeComponents](cn.zh-CN/API参考/应用信息/DescribeComponents.md)|获取应用创建部署时所需的组件版本|
|[DescribeEdasContainers](cn.zh-CN/API参考/应用信息/DescribeEdasContainers.md)|获取应用微服务容器组件列表|
|[DescribeApplicationImage](cn.zh-CN/API参考/应用信息/DescribeApplicationImage.md)|描述应用镜像信息|
|[DescribeApplicationInstances](cn.zh-CN/API参考/应用信息/DescribeApplicationInstances.md)|获取应用实例列表|
|[DescribeApplicationGroups](cn.zh-CN/API参考/应用信息/DescribeApplicationGroups.md)|获取应用实例分组|
|[ListApplications](cn.zh-CN/API参考/应用信息/ListApplications.md)|获取应用列表|
|[QueryResourceStatics](cn.zh-CN/API参考/应用信息/QueryResourceStatics.md)|获取应用的资源使用量|

## 应用生命周期 {#section_a0a_jg7_uy7 .section}

|API|描述|
|---|--|
|[DescribeApplicationStatus](cn.zh-CN/API参考/应用生命周期/DescribeApplicationStatus.md)|获取应用的状态信息|
|[DeployApplication](cn.zh-CN/API参考/应用生命周期/DeployApplication.md)|部署应用|
|[CreateApplication](cn.zh-CN/API参考/应用生命周期/CreateApplication.md)|创建一个SAE应用|
|[DeleteApplication](cn.zh-CN/API参考/应用生命周期/DeleteApplication.md)|删除应用|
|[StopApplication](cn.zh-CN/API参考/应用生命周期/StopApplication.md)|停止应用|
|[RescaleApplicationVertically](cn.zh-CN/API参考/应用生命周期/RescaleApplicationVertically.md)|改变应用实例规格|
|[StartApplication](cn.zh-CN/API参考/应用生命周期/StartApplication.md)|启动应用|
|[ConfirmPipelineBatch](cn.zh-CN/API参考/应用生命周期/ConfirmPipelineBatch.md)|是否开始一下批次|
|[ListChangeOrders](cn.zh-CN/API参考/应用生命周期/ListChangeOrders.md)|获取变更单列表|
|[AbortAndRollbackChangeOrder](cn.zh-CN/API参考/应用生命周期/AbortAndRollbackChangeOrder.md)|中止或回滚变更单|
|[DescribeChangeOrder](cn.zh-CN/API参考/应用生命周期/DescribeChangeOrder.md)|查询变更单信息|
|[DescribeInstanceSpecifications](cn.zh-CN/API参考/应用生命周期/DescribeInstanceSpecifications.md)|获取应用实例规格信息|
|[RescaleApplication](cn.zh-CN/API参考/应用生命周期/RescaleApplication.md)|应用扩缩|
|[RestartApplication](cn.zh-CN/API参考/应用生命周期/RestartApplication.md)|重启应用|
|[AbortChangeOrder](cn.zh-CN/API参考/应用生命周期/AbortChangeOrder.md)|中止变更单|

## SLB {#section_jdp_ypg_5bb .section}

|API|描述|
|---|--|
|[BindSlb](cn.zh-CN/API参考/SLB/BindSlb.md)|为应用绑定SLB|
|[UnbindSlb](cn.zh-CN/API参考/SLB/UnbindSlb.md)|解绑内网或公网SLB|
|[DescribeApplicationSlbs](cn.zh-CN/API参考/SLB/DescribeApplicationSlbs.md)|获取应用SLB配置信息|

## 微服务列表 {#section_two_jmd_noa .section}

|API|描述|
|---|--|
|[ListConsumedServices](cn.zh-CN/API参考/微服务列表/ListConsumedServices.md)|获取订阅的微服务列表|
|[ListPublishedServices](cn.zh-CN/API参考/微服务列表/ListPublishedServices.md)|获取发布的微服务列表|

