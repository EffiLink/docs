# Source: https://developers.effilink.co/api-reference/v5/platform-quotas.html

# [平台配额](https://developers.effilink.co/api-reference/v5/platform-quotas.html#%E5%B9%B3%E5%8F%B0%E9%85%8D%E9%A2%9D)

更新时间：2022-11-03 09:13

配额表示通过 API 为特定服务或产品创建的一些可计数对象，适用于 EffiLink 上的每个活跃帐户。

配额适用于所有主要 API 操作和通过UI执行的操作，例如创建营销活动或添加联系人。如果某些对象达到配额限制，则需要对帐户中可能未使用的对象执行删除操作，以便创建新对象。

### [营销活动配额](https://developers.effilink.co/api-reference/v5/platform-quotas.html#%E8%90%A5%E9%94%80%E6%B4%BB%E5%8A%A8%E9%85%8D%E9%A2%9D)

已创建的电子邮件营销活动或者短信营销活动的总数，即您账户中存储的营销活动数量上限（包括草稿）

| 类型 | 试用账号 | 正式账号 |
| --- | --- | --- |
| 邮件活动（个） | 100个 | 1000个 |
| 短信活动（个） | 100个 | 1000个 |

### [上传到内容库的媒介总量](https://developers.effilink.co/api-reference/v5/platform-quotas.html#%E4%B8%8A%E4%BC%A0%E5%88%B0%E5%86%85%E5%AE%B9%E5%BA%93%E7%9A%84%E5%AA%92%E4%BB%8B%E6%80%BB%E9%87%8F)

即推送到内容库的最大媒介量（GB）

| 试用账号 | 正式账号 |
| --- | --- |
| 10M 媒体文件 | 2G 媒体文件 |

### [自动化工作流总数](https://developers.effilink.co/api-reference/v5/platform-quotas.html#%E8%87%AA%E5%8A%A8%E5%8C%96%E5%B7%A5%E4%BD%9C%E6%B5%81%E6%80%BB%E6%95%B0)

即您账户中同时运行的营销自动化工作流的最大数量

| 试用账号 | 正式账号 |
| --- | --- |
| 1个活跃工作流 | 20个活跃工作流 |

### [联系人管理配额](https://developers.effilink.co/api-reference/v5/platform-quotas.html#%E8%81%94%E7%B3%BB%E4%BA%BA%E7%AE%A1%E7%90%86%E9%85%8D%E9%A2%9D)

创建的联系人属性总数 ，即您的联系人的自定义属性数量上限。统一为200个。

创建的联系组总数 ，即您账户中创建的联系人组别数量上限，统一为300个。

### [发送数量配额](https://developers.effilink.co/api-reference/v5/platform-quotas.html#%E5%8F%91%E9%80%81%E6%95%B0%E9%87%8F%E9%85%8D%E9%A2%9D)

即可以发送的邮件或者短信最大数量，事务邮件（短信）和营销邮件（短信）公用额度。

| 类型 | 试用账号 | 正式账号 |
| --- | --- | --- |
| 邮件 | 100 | 按需 |
| 短信 | 0 | 按需 |