# Source: https://developers.effilink.co/api-reference/v5/how-it-works.html

# [关键概念](https://developers.effilink.co/api-reference/v5/how-it-works.html#%E5%85%B3%E9%94%AE%E6%A6%82%E5%BF%B5)

更新时间：2025-01-15 10:29

以下是您在开始使用API之前需要了解的所有内容。

### [API服务接入点](https://developers.effilink.co/api-reference/v5/how-it-works.html#api%E6%9C%8D%E5%8A%A1%E6%8E%A5%E5%85%A5%E7%82%B9)

```
api.effilink.co
```

### [请求参数](https://developers.effilink.co/api-reference/v5/how-it-works.html#%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0)

Web API的请求必须通过HTTPS发送，数据格式为 JSON （application/json），每次请求都应包含[鉴权所需的头部字段](https://developers.effilink.co/api-reference/v5/api-authentication.html)：`content-type: application/json` 、`ApiKey` 、`Authorization`、`Timestamp`。

请求数据的**默认字符集为UTF-8**。

参数名是**区分大小写**的。

ApiKey可以在平台的[设置](https://app.effilink.co/setting/appAuth/)中添加、管理。

### [分页](https://developers.effilink.co/api-reference/v5/how-it-works.html#%E5%88%86%E9%A1%B5)

检索、查询类的接口，返回的结果可能会被分页，您可以使用以下参数来指定页码与每页记录数。

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| pageSize | 整数 | 每页返回的记录数 |
| pageIndex | 整数 | 返回第几页的数据，从1开始 |

### [返回参数](https://developers.effilink.co/api-reference/v5/how-it-works.html#%E8%BF%94%E5%9B%9E%E5%8F%82%E6%95%B0)

返回的响应信息都是JSON对象，不同接口返回的JSON对象是不同的。

错误对象包含错误代码和对应的描述信息。

### [API HTTP响应代码](https://developers.effilink.co/api-reference/v5/how-it-works.html#api-http%E5%93%8D%E5%BA%94%E4%BB%A3%E7%A0%81)

下面是接口可以返回的HTTP相应代码：

| HTTP code | 状态 | 描述 |
| --- | --- | --- |
| 200 | OK | 成功的请求 |
| 400 | Bad Request | 请求的数据格式不合法 |
| 404 | Not Found | 接口不存在 |
| 405 | Method Not Allowed | 不允许的请求方式，允许的方式有：GET、POST |
| 429 | Too Many Requests | 请求频率超限 |