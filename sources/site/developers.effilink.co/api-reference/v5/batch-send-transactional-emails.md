# Source: https://developers.effilink.co/api-reference/v5/batch-send-transactional-emails.html

# [批量发送个性化事务邮件](https://developers.effilink.co/api-reference/v5/batch-send-transactional-emails.html#%E6%89%B9%E9%87%8F%E5%8F%91%E9%80%81%E4%B8%AA%E6%80%A7%E5%8C%96%E4%BA%8B%E5%8A%A1%E9%82%AE%E4%BB%B6)

更新时间：2024-01-05 09:50

如果您想发送一批事务邮件，这些邮件使用相同的模板，但每封邮件都有个性化的动态内容。您不需要为每封邮件调用一次API接口，可以在一次请求中最多传递最多100套个性化内容。EffiLink 接口将把模板与个性化内容组装成邮件投递出去。

### [身份验证](https://developers.effilink.co/api-reference/v5/batch-send-transactional-emails.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [建立发送任务](https://developers.effilink.co/api-reference/v5/batch-send-transactional-emails.html#%E5%BB%BA%E7%AB%8B%E5%8F%91%E9%80%81%E4%BB%BB%E5%8A%A1)

POST /v5/transactional/mail/sends\_customised

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **subject** | string | 否 | 邮件主题。和templateName参数对应的模板subject二选一必填，都有值时，优先采用此参数值。支持个性化标签，使用方式和content参数中的个性化标签一致。 | 欢迎邮件 |
| **content** | string | 否 | 邮件内容。和templateName参数二选一必填，都有值时，优先采用templateName。邮件内容中使用个性化标签的话，要注意标签的格式为：{{xxx}} | |
| **templateName** | string | 否 | 邮件模板名称。和content参数二选一必填，都有值时，优先采用templateName。邮件模板内容中使用个性化标签的话，要注意标签的格式为：{{xxx}} | |
| **params** | object | 否 | 邮件内容个性化标签值。按邮件内容中是否存在标签，来对应使用 | |
| **senderMail** | string | 是 | 发送方邮箱 | norply@market.domain.com |
| **senderName** | string | 否 | 发送方名称，最大200 byte | 发送方Example |
| **replyTo** | string | 否 | 回复地址 | reply@market.domain.com |
| **sendDate** | string | 否 | 发送时间。不填时为立即发送。使用UTC时间按照ISO8601标准，格式为YYYY-MM-DDThh:mm:ssZ。 | 如，北京时间2023年1月10日20点0分0秒表示为2023-01-10T12:00:00Z。 |
| **messageVersions** | array\[object\] | 是 | 邮件个性化发送配置，可再以多个版本来划分个性化内容和对应收件人范围 | |
| **messageVersions.to** | array\[object\] | 是 | 该版本对应的邮件收件人。单版本最大数量20个。 | |
| **messageVersions.to.email** | string | 是 | 收件人邮箱 | zhangsan@easeye.com.cn |
| **messageVersions.to.name** | string | 否 | 收件人名称，最大100 byte | 张三 |
| **messageVersions.cc** | array\[object\] | 是 | 该版本对应的邮件抄送人。单版本最大数量20个。 | |
| **messageVersions.cc.email** | string | 是 | 抄送人邮箱 | lisi@easeye.com.cn |
| **messageVersions.cc.name** | string | 否 | 抄送人名称，最大100 byte | 李四 |
| **messageVersions.bcc** | array\[object\] | 是 | 该版本对应的邮件密抄送人。单版本最大数量20个。 | |
| **messageVersions.bcc.email** | string | 是 | 密抄送人邮箱 | wangwu@easeye.com.cn |
| **messageVersions.bcc.name** | string | 否 | 密抄送人名称，最大100 byte | 王五 |
| **messageVersions.subject** | string | 否 | 该版本的邮件主题，**优先级更高** | |
| **messageVersions.content** | string | 否 | 该版本的邮件内容，逻辑和全局参数类似，**但优先级更高** | |
| **messageVersions.templateName** | string | 否 | 该版本的邮件模板名称，逻辑和全局参数类似，**但优先级更高**，高于content | |
| **messageVersions.params** | object | 否 | 该版本的邮件内容个性化标签值。与基础params使用类似，并且与基础params中标签相同时，此版本中的标签值**优先级更高** | |
| **category** | string | 否 | 邮件类别。用以标识一封邮件所属类别，方便报表查询。最长100 byte，只支持大小写字母和阿拉伯数字 | 设置邮件类别为触发场景名称，比如账单邮件的类别可以是：bill；注册邮件的类别可以是：registration; |
| **campaign** | string | 否 | 邮件任务名称。最长100 byte，只支持大小写字母和阿拉伯数字 | 设置任务名称为用户传入的任务名称（如果有的话），或者“类别名称+触发日期”，比如bill\_201607或者registration\_20170207; |
| **trackOpen** | int | 否 | 是否跟踪邮件打开 | 为1时跟踪，其他值不跟踪 |
| **trackClick** | int | 否 | 是否跟踪邮件点击 | 为1时跟踪，其他值不跟踪 |
| **uniqueMsgID** | string | 否 | 用以唯一标识一封邮件（对请求方），在系统中作为外键存在。最大长度50 byte； | sendseqid-89897254234 |
| **attachment** | object | 否 | 邮件附件。仅支持一个文件 | |
| **attachment.fileName** | string | 是 | 邮件附件的文件名 | 附件文件01.txt |
| **attachment.fileData** | string | 是 | 邮件附件的文件内容，为用base64编码后的字符串 | MTIzNDU2 |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"subject": "欢迎邮件",
	"content": "<!DOCTYPE html><html><body>全局邮件内容：<p>{{paragraphText}}</p></body></html>",
	"params": {
		"paragraphText": "段落部分的个性化文本"
	},
	"senderMail": "norply@market.domain.com",
	"senderName": "发送方Example",
	"replyTo": "reply@market.domain.com",
	"sendDate": "2023-03-10T12:00:00Z",
	"messageVersions": [
		{
			"to": [
				{
					"email": "zhangsan@easeye.com.cn",
					"name": "张三"
				}
			],
			"cc": [
				{
					"email": "lisi@easeye.com.cn",
					"name": "李四"
				}
			],
			"bcc": [
				{
					"email": "wangwu@easeye.com.cn",
					"name": "王五"
				}
			]
		},
		{
			"to": [
				{
					"email": "lisi@easeye.com.cn",
					"name": "李四"
				},
				{
					"email": "wangwu@easeye.com.cn",
					"name": "王五"
				}
			],
			"subject": "欢迎邮件_新版本",
			"templateName": "邮件模板_新版本",
			"params": {
				"paragraphText": "段落部分的个性化文本_版本1"
			}
		}
	],
	"category": "bill",
	"campaign": "registration_20170207",
	"trackOpen": 1,
	"trackClick": 1,
	"uniqueMsgID": "sendseqid-89897254234",
	"attachment": {
		"fileName": "附件文件01.txt",
		"fileData": "MTIzNDU2"
	}
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

