# Source: https://developers.effilink.co/api-reference/v5/with-the-smtp-api.html

# [通过 SMTP 发送邮件](https://developers.effilink.co/api-reference/v5/with-the-smtp-api.html#%E9%80%9A%E8%BF%87-smtp-%E5%8F%91%E9%80%81%E9%82%AE%E4%BB%B6)

更新时间：2023-06-03 09:00

### [集成EffiLink SMTP](https://developers.effilink.co/api-reference/v5/with-the-smtp-api.html#%E9%9B%86%E6%88%90effilink-smtp)

1. [创建](https://developers.effilink.co/api-reference/v5/api-key-authentication.html) API Key。 

2. 设置接口的接入点(Host)为：`smtp.effilink.co`。 

3. 用户名可以填充任意字符，长度100字符以内。 

4. 密码请填充`API Key`。 

5. 依据业务需要选择不同端口(Port)。 

提示

- EffiLink 建议将接入点Host设置为 `smtp.effilink.co`，而不是直接指向 EffiLink 的IP地址。EffiLink 的IP地址偶尔会更改（维护或故障转移时），恕不另行通知，硬编码 IP 地址（尤其是没有定期检查更新的方法）可能会导致调用失败。
- 由于API Key足以进行身份验证，EffiLink不会使用SMTP用户名来认证你的请求，但我们建议使用你EffiLink账户的主要联系人邮箱作为用户名。

### [SMTP 端口](https://developers.effilink.co/api-reference/v5/with-the-smtp-api.html#smtp-%E7%AB%AF%E5%8F%A3)

| 业务类型 | 端口 | SSL加密端口 |
| --- | --- | --- |
| **营销推广** | 1026 | 4026 |
| **系统事务** | 1027 | 4027 |

提示

- 1026与1027端口是支持通过STARTTLS升级为加密链路的；
- 避免使用以下弱算法：SSLv3 或 TLS 1.0/1.1，尽可能使用 TLS 1.2 或以上，最好是 TLS 1.3；
- 避免使用以下弱加密套件：RC4, 3DES, AES-CBC, MD5, SHA1, NULL, EXPORT；

### [SMTP 扩展功能](https://developers.effilink.co/api-reference/v5/with-the-smtp-api.html#smtp-%E6%89%A9%E5%B1%95%E5%8A%9F%E8%83%BD)

现在，您已成功与 SMTP 集成，如果有更多的功能需求，请了解如何使用[SMTP 扩展功能](https://developers.effilink.co/api-reference/v5/building-an-x-easeye-header.html)。

### [速率限制](https://developers.effilink.co/api-reference/v5/with-the-smtp-api.html#%E9%80%9F%E7%8E%87%E9%99%90%E5%88%B6)

使用 EffiLink 的 SMTP 发送电子邮件时，必须了解以下速率限制：

- 您可以创建最多100个并发连接。
- 单个邮件的大小限制为不超过10M。

### [SMTP响应码](https://developers.effilink.co/api-reference/v5/with-the-smtp-api.html#smtp%E5%93%8D%E5%BA%94%E7%A0%81)

您的每次 SMTP 调用都会返回一个响应码。`200`响应码通常是调用成功，`400`响应码通常是临时错误，可以重试，`500`响应码是永久错误，不要再继续尝试了。

| 响应码 | 信息 | 说明 |
| --- | --- | --- |
| 250 | ok data code message \[txsID=LYGSPGXH\]; in reply to DATA | 此响应表示接口服务器已接受了邮件。 |
| 530 | Authentication failed. | 认证失败，可能使用了错误的API Key、API 密钥，或账户已过期。 |
| 540 | permission required | 权限未开通，请联系客服人员开通。 |
| 553 | mail from <xxxx@easeye.com.cn1> not allowed<br>code message \[txsID=JT9LSLJZ-1\]; in reply to MAIL | 发送方未在平台登记，还不能使用。如何添加请参考[发件人设置](https://developers.effilink.co/help/mailfrom.html)。 |
| 553 | mail <.xxxx@easeye.123> not allowed<br>(E.g., mailbox syntaxincorrect)<br>codemessage \[txsID=JT9LTF0I-1\]; in reply to RCPT | 接收方地址格式不正确，一个合法的邮件地址需要满足以下要求：<br>@前半部分，可以含有数字、大小写字母、.!#$%&'\*+/=?^\_\`{|}~- 等符号<br>@前半部分，只能字母或数字开头；<br>@前半部分，点不能连续多个，且不能在最后一位<br>@后半部分，可以含有数字、大小写字母、.-；<br>@后半部分，只能字母或数字开头与结尾；<br>@后半部分，点与减号不能连续 |
| 502 | Email content is too large(\[length\]) | 邮件内容太大，超过接口接收的上限，单个邮件的大小不能超过10M。 |
| 452 | Insufficient points error (the account balance<br>(accountId=287,userid=1237,availablePoints=10) is not enough)<br>code message \[txsID=JT9MNEZX-1\]; in reply to DATA | 账户余额不足，请联系客服充值。 |

### [代码示例](https://developers.effilink.co/api-reference/v5/with-the-smtp-api.html#%E4%BB%A3%E7%A0%81%E7%A4%BA%E4%BE%8B)

[点击下载](https://developers.effilink.co/api-reference/%E4%BA%BF%E4%B8%9Asmtp%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8demo_java_2025.zip)使用Java开发的调用Smtp接口示例。