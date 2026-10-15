# Source: https://developers.effilink.co/api-reference/v5/webhook.html

# [Webhook 推送](https://developers.effilink.co/api-reference/v5/webhook.html#webhook-%E6%8E%A8%E9%80%81)

更新时间：2023-06-03 09:00

## [概述](https://developers.effilink.co/api-reference/v5/webhook.html#%E6%A6%82%E8%BF%B0)

平台提供的 Webhook 功能可以在平台处理**邮件事件**时推送对应的事件数据，这意味着您可以近乎实时地接收数据，非常适合日志记录或与监控系统集成。

由于 Webhook 推送将数据传送到您的系统，因此它也非常适合备份和存储事件数据，以满足您自己的数据访问和保留需求。

## [邮件事件类型](https://developers.effilink.co/api-reference/v5/webhook.html#%E9%82%AE%E4%BB%B6%E4%BA%8B%E4%BB%B6%E7%B1%BB%E5%9E%8B)

Webhook 能够推送的邮件事件类型分为两类：投递结果和互动事件

- **已送达、退信、过滤** 等投递结果事件可以帮助您了解，邮件是否成功投递给客户。
- **打开、点击、退订、投诉** 等互动事件可帮助您了解，邮件送达后用户是否正在阅读您的邮件并与之互动。

