# DescribeComponents {#doc_api_sae_DescribeComponents .reference}

获取应用创建部署时所需的组件版本

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeComponents&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/resource/components HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|00000000-0000-0000-0000-000000000000|应用ID

 |
|Type|String|是|TOMCAT|支持的组件类型。

 -   Tomcat
-   JDK

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |支持的应用组件信息

 |
|ComponentDescription|String|Open JDK 8|组件描述

 |
|ComponentKey|String|Open JDK 8|组件ID

 |
|Expired|Boolean|false|是否过期

 |
|Type|String|JDK|组件类型

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
GET /pop/v1/sam/resource/components HTTP/1.1
公共请求头
{
  "AppId": "00000000-0000-0000-0000-000000000000"
  "Type": "TOMCAT"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeComponentsResponse>
	  <Data>
		    <ComponentKey>Open JDK 8</ComponentKey>
		    <Type>JDK</Type>
		    <Expired>false</Expired>
		    <ComponentDescription>Open JDK 8</ComponentDescription>
	  </Data>
	  <Data>
		    <ComponentKey>Open JDK 7</ComponentKey>
		    <Type>JDK</Type>
		    <Expired>false</Expired>
		    <ComponentDescription>Open JDK 7</ComponentDescription>
	  </Data>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <TraceId>000000000000000000000000000000</TraceId>
	  <Success>true</Success>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
</DescribeComponentsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":[
		{
			"ComponentKey":"Open JDK 8",
			"Type":"JDK",
			"ComponentDescription":"Open JDK 8",
			"Expired":false
		},
		{
			"ComponentKey":"Open JDK 7",
			"Type":"JDK",
			"ComponentDescription":"Open JDK 7",
			"Expired":false
		}
	],
	"Message":"success",
	"RequestId":"00000000-0000-0000-0000-000000000000",
	"TraceId":"000000000000000000000000000000",
	"ErrorCode":"success",
	"Success":"true",
	"Code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

