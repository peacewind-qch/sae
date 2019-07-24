# DescribeInstanceSpecifications {#doc_api_sae_DescribeInstanceSpecifications .reference}

获取应用实例规格信息

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeInstanceSpecifications&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/paas/quota/instanceSpecifications HTTP/1.1
```

## 请求参数 {#parameters .section}

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |实例规格信息

 |
|Cpu|Integer|2000|cpu大小，规格：微核

 |
|Enable|Boolean|true|是否可用

 |
|Id|Integer|4|规格配置ID

 |
|Memory|Integer|4096|内存配置，规格：MB

 |
|SpecInfo|String|通用型4|规格配置名称

 |
|Version|Integer|0|规格配置版本号

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
GET /pop/v1/paas/quota/instanceSpecifications HTTP/1.1
公共请求头
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceSpecifications>
	  <Message>success</Message>
	  <RequestId>3666F8BD-475B-4A0F-813D-330660965</RequestId>
	  <TraceId>0bc3b6e415638596990245792de7</TraceId>
	  <Data>
		    <SpecInfo>通用型1</SpecInfo>
		    <Version>0</Version>
		    <Memory>1024</Memory>
		    <Cpu>1000</Cpu>
		    <Enable>false</Enable>
		    <Id>1</Id>
	  </Data>
	  <Data>
		    <SpecInfo>通用型2</SpecInfo>
		    <Version>0</Version>
		    <Memory>2048</Memory>
		    <Cpu>1000</Cpu>
		    <Enable>true</Enable>
		    <Id>2</Id>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
</DescribeInstanceSpecifications>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":[
		{
			"Cpu":1000,
			"Memory":1024,
			"Enable":false,
			"SpecInfo":"通用型1",
			"Id":1,
			"Version":0
		},
		{
			"Cpu":1000,
			"Memory":2048,
			"Enable":true,
			"SpecInfo":"通用型2",
			"Id":2,
			"Version":0
		}
	],
	"Message":"success",
	"RequestId":"3666F8BD-475B-4A0F-813D-330660965",
	"TraceId":"0bc3b6e415638596990245792de7",
	"Success":true,
	"ErrorCode":"success",
	"Code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

