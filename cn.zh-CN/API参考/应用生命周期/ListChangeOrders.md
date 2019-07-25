# ListChangeOrders {#doc_api_sae_ListChangeOrders .reference}

获取变更单列表

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=ListChangeOrders&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/changeorder/ListChangeOrders HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|145341c-9708-4967-b3ec-24933767fd44|应用ID

 |
|CoStatus|String|否|2|0：准备 1：执行中 2：执行成功 3：执行失败 6：终止 10：系统异常执行失败

 |
|CoType|String|否|CoCreateApp|变更单类型

 |
|CurrentPage|Integer|否|1|当前分页

 |
|Key|String|否|test|模糊查询值

 |
|PageSize|Integer|否|20|分页大小

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |变更单列表信息

 |
|ChangeOrderList| | |变更单列表信息

 |
|AppId|String|164341c-9708-4967-b3ec-24933767fd44|应用ID

 |
|BatchCount|Integer|1|分批数

 |
|BatchType|String|自动|分批类型

 |
|ChangeOrderId|String|7fa5c0-9ebb-4bb4-b383-1f885447b109|变更单ID

 |
|CoType|String|创建应用|变更单类型

 |
|CoTypeCode|String|CoCreateApp|变更单类型CODE

 |
|CreateTime|String|2019-07-11 15:54:49|创建时间

 |
|Description|String|版本：1.0 | 镜像名称：nginx|描述信息

 |
|FinishTime|String|2019-07-11 20:12:58|结束时间

 |
|GroupId|String|c9ecd2-cf6c-46c3-9f20-525de202cf79|分组ID

 |
|Source|String|console|变更单操作入口来源

 |
|Status|Integer|2|0：准备 1：执行中 2：执行成功 3：执行失败 6：终止 10：系统异常执行失败

 |
|CurrentPage|Integer|1|当前分页

 |
|PageSize|Integer|20|分页大小

 |
|TotalSize|Integer|1|变更单总数

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附加信息

 |
|RequestId|String|XXXC03A-E74E-467E-B4E2-63E3F5AACF55|请求ID

 |
|Success|Boolean|true|是否成功

 |
|TraceId|String|0bc3915638507554994370d5056|调用链ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
GET /pop/v1/sam/changeorder/ListChangeOrders HTTP/1.1
公共请求头
{
  "AppId": "145341c-9708-4967-b3ec-24933767fd44"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ListChangeOrders>
	  <Message>success</Message>
	  <RequestId>65E1F-43BA-4D0C-8E61-E4D1337FA9B2</RequestId>
	  <TraceId>0bb6f815638568884597879d60be</TraceId>
	  <Data>
		    <PageSize>20</PageSize>
		    <CurrentPage>1</CurrentPage>
		    <ChangeOrderList>
			      <Status>2</Status>
			      <Description>版本：1.0 | 镜像名称：nginx </Description>
			      <CreateTime>2019-07-11 15:54:49</CreateTime>
			      <ChangeOrderId>7fa5c0-9ebb-4bb4-b383-1f885447b109</ChangeOrderId>
			      <BatchType>自动</BatchType>
			      <Source>console</Source>
			      <GroupId>c9ecd2-cf6c-46c3-9f20-525de202cf79</GroupId>
			      <AppId>164341c-9708-4967-b3ec-24933767fd44</AppId>
			      <CoTypeCode>CoCreateApp</CoTypeCode>
			      <FinishTime>2019-07-11 20:12:58</FinishTime>
			      <CoType>创建应用</CoType>
			      <BatchCount>1</BatchCount>
		    </ChangeOrderList>
		    <TotalSize>1</TotalSize>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
	</ListChangeOrders>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"ChangeOrderList":[
			{
				"Source":"console",
				"Status":2,
				"Description":"版本：1.0 | 镜像名称：nginx ",
				"BatchCount":1,
				"CoTypeCode":"CoCreateApp",
				"FinishTime":"2019-07-11 20:12:58",
				"BatchType":"自动",
				"CreateTime":"2019-07-11 15:54:49",
				"CoType":"创建应用",
				"AppId":"164341c-9708-4967-b3ec-24933767fd44",
				"ChangeOrderId":"7fa5c0-9ebb-4bb4-b383-1f885447b109",
				"GroupId":"c9ecd2-cf6c-46c3-9f20-525de202cf79"
			}
		],
		"PageSize":20,
		"TotalSize":1,
		"CurrentPage":1
	},
	"Message":"success",
	"RequestId":"65E1F-43BA-4D0C-8E61-E4D1337FA9B2",
	"TraceId":"0bb6f815638568884597879d60be",
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

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

