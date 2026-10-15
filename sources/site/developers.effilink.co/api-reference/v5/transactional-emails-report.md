# Source: https://developers.effilink.co/api-reference/v5/transactional-emails-report.html

# [获取事务邮件发送报表](https://developers.effilink.co/api-reference/v5/transactional-emails-report.html#%E8%8E%B7%E5%8F%96%E4%BA%8B%E5%8A%A1%E9%82%AE%E4%BB%B6%E5%8F%91%E9%80%81%E6%8A%A5%E8%A1%A8)

更新时间：2023-06-03 09:00

可以检索已发送事务邮件任务的统计数据，按天分组。

### [身份验证](https://developers.effilink.co/api-reference/v5/transactional-emails-report.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [检索任务的统计数据](https://developers.effilink.co/api-reference/v5/transactional-emails-report.html#%E6%A3%80%E7%B4%A2%E4%BB%BB%E5%8A%A1%E7%9A%84%E7%BB%9F%E8%AE%A1%E6%95%B0%E6%8D%AE)

POST /v5/transactional/mail/stats/get

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **startDate** | string | 是 | 查询的时间范围的起始时间（包含此天）。YYYY-MM-DD格式。 | 2025-05-01 |
| **endDate** | string | 是 | 查询的时间范围的结束时间（包含此天）。YYYY-MM-DD格式。 | 2025-05-31 |

请求示例

```
{
	"startDate": "2025-05-01",
	"endDate": "2025-05-31"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **mailStatsList** | array\[object\] | 邮件发送统计数据 |
| **mailStatsList.statsDate** | string | 以天为统计粒度 |
| **mailStatsList.sentCount** | int | 当天发送数 |
| **mailStatsList.openCount** | int | 当天打开数 |
| **mailStatsList.clickCount** | int | 当天点击数 |
| **mailStatsList.bounceCount** | int | 当天软退数 |
| **mailStatsList.unsentCount** | int | 当天过滤数 |
| **mailStatsList.unsubscribeCount** | int | 当天退订数 |

返回示例

```
{
    "code": 200,
    "message": null,
    "mailStatsList": [
        {
            "statsDate": "2025-05-01",
            "sentCount": 1,
            "openCount": 1,
            "clickCount": 1,
            "bounceCount": 0,
            "unsentCount": 0,
            "unsubscribeCount": 0
        },
        {
            "statsDate": "2025-05-02",
            "sentCount": 1,
            "openCount": 0,
            "clickCount": 0,
            "bounceCount": 0,
            "unsentCount": 0,
            "unsubscribeCount": 0
        }
    ]
}
```