这两种类型的事件都很重要，平台允许您配置 [Webhook 配置](https://app.effilink.co/setting/webhook)，您可以配置**默认的推送URL**，也可以**根据发送方配置**单独的URL。

## [Webhook数据包结构说明](https://developers.effilink.co/api-reference/v5/webhook.html#webhook%E6%95%B0%E6%8D%AE%E5%8C%85%E7%BB%93%E6%9E%84%E8%AF%B4%E6%98%8E)

1. 数据包是采取**json格式**推送；
2. 单次推送的数据包中会含有多个事件消息，最多**包含1000个事件消息**；
3. 每个事件消息代表一个事件，由若干个字段组成，传递该事件的相关信息；
4. 推送请求的**默认字符集为UTF-8**；
5. 样例数据包如下：

```
POST /easeyewebhookreceive/receive.aspx?id=9787435 HTTP/1.1
content-type: application/json;charset=UTF-8
User-Agent: YiyeWebhooks
Host: www.yiyetest.com
Accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
Connection: keep-alive
Content-Length: 1482

[{
    "Email": "demo1@lsh.com",
    "EventCode": "Delivered",
    "EventType": "3",
    "MailSeqId": 2505070900222412710,
    "ReceiveServer": "lsh-com.mail.protection.outlook.com[52.101.157.80]:25",
    "SenderEmail": "access_log@e-mail.contact.demo.com",
    "SentMailListName": "||",
    "SubmitDateTimeV2": "2025-05-07 09:00:22",
    "TriggeredDateTimeV2": "2025-05-07 09:00:26",
    "UniqueMsgID": "a75c3697-2ade-11f0-96fa-79c1da7ff337",
    "Guid": "5fc54d5fd5dc45fe8b0b55b652bb4169",
    "MailName": "邮件任务-2025-01-08 15:28:26"
},
{
    "BrowserType": "Browser Edge",
    "DeliveredTimeV2": "2025-03-06 15:32:48",
    "Email": "hao.wang@demo2.com",
    "EventCode": "Clicked",
    "EventType": "3",
    "IP": "58.214.47.61",
    "Link": "https://pv.companies.com/exhLogin?locale=zh-CN",
    "MailSeqId": 2503061532475081710,
    "Platform": "Desktop Windows NT &gt;=10",
    "SentMailListName": "||",
    "SubmitDateTimeV2": "2025-03-06 15:32:47",
    "Title": "",
    "TriggeredDateTimeV2": "2025-05-06 16:21:51",
    "UA": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36 Edg/135.0.0.0",
    "UniqueMsgID": "234543534543",
    "Guid": "5fc54d5fd5dc45fe8b0b55b652bb4169",
    "MailName": "邮件任务-2025-01-08 15:28:26"
}]
```

## [Webhook事件说明](https://developers.effilink.co/api-reference/v5/webhook.html#webhook%E4%BA%8B%E4%BB%B6%E8%AF%B4%E6%98%8E)

### [Dropped事件](https://developers.effilink.co/api-reference/v5/webhook.html#dropped%E4%BA%8B%E4%BB%B6)

事件说明：由于各种原因（具体请参考Reason中说明），导致该邮件没有发送；

| 属性名 | 类型 | 说明 |
| --- | --- | --- |
| EventCode | string | "Dropped" |
| Email | string | 接收方Email |
| EventType | string | 邮件的类型，<br>3：事务类邮件；<br>5：营销类邮件； |
| Reason | string | 未发送原因：<br>110：硬退过滤，历史上判定为无效地址而过滤；<br>111：发送策略过滤，按照策略要求被过滤的用户；<br>112：过期，在有效期内未能投递完毕；<br>210：退订过滤，历史上判定为退订用户而过滤； |
| SenderEmail | string | 发送方 |
| SentMailListName | string | 邮件提交时设置的category、campaign，以“||”连接，<br>样例：bill||bill\_202304 |
| TriggeredDateTimeV2 | string | 事件产生的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| UniqueMsgID | string | 邮件提交时设置的唯一标示 |
| Guid | string | 邮件任务的唯一Id |
| MailName | string | 邮件任务的名字 |

Dropped样例：

```
   {
       "EventCode":"Dropped",
       "Email":"test@test.easeye.net",
       "EventType":"3",
       "Reason":"112",
       "SenderEmail":"service@trigger.easeye.com",
       "SentMailListName":"bill||bill_202304",
       "TriggeredDateTimeV2":"2023-10-31 13:54:31",
       "UniqueMsgID":"23230232329",
       "Guid": "16ea5f590b684b5fad38dfcaec37d63e",
       "MailName": "邮件任务-2025-10-28 xxxx"
   }
```

### [Bounced事件](https://developers.effilink.co/api-reference/v5/webhook.html#bounced%E4%BA%8B%E4%BB%B6)

事件说明：由于各种原因（具体请参考Reason中说明），导致该邮件发送失败；

| 属性名 | 类型 | 说明 |
| --- | --- | --- |
| EventCode | string | "Bounced" |
| Email | string | 接收方Email |
| EventType | string | 邮件的类型，<br>3：事务类邮件；<br>5：营销类邮件； |
| Reason | string | 未发送原因：<br>100：硬退，本次投递过程中投递失败，原因是因为该地址是无效地址；<br>101：软退，本次投递过程中投递失败，原因是接收方服务器无法链接成功或者拒信（邮箱已满，或者设置了黑名单，或者判定为垃圾邮件； |
| SenderEmail | string | 发送方 |
| SentMailListName | string | 邮件提交时设置的category、campaign，以“||”连接，<br>样例：bill||bill\_202304 |
| SubmitDateTimeV2 | string | 邮件提交发送的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| TriggeredDateTimeV2 | string | 事件产生的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| UniqueMsgID | string | 邮件提交时设置的唯一标示 |
| FailedCause | string | 投递失败的原因，**需要进行base64解码** |
| Guid | string | 邮件任务的唯一Id |
| MailName | string | 邮件任务的名字 |

Bounced样例：

```
   {
       "EventCode":"Bounced",
       "Email":"test@test.easeye.net",
       "EventType":"3",
       "Reason":"100",
       "SenderEmail":"service@trigger.easeye.com",
       "SentMailListName":"",
       "SubmitDateTimeV2":"2023-10-31 13:54:31",
       "TriggeredDateTimeV2":"2023-10-31 13:54:31",
       "FailedCause":"Cjx0ZXN0QHRlc3QuZWFzZXllLm5ldD46IGhvc3QgdGVzdC5lYXNleWUubmV0WzEuMS4xLjFdIHNhaWQ6IDU1NCBJbnZhbGlkCiAgICByZWNpcGllbnQgKGluIHJlcGx5IHRvIFJDUFQgVE8gY29tbWFuZCkKCgo=",
       "UniqueMsgID":"892032348",
       "Guid": "16ea5f590b684b5fad38dfcaec37d63e",
       "MailName": "邮件任务-2025-10-28 xxxx"
   }
```

### [Delivered事件](https://developers.effilink.co/api-reference/v5/webhook.html#delivered%E4%BA%8B%E4%BB%B6)

事件说明：已送达,邮件已投递到联系人邮箱。

| 属性名 | 类型 | 说明 |
| --- | --- | --- |
| EventCode | string | "Delivered" |
| Email | string | 接收方Email |
| EventType | string | 邮件的类型，<br>3：事务类邮件；<br>5：营销类邮件； |
| SenderEmail | string | 发送方 |
| SentMailListName | string | 邮件提交时设置的category、campaign，以“||”连接，<br>样例：bill||bill\_202304 |
| SubmitDateTimeV2 | string | 邮件提交发送的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| TriggeredDateTimeV2 | string | 事件产生的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| UniqueMsgID | string | 邮件提交时设置的唯一标示 |
| ReceiveServer | string | 接收该信件的邮件服务器 |
| Guid | string | 邮件任务的唯一Id |
| MailName | string | 邮件任务的名字 |

Delivered样例：

```
   {
       "EventCode":"Delivered",
       "Email":"test@test.easeye.net",
       "EventType":"5",
       "ReceiveServer":"test.easeye.net[1.1.1.1]:25",
       "SenderEmail":"service@trigger.easeye.com",
       "SentMailListName":"",
       "SubmitDateTimeV2":"2023-10-31 13:54:31",
       "TriggeredDateTimeV2":"2023-10-31 13:54:31",
       "UniqueMsgID":"892052719",
       "Guid": "16ea5f590b684b5fad38dfcaec37d63e",
       "MailName": "邮件任务-2025-10-28 xxxx"
   }
```

### [Opened事件](https://developers.effilink.co/api-reference/v5/webhook.html#opened%E4%BA%8B%E4%BB%B6)

事件说明：联系人打开了邮件。每次打开都会产生一个此类事件消息；

| 属性名 | 类型 | 说明 |
| --- | --- | --- |
| EventCode | string | "Opened" |
| Email | string | 接收方Email |
| EventType | string | 邮件的类型，<br>3：事务类邮件；<br>5：营销类邮件； |
| SentMailListName | string | 邮件提交时设置的category、campaign，以“||”连接，<br>样例：bill||bill\_202304 |
| SubmitDateTimeV2 | string | 邮件提交发送的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| DeliveredTimeV2 | string | 邮件投递成功的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| TriggeredDateTimeV2 | string | 事件产生的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| UniqueMsgID | string | 邮件提交时设置的唯一标示 |
| IP | string | 事件发生时的客户端IP； |
| Platform | string | 事件发生时的客户端操作系统； |
| BrowserType | string | 事件发生时的客户端软件名称； |
| UA | string | 事件发生时的客户端标识（UserAgent）； |
| Guid | string | 邮件任务的唯一Id |
| MailName | string | 邮件任务的名字 |

Opened样例：

```
   {
       "EventCode":"Opened",
       "BrowserType":"",
       "DeliveredTimeV2":"2023-10-31 13:54:31",
       "Email":"test@test.easeye.net",
       "EventType":"3",
       "IP":"1.1.1.1",
       "Platform":"",
       "SentMailListName":"",
       "SubmitDateTimeV2":"2023-10-31 13:54:31",
       "TriggeredDateTimeV2":"2023-10-31 13:54:31",
       "UA":"Mozilla\/5.0 (Windows NT 6.3; WOW64) AppleWebKit\/537.36 (KHTML,like Gecko) Chrome\/45.0.2454.101 Safari\/537.36",
       "UniqueMsgID":"1809631",
       "Guid": "16ea5f590b684b5fad38dfcaec37d63e",
       "MailName": "邮件任务-2025-10-28 xxxx"
   }
```

### [Clicked事件](https://developers.effilink.co/api-reference/v5/webhook.html#clicked%E4%BA%8B%E4%BB%B6)

事件说明：联系人点击了邮件内的某个链接(开启链接跟踪才会产生此数据)。每次点击都会产生一个此类事件消息。

| 属性名 | 类型 | 说明 |
| --- | --- | --- |
| EventCode | string | "Clicked" |
| Email | string | 接收方Email |
| EventType | string | 邮件的类型，<br>3：事务类邮件；<br>5：营销类邮件； |
| SentMailListName | string | 邮件提交时设置的category、campaign，以“||”连接，<br>样例：bill||bill\_202304 |
| SubmitDateTimeV2 | string | 邮件提交发送的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| DeliveredTimeV2 | string | 邮件投递成功的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| TriggeredDateTimeV2 | string | 事件产生的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| UniqueMsgID | string | 邮件提交时设置的唯一标示 |
| IP | string | 事件发生时的客户端IP； |
| Platform | string | 事件发生时的客户端操作系统； |
| BrowserType | string | 事件发生时的客户端软件名称； |
| UA | string | 事件发生时的客户端标识（UserAgent）； |
| Link | string | 邮件中被点击链接的URL； |
| Guid | string | 邮件任务的唯一Id |
| MailName | string | 邮件任务的名字 |

Clicked样例：

```
   {
       "EventCode":"Clicked",
       "BrowserType":"Mobile Safari",
       "DeliveredTimeV2":"2023-10-31 13:54:31",
       "Email":"test@test.easeye.net",
       "EventType":"3",
       "IP":"1.1.1.1",
       "Link":"https:\/\/www.baidu.com\/def\/index.htm?ab=0&cd=ef",
       "Platform":"iOS",
       "SentMailListName":"",
       "SubmitDateTimeV2":"2023-10-31 13:54:31",
       "TriggeredDateTimeV2":"2023-10-31 13:54:31",
       "UA":"Mozilla\/5.0 (iPhone; CPU iPhone OS 10_2 like Mac OS X) AppleWebKit\/602.3.12 (KHTML,like Gecko) Mobile\/14C92 (4347662848)",
       "UniqueMsgID":"5611974",
       "Guid": "16ea5f590b684b5fad38dfcaec37d63e",
       "MailName": "邮件任务-2025-10-28 xxxx"
   }
```

### [Unsubscribed事件](https://developers.effilink.co/api-reference/v5/webhook.html#unsubscribed%E4%BA%8B%E4%BB%B6)

事件说明：联系人要求退订，不再接收营销邮件。

| 属性名 | 类型 | 说明 |
| --- | --- | --- |
| EventCode | string | "Unsubscribed" |
| Email | string | 接收方Email |
| EventType | string | 邮件的类型，<br>3：事务类邮件；<br>5：营销类邮件； |
| SentMailListName | string | 邮件提交时设置的category、campaign，以“||”连接，<br>样例：bill||bill\_202304 |
| TriggeredDateTimeV2 | string | 事件产生的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| UniqueMsgID | string | 邮件提交时设置的唯一标示 |
| Guid | string | 邮件任务的唯一Id |
| MailName | string | 邮件任务的名字 |
| Reason | string | 退订的原因 |

Unsubscribed样例：

```
   {
       "EventCode":"Unsubscribed",
       "Email":"test@test.easeye.net",
       "EventType":"3",
       "SentMailListName":"",
       "TriggeredDateTimeV2":"2023-10-31 13:54:31",
       "UniqueMsgID":"1795046",
       "Guid": "16ea5f590b684b5fad38dfcaec37d63e",
       "MailName": "邮件任务-2025-10-28 xxxx",
       "Reason": "(语言：英语)邮件无法正常显示;"
   }
```

### [SpamReport事件](https://developers.effilink.co/api-reference/v5/webhook.html#spamreport%E4%BA%8B%E4%BB%B6)

事件说明：垃圾邮件投诉，联系人向ESP举报此邮件是垃圾邮件。

| 属性名 | 类型 | 说明 |
| --- | --- | --- |
| EventCode | string | "SpamReport" |
| Email | string | 接收方Email |
| EventType | string | 邮件的类型，<br>3：事务类邮件；<br>5：营销类邮件； |
| SenderEmail | string | 发送方 |
| SentMailListName | string | 邮件提交时设置的category、campaign，以“||”连接，<br>样例：bill||bill\_202304 |
| TriggeredDateTimeV2 | string | 事件产生的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| UniqueMsgID | string | 邮件提交时设置的唯一标示 |
| Guid | string | 邮件任务的唯一Id |
| MailName | string | 邮件任务的名字 |

SpamReport样例：

```
   {
       "EventCode":"SpamReport",
       "Email":"test@test.easeye.net",
       "EventType":"5",
       "SenderEmail":"service@trigger.easeye.com",
       "SentMailListName":"",
       "TriggeredDateTimeV2":"2023-10-31 13:54:31",
       "UniqueMsgID":"891025625",
       "Guid": "16ea5f590b684b5fad38dfcaec37d63e",
       "MailName": "邮件任务-2025-10-28 xxxx"
   }
```

### [TaskStatus事件](https://developers.effilink.co/api-reference/v5/webhook.html#taskstatus%E4%BA%8B%E4%BB%B6)

事件说明：邮件任务状态相关事件；

| 属性名 | 类型 | 说明 |
| --- | --- | --- |
| EventCode | string | "TaskStatus" |
| StatusCode | string | 邮件任务状态值，取值范围：<br>Created（创建）<br>Completed（投递完成） |
| TriggeredDateTimeV2 | string | 事件产生的时间，格式为yyyy-MM-dd HH:mm:ss，<br>样例：2023-10-31 13:54:31 |
| MailName | string | 邮件任务的名字 |
| Guid | string | 邮件任务的唯一Id |
| Creator | string | 邮件任务创建者 |
| LanguageCode | string | 邮件任务语言代码。仅在StatusCode=Completed时返回。<br>值说明：zh-cn（简体中文）、en（英文）、ja（日文）、ko（韩文）、de（德文）、tt（俄文）、es（西班牙文）、zh-tw（繁体中文）、ar（阿拉伯文）、pt-br（葡萄牙文-巴西）、id（印尼文）。 |
| MarketName | string | 邮件任务活动名称。仅在StatusCode=Completed时返回。 |
| SubscriptName | string | 邮件任务订阅名称。仅在StatusCode=Completed时返回。 |
| ProjectCode | string | 邮件任务项目代码。仅在StatusCode=Completed时返回。 |
| Description | string | 邮件任务备注。仅在StatusCode=Completed时返回。 |

TaskStatus样例：

```
   {
       "EventCode":"TaskStatus",
       "StatusCode":"Completed",
       "TriggeredDateTimeV2":"2023-10-31 13:54:31",
       "MailName":"邮件任务-2025-10-28 xxxx",
       "Guid": "16ea5f590b684b5fad38dfcaec37d63e",
       "Creator":"操作员01",
       "LanguageCode":"zh-cn",
       "MarketName":"示例活动01",
       "SubscriptName":"Newsletter | 新闻通讯",
       "ProjectCode":"PRJ20260301",
       "Description":"描述xxx"
   }
```