# Source: https://developers.effilink.co/api-reference/v5/senders.html

# [发送方](https://developers.effilink.co/api-reference/v5/senders.html#%E5%8F%91%E9%80%81%E6%96%B9)

更新时间：2023-06-03 09:00

管理或获取你的邮件发送方相关的数据

### [身份验证](https://developers.effilink.co/api-reference/v5/senders.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

## [检索发送方](https://developers.effilink.co/api-reference/v5/senders.html#%E6%A3%80%E7%B4%A2%E5%8F%91%E9%80%81%E6%96%B9)

POST /v5/verified\_senders/get

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **senderEmail** | string | 否 | 要查询的发送方地址。填写时仅返回指定发送方的情况；不填写则返回用户下所有发送方的情况 | norply@market.domain.com |

请求示例

```
{
	"senderEmail": "norply@market.domain.com"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **mailFromDomains** | array\[object\] | 发送方的情况列表 |
| **mailFromDomains.fromDomain** | string | 发送方域名 |
| **mailFromDomains.mxStatus** | int | 发送方的MX检查状态。取值范围：正常（1），异常（0） |
| **mailFromDomains.spfStatus** | int | 发送方的SPF检查状态。取值范围：正常（1），异常（0） |
| **mailFromDomains.dkimStatus** | int | 发送方的DKIM检查状态。取值范围：正常（1），异常（0） |
| **mailFromDomains.dmarcStatus** | int | 发送方的DMARC检查状态。取值范围：正常（1），异常（0） |
| **mailFromDomains.isValidate** | int | 发送方的总检查状态 。取值范围：正常（1），异常（0）。mxStatus、spfStatus、dkimStatus、dmarcStatus值都为1时此值为1，否则值为0 |
| **mailFromDomains.isYiyeDomain** | int | 发送方是否为EffiLink提供的发送方。取值范围：是（1），否 （0） |
| **mailFromDomains.senderType** | int | 发送方的类型。取值范围：营销类（1），事务类（2） |

返回示例

```
{
	"code": 200,
	"message": "",
	"mailFromDomains": [
		{
			"fromDomain": "norply@market.domain.com",
			"mxStatus": 1,
			"spfStatus": 1,
			"dkimStatus": 1,
			"dmarcStatus": 1,
			"isValidate": 1,
			"isYiyeDomain": 1,
			"senderType": 1
		}
	]
}
```

## [添加发送方](https://developers.effilink.co/api-reference/v5/senders.html#%E6%B7%BB%E5%8A%A0%E5%8F%91%E9%80%81%E6%96%B9)

POST /v5/verified\_senders/add

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **senderEmail** | string | 是 | 待添加的发送方地址。非顶级域名 | norply@market.domain.com |
| **senderType** | string | 是 | 发送方地址的类型 | 取值范围：1和2。营销（1），事务（2） |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"senderEmail": "norply@market.domain.com",
	"senderType": "1"
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

## [检验发送方域名](https://developers.effilink.co/api-reference/v5/senders.html#%E6%A3%80%E9%AA%8C%E5%8F%91%E9%80%81%E6%96%B9%E5%9F%9F%E5%90%8D)

POST /v5/verified\_senders/verify

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **fromDomain** | string | 是 | 待检验的发送方 | norply@market.domain.com |
| **selector** | string | 是 | 检验发送方的DKIM时所使用的selector | easeye2007 |

请求示例

```
{
	"fromDomain": "norply@market.domain.com",
	"selector": "easeye2007"
}
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **valid** | boolean | 发送方的总检验结果 |
| **goodMX** | boolean | 发送方MX的检验结果 |
| **goodSPF** | boolean | 发送方SPF的检验结果 |
| **goodDKIM** | boolean | 发送方DKIM的检验结果 |
| **goodDMARC** | boolean | 发送方DMARC的检验结果 |

返回示例

```
{
	"code": 200,
	"message": "",
	"valid": true,
	"goodMX": true,
	"goodSPF": true,
	"goodDKIM": true,
	"goodDMARC": true
}
```

## [删除发送方](https://developers.effilink.co/api-reference/v5/senders.html#%E5%88%A0%E9%99%A4%E5%8F%91%E9%80%81%E6%96%B9)

POST /v5/verified\_senders/delete

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **senderEmail** | string | 是 | 要删除的发送方 | norply@market.domain.com |
| **sandboxMode** | boolean | 否 | 是否使用[沙盒模式](https://developers.effilink.co/api-reference/v5/using-sandbox-mode-to-send-an-email.html) | 取值范围：true、false。使用沙盒模式（true），不使用沙盒模式（false）。不填写时默认为不使用 |

请求示例

```
{
	"senderEmail": "norply@market.domain.com"
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