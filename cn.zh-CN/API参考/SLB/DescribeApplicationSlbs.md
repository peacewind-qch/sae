# DescribeApplicationSlbs {#doc_api_sae_DescribeApplicationSlbs .reference}

获取应用SLB配置信息

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeApplicationSlbs&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/app/slb HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|AppId|String|是|017f39b8-dfa4-4e16-a84b-1dcee4b17106|目标应用ID

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态或 POP 错误码

 |
|Data| | |返回结果

 |
|Internet| | |公网SLB配置

 |
|Port|Integer|80|SLB监听端口

 |
|Protocol|String|TCP|支持的协议

 |
|TargetPort|Integer|8080|容器端口

 |
|InternetIp|String|59.74.23.155|公网SLB地址

 |
|Intranet| | |内网SLB配置

 |
|Port|Integer|80|SLB监听端口

 |
|Protocol|String|TCP|支持的协议

 |
|TargetPort|Integer|8080|容器端口

 |
|IntranetIp|String|192.168.2.66|内网SLB地址

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
GET /pop/v1/sam/app/slb HTTP/1.1
公共请求头
{
  "AppId": "017f39b8-dfa4-4e16-a84b-1dcee4b17106"
}
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeApplicationSlbsResponse>
	  <Message>success</Message>
	  <RequestId>7CFB4988-7267-4397-A648-0941471AA0D5</RequestId>
	  <TraceId>0bc3b6e215639348698488298d221e</TraceId>
	  <Data>
		    <InternetIp>112.124.199.136</InternetIp>
		    <Intranet>
			      <TargetPort>8080</TargetPort>
			      <Port>80</Port>
			      <Protocol>TCP</Protocol>
		    </Intranet>
		    <Internet>
			      <TargetPort>8080</TargetPort>
			      <Port>65530</Port>
			      <Protocol>TCP</Protocol>
		    </Internet>
		    <IntranetIp>192.168.0.29</IntranetIp>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
</DescribeApplicationSlbsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":{
		"IntranetIp":"192.168.0.29",
		"InternetIp":"112.124.199.136",
		"Intranet":[
			{
				"Port":80,
				"TargetPort":8080,
				"Protocol":"TCP"
			}
		],
		"Internet":[
			{
				"Port":65530,
				"TargetPort":8080,
				"Protocol":"TCP"
			}
		]
	},
	"Message":"success",
	"RequestId":"7CFB4988-7267-4397-A648-0941471AA0D5",
	"TraceId":"0bc3b6e215639348698488298d221e",
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
|400|InvalidParameter.Obviously|The specified parameter is invalid \{%s\}.|不合法的参数\{%s\}|
|400|InvalidParameter.WithMessage|The parameter is invalid \{%s\}: %s|不合法的参数\{%s\}：%s|

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

