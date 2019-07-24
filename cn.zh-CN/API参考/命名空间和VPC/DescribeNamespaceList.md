# DescribeNamespaceList {#doc_api_sae_DescribeNamespaceList .reference}

获取命名空间列表

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=sae&api=DescribeNamespaceList&type=ROA&version=2019-05-06)

## 请求头 {#requestHeadList .section}

该接口使用公共请求头，无特殊请求头。请参见公共请求参数文档。

## 请求语法 {#requestGrammer .section}

```
GET /pop/v1/sam/namespace/describeNamespaceList HTTP/1.1
```

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|ContainCustom|Boolean|是|true|是否返回自定义命名空间

 |
|HybridCloudExclude|Boolean|否|true|是否排除混合云命名空间

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Code|String|200|接口状态

 |
|Data| | |命名空间列表

 |
|AgentInstall|String|http://edas-bj.oss-cn-beijing-internal.aliyuncs.com/test/install.sh|EDAS Agent安装命令

 |
|Current|Boolean|false|已废弃

 |
|Custom|Boolean|true|自定义命名空间

 |
|HybridCloudEnable|Boolean|false|混合云命名空间

 |
|NamespaceId|String|cn-beijing:test|命名空间ID

 |
|NamespaceName|String|test|命名空间名称

 |
|RegionId|String|cn-beijing|命名空间归属的Region

 |
|VSwitchId|String|vsw-2ze559r1z1bpwqxwpa8o9|VSwitch ID

 |
|VpcId|String|vpc-2ze0i263cnn311nvji7jj|VPC ID

 |
|ErrorCode|String|success|错误码

 |
|Message|String|success|附加信息

 |
|RequestId|String|30375C38-F4ED-4135-A0AE-5C75DC7F7B3F|请求ID

 |
|Success|Boolean|true|是否成功标识

 |
|TraceId|String|ac1a0b2215622920113732501e6d56|调用ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://[Endpoint]/?<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeNamespaceListResponse>
	  <Message>success</Message>
	  <RequestId>30375C38-F4ED-4135-A0AE-5C75DC7F7B3F</RequestId>
	  <TraceId>ac1a0b2215622920113732501e6d56</TraceId>
	  <Data>
		    <NamespaceName>华北2</NamespaceName>
		    <VpcId>vpc-2ze0i263cnn311nvji7jj</VpcId>
		    <VSwitchId>vsw-2ze559r1z1bpwqxwpa8o9</VSwitchId>
		    <AgentInstall>http://edas-bj.oss-cn-beijing-internal.aliyuncs.com/test/install.sh</AgentInstall>
		    <Custom>false</Custom>
		    <RegionId>cn-beijing</RegionId>
		    <NamespaceId>cn-beijing</NamespaceId>
		    <Current>false</Current>
		    <HybridCloudEnable>false</HybridCloudEnable>
	  </Data>
	  <Data>
		    <NamespaceName>xxx</NamespaceName>
		    <AgentInstall>http://edas-qd.oss-cn-qingdao-internal.aliyuncs.com/test/install.sh</AgentInstall>
		    <Custom>true</Custom>
		    <RegionId>cn-beijing</RegionId>
		    <NamespaceId>cn-beijing:xxx</NamespaceId>
		    <Current>false</Current>
		    <HybridCloudEnable>false</HybridCloudEnable>
	  </Data>
	  <ErrorCode>success</ErrorCode>
	  <Code>200</Code>
	  <Success>true</Success>
</DescribeNamespaceListResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"Data":[
		{
			"AgentInstall":"http://edas-bj.oss-cn-beijing-internal.aliyuncs.com/test/install.sh",
			"NamespaceName":"华北2",
			"RegionId":"cn-beijing",
			"HybridCloudEnable":false,
			"Custom":false,
			"VSwitchId":"vsw-2ze559r1z1bpwqxwpa8o9",
			"VpcId":"vpc-2ze0i263cnn311nvji7jj",
			"Current":false,
			"NamespaceId":"cn-beijing"
		},
		{
			"AgentInstall":"http://edas-qd.oss-cn-qingdao-internal.aliyuncs.com/test/install.sh",
			"NamespaceName":"xxx",
			"RegionId":"cn-beijing",
			"HybridCloudEnable":false,
			"Custom":true,
			"Current":false,
			"NamespaceId":"cn-beijing:xxx"
		}
	],
	"Message":"success",
	"RequestId":"30375C38-F4ED-4135-A0AE-5C75DC7F7B3F",
	"TraceId":"ac1a0b2215622920113732501e6d56",
	"Success":true,
	"ErrorCode":"success",
	"Code":200
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/sae)查看更多错误码。

