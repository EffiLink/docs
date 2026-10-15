# Source: https://developers.effilink.co/api-reference/v5/how-to-send-transactional-emails.html

# [如何发送事务类邮件](https://developers.effilink.co/api-reference/v5/how-to-send-transactional-emails.html#%E5%A6%82%E4%BD%95%E5%8F%91%E9%80%81%E4%BA%8B%E5%8A%A1%E7%B1%BB%E9%82%AE%E4%BB%B6)

更新时间：2023-06-03 09:00

### [通过 API 或 SMTP 发送](https://developers.effilink.co/api-reference/v5/how-to-send-transactional-emails.html#%E9%80%9A%E8%BF%87-api-%E6%88%96-smtp-%E5%8F%91%E9%80%81)

设置帐户并完成身份认证后，您可以通过两种方式开始发送：事务类邮件API 或 SMTP 集成。

在邮件送达率方面，使用 API 或 SMTP 集成没有明显差异——EffiLink 发送电子邮件的实际流程相同。

### [如何选择](https://developers.effilink.co/api-reference/v5/how-to-send-transactional-emails.html#%E5%A6%82%E4%BD%95%E9%80%89%E6%8B%A9)

1. SMTP 是一种仅用于发送的协议，但 事务类邮件 API 不仅允许您发送，还允许您在自己的应用或系统中查看和解析报告数据。该 API 还提供更全面的集成，因此会在发送时报告更具体的错误。
2. 事务类邮件API 的邮件接收速度更快，因为 HTTP 比 SMTP 更简洁，但我们已采取措施帮助您减少使用 SMTP 时的延迟，您可能感觉不到两者之间有太大的差异。如果您需要考虑速度，不妨同时测试这两种方式（包括任何内容生成），看看哪种方式在您的特定环境中总体上速度更快。

要查看 事务类API 和参数的完整列表，请参阅 [事务类邮件 API](https://developers.effilink.co/api-reference/v5/batch-send-transactional-emails.html)；如需查看 SMTP 的完整说明，请参阅 [SMTP 集成](https://developers.effilink.co/api-reference/v5/with-the-smtp-api.html)。