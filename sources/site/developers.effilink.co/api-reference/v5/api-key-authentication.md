# Source: https://developers.effilink.co/api-reference/v5/api-key-authentication.html

# API Key获取与使用

更新时间：2024-06-03 09:00

您需要一个EffiLink 帐户，可以从我们的[注册页面](https://www.effilink.co/register)免费创建一个。 确认帐户后，请从设置->接口设置->API Keys 中获取 API 密钥。

### [如何获取API Key](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E5%A6%82%E4%BD%95%E8%8E%B7%E5%8F%96api-key)

1. 登录帐户后，点击屏幕右上角"**设置**”;

![](https://developers.effilink.co/api-reference/v5/assets/quick-start-1-vf_WIEWk.png)

2. 点击左侧菜单中的：接口配置->[API Keys](https://app.effilink.co/setting/apikey/);

![](https://developers.effilink.co/api-reference/v5/assets/quick-start-2-Ii8TwKC5.png)

3. 在API Keys管理页面中，点击右上角的“**创建API Key**”；

![如何获取API Key-3](https://developers.effilink.co/api-reference/v5/assets/quick-start-3-DEkB0vvr.png)

4. 将系统生成的 API Key **保存**在安全的地方，其中后半部分只在生成时展示一次；

![如何获取API Key-4](https://developers.effilink.co/api-reference/v5/assets/quick-start-4-CqO4LXq0.png)

### [使用API Key](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E4%BD%BF%E7%94%A8api-key)

在您[获取API Key](https://developers.effilink.co/api-reference/v5/api-key-authentication.html#%E5%A6%82%E4%BD%95%E8%8E%B7%E5%8F%96api-key)后，请在所有 API 请求的 ApiKey标头中包含您的 API 密钥。您的 API Key用于识别您的帐户并授权 API 访问。请在每个请求中包含此密钥以验证您的调用。

示例

```
curl --request POST \
  --url https://api.effilink.co/v5/transactional/mail/sends_customised \
  --header 'Content-Type: application/json' \
  --header 'ApiKey: 3BTWNKN0ZDQIZBQ33XCO-VzNnMBUbDLloZkKMHqEeqg2byrNpVyrqf-XI1sAk' \
  --data '{"data":"here"}'
```