# DescribeRegions {#doc_api_sae_DescribeRegions .reference}

使用 DescribeRegions 查询可用地域。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeRegions&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/paas/regionConfig HTTP/1.1
```

## 请求参数 {#parameters .section}

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|Integer|200|接口状态

 |
|Message|String|success|附加信息

 |
|Regions| | |地域列表

 |
|RequestId|String|DDE85827-B0B3-4E56-86E8-17C420090D5C|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
GET /pop/v1/paas/regionConfig HTTP/1.1
公共请求头
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeRegionsResponse>
	  <Message>success</Message>
	  <RequestId>DDE85827-B0B3-4E56-86E8-17C420090D5C</RequestId>
	  <Regions>
		    <Region>
			      <RegionId>cn-shanghai</RegionId>
			      <RegionEndpoint>sae.cn-shanghai.aliyuncs.com</RegionEndpoint>
			      <LocalName>华东2（上海）</LocalName>
		    </Region>
		    <Region>
			      <RegionId>cn-hangzhou</RegionId>
			      <RegionEndpoint>sae.cn-hangzhou.aliyuncs.com</RegionEndpoint>
			      <LocalName>华东1（杭州）</LocalName>
		    </Region>
	  </Regions>
	  <Code>200</Code>
</DescribeRegionsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Message":"success",
	"RequestId":"DDE85827-B0B3-4E56-86E8-17C420090D5C",
	"Regions":{
		"Region":[
			{
				"RegionId":"cn-shanghai",
				"RegionEndpoint":"sae.cn-shanghai.aliyuncs.com",
				"LocalName":"华东2（上海）"
			},
			{
				"RegionId":"cn-hangzhou",
				"RegionEndpoint":"sae.cn-hangzhou.aliyuncs.com",
				"LocalName":"华东1（杭州）"
			}
		]
	},
	"Code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

