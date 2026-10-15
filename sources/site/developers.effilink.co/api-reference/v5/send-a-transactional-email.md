# Source: https://developers.effilink.co/api-reference/v5/send-a-transactional-email.html

# [发送事务邮件](https://developers.effilink.co/api-reference/v5/send-a-transactional-email.html#%E5%8F%91%E9%80%81%E4%BA%8B%E5%8A%A1%E9%82%AE%E4%BB%B6)

更新时间：2024-01-05 09:50

本接口可以用于发送单封的事务类的邮件，可以直接传递完整的邮件内容，也可以调用已存在的模板并添加个性化内容。

### [身份验证](https://developers.effilink.co/api-reference/v5/send-a-transactional-email.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [建立发送任务](https://developers.effilink.co/api-reference/v5/send-a-transactional-email.html#%E5%BB%BA%E7%AB%8B%E5%8F%91%E9%80%81%E4%BB%BB%E5%8A%A1)

POST /v5/transactional/mail/sends\_customised

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **subject** | string | 是 | 邮件主题 | 欢迎邮件 |
| **content** | string | 是 | 邮件内容 | 欢迎邮件\_邮件内容 |
| **senderMail** | string | 是 | 发送方邮箱 | norply@market.domain.com |
| **senderName** | string | 否 | 发送方名称 | 发送方Example |
| **replyTo** | string | 否 | 回复地址 | reply@market.domain.com |
| **sendDate** | string | 否 | 发送时间。不填时为立即发送。使用UTC时间按照ISO8601标准，格式为YYYY-MM-DDThh:mm:ssZ。 | 如，北京时间2023年1月10日20点0分0秒表示为2023-01-10T12:00:00Z。 |
| **to** | object | 是 | 邮件收件人 | |
| **to.email** | string | 是 | 收件人邮箱 | zhangsan@easeye.com.cn |
| **to.name** | string | 否 | 收件人名称 | 张三 |
| **category** | string | 否 | 邮件类别。用以标识一封邮件所属类别，方便报表查询。最长100 byte，只支持大小写字母和阿拉伯数字 | 设置邮件类别为触发场景名称，比如账单邮件的类别可以是：bill；注册邮件的类别可以是：registration; |
| **campaign** | string | 否 | 邮件任务名称。最长100 byte，只支持大小写字母和阿拉伯数字 | 设置任务名称为用户传入的任务名称（如果有的话），或者“类别名称+触发日期”，比如bill\_201607或者registration\_20170207; |
| **trackOpen** | int | 否 | 是否跟踪邮件打开 | 为1时跟踪，其他值不跟踪 |
| **trackClick** | int | 否 | 是否跟踪邮件点击 | 为1时跟踪，其他值不跟踪。<br>如果想**禁用**单个链接的点击追踪，请将 `ef:disable-tracking` 参数（必须小写）添加到链接属性中。 |
| **uniqueMsgID** | string | 否 | 用以唯一标识一封邮件（对请求方），在系统中作为外键存在。最大长度50 byte； | sendseqid-89897254234 |
| **attachment** | object | 否 | 邮件附件。仅支持一个文件 | |
| **attachment.fileName** | string | 是 | 邮件附件的文件名 | 附件文件01.txt |
| **attachment.fileData** | string | 是 | 邮件附件的文件内容，为用base64编码后的字符串 | MTIzNDU2 |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"subject": "欢迎邮件",
	"content": "欢迎邮件_邮件内容",
	"senderMail": "norply@market.domain.com",
	"senderName": "发送方Example",
	"replyTo": "reply@market.domain.com",
	"sendDate": "2023-03-10T12:00:00Z",
	"to": {
		"email": "zhangsan@easeye.com.cn",
		"name": "张三"
	},
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
| **400** | 请填写收件人 | 未填写参数值to |
| **400** | 收件人中邮箱未填写 | 未填写to中的email参数值 |
| **400** | 收件人中邮箱不合法 | to中的email参数值未通过邮箱格式校验 |
| **400** | 发送方名称超长 | senderName参数值超过允许的最大长度 |
| **403** | 发送方地址不存在 | senderMail未对应该账户的发送方配置 |
| **400** | 回复地址不合法 | replyTo未通过邮箱格式校验 |
| **400** | 请填写邮件内容 | content和templateName都未填写 |
| **403** | 未找到对应名称的邮件模板 | templateName参数值未查询到对应的邮件模板 |
| **403** | 点数不足 | 该账户的邮件点数不足 |