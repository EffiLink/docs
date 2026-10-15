# Source: https://developers.effilink.co/api-reference/v5/tracking-your-mail.html

# [事务邮件跟踪](https://developers.effilink.co/api-reference/v5/tracking-your-mail.html#%E4%BA%8B%E5%8A%A1%E9%82%AE%E4%BB%B6%E8%B7%9F%E8%B8%AA)

更新时间：2023-06-03 09:00

您可以通过下面的参数来设置是否要对本次请求发送的邮件进行打开或点击追踪。

### [邮件是否跟踪打开与点击](https://developers.effilink.co/api-reference/v5/tracking-your-mail.html#%E9%82%AE%E4%BB%B6%E6%98%AF%E5%90%A6%E8%B7%9F%E8%B8%AA%E6%89%93%E5%BC%80%E4%B8%8E%E7%82%B9%E5%87%BB)

可以设置trackOpen、trackClick来告诉接口，是否要对邮件进行打开跟踪与点击跟踪。设置为“1”时跟踪，不设置或其他值不跟踪。

请求示例

```
{
	"subject": "欢迎邮件",
	"content": "欢迎邮件_邮件内容",
	"senderMail": "norply@market.domain.com",
	"senderName": "发送方Example",
	"to": {
		"email": "zhangsan@easeye.com.cn",
		"name": "张三"
	},
	"trackOpen": 1,
	"trackClick": 1,
	"uniqueMsgID": "sendseqid-89897254234"
}
```