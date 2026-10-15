# Source: https://developers.effilink.co/api-reference/v5/sms-send.html

# [发送短信](https://developers.effilink.co/api-reference/v5/sms-send.html#%E5%8F%91%E9%80%81%E7%9F%AD%E4%BF%A1)

更新时间：2024-09-10 16:00

向指定的手机号码发送文本短信，支持批量提交手机号码。基于监管要求，短信的内容与签名需要事先在平台添加并提交给运营商审核。

### [身份验证](https://developers.effilink.co/api-reference/v5/sms-send.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [发送短信](https://developers.effilink.co/api-reference/v5/sms-send.html#%E5%8F%91%E9%80%81%E7%9F%AD%E4%BF%A1-1)

POST /v5/sms/sends

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **content** | string | 是 | 短信内容。应包含短信签名，且短信内容匹配短信模板格式。 | 【亿业】短信 |
| **toList** | array\[object\] | 是 | 短信发送集合 | |
| **toList.mobile** | string | 是 | 短信送达的手机号码 | 188xxxx8888 |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"content": "【亿业】全局短信内容",
	"toList": [
		{
			"mobile": "188xxxx6666"
		},
		{
			"mobile": "188xxxx8888"
		},
		{
			"mobile": "188xxxx9999"
		}
	]
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