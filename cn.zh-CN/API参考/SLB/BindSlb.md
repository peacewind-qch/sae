# BindSlb {#doc_api_sae_BindSlb .reference}

为应用绑定SLB

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=BindSlb&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
POST /pop/v1/sam/app/slb HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|0099b7be-5f5b-4512-a7fc-56049ef1aa6b|部署成功的目标应用ID

 |
|Internet|String|否|\[\{"port":80,"targetPort":8080,"protocol":"TCP"\}\]|绑定公网SLB。例如: \\\{"port":80,"targetPort":8080,"protocol":"TCP"\}\\，表示将容器的8080端口通过slb的80端口暴露服务，协议为TCP，为空忽略。

 |
|Intranet|String|否|\[\{"port":80,"targetPort":8080,"protocol":"TCP"\}\]|绑定私网SLB。例如: \\\{"port":80,"targetPort":8080,"protocol":"TCP"\}\\，表示将容器的8080端口通过slb的80端口暴露服务，协议为TCP，为空忽略。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |返回结果

 |
|ChangeOrderId|String|01db03d3-3ee9-48b3-b3d0-dfce2d88ab31|返回的发布单ID，用于查询任务执行状态。

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
POST /pop/v1/sam/app/slb HTTP/1.1
公共请求头
{
  "AppId": "0099b7be-5f5b-4512-a7fc-56049ef1aa6b"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<BindSlb>
	  <Data>
		    <ChangeOrderId>01db03d3-3ee9-48b3-b3d0-dfce2d88ab31</ChangeOrderId>
	  </Data>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <TraceId>000000000000000000000000000000</TraceId>
	  <Success>true</Success>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
</BindSlb>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"ChangeOrderId":"01db03d3-3ee9-48b3-b3d0-dfce2d88ab31"
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
|400|Application.ChangerOrderRunning|An application change process is in progress. Please try again later.|应用有变更流程正在执行，请稍后重试。|
|400|Application.InvalidStatus|The application status is abnormal. Please try again later.|应用状态异常，请稍后重试。|
|400|Application.NotDeployYet|The application has not been deployed. Please deploy it and try again.|应用没有部署，请部署后重试。|
|400|InvalidApplication.NotFound|The current application does not exist.|找不到当前应用|
|400|InvalidParam.ProtocolNotSupport|Only TCP protocol is supported.|不支持指定的协议，只支持TCP协议。|
|400|InvalidParameter.NotEmpty|You must specify the parameter %s.|不合法的参数：%s 不能为空|
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

