# AbortAndRollbackChangeOrder {#doc_api_sae_AbortAndRollbackChangeOrder .reference}

中止或回滚变更单

\#\#请求语法

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=AbortAndRollbackChangeOrder&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
PUT /pop/v5/changeorder/ChangeOrderAbortAndRollback HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ChangeOrderId|String|是|xxx-xxxx-xxx-xxxx|变更单ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |变更单信息

 |
|ChangeOrderId|String|xxx-xxxx-xxx-xxxx|变更单ID

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
PUT /pop/v5/changeorder/ChangeOrderAbortAndRollback HTTP/1.1
公共请求头
{
  "ChangeOrderId": "xxx-xxxx-xxx-xxxx"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AbortAndRollbackChangeOrder>
	  <Data>
		    <ChangeOrderId>xxx-xxxx-xxx-xxxx</ChangeOrderId>
	  </Data>
	  <Message>success</Message>
	  <TraceId>000000000000000000000000000000</TraceId>
      <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <Success>true</Success>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
</AbortAndRollbackChangeOrder>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"ChangeOrderId":"xxx-xxxx-xxx-xxxx"
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
|400|Resouce.no.permission|You are not authorized to operate on the specified resources.|没有权限操作资源|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|InvalidChangeOrder.NotFound|The current change order does not exist.|变更单不存在|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

