# Source: https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html

# [沙盒模式说明](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html#%E6%B2%99%E7%9B%92%E6%A8%A1%E5%BC%8F%E8%AF%B4%E6%98%8E)

更新时间：2025-01-16 17:13

您可以利用沙盒模式在不影响正式生产环境的前提下，模拟接口调用和业务流程。

凡是支持沙盒模式的方法，都会显式在参数列表中标注当前方法支持沙盒模式，没有标注则不支持沙盒模式。

可以通过如下参数来告知接口，本次请求是沙盒请求：

```
{
    "sandboxMode":true
}
```

### [它是如何工作的？](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html#%E5%AE%83%E6%98%AF%E5%A6%82%E4%BD%95%E5%B7%A5%E4%BD%9C%E7%9A%84)

当接口收到沙盒请求时，对请求数据做完检查后，直接反馈能否运行顺畅，不会对其他的业务数据做任何修改。如下所示，沙盒模式标识已经包含其中。

```
curl --request POST \
     --url https://api.easeye.com.cn/v5/marketing/mail/sends \
     --header 'accept: application/json' \
     --header 'ApiKey: ' \
     --header 'Authorization: ' \
     --header 'Timestamp: ' \
     --header 'content-type: application/json' \
     --data '
{
	"mailName": "发送任务01",
	"subject": "欢迎邮件",
	"content": "欢迎邮件_邮件内容",
	"senderName": "发送方Example",
	"senderMail": "norply@market.domain.com",
	"sendDate": "2023-03-10T12:00:00Z",
	"sendGroupNameList": [
		"发送组01",
		"发送组02"
	],
	"sandboxMode": true
}
'
```

**请求响应**

不会有人收到邮件，也不会建立对应的邮件任务。下面是一个示例响应。

```
{
	"code": 200,
	"message": ""
}
```