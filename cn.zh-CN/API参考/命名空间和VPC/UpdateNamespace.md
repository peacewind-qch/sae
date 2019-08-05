# UpdateNamespace {#doc_api_sae_UpdateNamespace .reference}

更新命名空间信息

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=UpdateNamespace&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
PUT /pop/v1/paas/namespace HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|NamespaceId|String|是|cn-beijing:test|命名空间ID

 |
|NamespaceName|String|是|name|命名空间名称

 |
|NamespaceDescription|String|否|desc|命名空间描述

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |命名空间信息

 |
|NamespaceDescription|String|desc|命名空间描述

 |
|NamespaceId|String|cn-beijing:test|命名空间ID

 |
|NamespaceName|String|name|命名空间名称

 |
|RegionId|String|cn-beijing|地域

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
PUT /pop/v1/paas/namespace HTTP/1.1
公共请求头
{
  "NamespaceId": "cn-beijing:test"
  "NamespaceName": "name"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<UpdateNamespaceResponse>
	  <Data>
		    <NamespaceName>name</NamespaceName>
		    <RegionId>cn-beijing</RegionId>
		    <NamespaceDescription>desc</NamespaceDescription>
		    <NamespaceId>cn-beijing:test</NamespaceId>
	  </Data>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <TraceId>000000000000000000000000000000</TraceId>
	  <Success>true</Success>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
</UpdateNamespaceResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"NamespaceName":"name",
		"RegionId":"cn-beijing",
		"NamespaceDescription":"desc",
		"NamespaceId":"cn-beijing:test"
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
|404|InvalidNamespaceId.NotFound|The specified NamespaceId does not exist.|指定的NamespaceId不存在。|
|400|InvalidNamespaceName.Format|The specified NamespaceName is invalid. The name of the namespace cannot exceed 63 characters in length.|指定的NamespaceName不合法。命名空间名称的长度不能超过63个字符。|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

