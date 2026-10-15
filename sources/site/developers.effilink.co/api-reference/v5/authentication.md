# Source: https://developers.effilink.co/api-reference/v5/authentication.html

# [身份认证](https://developers.effilink.co/api-reference/v5/authentication.html#%E8%BA%AB%E4%BB%BD%E8%AE%A4%E8%AF%81)

更新时间：2026-03-03 09:13

EffiLink 主要采用两种身份认证方案： 

[**API Key**\\ \\ 使用 API Key 直接访问接口。\\ \\ **使用场景**\\ \\ 用于服务器与服务器之间的直接集成，此时需要您在两端均有控制权。](https://developers.effilink.co/api-reference/v5/api-key-authentication.html) [**OAuth 2**\\ \\ 用于需要授权第三方访问与集成。\\ \\ **使用场景**\\ \\ 适用于企业内按用户单独授权的私有集成场景。](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html)

### [API Key认证](https://developers.effilink.co/api-reference/v5/authentication.html#api-key%E8%AE%A4%E8%AF%81)

您在向接口端点（EndPoint)发送请求时，通过在请求中携带的 apikey（在 HTTP Header 中）来验证身份

您可以从 EffiLink 帐户中获取 API Key，默认每个团队可以保留三组 API Key。

如需更多帮助，请在此处查阅 [API Key获取与使用指南](https://developers.effilink.co/api-reference/v5/api-key-authentication.html)。

### [OAuth 2 认证](https://developers.effilink.co/api-reference/v5/authentication.html#oauth-2-%E8%AE%A4%E8%AF%81)

如果您希望将 EffiLink 的功能集成到其他的企业级应用中，请优先使用 OAuth 2 认证。

EffiLink API 服务器能够提供一个Token作为您授权第三方访问接口的身份验证证明，Token允许定义有效期（例如30天），会被存储在 EffiLink 的Token服务器，Token服务器提供权限并授权第三方应用访问。

更多细节，请参阅[OAuth身份验证](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html)。

提示

在开始使用 OAuth 2 设置身份验证之前，您需要了解何时无需使用 OAuth 2，而应该使用 API 密钥。

简而言之：如果您编写的代码将应用程序数据与EffiLink帐户数据紧密耦合，请使用 API Key。如果您需要访问其他人能访问您的EffiLink帐户数据，则应该使用 OAuth 2。