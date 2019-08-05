# DescribeApplicationInstances {#doc_api_sae_DescribeApplicationInstances .reference}

获取应用实例列表

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationInstances&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/app/describeApplicationInstances HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|00000000-0000-0000-0000-000000000000|应用ID

 |
|GroupId|String|是|00000000-0000-0000-0000-000000000000|应用分组ID。请通过 DescribeApplicationGroups 接口获得

 |
|CurrentPage|Integer|否|1|页码

 |
|PageSize|Integer|否|10|页面大小

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |应用实例信息

 |
|CurrentPage|Integer|1|页码

 |
|Instances| | |应用实例列表

 |
|CreateTimeStamp|Long|1558442609000|实例创建时间戳，单位毫秒

 |
|GroupId|String|00000000-0000-0000-0000-000000000000|实例所属分组ID

 |
|GroupId|String|00000000-0000-0000-0000-000000000000|实例所属分组ID

 |
|InstanceContainerIp|String|192.168.1.1|实例内网IP

 |
|InstanceContainerStatus|String|Running|实例运行状态。如 Running 为已启动

 |
|InstanceId|String|00000000-0000-0000-0000-000000000000|实例ID

 |
|PageSize|Integer|10|页码大小

 |
|TotalSize|Integer|30|实例总数

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
GET /pop/v1/sam/app/describeApplicationInstances HTTP/1.1
公共请求头
{
  "AppId": "00000000-0000-0000-0000-000000000000"
  "GroupId": "00000000-0000-0000-0000-000000000000"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeApplicationInstancesResponse>
	  <Data>
		    <PageSize>1</PageSize>
		    <Instances>
			      <CreateTimeStamp>1558442609000</CreateTimeStamp>
			      <InstanceContainerIp>192.168.1.1</InstanceContainerIp>
			      <InstanceId>xxx</InstanceId>
			      <InstanceContainerStatus>Running</InstanceContainerStatus>
			      <GroupId>00000000-0000-0000-0000-000000000000</GroupId>
		    </Instances>
		    <TotalSize>2</TotalSize>
		    <CurrentPage>1</CurrentPage>
	  </Data>
	  <Message>success</Message>
	  <RequestId>00000000-0000-0000-0000-000000000000</RequestId>
	  <TraceId>000000000000000000000000000000</TraceId>
	  <ErrorCode>success</ErrorCode>
	  <Success>true</Success>
	  <Code>200</Code>
</DescribeApplicationInstancesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"PageSize":1,
		"Instances":[
			{
				"CreateTimeStamp":1558442609000,
				"InstanceContainerIp":"192.168.1.1",
				"InstanceId":"xxx",
				"GroupId":"00000000-0000-0000-0000-000000000000",
				"InstanceContainerStatus":"Running"
			}
		],
		"CurrentPage":1,
		"TotalSize":2
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

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

