# ListLogConfigs {#doc_api_sae_ListLogConfigs .reference}

获取应用日志列表

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListLogConfigs&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/log/listLogConfigs HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|56f77b65-788d-442a-9885-7f20d91f3672|应用ID

 |
|CurrentPage|Integer|是|1|当前页

 |
|PageSize|Integer|是|10|页大小

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口返回状态

 |
|Data| | |文件日志信息

 |
|CurrentPage|Integer|1|当前页

 |
|LogConfigs| | |日志配置

 |
|ConfigName|String|sae-1f240907a6faf58c653f09e81b7e316e|日志服务配置名称

 |
|CreateTime|String|2019-08-29 17:18:00|日志配置创建时间

 |
|LogDir|String|/root/logs/hsf/hsf.log|日志文件路径

 |
|LogType|String|file\_log|日志类型，当前只支持文件日志

 |
|RegionId|String|cn-beijing|Region ID

 |
|SlsLogStore|String|sae-1f240907a6faf58c653f09e81b7e316e|日志服务日志存储名

 |
|SlsProject|String|sae-56f77b65-788d-442a-9885-7f20d91f3672|日志服务Project

 |
|StoreType|String|sls|日志服务存储类型

 |
|PageSize|Integer|10|页大小

 |
|TotalSize|Integer|1|总条数

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附件信息

 |
|RequestId|String|ac1d5e2c15671581252413581d37bd|请求ID

 |
|Success|Boolean|true|是否成功

 |
|TraceId|String|ac1d5e2c15671581252413581d37bd|调用链ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
GET /pop/v1/sam/log/listLogConfigs HTTP/1.1
公共请求头
{
  "AppId": ""
  "CurrentPage": 
  "PageSize": 
}
```

正常返回示例

`JSON` 格式

``` {#json_return_success_demo}
{
	"successResponse":true,
	"requestId":"ac1d5e2c15671581252413581d37bd",
	"data":{
		"Data":{
			"PageSize":10,
			"TotalSize":1,
			"CurrentPage":1,
			"LogConfigs":[
				{
					"SlsLogStore":"sae-1f240907a6faf58c653f09e81b7e316e",
					"LogDir":"/root/logs/hsf/hsf.log",
					"RegionId":"cn-beijing",
					"CreateTime":"2019-08-29 17:18:00",
					"ConfigName":"sae-1f240907a6faf58c653f09e81b7e316e",
					"StoreType":"sls",
					"LogType":"file_log",
					"SlsProject":"sae-56f77b65-788d-442a-9885-7f20d91f3672"
				}
			]
		},
		"Message":"success",
		"TraceId":"ac1d5e2c15671581252413581d37bd",
		"Success":true,
		"ErrorCode":"success",
		"Code":200
	},
	"code":"200"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

