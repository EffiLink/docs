# Source: [https://developers.effilink.co/api-reference/v5/sends.html](https://developers.effilink.co/api-reference/v5/sends.html)

# [邮件营销任务](https://developers.effilink.co/api-reference/v5/sends.html#%E9%82%AE%E4%BB%B6%E8%90%A5%E9%94%80%E4%BB%BB%E5%8A%A1)

更新时间：2023-06-03 09:00

营销任务是您在EffiLink，通过任务形式发送电子邮件的方式。

可以建立、删除、检索邮件营销任务，此邮件任务是基于联系组的数据来组装邮件内容的，可以立即发送，也可以定时在未来发送。

### [身份验证](https://developers.effilink.co/api-reference/v5/sends.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [建立发送任务](https://developers.effilink.co/api-reference/v5/sends.html#%E5%BB%BA%E7%AB%8B%E5%8F%91%E9%80%81%E4%BB%BB%E5%8A%A1)

POST /v5/campaign/mail/sends

向指定的单个或多个联系组的人群发送指定的内容，调用此方法前请确保已经把人群数据[导入到对应的联系组](https://developers.effilink.co/api-reference/v5/contacts.html#%E6%89%B9%E9%87%8F%E5%AF%BC%E5%85%A5%E8%81%94%E7%B3%BB%E4%BA%BA)中。

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |  |
| --- | --- | --- | --- | --- | --- |
| **mailName** | string | 是 | 邮件任务名称，最大200 byte | 发送任务01 |  |
| **senderMail** | string | 是 | 发送方邮箱 | [norply@market.domain.com](mailto:norply@market.domain.com) |  |
| **senderName** | string | 否 | 发送方名称。不填写时，默认为senderMail参数的值。 | 发送方Example |  |
| **subject** | string | 否 | 邮件主题 | 欢迎邮件 |  |
| **content** | string | 否 | 邮件内容 | 欢迎邮件_邮件内容 |  |
| **sendDate** | string | 否 | 发送时间。不填时为当前时间。使用UTC时间按照ISO8601标准，格式为YYYY-MM-DDThh:mm:ssZ。 | 如，北京时间2023年1月10日20点0分0秒表示为2023-01-10T12:00:00Z。 |  |
| **onlySave** | boolean | 否 | 是否仅保存邮件任务。 | 取值范围：true、false。仅保存（true），保存并发送（false）。不填写时默认为“false保存并发送” |  |
| **sendListNames** | array[string] | 否 | 发送组名称列表。仅在onlySave为true时非必填，否则为必填值。 | ["发送组01","发送组02"] |  |
| **repelListNames** | array[string] | 否 | 排斥组名称列表 | ["排斥组01"] |  |
| **replyTo** | string | 否 | 回复地址 | [reply@market.domain.com](mailto:reply@market.domain.com) |  |
| **attachment** | object | 否 | 邮件附件。仅支持一个文件 |  |  |
| **attachment.fileName** | string | 是 | 邮件附件的文件名 | 附件文件01.txt |  |
| **attachment.fileData** | string | 是 | 邮件附件的文件内容，为用base64编码后的字符串 | MTIzNDU2 |  |
| **languageCode** | string | 否 | 语言代码。选择邮件语言后，系统模块（如退订）将自动翻译为该语言。取值范围：zh-cn、en、ja、ko、de、tt、es、zh-tw、ar、pt-br、id。值说明：zh-cn（简体中文）、en（英文）、ja（日文）、ko（韩文）、de（德文）、tt（俄文）、es（西班牙文）、zh-tw（繁体中文）、ar（阿拉伯文）、pt-br（葡萄牙文-巴西）、id（印尼文）。 | zh-cn |  |
| **marketName** | string | 否 | 活动名称。将邮件任务关联至活动，以便跟踪并统一管理。需要预先创建好该活动。 | 示例活动01 |  |
| **subscriptName** | string | 否 | 订阅名称。用户订阅电子邮件通讯时，选择性地接收“特定目的”的邮件类型。需要预先创建好该订阅。 | Newsletter | 新闻通讯 |
| **projectCode** | string | 否 | 项目代码。若该项目代码不存在，则自动创建此项目。 | PRJ20260301 |  |
| **editorType** | string | 否 | 编辑器类型，对应UI界面。取值范围：CLASSIC、DRAG。CLASSIC（经典式编辑器），DRAG（拖拽式编辑器)，默认为DRAG。 | CLASSIC |  |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |  |

