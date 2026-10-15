# Source: https://developers.effilink.co/api-reference/v5/report.html

# [获取营销活动报告](https://developers.effilink.co/api-reference/v5/report.html#%E8%8E%B7%E5%8F%96%E8%90%A5%E9%94%80%E6%B4%BB%E5%8A%A8%E6%8A%A5%E5%91%8A)

更新时间：2023-06-03 09:00

可以检索已发送邮件任务的统计数据。

### [身份验证](https://developers.effilink.co/api-reference/v5/report.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-authentication.html)。

### [检索任务的统计数据](https://developers.effilink.co/api-reference/v5/report.html#%E6%A3%80%E7%B4%A2%E4%BB%BB%E5%8A%A1%E7%9A%84%E7%BB%9F%E8%AE%A1%E6%95%B0%E6%8D%AE)

POST /v5/campaign/mail/stats/get

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **startDate** | string | 是 | 查询的时间范围的起始时间（包含此天）。YYYY-MM-DD格式。 | 2025-05-01 |
| **endDate** | string | 是 | 查询的时间范围的结束时间（包含此天）。YYYY-MM-DD格式。 | 2025-05-31 |
| **mailName** | string | 否 | 邮件任务名称 | 发送任务01 |
| **type** | string | 否 | 邮件任务类型 | 取值范围：MailList、ABTest。普通邮件任务（MailList），AB测试邮件任务（ABTest） |

请求示例

```
{
	"startDate": "2025-05-01",
	"endDate": "2025-05-31",
	"mailName": "发送任务01",
	"type": "MailList"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **mailStatsList** | array\[object\] | 邮件任务统计数据 |
| **mailStatsList.mailName** | string | 邮件任务名称 |
| **mailStatsList.mailSendDate** | timestamp | 邮件任务发送时间 |
| **mailStatsList.sentCount** | int | 邮件任务发送数 |
| **mailStatsList.openCount** | int | 邮件任务打开数 |
| **mailStatsList.clickCount** | int | 邮件任务点击数 |
| **mailStatsList.hardBounce** | int | 邮件任务硬退数 |
| **mailStatsList.softBounce** | int | 邮件任务软退数 |
| **mailStatsList.unsentCount** | int | 邮件任务过滤数 |
| **mailStatsList.unsubscribeCount** | int | 邮件任务退订数 |
| **totalRecords** | int | 查询时间段的邮件任务统计数据总数量 |

返回示例

```
{
	"code": 200,
	"message": null,
	"mailStatsList": [
		{
			"mailName": "发送任务01",
			"mailSendDate": 1747879200000,
			"sentCount": 1,
			"openCount": 0,
			"clickCount": 0,
			"hardBounce": 0,
			"softBounce": 0,
			"unsentCount": 0,
			"unsubscribeCount": 0
		},
		{
			"mailName": "发送任务02",
			"mailSendDate": 1748594566000,
			"sentCount": 1,
			"openCount": 1,
			"clickCount": 1,
			"hardBounce": 0,
			"softBounce": 0,
			"unsentCount": 0,
			"unsubscribeCount": 0
		}
	],
	"totalRecords": 2
}
```