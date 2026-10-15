# Source: https://developers.effilink.co/api-reference/v5/send-abtest.html

# [AB测试发送](https://developers.effilink.co/api-reference/v5/send-abtest.html#ab%E6%B5%8B%E8%AF%95%E5%8F%91%E9%80%81)

更新时间：2023-06-03 09:00

A/B测试是指在大批量发送前将数据按照比例随机抽样，对不同样本进行如主题、内容等差异化发送，以选择效果更好的样本用于大批量的发送，有助于进一步提升邮件营销效果。

### [身份验证](https://developers.effilink.co/api-reference/v5/send-abtest.html#%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81)

验证方式看[这里](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)。

### [建立AB测试发送任务](https://developers.effilink.co/api-reference/v5/send-abtest.html#%E5%BB%BA%E7%AB%8Bab%E6%B5%8B%E8%AF%95%E5%8F%91%E9%80%81%E4%BB%BB%E5%8A%A1)

POST /v5/campaign/mail/sends\_abtest

向指定的单个或多个联系组的人群发送指定的内容，调用此方法前请确保已经把人群数据[导入到对应的联系组](https://developers.effilink.co/api-reference/v5/contacts.html#%E6%89%B9%E9%87%8F%E5%AF%BC%E5%85%A5%E8%81%94%E7%B3%BB%E4%BA%BA)中。

**请求参数**

| 名称 | 类型 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- | --- |
| **mailName** | string | 是 | 邮件任务名称，最大200 byte。如到期未产生优胜者，则继续使用此主版本的主题和内容进行发送 | AB测试邮件任务01 |
| **subject** | string | 是 | 邮件主题 | AB测试邮件 |
| **content** | string | 是 | 邮件内容 | AB测试邮件\_邮件内容 |
| **senderName** | string | 是 | 发送方名称 | 发送方Example |
| **senderMail** | string | 是 | 发送方邮箱 | norply@market.domain.com |
| **replyTo** | string | 否 | 回复地址 | reply@market.domain.com |
| **sendDate** | string | 否 | 发送时间。不填时为立即发送。发送时间值不能晚于当前时间30天。使用UTC时间按照ISO8601标准，格式为YYYY-MM-DDThh:mm:ssZ。 | 如，北京时间2023年1月10日20点0分0秒表示为2023-01-10T12:00:00Z。 |
| **sendListNames** | array\[string\] | 是 | 发送组名称列表。各发送组对应的联系人总数不能少于10个 | \["发送组01","发送组02"\] |
| **repelListNames** | array\[string\] | 否 | 排斥组名称列表 | \["排斥组01"\] |
| **abTestVersions** | array\[object\] | 是 | AB测试其他版本内容配置。其他版本数量最少为1，最大为4。其中subject和content按需使用，但一个版本中不可都不填 | |
| **abTestVersions.subject** | object | 否 | AB测试该版本的邮件主题 | AB测试邮件B |
| **abTestVersions.content** | object | 否 | AB测试该版本的邮件内容 | AB测试邮件\_邮件内容B |
| **timeLimit** | string | 是 | 测试期限（单位：小时） | 1 |
| **percent** | string | 是 | 测试版本百分比。各测试版本百分比相同，剩余百分比即胜出版本的发送量。 | 10 |
| **abTestType** | string | 否 | AB测试指标类型。取值范围：open、click。打开率（open），点击率（click），默认open | click |

请求示例

```
{
	"mailName": "AB测试邮件任务01",
	"subject": "AB测试邮件",
	"content": "AB测试邮件_邮件内容",
	"senderName": "发送方Example",
	"senderMail": "norply@market.domain.com",
	"replyTo": "reply@market.domain.com",
	"sendDate": "2023-03-10T12:00:00Z",
	"sendListNames": [
		"发送组01",
		"发送组02"
	],
	"repelListNames": [
		"排斥组01"
	],
	"abTestVersions": [
		{
			"subject": "AB测试邮件B",
			"content": "AB测试邮件_邮件内容B"
		}
	],
	"timeLimit": 1,
	"percent": 10,
	"abTestType": "click"
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

常见返回值说明

| code | message | 说明 |
| --- | --- | --- |
| **400** | 参数不足 | 有必填参数未填写 |
| **400** | mailName超长 | mailName参数值超过允许的最大长度 |
| **400** | 发送时间值非法 | sendDate参数值的格式不正确 |
| **403** | 发送时间值不能早于当前时间1小时 | sendDate参数值过早 |
| **403** | 发送时间值不能晚于当前时间30天 | sendDate参数值过晚 |
| **400** | 未填写发送组 | 未填写sendListNames参数 |
| **400** | 未填写AB测试其他版本 | 未填写abTestVersions参数 |
| **400** | AB测试版本最多支持5个 | abTestVersions参数中的版本数最多为4个 |
| **400** | AB测试版本中Subject和Content不可都为空 | abTestVersions参数中的Subject和Content不可都为空 |
| **400** | timeLimit范围仅支持1-100（小时） | timeLimit值的范围为1-100 |
| **400** | percent结合版本数量已超过100% | percent值与版本数叠加超过了100% |
| **400** | 不支持的abTestType类型 | abTestType参数值不在允许值的范围 |
| **500** | 添加邮件任务失败 | |
| **500** | 创建AB测试邮件任务失败 | 此时会保留此次创建的主版本邮件任务 |
| **500** | AB测试邮件任务检查未通过 | 此时会保留此次创建的所有版本的AB测试邮件任务 |