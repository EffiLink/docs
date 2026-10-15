# Source: https://developers.effilink.co/api-reference/v5/lists.html

# [联系组](https://developers.effilink.co/api-reference/v5/lists.html#%E8%81%94%E7%B3%BB%E7%BB%84)

更新时间：2023-06-03 09:00

联系组是联系人的静态集合。此 API 允许您与联系组进行交互

### [身份验证](https://developers.effilink.co/api-reference/v5/lists.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [添加联系组](https://developers.effilink.co/api-reference/v5/lists.html#%E6%B7%BB%E5%8A%A0%E8%81%94%E7%B3%BB%E7%BB%84)

POST /v5/lists/add

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **listName** | string | 是 | 联系组名称 | 推广活动 |
| **listDescription** | string | 否 | 联系组的描述信息 | 推广活动描述信息 |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
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

### [检索联系组](https://developers.effilink.co/api-reference/v5/lists.html#%E6%A3%80%E7%B4%A2%E8%81%94%E7%B3%BB%E7%BB%84)

POST /v5/lists/get

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **search** | string | 否 | 联系组名称搜索值 | 推广活动 |
| **listType** | string | 否 | 联系组类型 | 取值范围：0、1。动态组（0），静态组（1） |
| **sort** | string | 否 | 排序字段 | 取值范围：CreateDate、ModifyDate。创建时间（CreateDate），更新时间（ModifyDate） |
| **pageSize** | int | 否 | 每页行数。默认值为10 | 10 |
| **pageIndex** | int | 否 | 当前页数。默认值为1 | 1 |

请求示例

```
{
	"search": "推广活动",
	"listType": 1,
	"sort": "CreateDate",
	"pageSize": 10,
	"pageIndex": 1
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **lists** | array\[object\] | 相关联系组数据 |
| **lists.Id** | int | 联系组Id |
| **lists.TeamId** | int | 联系组TeamId |
| **lists.ListName** | string | 联系组名称 |
| **lists.ListStatus** | int | 联系组状态：正常 1 |
| **lists.ListType** | int | 联系组类型：动态组\[0\]；静态组\[1\] |
| **lists.ListFilters** | string | 动态联系组的过滤条件 |
| **lists.CreateUserId** | int | 联系组创建用户Id |
| **lists.CreateDate** | date | 联系组创建时间 |
| **lists.ModifyDate** | date | 联系组修改时间 |
| **totalRecords** | int | 相关联系组的总数量 |

返回示例

```
{
	"code": 200,
	"message": "",
	"lists": [
		{
			"Id": "123",
			"TeamId": "123",
			"listName": "推广活动",
			"ListStatus": 1,
			"ListType": 1,
			"CreateUserId": 123,
			"CreateDate": "2023-10-30T08:15:54.921Z",
			"ModifyDate": "2023-10-30T08:15:54.921Z"
		}
	],
	"totalRecords": 1
}
```

### [删除联系组](https://developers.effilink.co/api-reference/v5/lists.html#%E5%88%A0%E9%99%A4%E8%81%94%E7%B3%BB%E7%BB%84)

POST /v5/lists/delete

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **listName** | string | 是 | 要删除的联系组名 | name1 |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"listName": "name1"
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