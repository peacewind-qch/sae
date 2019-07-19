# ListConsumedServices {#doc_api_sae_ListConsumedServices .reference}

获取订阅的微服务列表

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListConsumedServices&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/service/listConsumedServices HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|00000000-0000-0000-0000-000000000000|应用ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |微服务列表信息

 |
|AppId|String|00000000-0000-0000-0000-000000000000|应用ID

 |
|Group2Ip|String|\{\}|保留字段

 |
|Groups| |HSF|消费的服务对应的组别

 |
|Ips| |10.0.0.1|服务订阅地址

 |
|Name|String|com.alibaba.nodejs.ItemService|发布的服务名称

 |
|Type|String|RPC|发布的服务类型

 |
|Version|String|1.0.0|发布的服务版本

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
GET /pop/v1/sam/service/listConsumedServices HTTP/1.1
公共请求头
{
  "AppId": "00000000-0000-0000-0000-000000000000"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListConsumedServicesResponse>
	  <Data>
		    <Groups>HSF</Groups>
		    <Name>com.alibaba.nodejs.ItemService</Name>
		    <Type>RPC</Type>
		    <Group2Ip></Group2Ip>
		    <Version>1.0.0</Version>
	  </Data>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <TraceId>000000000000000000000000000000</TraceId>
	  <ErrorCode>success</ErrorCode>
	  <Success>true</Success>
	  <Code>200</Code>
</ListConsumedServicesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":[
		{
			"Name":"com.alibaba.nodejs.ItemService",
			"Groups":[
				"HSF"
			],
			"Type":"RPC",
			"Group2Ip":{},
			"Version":"1.0.0",
			"Ips":[]
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