请求示例

```text
{
	"mailName": "发送任务01",
	"senderMail": "norply@market.domain.com",
	"senderName": "发送方Example",
	"subject": "欢迎邮件",
	"content": "欢迎邮件_邮件内容",
	"sendDate": "2023-03-10T12:00:00Z",
	"sendListNames": [
		"发送组01",
		"发送组02"
	],
	"repelListNames": [
		"排斥组01"
	],
	"replyTo": "reply@market.domain.com",
	"attachment": {
		"fileName": "附件文件01.txt",
		"fileData": "MTIzNDU2"
	},
	"languageCode": "zh-cn",
	"marketName": "示例活动01",
	"subscriptName": "Newsletter | 新闻通讯",
	"projectCode": "PRJ20260301",
	"editorType": "CLASSIC"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **id** | long | 对应的邮件任务ID |
| **guid** | string | 对应的邮件任务GUID |

返回示例

```text
{
	"code": 200,
	"message": "",
	"id": 1120,
	"guid": "915cb709ac96418495fcf4f666f15c0d"
}
```

常见返回值说明

| code | message | 说明 |
| --- | --- | --- |
| **400** | 参数不足 | 有必填参数未填写 |
| **400** | mailName超长 | mailName参数值超过允许的最大长度 |
| **400** | 发送时间值非法 | sendDate参数值的格式不正确 |
| **400** | 邮件附件未填写完整 | 填写了attachment参数，但缺失其中的fileName参数或fileData参数 |
| **400** | 未填写发送组 | 未填写sendListNames参数 |
| **403** | 未找到发送组 | sendListNames参数值未查询到对应的发送组 |
| **403** | 未找到排除组 | repelListNames参数值未查询到对应的排除组 |
| **500** | 创建邮件任务时失败 |  |
| **500** | 添加邮件任务附件时失败 | 此时会保留此次创建的邮件任务 |
| **500** | 邮件任务检查未通过 | 此时会保留此次创建的邮件任务 |

### [取消任务](https://developers.effilink.co/api-reference/v5/sends.html#%E5%8F%96%E6%B6%88%E4%BB%BB%E5%8A%A1)

POST /v5/campaign/mail/cancel

根据名字取消指定的定时邮件任务，已过了发送时间的任务不能取消

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **mailName** | string | 是 | 邮件任务名称 | 邮件任务01 |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```text
{
	"mailName": "邮件任务01"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |

返回示例

```text
{
	"code": 200,
	"message": ""
}
```

### [检索任务](https://developers.effilink.co/api-reference/v5/sends.html#%E6%A3%80%E7%B4%A2%E4%BB%BB%E5%8A%A1)

POST /v5/campaign/mail/get

根据任务名字、邮件主题、发送方等查询邮件任务详情，和它的报表数据。

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **mailName** | string | 否 | 该邮件任务名称相关的邮件任务 | 发送任务01 |
| **subject** | string | 否 | 该邮件主题相关的邮件任务 | 欢迎邮件 |
| **senderMail** | string | 否 | 该发送方邮箱相关的邮件任务 | [norply@market.domain.com](mailto:norply@market.domain.com) |
| **type** | string | 否 | 该邮件任务类型相关的邮件任务 | 取值范围：MailList、ABTest。普通邮件任务（MailList），AB测试邮件任务（ABTest） |
| **allTeam** | boolean | 否 | 查询本团队下的邮件任务、还是本公司下全部团队的邮件任务 | 取值范围：true、false。全部团队（true），本团队（false）。不填写时默认为本团队。查询全部团队任务需开通权限 |
| **pageSize** | int | 否 | 每页行数。默认值为10 | 10 |
| **pageIndex** | int | 否 | 当前页数。默认值为1 | 1 |

请求示例

```text
{
	"mailName": "发送任务01",
	"subject": "欢迎邮件",
	"senderMail": "norply@market.domain.com",
	"type": "MailList",
	"allTeam": false,
	"mailStatus": [-1,2],
	"pageSize": 10,
	"pageIndex": 1
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **mailList** | array[object] | 相关邮件任务数据 |
| **mailList.mailName** | string | 邮件任务名称 |
| **mailList.subject** | string | 邮件主题 |
| **mailList.mailContent** | string | 邮件内容 |
| **mailList.senderName** | string | 发送方名称 |
| **mailList.senderMail** | string | 发送方邮箱 |
| **mailList.replyTo** | string | 回复地址 |
| **mailList.rcptEmails** | array[string] | 联系人邮箱列表 |
| **mailList.repelEmails** | array[string] | 排斥联系人邮箱列表 |
| **mailList.rcptListNames** | array[string] | 联系组名称列表 |
| **mailList.repelListNames** | array[string] | 排斥组名称列表 |
| **mailList.sendByDateTime** | date | 邮件任务发送时间 |
| **mailList.taskType** | string | 邮件任务类型。值范围：普通邮件任务（MailList），AB测试邮件任务（ABTest） |
| **mailList.mailStatus** | int | 邮件任务状态。值范围：草稿（-1）、发送中（1）、发送完成（2）、发送失败（4） |
| **mailList.guid** | string | 邮件任务唯一标识值 |
| **mailList.teamName** | string | 邮件任务所属的团队名称 |
| **mailList.mailStats** | object | 邮件发送统计。仅在mailStatus=2，即发送完成状态时才返回 |
| **mailList.mailStats.sentCount** | int | 邮件任务发送总数 |
| **mailList.mailStats.deliveredCount** | int | 邮件任务送达数 |
| **mailList.mailStats.openCount** | int | 邮件任务打开数 |
| **mailList.mailStats.clickCount** | int | 邮件任务点击数 |
| **mailList.mailStats.hardBounce** | int | 邮件任务硬退数 |
| **mailList.mailStats.softBounce** | int | 邮件任务软退数 |
| **mailList.mailStats.unsentCount** | int | 邮件任务过滤数 |
| **mailList.mailStats.unsubscribeCount** | int | 邮件任务退订数 |
| **languageCode** | string | 语言代码 |
| **marketName** | string | 活动名称 |
| **subscriptName** | string | 订阅名称 |
| **projectCode** | string | 项目代码 |
| **reviewerName** | string | 审核人名称 |
| **totalRecords** | int | 相关邮件任务的总数量 |

返回示例

```text
{
	"code": 200,
	"message": "",
	"mailList": [
		{
			"mailName": "发送任务01",
			"subject": "欢迎邮件",
			"mailContent": "欢迎邮件_邮件内容",
			"senderName": "发送方Example",
			"senderMail": "norply@market.domain.com",
			"replyTo": "reply@market.domain.com",
			"rcptEmails": [
				"zhangsan@easeye.com.cn"
			],
			"repelEmails": [
				"lisi@easeye.com.cn"
			],
			"rcptListNames": [
				"发送组01"
			],
			"repelListNames": [
				"黑名单01"
			],
			"sendByDateTime": 1761199614000,
			"taskType": "MailList",
			"mailStatus": 2,
			"guid": "f1f3cd95c52c4fcfaf9d5658f5364a90",
			"teamName": "测试团队",
			"mailStats": {
				"sentCount": 6,
				"deliveredCount": 3,
				"openCount": 2,
				"clickCount": 1,
				"hardBounce": 0,
				"softBounce": 3,
				"unsentCount": 2,
				"unsubscribeCount": 0
			},
			"languageCode": "zh-cn",
			"marketName": "示例活动01",
			"subscriptName": "Newsletter | 新闻通讯",
			"projectCode": "PRJ20260301",
			"reviewerName": "管理员01"
		}
	],
	"totalRecords": 1
}
```

### [删除任务](https://developers.effilink.co/api-reference/v5/sends.html#%E5%88%A0%E9%99%A4%E4%BB%BB%E5%8A%A1)

POST /v5/campaign/mail/delete

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **mailName** | string | 是 | 邮件任务名称 | 邮件任务01 |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```text
{
	"mailName": "邮件任务01"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |

返回示例

```text
{
	"code": 200,
	"message": ""
}
```
