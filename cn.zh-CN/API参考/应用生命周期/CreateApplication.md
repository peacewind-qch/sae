# CreateApplication {#doc_api_sae_CreateApplication .reference}

创建一个SAE应用

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=CreateApplication&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
POST /pop/v1/sam/app/createApplication HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppName|String|是|test-app|应用名称。允许数字，字母以及中划线组合。必须字母打头，最大长度36个字符

 |
|NamespaceId|String|是|cn-beijing:test|EDAS命名空间对应ID。只支持名称为小写字母加中划线的命名空间，必须以字母开头。命名空间可从DescribeNamespaceList接口获取。

 |
|PackageType|String|是|FatJar|应用包类型。支持FatJar、War、Image。

 |
|Replicas|Integer|是|1|初始实例数。

 |
|AppDescription|String|否|This is a test description.|应用描述信息。不超过1024个字符

 |
|Command|String|否|sleep|镜像启动命令。该命令必须为容器内存在的可执行的对象。例如: sleep。设置该命令将导致镜像原本的启动命令失效。

 |
|CommandArgs|String|否|1d|镜像启动命令参数。上述启动命令所需参数。例如: \\"1d"\\

 |
|Cpu|Integer|否|1000|每个实例所需的CPU，单位为毫核，不能为0。目前仅支持固定规格的实例类型。

 |
|CustomHostAlias|String|否|\[\{"hostName":"samplehost","ip":"127.0.0.1"\}\]|容器内自定义host映射。例如: \\\{"hostName":"samplehost","ip":"127.0.0.1"\}\\

 |
|Deploy|Boolean|否|true|是否立即部署生效。默认为否。

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
|Memory|Integer|否|1024|每个实例所需的内存，单位为MB，不能为0。目前仅支持固定规格的实例类型。

 |
|PackageUrl|String|否|http://myoss.oss-cn-hangzhou.aliyuncs.com/my-buc/2019-06-30/sae-test.jar|部署包地址。只有FatJar或War类型应用可以配置部署包地址。

 |
|PackageVersion|String|否|1.0.0|部署的包的版本号，War FatJar类型必填。请自定义它的含义。

 |
|Readiness|String|否|\{"exec":\{"command":\["sleep","6s"\]\},"initialDelaySeconds":15,"timeoutSeconds":12\}|应用启动状态检查，多次健康检查失败的容器将被杀死并重启。不通过健康检查的容器将不会有SLB流量进入。例如: \{"exec":\{"command":\\"sleep","6s"\\\},"initialDelaySeconds":15,"timeoutSeconds":12\}

 |
|VSwitchId|String|否|vsw-xxxxxxxxxxxxxxxxxxx|应用实例弹性网卡所在的虚拟交换机。该交换机必须位于上述VPC内。该交换机与EDAS命名空间同样存在绑定关系。不填则为命名空间绑定的VSwitchId。

 |
|VpcId|String|否|vpc-xxxxxxxxxxxxxxxxxxx|EDAS命名空间对应的VPC。在serverless中，一个命名空间只能对应一个VPC，且不能修改。第一次在命名空间内创建Serverless应用将形成绑定关系。多个命名空间可以对应一个VPC。不填则为命名空间绑定的VpcId。

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
|AppId|String|017f39b8-dfa4-4e16-a84b-1dcee4b17106|创建成功的应用ID。

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
POST /pop/v1/sam/app/createApplication HTTP/1.1
公共请求头
{
  "AppName": "test-app"
  "NamespaceId": "cn-beijing:test"
  "PackageType": "FatJar"
  "Replicas": "1"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<CreateApplication>
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
</CreateApplication>
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
|400|Application.MissingJdk|Your application must at least contain a JDK component.|应用必须至少包含JDK组件|
|404|InvalidNamespaceId.NotFound|The specified NamespaceId does not exist.|指定的NamespaceId不存在。|
|400|InvalidPackageType.NotFound|The package type must be War, FatJar, or Image.|包类型必须为War、Fatjar或Image|
|400|InvalidParameter.FileName|The application deployment package name is invalid. This name can contain only alphanumeric characters, hyphens \(-\), and underscores \(\_\). In addition, you can upload JAR files only if the selected deployment version supports JAR file. Otherwise, upload WAR files only.|应用部署程序包名称无效。名称只能包含字母、数字和特殊字符“-”“\_”。另外，仅当选择的部署版本支持JAR部署时方可上传JAR包，否则只能上传WAR包。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s 不能为空|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}|
|400|JarApplication.MissingJdk|A FatJar application must contain JDK.|FatJAR类型应用必须包含JDK|
|400|NoAvailableCluster.NotFound|No clusters are available for the current region.|当前地域没有可用集群|
|400|NoComputeResourceQuota.Exceed|Your compute resource is insufficient. Please submit a ticket to raise the quota.|计算资源不足，请提交工单增加计算资源额度。|
|400|PandoraApplication.MissingJdk|The Pandora application is missing a JDK component.|pandora应用缺少JDK组件|
|400|PandoraApplication.OnlyJdk|A Pandora application only requires JDK component.|pandora应用只需要JDK组件|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s|
|400|InvalidComponent.NotFound|The current component \(such as JDK, Tomcat, or EDASWebContainer\) does not exist.|找不到当前组件（JDK、Tomcat、EDASWebContainer等）|
|400|InvalidHostnameIp.Invalid|The hostname and/or IP is invalid: Hostname \[%s\], IP \[%s\].|主机名和/或IP不合法：主机名\[%s\]，IP\[%s\]。|
|400|InvalidInstanceSpecification.Unsupported|The instance specification is not supported: CPU \[%s\], memory \[%s\].|不支持的实例规格。CPU\[%s\]，Memory\[%s\]。|
|400|InvalidServerlessRegion.Unsupported|The current region is not supported: %s|不支持当前地域：%s|
|404|InvalidVpcId.NotFound|The specified VpcId does not exist.|指定的VpcId不存在。|
|400|WarApplication.MissingJdkWebcontainer|A War application must contain JDK and Tomcat.|War类型应用必须包含JDK和Tomcat|
|400|InvalidNamespace.WithUppercase|This namespace does not support creating SAE apps because it contains uppercase letters.|命名空间不支持创建SAE应用，因为它带有大写字母。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

