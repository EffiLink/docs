# Source: https://developers.effilink.co/api-reference/v5/sms-batch-send.html

# [批量发送个性化短信](https://developers.effilink.co/api-reference/v5/sms-batch-send.html#%E6%89%B9%E9%87%8F%E5%8F%91%E9%80%81%E4%B8%AA%E6%80%A7%E5%8C%96%E7%9F%AD%E4%BF%A1)

更新时间：2024-01-05 09:50

如果您想发送一批个性化短信，这些短信使用相同的模板，但每个短信都有个性化的动态内容。您不需要为每个短信调用一次API接口，可以在一次请求中最多传递最多100套个性化内容。EffiLink 接口将把模板与个性化内容组装成短信投递出去。

### [身份验证](https://developers.effilink.co/api-reference/v5/sms-batch-send.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [建立发送任务](https://developers.effilink.co/api-reference/v5/sms-batch-send.html#%E5%BB%BA%E7%AB%8B%E5%8F%91%E9%80%81%E4%BB%BB%E5%8A%A1)

POST /v5/sms/sends

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **content** | string | 否 | 短信内容。应包含短信签名，且短信内容匹配短信模板格式。和templateName参数二选一必填，都有值时，优先采用templateName。短信内容中使用个性化标签的话，要注意标签的格式为：{{xxx}} | 【亿业】短信 |
| **templateName** | string | 否 | 短信模板名称。和content参数二选一必填，都有值时，优先采用templateName。短信模板内容中使用个性化标签的话，要注意标签的格式为：{{xxx}} | 短信模板名称 |
| **params** | object | 否 | 短信内容个性化标签值。按短信内容中是否存在标签，来对应使用 | |
| **toList** | array\[object\] | 是 | 短信发送集合 | |
| **toList.mobile** | string | 是 | 短信送达的手机号码 | 188xxxx8888 |
| **toList.content** | string | 否 | 该手机号码对应的个性化短信内容，逻辑和全局参数类似，**但优先级更高** | |
| **toList.templateName** | string | 否 | 该手机号码对应的个性化短信模板名称，逻辑和全局参数类似，**但优先级更高**，高于content | |
| **toList.params** | object | 否 | 该手机号码对应的短信内容个性化标签值。与基础params使用类似，并且与基础params中标签相同时，此版本中的标签值**优先级更高** | |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"content": "【亿业】全局短信内容{{paragraphText}}",
	"templateName": "全局短信模板名称",
	"params": {
		"paragraphText": "短信个性化文本"
	},
	"toList": [
		{
			"mobile": "188xxxx6666"
		},
		{
			"mobile": "188xxxx8888",
			"content": "【亿业】短信188内容"
		},
		{
			"mobile": "188xxxx9999",
			"templateName": "短信模板名称1"
		},
		{
			"mobile": "188xxxx0000",
			"templateName": "短信模板名称1",
			"params": {
				"paragraphText": "短信个性化文本0000"
			}
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