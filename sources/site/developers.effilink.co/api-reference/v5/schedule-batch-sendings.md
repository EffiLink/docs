# Source: https://developers.effilink.co/api-reference/v5/schedule-batch-sendings.html

# [按计划发送事务邮件](https://developers.effilink.co/api-reference/v5/schedule-batch-sendings.html#%E6%8C%89%E8%AE%A1%E5%88%92%E5%8F%91%E9%80%81%E4%BA%8B%E5%8A%A1%E9%82%AE%E4%BB%B6)

更新时间：2024-01-05 09:50

当您需要同时发送大量邮件时，设置定时发送计划会非常方便。如果您短时间内高频次调用API，可能会请求次数上限的问题，如果提前安排发送，可以更容易地提前处理所有API调用。。

### [设置发送时间](https://developers.effilink.co/api-reference/v5/schedule-batch-sendings.html#%E8%AE%BE%E7%BD%AE%E5%8F%91%E9%80%81%E6%97%B6%E9%97%B4)

为了能定时发送，您需要在调用事务邮件发送接口时设置sendDate参数，此参数为ISO8601格式（UTC时区），您可以定时在未来72小时内。

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
	}
}
```