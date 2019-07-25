# DescribeChangeOrder {#doc_api_sae_DescribeChangeOrder .reference}

查询变更单信息

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeChangeOrder&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/changeorder/DescribeChangeOrder HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ChangeOrderId|String|是|76fa5c0-9ebb-4bb4-b383-1f885447b109|变更单ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |变更单信息

 |
|AppName|String|app-test|应用名称

 |
|Auto|Boolean|true|是否为自动分批

 |
|BatchCount|Integer|1|分批数

 |
|BatchType|String|自动|分批类型

 |
|BatchWaitTime|Integer|0|自动分批方式，等待多长时间开始下一批次，单位：分钟

 |
|ChangeOrderId|String|765fa5c0-9ebb-4bb4-b383-1f885447b109|变更单ID

 |
|CoType|String|变更类型|创建应用

 |
|CoTypeCode|String|CoCreateApp|变更类型CODE

 |
|CreateTime|String|2019-07-11 15:54:49|创建时间

 |
|CurrentPipelineId|String|06-ba2d-46ea-9e79-0727fbca6eda|当前批次ID

 |
|Description|String|版本：1.0 | 镜像名称：nginx|变更单描述信息

 |
|ErrorMessage|String|success|错误信息

 |
|Pipelines| | |批次信息

 |
|BatchType|Integer|0|分批类型

 |
|ParallelCount|Integer|0|分批内并行任务数

 |
|PipelineId|String|0cffd-ba2d-46ea-9e79-0727fbca|批次ID

 |
|PipelineName|String|第1批变更|批次名称

 |
|StartTime|Long|1562831689704|开始时间

 |
|Status|Integer|2|批次状态，0：准备 1：执行中 2：执行成功 3：执行失败 6：终止 10：系统异常执行失败

 |
|UpdateTime|Long|1562847178007|最近更新时间

 |
|Status|Integer|2|变更单状态，0：准备 1：执行中 2：执行成功 3：执行失败 6：终止 10：系统异常执行失败

 |
|SupportRollback|Boolean|false|是否支持回滚

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
GET /pop/v1/sam/changeorder/DescribeChangeOrder HTTP/1.1
公共请求头
{
  "ChangeOrderId": "76fa5c0-9ebb-4bb4-b383-1f885447b109"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeChangeOrder>
	  <Message>success</Message>
	  <RequestId>XXXC03A-E74E-467E-B4E2-63E3F5AACF55</RequestId>
	  <TraceId>0bc3915638507554994370d5056</TraceId>
	  <Data>
		    <Status>2</Status>
		    <Description>版本：1.0 | 镜像名称：nginx </Description>
		    <Pipelines>
			      <Status>2</Status>
			      <PipelineName>第1批变更</PipelineName>
			      <ParallelCount>0</ParallelCount>
			      <UpdateTime>1562847178007</UpdateTime>
			      <StartTime>1562831689704</StartTime>
			      <PipelineId>0cffd-ba2d-46ea-9e79-0727fbca6eda</PipelineId>
			      <BatchType>0</BatchType>
		    </Pipelines>
		    <CreateTime>2019-07-11 15:54:49</CreateTime>
		    <ChangeOrderId>765fa5c0-9ebb-4bb4-b383-1f885447b109</ChangeOrderId>
		    <BatchType>自动</BatchType>
		    <AppName>app-test</AppName>
		    <Auto>true</Auto>
		    <CurrentPipelineId>06-ba2d-46ea-9e79-0727fbca6eda</CurrentPipelineId>
		    <CoTypeCode>CoCreateApp</CoTypeCode>
		    <SupportRollback>false</SupportRollback>
		    <BatchWaitTime>0</BatchWaitTime>
		    <CoType>创建应用</CoType>
		    <BatchCount>1</BatchCount>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
</DescribeChangeOrder>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"Description":"版本：1.0 | 镜像名称：nginx ",
		"BatchType":"自动",
		"CoType":"创建应用",
		"ChangeOrderId":"765fa5c0-9ebb-4bb4-b383-1f885447b109",
		"SupportRollback":false,
		"Status":2,
		"BatchCount":1,
		"CoTypeCode":"CoCreateApp",
		"CreateTime":"2019-07-11 15:54:49",
		"Auto":true,
		"AppName":"app-test",
		"Pipelines":[
			{
				"ParallelCount":0,
				"Status":2,
				"PipelineName":"第1批变更",
				"BatchType":0,
				"PipelineId":"0cffd-ba2d-46ea-9e79-0727fbca6eda",
				"UpdateTime":1562847178007,
				"StartTime":1562831689704
			}
		],
		"CurrentPipelineId":"06-ba2d-46ea-9e79-0727fbca6eda",
		"BatchWaitTime":0
	},
	"Message":"success",
	"RequestId":"XXXC03A-E74E-467E-B4E2-63E3F5AACF55",
	"TraceId":"0bc3915638507554994370d5056",
	"Success":true,
	"ErrorCode":"success",
	"Code":200
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s 不能为空|
|400|Resouce.no.permission|You are not authorized to operate on the specified resources.|没有权限操作资源|
|400|InvalidChangeOrder.NotFound|The current change order does not exist.|变更单不存在|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

