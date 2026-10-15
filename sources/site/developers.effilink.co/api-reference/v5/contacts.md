# Source: https://developers.effilink.co/api-reference/v5/contacts.html

# [联系人](https://developers.effilink.co/api-reference/v5/contacts.html#%E8%81%94%E7%B3%BB%E4%BA%BA)

更新时间：2023-06-03 09:00

允许在账户中添加、更新和删除联系人，还可以批量导入联系人。

### [身份验证](https://developers.effilink.co/api-reference/v5/contacts.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [添加或更新单个联系人](https://developers.effilink.co/api-reference/v5/contacts.html#%E6%B7%BB%E5%8A%A0%E6%88%96%E6%9B%B4%E6%96%B0%E5%8D%95%E4%B8%AA%E8%81%94%E7%B3%BB%E4%BA%BA)

POST /v5/contacts/upsert

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **name** | string | 否 | 联系人名称。不填写时以email参数为名称值 | 张三 |
| **email** | string | 是 | 联系人的邮箱地址。此值不填写时，则phoneNumber参数为必填 | zhangsan@easeye.com.cn |
| **phoneNumber** | string | 否 | 联系人的联系电话。此值不填写时，则email参数为必填 | 13800000000 |
| **listName** | string | 否 | 将该联系人归于某一联系组 | 123 |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"name": "张三",
	"email": "zhangsan@easeye.com.cn",
	"phoneNumber": "13800000000",
	"listName": "123"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |

返回示例

```
{
	"code": 200,
	"message": ""
}
```

### [批量导入联系人](https://developers.effilink.co/api-reference/v5/contacts.html#%E6%89%B9%E9%87%8F%E5%AF%BC%E5%85%A5%E8%81%94%E7%B3%BB%E4%BA%BA)

