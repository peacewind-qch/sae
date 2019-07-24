# ListApplications {#doc_api_sae_ListApplications .reference}

获取应用列表

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListApplications&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```

```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|CurrentPage|Integer|是|1|当前页数

 |
|AppName|String|否|demo-app|应用名

 |
|PageSize|Integer|否|20|页大小

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态

 |
|Data| | |应用列表

 |
|Applications| | |应用列表

 |
|AppDeletingStatus|Boolean|false|是否正在删除

 |
|AppId|String|f7730764-d88f-4b9a-8d8e-cd8efbfee1f0|应用ID

 |
|AppName|String|demo-app|应用名称

 |
|Instances|Integer|2|应用节点个数

 |
|RegionId|String|cn-beijing|Region ID

 |
|RunningInstances|Integer|2|运行中的实例个数

 |
|CurrentPage|Integer|1|当前页数

 |
|PageSize|Integer|20|页大小

 |
|TotalSize|Integer|2|应用总个数

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附加信息

 |
|RequestId|String|B4D805CA-926D-41B1-8E63-7AD0C1EDBE8A|请求ID

 |
|Success|Boolean|true|是否成功标识

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
		"PageSize":10,
		"Applications":[
			{
				"RunningInstances":0,
				"RegionId":"cn-beijing",
				"AppId":"f7730764-d88f-4b9a-8d8e-cd8efbfee1f0",
				"Instances":2,
				"AppName":"xxxx",
				"AppDeletingStatus":false
			},
			{
				"RunningInstances":0,
				"RegionId":"cn-beijing",
				"AppId":"a4a60839-3464-4d7b-8b33-9e8697b7b156",
				"Instances":1,
				"AppName":"xxxxx",
				"AppDeletingStatus":false
			}
		],
		"TotalSize":2,
		"CurrentPage":1
	},
	"Message":"success",
	"RequestId":"B4D805CA-926D-41B1-8E63-7AD0C1EDBE8A",
	"Success":true,
	"ErrorCode":"success",
	"Code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

