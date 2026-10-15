# Source: https://developers.effilink.co/api-reference/v5/template.html

# [模板管理](https://developers.effilink.co/api-reference/v5/template.html#%E6%A8%A1%E6%9D%BF%E7%AE%A1%E7%90%86)

更新时间：2023-06-03 09:00

管理您的模板。模板是一个 HTML 文件，用于创建营销活动的布局和基本设计。

可以添加邮件模板到 EffiLink 平台中，也可以修改、删除、检索已添加的模板。

### [身份验证](https://developers.effilink.co/api-reference/v5/template.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [新增邮件模板](https://developers.effilink.co/api-reference/v5/template.html#%E6%96%B0%E5%A2%9E%E9%82%AE%E4%BB%B6%E6%A8%A1%E6%9D%BF)

POST /v5/campaign/mail/template/add

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **templateName** | string | 是 | 邮件模板名称，最大250 byte | 欢迎邮件模板01 |
| **templateContent** | string | 是 | 邮件模板内容 | 欢迎邮件\_邮件内容 |
| **templateSubject** | string | 是 | 邮件模板主题 | 欢迎邮件 |
| **editorType** | string | 否 | 编辑器类型，对应UI界面。取值范围：CLASSIC、DRAG。CLASSIC（经典式编辑器），DRAG（拖拽式编辑器)，默认为DRAG。 | CLASSIC |

请求示例

```
{
	"templateName": "欢迎邮件模板01",
	"templateContent": "欢迎邮件_邮件内容",
	"templateSubject": "欢迎邮件",
	"editorType": "CLASSIC"
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

### [检索邮件模板](https://developers.effilink.co/api-reference/v5/template.html#%E6%A3%80%E7%B4%A2%E9%82%AE%E4%BB%B6%E6%A8%A1%E6%9D%BF)

POST /v5/campaign/mail/template/get

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **templateName** | string | 否 | 要指定查询的邮件模板名称 | 欢迎邮件模板01 |
| **pageSize** | int | 否 | 每页行数。默认值为10 | 10 |
| **pageIndex** | int | 否 | 当前页数。默认值为1 | 1 |

请求示例

```
{
	"templateName": "欢迎邮件模板01",
	"pageSize": 10,
	"pageIndex": 1
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **templateList** | array\[object\] | 对返回码的文本描述内容 |
| **templateList.templateName** | string | 邮件模板名称 |
| **templateList.templateContent** | string | 邮件模板内容 |
| **templateList.templateSubject** | string | 邮件模板主题 |
| **templateList.createDate** | Date | 邮件模板的创建时间 |
| **totalRecords** | int | 相关邮件模板的总数量 |

返回示例

```
{
	"code": 200,
	"message": "",
	"templateList": [
		{
			"templateName": "欢迎邮件模板01",
			"templateContent": "欢迎邮件_邮件内容",
			"templateSubject": "欢迎邮件",
			"createDate": "2023-10-30 08:15:54.921"
		}
	],
	"totalRecords": 1
}
```

### [删除邮件模板](https://developers.effilink.co/api-reference/v5/template.html#%E5%88%A0%E9%99%A4%E9%82%AE%E4%BB%B6%E6%A8%A1%E6%9D%BF)

POST /v5/campaign/mail/template/delete

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **templateName** | string | 是 | 要删除的邮件模板名称 | 欢迎邮件模板01 |

请求示例

```
{
	"templateName": "欢迎邮件模板01"
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