# Source: https://developers.effilink.co/api-reference/v5/webhook-config.html

# [Webhook配置管理](https://developers.effilink.co/api-reference/v5/webhook-config.html#webhook%E9%85%8D%E7%BD%AE%E7%AE%A1%E7%90%86)

更新时间：2024-09-10 16:00

通过本接口可以设置哪些事件进行推送、推送到哪个接口，并可以进一步按发送方来设置接收接口。

### [身份验证](https://developers.effilink.co/api-reference/v5/webhook-config.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-authentication.html)。

### [检索Webhook配置](https://developers.effilink.co/api-reference/v5/webhook-config.html#%E6%A3%80%E7%B4%A2webhook%E9%85%8D%E7%BD%AE)

POST /v5/webhook/get

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **transEvent** | object | 接收Webhook推送的事件范围。无配置时返回null |
| **transEvent.dropped** | boolean | 是否接收Dropped事件推送 |
| **transEvent.bounced** | boolean | 是否接收Bounced事件推送 |
| **transEvent.delivered** | boolean | 是否接收Delivered事件推送 |
| **transEvent.spamReport** | boolean | 是否接收SpamReport事件推送 |
| **transEvent.opened** | boolean | 是否接收Opened事件推送 |
| **transEvent.clicked** | boolean | 是否接收Clicked事件推送 |
| **transEvent.unsubscribed** | boolean | 是否接收Unsubscribed事件推送 |
| **transCallbackUrl** | string | Webhook推送地址。无配置时返回null |
| **transCallbackUrlExtra** | array\[object\] | Webhook推送对发送方的拓展。无配置时返回null |
| **transCallbackUrlExtra.sender** | string | 该发送方的Webhook配置 |
| **transCallbackUrlExtra.url** | string | 该发送方的Webhook推送地址 |
| **transEnable** | boolean | 是否开启Webhook推送。无配置时返回null |

返回示例1

```
{
    "code": 200,
    "message": null,
    "transEvent": {
        "dropped": true,
        "bounced": true,
        "delivered": true,
        "spamReport": true,
        "opened": true,
        "clicked": true,
        "unsubscribed": true
    },
    "transCallbackUrl": "http://192.168.100.226/h1",
    "transCallbackUrlExtra": [
        {
            "sender": "norply@market.domain.com",
            "url": "http://192.168.100.226/h2"
        }
    ],
    "transEnable": true
}
```

返回示例2

```
{
    "code": 200,
    "message": null,
    "transEvent": null,
    "transCallbackUrl": null,
    "transCallbackUrlExtra": null,
    "transEnable": null
}
```

### [保存Webhook配置](https://developers.effilink.co/api-reference/v5/webhook-config.html#%E4%BF%9D%E5%AD%98webhook%E9%85%8D%E7%BD%AE)

POST /v5/webhook/save

下列请求参数对应参数有值时才保存，不传值时保持原值不变。

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **transEvent** | object | 否 | 配置接收Webhook推送的事件范围 | |
| **transEvent.dropped** | boolean | 否 | 是否接收Dropped事件推送 | 取值范围：true、false。接收该事件推送（true），不接收该事件推送（false） |
| **transEvent.bounced** | boolean | 否 | 是否接收Bounced事件推送 | 取值范围：true、false。接收该事件推送（true），不接收该事件推送（false） |
| **transEvent.delivered** | boolean | 否 | 是否接收Delivered事件推送 | 取值范围：true、false。接收该事件推送（true），不接收该事件推送（false） |
| **transEvent.spamReport** | boolean | 否 | 是否接收SpamReport事件推送 | 取值范围：true、false。接收该事件推送（true），不接收该事件推送（false） |
| **transEvent.opened** | boolean | 否 | 是否接收Opened事件推送 | 取值范围：true、false。接收该事件推送（true），不接收该事件推送（false） |
| **transEvent.clicked** | boolean | 否 | 是否接收Clicked事件推送 | 取值范围：true、false。接收该事件推送（true），不接收该事件推送（false） |
| **transEvent.unsubscribed** | boolean | 否 | 是否接收Unsubscribed事件推送 | 取值范围：true、false。接收该事件推送（true），不接收该事件推送（false） |
| **transCallbackUrl** | string | 否 | Webhook推送地址。需为http://或https://格式 | http://192.168.100.226/h1 |
| **transCallbackUrlExtra** | array\[object\] | 否 | Webhook推送对发送方的拓展 | |
| **transCallbackUrlExtra.sender** | string | 是 | 该发送方的Webhook配置 | norply@market.domain.com |
| **transCallbackUrlExtra.url** | string | 否 | 该发送方的Webhook推送地址。需为http://或https://格式 | http://192.168.100.226/h2 |
| **transCallbackUrlExtraUpdateMode** | string | 否 | Webhook推送对发送方拓展的更新方式 | 支持两种：save、replace。save（有则更新，无则新增。默认），replace（全量覆盖） |
| **transEnable** | boolean | 否 | 是否开启Webhook推送 | 取值范围：true、false。接收Webhook推送（true），不接收Webhook推送（false） |

请求示例1，更新全部设置

```
{
	"transEvent": {
		"dropped": true,
		"bounced": false,
		"delivered": false,
		"spamReport": false,
		"opened": false,
		"clicked": false,
		"unsubscribed": false
	},
	"transCallbackUrl": "http://192.168.100.226/h1",
	"transCallbackUrlExtra": [
		{
			"sender": "norply@market.domain.com",
			"url": "http://192.168.100.226/h2"
		}
	],
	"transCallbackUrlExtraUpdateMode": "replace",
	"transEnable": true
}
```

请求示例2，为一个新发送方添加推送地址。如果该发送方已经配置过，将更新它对应的推送地址，如果不存在则新增相应的推送配置

```
{
	"transCallbackUrlExtra": [
		{
			"sender": "newFrom@market.domain.com",
			"url": "http://192.168.100.226/receive2"
		}
	],
	"transCallbackUrlExtraUpdateMode": "save"
}
```

请求示例3，删除指定发送方对应的推送地址。

```
{
	"transCallbackUrlExtra": [
		{
			"sender": "newFrom@market.domain.com",
			"url": ""
		}
	],
	"transCallbackUrlExtraUpdateMode": "save"
}
```

请求示例4，关闭所有推送

```
{
	"transEnable": false
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