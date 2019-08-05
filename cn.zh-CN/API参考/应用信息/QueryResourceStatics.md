# QueryResourceStatics {#doc_api_sae_QueryResourceStatics .reference}

获取应用的资源使用量

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=QueryResourceStatics&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```

```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|7171a6ca-d1cd-4928-8642-7d5cfe69a26c|应用ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态

 |
|Data| | |资源使用信息

 |
|RealTimeRes| | |实时资源使用量

 |
|Cpu|Integer|13|CPU使用量，单位 Core

 -   min

 |
|Memory|Integer|26|内存使用量，单位 GiB

 -   min

 |
|Summary| | |当月资源使用信息

 |
|Cpu|Integer|3354|CPU使用量，单位 Core

 -   min

 |
|Memory|Integer|6708|内存使用量，单位 GiB

 -   min

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附加信息

 |
|RequestId|String|7CCF7092-72CA-4431-90D6-C7D9875267AA|请求ID

 |
|Success|Boolean|true|是否成功标识

 |
|TraceId|String|ac1a08a015623098794277264e20c8|调用ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?<公共请求参数>

```

正常返回示例

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"RealTimeRes":{
			"Cpu":13,
			"Memory":26
		},
		"Summary":{
			"Cpu":3354,
			"Memory":6708
		}
	},
	"Message":"success",
	"RequestId":"7CCF7092-72CA-4431-90D6-C7D9875267AA",
	"TraceId":"ac1a08a015623098794277264e20c8",
	"Success":true,
	"ErrorCode":"success",
	"Code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