常见返回值说明

| code | message | 说明 |
| --- | --- | --- |
| **400** | 参数不足 | 有必填参数未填写 |
| **400** | 发送时间值格式不正确 | sendDate参数值的格式不正确 |
| **400** | category字段值超长 | category参数值超过允许的最大长度 |
| **400** | campaign字段值超长 | campaign参数值超过允许的最大长度 |
| **400** | uniqueMsgID字段值超长 | uniqueMsgID参数值超过允许的最大长度 |
| **400** | 请填写收件人 | 未填写messageVersions中的to参数值 |
| **400** | messageVersions中的收件人未填写 | 未填写messageVersions中的to中的email参数值 |
| **400** | 未找到messageVersions中对应名称的邮件模板 | messageVersions中的templateName参数值未查询到对应的邮件模板 |
| **400** | 发送方名称超长 | senderName参数值超过允许的最大长度 |
| **403** | 发送方地址不存在 | senderMail未对应该账户的发送方配置 |
| **400** | 回复地址不合法 | replyTo未通过邮箱格式校验 |
| **400** | 请填写邮件内容 | content和templateName都未填写 |
| **403** | 未找到对应名称的邮件模板 | templateName参数值未查询到对应的邮件模板 |
| **403** | 点数不足 | 该账户的邮件点数不足 |