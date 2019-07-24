# ConfirmPipelineBatch {#doc_api_sae_ConfirmPipelineBatch .reference}

是否开始一下批次

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ConfirmPipelineBatch&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/changeorder/ConfirmPipelineBatch HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Confirm|Boolean|是|true|是否开始下一批次

 |
|PipelineId|String|是|xxx-xxx-xxx-xxx|批次 ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |批次信息

 |
|PipelineId|String|xxx-xxx-xxx-xxx|批次ID

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附加信息

 |
|RequestId|String|0000-0000-0000-0000|请求ID

 |
|Success|Boolean|true|是否成功

 |
|TraceId|String|000000000000000000000000000000|调用链ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
GET /pop/v1/sam/changeorder/ConfirmPipelineBatch HTTP/1.1
公共请求头
{
  "Confirm": true
  "PipelineId": "xxx-xxx-xxx-xxx"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ConfirmPipelineBatch>
	  <Data>
		    <PipelineId>xxx-xxx-xxx-xxx</PipelineId>
	  </Data>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <TraceId>000000000000000000000000000000</TraceId>
	  <Success>true</Success>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
</ConfirmPipelineBatch>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"PipelineId":"xxx-xxx-xxx-xxx"
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
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s 不能为空|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

