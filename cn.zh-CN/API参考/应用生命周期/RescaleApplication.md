# RescaleApplication {#doc_api_sae_RescaleApplication .reference}

应用扩缩

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=RescaleApplication&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
PUT /pop/v1/sam/app/rescaleApplication HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|0099b7be-5f5b-4512-a7fc-56049ef1aa6b|目标应用ID

 |
|Replicas|Integer|是|2|目标实例数

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |返回结果

 |
|ChangeOrderId|String|0e09829f-4914-4612-bc88-6f52fd813c33|发布单ID

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附加信息

 |
|RequestId|String|00000000-0000-0000-0000-000000000000|请求ID

 |
|Success|Boolean|true|是否成功

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
PUT /pop/v1/sam/app/rescaleApplication HTTP/1.1
公共请求头
{
  "AppId": "0099b7be-5f5b-4512-a7fc-56049ef1aa6b"
  "Replicas": "2"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<RescaleApplicationResponse>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <Data>
		    <ChangeOrderId>0e09829f-4914-4612-bc88-6f52fd813c33</ChangeOrderId>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
</RescaleApplicationResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"ChangeOrderId":"0e09829f-4914-4612-bc88-6f52fd813c33"
	},
	"Message":"success",
	"RequestId":"00000000-0000-0000-0000-000000000000",
	"Success":true,
	"ErrorCode":"success",
	"Code":200
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|Application.InvalidStatus|The application status is abnormal. Please try again later.|应用状态异常，请稍后重试。|
|400|Application.NotDeployYet|The application has not been deployed. Please deploy it and try again.|应用没有部署，请部署后重试。|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s 不能为空|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