POST /v5/contacts/imports

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **contactData** | array\[array\[object\]\] | 是 | 联系人数据 | |
| **contactDataMapping** | array\[object\] | 是 | 联系人数据的映射描述 | |
| **contactDataMapping.columnNum** | int | 是 | 映射序号，从0开始。对应contactData中一组数据的属性值顺序 | 取值范围：0、1，2，... |
| **contactDataMapping.propertyName** | string | 是 | 联系人的属性字段值。其中属性邮箱\[email\]和手机号\[phoneNumber\]不可同时不选择。 | [查看系统预定义属性](https://developers.effilink.co/api-reference/v5/property.html)<br>[查看用户自定义属性](https://app.effilink.co/setting/property)<br>请使用其中的“**标识**”这一列 |
| **updateMode** | int | 是 | 更新方式 | 取值范围：1、2、3。创建和更新（1），只创建新的（2），只更新现有的（3） |
| **listName** | string | 否 | 导入组的名字。 不填写时，仅导入联系人；填写时，若没有对应名称的组则新建组，若有对应名称的组则使用现有组 | 新客户 |
| **listDescription** | string | 否 | 导入组的描述信息。仅在listName参数传递值时生效。 | 拉新注册 |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"contactData": [
		[
			"zhangsan@easeye.com.cn",
			"张三"
		],
		[
			"lisi@easeye.net",
			"李四"
		]
	],
	"contactDataMapping": [
		{
			"columnNum": 0,
			"propertyName": "email"
		},
		{
			"columnNum": 1,
			"propertyName": "name"
		}
	],
	"updateMode": 1,
	"listName": "推广活动",
	"listDescription": "推广活动描述信息"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |

返回示例

```
{
	"code": 200,
	"message": ""
}
```

### [检索单个联系人](https://developers.effilink.co/api-reference/v5/contacts.html#%E6%A3%80%E7%B4%A2%E5%8D%95%E4%B8%AA%E8%81%94%E7%B3%BB%E4%BA%BA)

POST /v5/contacts/get

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **email** | string | 是 | 待查询的联系人邮箱地址 | zhangsan@easeye.com.cn |

请求示例

```
{
	"email": "zhangsan@easeye.com.cn"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **contact** | object | 联系人数据 |
| **contact.id** | string | 联系人Id |
| **contact.name** | string | 联系人名称 |
| **contact.email** | string | 联系人的邮箱地址 |
| **contact.phoneNumber** | string | 联系人的联系电话 |
| **contact.properties** | object | 联系人的属性信息 |
| **contact.createDate** | date | 联系人创建时间 |
| **contact.modifyTime** | date | 联系人最后修改时间 |
| **contact.createUserId** | int | 联系人的创建用户Id |

返回示例

```
{
	"code": 200,
	"message": "",
	"contact": {
		"id": "653f663a17e04f6e5a263de6",
		"name": "张三",
		"email": "zhangsan@easeye.com.cn",
		"phoneNumber": "13800000000",
		"properties": {
			"company_address": "公司地址",
			"email_bounced_flag": "1000",
			"email_bounced_time": "2024-02-21T02:11:11.217Z",
			"cu1262_4": "fen11",
			"cu1262_9": "ds4"
		},
		"createDate": "2023-10-30T08:15:54.921Z",
		"modifyTime": "2025-04-21T05:53:01.089Z",
		"createUserId": 123
	}
}
```

### [检索联系组内的联系人](https://developers.effilink.co/api-reference/v5/contacts.html#%E6%A3%80%E7%B4%A2%E8%81%94%E7%B3%BB%E7%BB%84%E5%86%85%E7%9A%84%E8%81%94%E7%B3%BB%E4%BA%BA)

POST /v5/contacts/list/get

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **listName** | string | 是 | 要查询的联系组名称 | 推广活动 |
| **pageSize** | int | 否 | 每页行数。默认值为200，最大值为1000 | 200 |
| **pageIndex** | int | 否 | 当前页数。默认值为1 | 1 |
| **teamName** | string | 否 | 要指定查询此团队名称对应的联系组。不传值时默认为查询当前团队的联系组。<br>查询其他团队的联系组需开通权限。 | 测试团队 |

请求示例

```
{
	"listName": "zhangsan@easeye.com.cn"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **contactList** | array\[object\] | 联系人数据 |
| **contactList.id** | string | 联系人Id |
| **contactList.name** | string | 联系人名称 |
| **contactList.email** | string | 联系人的邮箱地址 |
| **contactList.phoneNumber** | string | 联系人的联系电话 |
| **contactList.properties** | object | 联系人的属性信息 |
| **contactList.createDate** | date | 联系人创建时间 |
| **contactList.modifyTime** | date | 联系人最后修改时间 |
| **contactList.createUserId** | int | 联系人的创建用户Id |

返回示例

```
{
	"code": 200,
	"message": "",
	"requestId": "c099390b486c4d6fb8a62ca5153c9805",
	"contactList": [
		{
			"id": "653f663a17e04f6e5a263de6",
			"name": "张三",
			"email": "zhangsan@easeye.com.cn",
			"phoneNumber": "13800000000",
			"properties": {
				"company_address": "公司地址1",
				"email_bounced_flag": "1000",
				"email_bounced_time": "2024-02-21T02:11:11.217Z",
				"cu1262_4": "fen11",
				"cu1262_9": "ds4"
			},
			"createDate": "2023-10-30T08:15:54.921Z",
			"modifyTime": "2025-04-21T05:53:01.089Z",
			"createUserId": 123
		},
		{
			"id": "653f663a17e04f6e5a263de7",
			"name": "李四",
			"email": "lisi@easeye.com.cn",
			"phoneNumber": "13900000000",
			"properties": {
				"company_address": "公司地址2",
				"email_bounced_flag": "1000",
				"email_bounced_time": "2024-02-21T02:11:11.217Z",
				"cu1262_4": "fen22",
				"cu1262_9": "ds5"
			},
			"createDate": "2023-10-30T08:15:54.921Z",
			"modifyTime": "2025-04-21T05:53:01.089Z",
			"createUserId": 123
		}
	]
}
```

### [删除联系人](https://developers.effilink.co/api-reference/v5/contacts.html#%E5%88%A0%E9%99%A4%E8%81%94%E7%B3%BB%E4%BA%BA)

POST /v5/contacts/delete

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **email** | string | 是 | 待删除的联系人邮箱地址 | zhangsan@easeye.com.cn |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"email": "zhangsan@easeye.com.cn"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |

返回示例

```
{
	"code": 200,
	"message": ""
}
```