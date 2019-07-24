# DeployApplication {#doc_api_sae_DeployApplication .reference}

部署应用

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DeployApplication&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
POST /pop/v1/sam/app/deployApplication HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|否|017f39b8-dfa4-4e16-a84b-1dcee4b17106|需要部署的应用ID

 |
|BatchWaitTime|Integer|否|10|分批等待时间。单位秒。

 |
|Command|String|否|sleep|镜像启动命令。该命令必须为容器内存在的可执行的对象。例如: sleep。设置该命令将导致镜像原本的启动命令失效。

 |
|CommandArgs|String|否|1d|镜像启动命令参数。上述启动命令所需参数。例如: \\"1d"\\

 |
|CustomHostAlias|String|否|\[\{"hostName":"samplehost","ip":"127.0.0.1"\}\]|容器内自定义host映射。例如: \\\{"hostName":"samplehost","ip":"127.0.0.1"\}\\

 |
|EdasContainerVersion|String|否|3.5.3|EDAS pandora应用使用的运行环境

 |
|Envs|String|否|\[\{"name":"envtmp","value":"0"\}\]|容器环境变量参数。例如: \\\{"name":"envtmp","value":"0"\}\\

 |
|ImageUrl|String|否|registry.cn-hangzhou.aliyuncs.com/sae\_test/ali\_sae\_test:0.0.1|镜像地址。只有Image类型应用可以配置镜像地址。

 |
|JarStartArgs|String|否|custom-args|Jar包启动应用参数。应用默认启动命令: $JAVA\_HOME/bin/java $JarStartOptions -jar $CATALINA\_OPTS "$package\_path" $JarStartArgs

 |
|JarStartOptions|String|否|custom-option|Jar包启动应用选项。应用默认启动命令: $JAVA\_HOME/bin/java $JarStartOptions -jar $CATALINA\_OPTS "$package\_path" $JarStartArgs

 |
|Jdk|String|否|Open JDK 8|部署的包依赖的JDK版本。镜像不支持。

 |
|Liveness|String|否|\{"exec":\{"command":\["sleep","5s"\]\},"initialDelaySeconds":10,"timeoutSeconds":11\}|容器健康检查，健康检查失败的容器将被杀死并恢复。目前仅支持容器内下发命令的方式。\{"exec":\{"command":\\"sleep","5s"\\\},"initialDelaySeconds":10,"timeoutSeconds":11\}

 |
|MinReadyInstances|Integer|否|1|最小可用实例数。任何变更都尽量不会违背这个设置，保证业务稳定性。

 |
|PackageUrl|String|否|http://myoss.oss-cn-hangzhou.aliyuncs.com/my-buc/2019-06-30/sae-test.jar|部署包地址。只有FatJar或War类型应用可以配置部署包地址。

 |
|PackageVersion|String|否|1.0.1|部署的包的版本号，War FatJar类型必填。请自定义它的含义。

 |
|Readiness|String|否|\{"exec":\{"command":\["sleep","6s"\]\},"initialDelaySeconds":15,"timeoutSeconds":12\}|应用启动状态检查，多次健康检查失败的容器将被杀死并重启。不通过健康检查的容器将不会有SLB流量进入。例如: \{"exec":\{"command":\\"sleep","6s"\\\},"initialDelaySeconds":15,"timeoutSeconds":12\}

 |
|UpdateStrategy|String|否|\{\}|部署策略

 |
|WebContainer|String|否|apache-tomcat-7.0.91|部署的包依赖的tomcat版本。镜像不支持。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |返回结果

 |
|AppId|String|017f39b8-dfa4-4e16-a84b-1dcee4b17106|应用ID。

 |
|ChangeOrderId|String|01db03d3-3ee9-48b3-b3d0-dfce2d88ab31|返回的发布单ID，用于查询任务执行状态。

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附加信息

 |
|RequestId|String|00000000-0000-0000-0000-000000000000|请求ID

 |
|Success|Boolean|true|是否成功

 |
|TraceId|String|00000000-0000-0000-0000-000000000000|调用链ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
POST /pop/v1/sam/app/deployApplication HTTP/1.1
公共请求头
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DeployApplication>
	  <Data>
		    <ChangeOrderId>01db03d3-3ee9-48b3-b3d0-dfce2d88ab31</ChangeOrderId>
            <AppId>017f39b8-dfa4-4e16-a84b-1dcee4b17106</AppId>
      </Data>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <TraceId>000000000000000000000000000000</TraceId>
	  <Success>true</Success>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
</DeployApplication>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"AppId":"017f39b8-dfa4-4e16-a84b-1dcee4b17106",
		"ChangeOrderId":"01db03d3-3ee9-48b3-b3d0-dfce2d88ab31"
	},
	"Message":"success",
	"RequestId":"00000000-0000-0000-0000-000000000000",
	"TraceId":"000000000000000000000000000000",
	"ErrorCode":"success",
	"Success":true,
	"Code":200
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|Application.InvalidStatus|The application status is abnormal. Please try again later.|应用状态异常，请稍后重试。|
|400|Application.MissingJdk|Your application must at least contain a JDK component.|应用必须至少包含JDK组件|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用|
|400|InvalidComponent.NotFound|The current component \(such as JDK, Tomcat, or EDASWebContainer\) does not exist.|找不到当前组件（JDK、Tomcat、EDASWebContainer等）|
|400|InvalidHostnameIp.Invalid|The hostname and/or IP is invalid: Hostname \[%s\], IP \[%s\].|主机名和/或IP不合法：主机名\[%s\]，IP\[%s\]。|
|400|InvalidInstanceSpecification.Unsupported|The instance specification is not supported: CPU \[%s\], memory \[%s\].|不支持的实例规格。CPU\[%s\]，Memory\[%s\]。|
|404|InvalidNamespaceId.NotFound|The specified NamespaceId does not exist.|指定的NamespaceId不存在。|
|400|InvalidPackageType.NotFound|The package type must be War, FatJar, or Image.|包类型必须为War、Fatjar或Image|
|400|InvalidParameter.FileName|The application deployment package name is invalid. This name can contain only alphanumeric characters, hyphens \(-\), and underscores \(\_\). In addition, you can upload JAR files only if the selected deployment version supports JAR file. Otherwise, upload WAR files only.|应用部署程序包名称无效。名称只能包含字母、数字和特殊字符“-”“\_”。另外，仅当选择的部署版本支持JAR部署时方可上传JAR包，否则只能上传WAR包。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s 不能为空|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s|
|400|JarApplication.MissingJdk|A FatJar application must contain JDK.|FatJAR类型应用必须包含JDK|
|400|NoComputeResourceQuota.Exceed|Your compute resource is insufficient. Please submit a ticket to raise the quota.|计算资源不足，请提交工单增加计算资源额度。|
|400|PandoraApplication.MissingJdk|The Pandora application is missing a JDK component.|pandora应用缺少JDK组件|
|400|PandoraApplication.OnlyJdk|A Pandora application only requires JDK component.|pandora应用只需要JDK组件|
|400|WarApplication.MissingJdkWebcontainer|A War application must contain JDK and Tomcat.|War类型应用必须包含JDK和Tomcat|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

