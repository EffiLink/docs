# Source: https://developers.effilink.co/api-reference/v5/api-limits.html

# [API 速率限制](https://developers.effilink.co/api-reference/v5/api-limits.html#api-%E9%80%9F%E7%8E%87%E9%99%90%E5%88%B6)

更新时间：2022-11-03 09:13

EffiLink API是为客户提供的公共接口服务，为了提供尽可能好的体验，我们对API的请求频率做了一定的限制。

### [SMTP 端口速率限制](https://developers.effilink.co/api-reference/v5/api-limits.html#smtp-%E7%AB%AF%E5%8F%A3%E9%80%9F%E7%8E%87%E9%99%90%E5%88%B6)

- 您可以创建最多100个并发连接。
- 单个邮件的大小限制为不超过10M，如果您有发送更大邮件的需求请与客服联系。

### [Web API速率限制](https://developers.effilink.co/api-reference/v5/api-limits.html#web-api%E9%80%9F%E7%8E%87%E9%99%90%E5%88%B6)

Web API主要为批量发送营销邮件设计，默认速率限制如下：

| 接口 | 每小时 | 每秒 |
| --- | --- | --- |
| /v5/transactional | \- | 10 |
| /v5/verified\_senders | 1000 | \- |
| /v5/contacts | 7200 | 2 |
| /v5/campaign | 7200 | 2 |
| 其他 | 1000 | \- |