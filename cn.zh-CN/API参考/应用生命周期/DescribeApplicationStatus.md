# DescribeApplicationStatus {#doc_api_sae_DescribeApplicationStatus .reference}

获取应用的状态信息

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationStatus&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/app/describeApplicationStatus HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|0099b7be-5f5b-4512-a7fc-56049ef1aa6b|目标应用ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |返回结果

 |
|AppId|String|0099b7be-5f5b-4512-a7fc-56049ef1aa6b|当前应用ID

 |
|ArmsAdvancedEnabled|String|false|是否开通ARMS高级版

 |
|ArmsApmInfo|String|\{"appId":"0099b7be-5f5b-4512-a7fc-56049ef1aa6b","licenseKey":"d5cgdt5pu0@7303f55292a2d5f"\}|该应用在ARMS侧产品元数据信息

 |
|CreateTime|String|1563373372746|应用创建时间

 |
|CurrentStatus|String|RUNNING|应用当前状态

 |
|LastChangeOrderId|String|1ccc2339-fc19-49aa-bda0-1e7b84977515|上一次执行的发布单ID，未执行过或发布单信息过期则为空

 |
|LastChangeOrderRunning|Boolean|false|上一次发布单是否处于执行中

 |
|LastChangeOrderStatus|String|SUCCESS|上一次发布单状态

 |
|RunningInstances|Integer|1|当前应用运行中的实例数

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
GET /pop/v1/sam/app/describeApplicationStatus HTTP/1.1
公共请求头
{
  "AppId": "0099b7be-5f5b-4512-a7fc-56049ef1aa6b"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeApplicationStatusResponse>
	  <Code>200</Code>
	  <Data>
		    <AppId>0099b7be-5f5b-4512-a7fc-56049ef1aa6b</AppId>
		    <ArmsAdvancedEnabled>false</ArmsAdvancedEnabled>
		    <ArmsApmInfo>
			      <appId>0099b7be-5f5b-4512-a7fc-56049ef1aa6b</appId>
			      <licenseKey>d5cgdt5pu0@7303f55292a2d5f</licenseKey>
		    </ArmsApmInfo>
		    <CreateTime>1563373372746</CreateTime>
		    <CurrentStatus>RUNNING</CurrentStatus>
		    <LastChangeOrderId>1ccc2339-fc19-49aa-bda0-1e7b84977515</LastChangeOrderId>
		    <LastChangeOrderRunning>false</LastChangeOrderRunning>
		    <LastChangeOrderStatus>SUCCESS</LastChangeOrderStatus>
		    <RunningInstances>1</RunningInstances>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <Success>true</Success>
	  <TraceId>000000000000000000000000000000</TraceId>
</DescribeApplicationStatusResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"LastChangeOrderStatus":"SUCCESS",
		"RunningInstances":1,
		"CreateTime":"1563373372746",
		"ArmsAdvancedEnabled":false,
		"AppId":"0099b7be-5f5b-4512-a7fc-56049ef1aa6b",
		"CurrentStatus":"RUNNING",
		"LastChangeOrderId":"1ccc2339-fc19-49aa-bda0-1e7b84977515",
		"ArmsApmInfo":{
			"appId":"0099b7be-5f5b-4512-a7fc-56049ef1aa6b",
			"licenseKey":"d5cgdt5pu0@7303f55292a2d5f"
		},
		"LastChangeOrderRunning":false
	},
	"Message":"success",
	"RequestId":"00000000-0000-0000-0000-000000000000",
	"TraceId":"000000000000000000000000000000",
	"Success":true,
	"ErrorCode":"success",
	"Code":200
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s 不能为空|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

