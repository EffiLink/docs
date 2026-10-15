# Source: https://developers.effilink.co/api-reference/v5/sms-report.html

# [获取短信报表](https://developers.effilink.co/api-reference/v5/sms-report.html#%E8%8E%B7%E5%8F%96%E7%9F%AD%E4%BF%A1%E6%8A%A5%E8%A1%A8)

更新时间：2023-06-03 09:00

可以检索通过接口发送的短信统计数据。

### [身份验证](https://developers.effilink.co/api-reference/v5/sms-report.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [检索任务的统计数据](https://developers.effilink.co/api-reference/v5/sms-report.html#%E6%A3%80%E7%B4%A2%E4%BB%BB%E5%8A%A1%E7%9A%84%E7%BB%9F%E8%AE%A1%E6%95%B0%E6%8D%AE)

POST /v5/sms/stats/get

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
| **mailStatsList** | array\[object\] | 短信统计数据 |
| **mailStatsList.statDate** | string | 统计维度（天） |
| **mailStatsList.sentCount** | int | 发送总数 |
| **mailStatsList.successCount** | int | 发送成功数 |
| **mailStatsList.failCount** | int | 发送失败数 |
| **mailStatsList.reportFailedCount** | int | 发送成功中的反馈失败数 |
| **mailStatsList.chargedPoint** | int | 扣点数 |

返回示例

```
{
	"code": 200,
	"message": "",
    "smsStatsList": [
        {
            "statDate": "2024-09-11",
            "sentCount": 8,
            "successCount": 6,
            "failCount": 2,
            "reportFailedCount": 5,
            "chargedPoint": 6
        }
    ]
}
```