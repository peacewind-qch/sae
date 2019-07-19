# DescribeApplicationGroups {#doc_api_sae_DescribeApplicationGroups .reference}

获取应用实例分组

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationGroups&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/app/describeApplicationGroups HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|00000000-0000-0000-0000-000000000000|应用ID

 |
|CurrentPage|Integer|否|1|页码

 |
|PageSize|Integer|否|10|页面大小

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |应用分组信息

 |
|EdasContainerVersion|String|3.5.3|部署时所使用的 EdasContainer 版本。如3.5.3

 |
|GroupId|String|00000000-0000-0000-0000-000000000000|分组ID

 |
|GroupName|String|\_DEFAULT\_GROUP|分组名称。

 -   \_DEFAULT\_GROUP ：默认分组

 |
|GroupType|Integer|0|分组类型

 |
|ImageUrl|String|registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest|部署时设置的 ImageUrl

 |
|Jdk|String|Open JDK 8|部署时设置的 JDK

 |
|PackageType|String|Image|部署类型。

 -   Image：采用 ImageUrl 进行部署

 |
|PackageUrl|String|registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest|部署时上传/设置的 WAR/JAR 包地址

 |
|PackageVersion|String|1.0.0|部署时设置的软件版本。若为 ImageUrl 部署，自动生成

 |
|Replicas|Integer|10|所有实例数

 |
|RunningInstances|Integer|1|运行中的实例数

 |
|WebContainer|String|Apache Tomcat 7|部署时设置的 WebContainer

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附加信息

 |
|RequestId|String|00000000-0000-0000-0000-000000000000|请求ID

 |
|Success|Boolean|true|是否成功

 |
|TraceId|String|000000000000000000000000000000|调用链ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
GET /pop/v1/sam/app/describeApplicationGroups HTTP/1.1
公共请求头
{
  "AppId": ""
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeApplicationGroupsResponse>
	  <Data>
		    <GroupType>0</GroupType>
		    <RunningInstances>2</RunningInstances>
		    <PackageType>Image</PackageType>
		    <GroupName>_DEFAULT_GROUP</GroupName>
		    <PackageVersion>2019-04-26 15:56:34.115</PackageVersion>
		    <ImageUrl>registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest</ImageUrl>
		    <Replicas>2</Replicas>
		    <GroupId>00000000-0000-0000-0000-000000000000</GroupId>
	  </Data>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <TraceId>000000000000000000000000000000</TraceId>
	  <ErrorCode>success</ErrorCode>
	  <Success>true</Success>
	  <Code>200</Code>
</DescribeApplicationGroupsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":[
		{
			"GroupType":0,
			"PackageType":"Image",
			"RunningInstances":2,
			"GroupName":"_DEFAULT_GROUP",
			"PackageVersion":"2019-04-26 15:56:34.115",
			"ImageUrl":"registry-vpc.cn-hangzhou.aliyuncs.com/demo/nginx:latest",
			"Replicas":2,
			"GroupId":"00000000-0000-0000-0000-000000000000"
		}
	],
	"Message":"success",
	"RequestId":"00000000-0000-0000-0000-000000000000",
	"TraceId":"000000000000000000000000000000",
	"Success":true,
	"ErrorCode":"success",
	"Code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

