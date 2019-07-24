# DescribeApplicationConfig {#doc_api_sae_DescribeApplicationConfig .reference}

获取应用配置信息。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationConfig&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/app/describeApplicationConfig HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|否|7171a6ca-d1cd-4928-8642-7d5cfe69a26c|应用ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态

 |
|Data| | |应用信息

 |
|AppDescription|String|示例应用|应用描述信息

 |
|AppId|String|7171a6ca-d1cd-4928-8642-7d5cfe69a26c|应用ID

 |
|AppName|String|demo-app|应用名称

 |
|BatchWaitTime|Integer|10|分批发布时批次间的等待时间（单位秒）

 |
|Command|String|/bin/bash|应用容器启动命令

 |
|CommandArgs|String|\["-c","echo 1234"\]|应用容器启动命令参数

 |
|Cpu|Integer|1000|应用CPU规格（单位豪核，1核=1000豪核）

 |
|CustomHostAlias|String|\[\{"hostName":"test.host.name","ip":"0.0.0.0"\}\]|Hosts绑定设置

 |
|EdasContainerVersion|String|3.5.3|EDAS应用环境版本

 |
|Envs|String|\[\{"name":"TEST\_ENV\_KEY","value":"TEST\_ENV\_VAR"\}\]|环境变量

 |
|ImageUrl|String|docker.io/library/nginx:1.14.2|镜像地址

 |
|JarStartArgs|String|start|Jar包部署应用的args设置

 |
|JarStartOptions|String|-Dtest=true|Jar包部署应用的options设置

 |
|Jdk|String|Open JDK 8|应用使用的JDK版本信息

 |
|Liveness|String|\{"exec":\{"command":\["curl http://localhost:8080"\]\},"initialDelaySeconds":20,"timeoutSeconds":3\}|应用实例存活检查\(Liveness配置\)

 |
|Memory|Integer|2048|应用内存规格（单位MB）

 |
|MinReadyInstances|Integer|1|最小存活实例数

 |
|NamespaceId|String|cn-beijing:test|EDAS命名空间ID

 |
|PackageType|String|War|应用部署类型（Image, War, Jar）

 |
|PackageUrl|String|https://edas-bj.oss-cn-beijing.aliyuncs.com/apps/K8S\_APP\_ID/d4c97c37-aba3-403e-ae1e-6f7d87423016/hello-edas.war|应用部署包地址

 |
|PackageVersion|String|1.0|应用部署包版本

 |
|Readiness|String|\{"exec":\{"command":\["curl http://localhost:8080"\]\},"initialDelaySeconds":20,"timeoutSeconds":5\}|应用业务就绪检查\(Readiness配置\)

 |
|Replicas|Integer|2|应用实例个数

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附加信息

 |
|RequestId|String|01CF26C7-00A3-4AA6-BA76-7E95F2A3B6FF|请求ID

 |
|Success|Boolean|true|是否成功标识

 |
|TraceId|String|ac1a0b2215622246421415014e6d54|调用链ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
GET /pop/v1/sam/app/describeApplicationConfig HTTP/1.1
公共请求头
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeApplicationConfigResponse>
	  <Message>success</Message>
	  <RequestId>01CF26C7-00A3-4AA6-BA76-7E95F2A3B6FF</RequestId>
	  <TraceId>ac1a0b2215622246421415014e6d54</TraceId>
	  <Data>
		    <AppDescription></AppDescription>
		    <Liveness></Liveness>
		    <Memory>2048</Memory>
		    <WebContainer>apache-tomcat-7.0.91</WebContainer>
		    <Cpu>1000</Cpu>
		    <PackageVersion>222</PackageVersion>
		    <AppName>demo-app</AppName>
		    <Jdk>Open JDK 8</Jdk>
		    <JarStartArgs></JarStartArgs>
		    <MinReadyInstances>0</MinReadyInstances>
		    <Readiness></Readiness>
		    <PackageType>War</PackageType>
		    <CommandArgs></CommandArgs>
		    <VSwitchId>vsw-xxxxx</VSwitchId>
		    <Envs>[{"name":"TEST_ENV_KEY","value":"TEST_ENV_VAR"}]</Envs>
		    <JarStartOptions></JarStartOptions>
		    <Replicas>1</Replicas>
		    <CustomHostAlias>[{"hostName":"test.host.name","ip":"0.0.0.0"}]</CustomHostAlias>
		    <AppId>7171a6ca-d1cd-4928-8642-7d5cfe69a26c</AppId>
		    <VpcId>vpc-xxxx</VpcId>
		    <Command></Command>
		    <PackageUrl>https://edas-bj.oss-cn-beijing.aliyuncs.com/hello-edas.war</PackageUrl>
		    <BatchWaitTime>10</BatchWaitTime>
		    <NamespaceId>cn-beijing</NamespaceId>
		    <RegionId>cn-beijing</RegionId>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
</DescribeApplicationConfigResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"Command":"",
		"MinReadyInstances":0,
		"Readiness":"",
		"AppId":"7171a6ca-d1cd-4928-8642-7d5cfe69a26c",
		"VSwitchId":"vsw-xxxxx",
		"VpcId":"vpc-xxxx",
		"Cpu":1000,
		"Memory":2048,
		"PackageType":"War",
		"CommandArgs":"",
		"AppDescription":"",
		"AppName":"demo-app",
		"NamespaceId":"cn-beijing",
		"Jdk":"Open JDK 8",
		"JarStartOptions":"",
		"PackageVersion":"222",
		"CustomHostAlias":"[{\"hostName\":\"test.host.name\",\"ip\":\"0.0.0.0\"}]",
		"JarStartArgs":"",
		"Envs":"[{\"name\":\"TEST_ENV_KEY\",\"value\":\"TEST_ENV_VAR\"}]",
		"RegionId":"cn-beijing",
		"PackageUrl":"https://edas-bj.oss-cn-beijing.aliyuncs.com/hello-edas.war",
		"WebContainer":"apache-tomcat-7.0.91",
		"Liveness":"",
		"Replicas":1,
		"BatchWaitTime":10
	},
	"Message":"success",
	"RequestId":"01CF26C7-00A3-4AA6-BA76-7E95F2A3B6FF",
	"TraceId":"ac1a0b2215622246421415014e6d54",
	"Success":true,
	"ErrorCode":"success",
	"Code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

