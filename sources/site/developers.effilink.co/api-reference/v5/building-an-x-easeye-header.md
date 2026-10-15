# Source: https://developers.effilink.co/api-reference/v5/building-an-x-easeye-header.html

# [SMTP扩展功能](https://developers.effilink.co/api-reference/v5/building-an-x-easeye-header.html#smtp%E6%89%A9%E5%B1%95%E5%8A%9F%E8%83%BD)

## [支持哪些扩展功能](https://developers.effilink.co/api-reference/v5/building-an-x-easeye-header.html#%E6%94%AF%E6%8C%81%E5%93%AA%E4%BA%9B%E6%89%A9%E5%B1%95%E5%8A%9F%E8%83%BD)

1. **支持设置邮件类别和任务名称.** 
 主要是为了后续查询报表时使用，方便操作人员分类/分任务查看不同的类别和任务的发送效果；推荐使用方式如下： 
 **邮件类别**：设置邮件类别为触发场景名称，比如账单邮件的类别可以是：bill；注册邮件的类别可以是：registration; 
 **任务名称**：设置任务名称为用户传入的任务名称（如果有的话），或者“类别名称+触发日期”，比如bill\_201607或者registration\_20170207;

```
X-Easeye-API: {
   "category": "bill",
   "campaign": "bill_201607"
}
```

2. **支持设置是否跟踪打开和跟踪点击.** 
 SMTP邮件系统默认不跟踪打开和点击，如果需要跟踪，请分别设置`track_open`、`track_click`为：`1`;

```
X-Easeye-API: {
   "send_options": {
       "track_open":1,
       "track_click":1
      }
}
```

对于 HTML 邮件，点击追踪适用于 `<a>` 标签中的所有链接，但不会添加到 `mailto` 和电子邮件地址链接中。某些电子邮件客户端和 Web 浏览器会截断超过一定长度的链接。在将较长的链接添加到邮件之前，请务必检查是否可以缩短它们。

**<禁用单个链接的点击追踪>**: 请将 `ef:disable-tracking` 参数（必须小写）添加到链接属性中。例如：

```
<a href="http://linkthatshouldnotbetracked.com" ef:disable-tracking>点击此处报名</a>
```

注意：如果您发现您的 URL 未被跟踪，请确认是否已在“send\_options”中启用点击跟踪。

3. **支持设置自定义跟踪域名.** 
 一般如果公司有多个网站，且主域名不同，才需要修改本配置;

```
X-Easeye-API: {
   "send_options": {
       "custom_domain":"http://linktrace.test.com"
      }
}
```

4. **支持设置优先级别.** 
 仅仅在：有私有通道，且发送的事务邮件同时有实时触发（注册激活密码找回）和批量触发（账单）的场景下才使用; 
 可以为实时触发邮件设置较高的优先级别，批量触发的邮件设置偏低的优先级别，以避免互相干扰;

```
X-Easeye-API: {
   "priority": "low"
}
```

5. **支持单封信件定位功能**. 
 每封信件可以赋一个唯一的ID，方便同一个接收方短时间多次发送时，能够快速定位到任意一封邮件;

```
X-Easeye-UniqueMsgID: sendseqid-89897254234
```

## [如何支持扩展功能](https://developers.effilink.co/api-reference/v5/building-an-x-easeye-header.html#%E5%A6%82%E4%BD%95%E6%94%AF%E6%8C%81%E6%89%A9%E5%B1%95%E5%8A%9F%E8%83%BD)

扩展功能是通过添加额外的header来实现的；主要有三个header：`X-Easeye-API` 、 `X-Easeye-UniqueMsgID` 、 `X-Easeye-ExpirationDate`

### [X-Easeye-API](https://developers.effilink.co/api-reference/v5/building-an-x-easeye-header.html#x-easeye-api)

本Header的值是一段 JSON 字符串,用以传递发送的选项；支持的功能和相应的配置值如下：

1. 支持设置邮件类别和任务名称； 
 **category**：邮件类别；最大长度100个byte，字符范围是大小写字母和阿拉伯数字； 
 **campaign**：邮件任务名称；最大长度100个byte，字符范围是大小写字母和阿拉伯数字；
2. 通过设置send\_options来实现的功能； 
 **track\_open**：是否跟踪邮件打开,只有当邮件内容为"text/html"时有效,为 1 时跟踪,其他值不跟踪。 
 **track\_click**：是否跟踪邮件点击,为 1 时跟踪,其他值不跟踪。 
 **track\_subscription**：是否添加退订链接，为 1 时添加,其他值不添加。 
 **custom\_domain**：自定义跟踪域名。要求此域名已在平台验证通过,否则将采用系统缺省域名。 

3. 支持设置优先级别； 
 **priority**：邮件优先级,可设定为 high、median 和 low三种,不填的话默认为 low；

```
样例如下：
 X-Easeye-API: {
   "category": "Registration",
   "campaign": "registration email for new users",
   "send_options": {
       "track_open": 1,
       "track_click":1,
       "track_subscription":1,
       "custom_domain":"http://linktrace.test.com"
       },
   "priority":"low"
   }
```

### [X-Easeye-UniqueMsgID](https://developers.effilink.co/api-reference/v5/building-an-x-easeye-header.html#x-easeye-uniquemsgid)

用以唯一标识一封邮件(对发送方)，最大长度50 byte，字符范围是大小写字母，阿拉伯数字和减号；

```
样例如下：
 X-Easeye-UniqueMsgID: sendseqid-89897254234
```

### [X-Easeye-ExpirationDate](https://developers.effilink.co/api-reference/v5/building-an-x-easeye-header.html#x-easeye-expirationdate)

设置信件的过期时间，在此时间之后仍没能投递出去的邮件将反馈为过期状态； 
时间格式为：yyyy-MM-dd HH:mm:ss，时区为东八区；

```
 X-Easeye-ExpirationDate: 2018-10-09 11:03:25
```