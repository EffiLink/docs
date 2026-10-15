# Source: https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html

# [OAuth 2 认证](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html#oauth-2-%E8%AE%A4%E8%AF%81)

更新时间：2024-11-03 09:13

OAuth 2 身份验证为开发者提供了一种安全的方式，代表EffiLink用户访问 EffiLink API 数据。OAuth 2 身份验证最常见的用途是设置第三方应用程序与EffiLink之间的集成,从而将您的应用程序数据与EffiLink同步，以便EffiLink可以发送营销或者交易邮件。

在本指南中，我们将逐步介绍如何设置 OAuth 2 来验证应用程序用户的身份，然后演示如何使用 OAuth 2 访问令牌调用 Marketing API。

### [前提条件](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html#%E5%89%8D%E6%8F%90%E6%9D%A1%E4%BB%B6)

了解 OAuth 2 的基础知识，包括：

- 授权服务器
- 客户端应用程序
- 资源所有者
- 访问令牌

### [授权您的应用程序](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html#%E6%8E%88%E6%9D%83%E6%82%A8%E7%9A%84%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F)

授权您的应用程序以获取 OAuth 凭据。

授权过程中使用的client\_id（应用Id）、client\_secret（应用密钥）、redirect\_uri（重定向地址）需要在平台配置：

![](https://developers.effilink.co/api-reference/v5/assets/oauth2-1-DY1IKp4p.png)

### [OAuth 2 流程](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html#oauth-2-%E6%B5%81%E7%A8%8B)

![](https://developers.effilink.co/api-reference/v5/assets/oauth2-2-CVYu9ksC.png)

#### [使用步骤：](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html#%E4%BD%BF%E7%94%A8%E6%AD%A5%E9%AA%A4)

1. 用户安装了您的应用程序（您的App）。 

2. 用户访问您的App，您的App加载EffiLink的授权弹出窗口。 

3. 用户选择是否同意授权。 

4. 若用户同意授权，则EffiLink将用户重定向到第一步指定的重定向URI，同时附上一个授权码（code）。 

5. 第三方服务收到授权码（code），向EffiLink申请凭证（AccessToken）。 

6. EffiLink检查授权码（code）的有效性，通过后颁发凭证（AccessToken）。 

7. 第三方服务通过此凭证（AccessToken）访问EffiLink的业务 API。 

### [OAuth 2 集成指南](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html#oauth-2-%E9%9B%86%E6%88%90%E6%8C%87%E5%8D%97)

在您的应用程序中实现 OAuth 2 身份验证

本指南演示如何在应用程序中实现 OAuth 2 身份验证。开始之前，请先熟悉EffiLink使用的 OAuth 2 流程。

#### [第一步：构造EffiLink的OAuth 2 授权页链接](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html#%E7%AC%AC%E4%B8%80%E6%AD%A5-%E6%9E%84%E9%80%A0effilink%E7%9A%84oauth-2-%E6%8E%88%E6%9D%83%E9%A1%B5%E9%93%BE%E6%8E%A5)

GET /v5/auth/oauth/authorize

**请求参数**

| 名称 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- |
| **client\_id** | 是 | OAuth应用Id | 1751651162214168 |
| **response\_type** | 是 | 返回类型 | 固定值：code |
| **redirect\_uri** | 是 | 授权后重定向的回调链接地址，请使用urlencode对链接进行处理 | https%3A%2F%2Fapp.effilink.co%2FoauthCodeCallback |
| **scope** | 是 | 应用授权作用域。 | 固定值：All |

请求示例

```
curl --request GET \
  --url https://api.effilink.co/v5/auth/oauth/authorize?client_id=1751651162214168&response_type=code&redirect_uri=https%3A%2F%2Fapp.effilink.co%2FoauthCodeCallback&scope=All
```

**请求返回** 
返回EffiLink授权页。 
用户在授权页授权后，将重定向到传递的redirect\_uri参数值，并且携带code参数。注意，code的有效期为5分钟。 

#### [第二步：通过授权码（code）获取凭证（AccessToken）](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html#%E7%AC%AC%E4%BA%8C%E6%AD%A5-%E9%80%9A%E8%BF%87%E6%8E%88%E6%9D%83%E7%A0%81-code-%E8%8E%B7%E5%8F%96%E5%87%AD%E8%AF%81-accesstoken)

GET /v5/auth/oauth/token

**请求参数**

| 名称 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- |
| **grant\_type** | 是 | 授权方式 | 固定值：authorization\_code |
| **client\_id** | 是 | OAuth应用Id | 1751651162214168 |
| **client\_secret** | 是 | OAuth应用密钥 | 768e04e13b5f4a3ca67de0a21b3ca7d5 |
| **code** | 是 | 用户授权后重定向返回的code值 | ae3cae67d13b5fe0a21b3cae7d |

请求示例

```
curl --request GET \
  --url https://api.effilink.co/v5/auth/oauth/token?grant_type=authorization_code&client_id=1751651162214168&client_secret=768e04e13b5f4a3ca67de0a21b3ca7d5&code=ae3cae67d13b5fe0a21b3cae7d
```

**返回参数**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| **code** | int | 返回码 |
| **message** | string | 对返回码的文本描述内容 |
| **accessToken** | string | 获取到的凭证，最长为512字节。同一个ApiKey在凭证的有效期内仅会生成一个相同的AccessToken |
| **expiresIn** | int | 凭证的剩余有效时间（秒）。-1表示永久有效。有效期剩余5分钟以内时，可生成一个新的AccessToken，在此期间新老AccessToken同时有效 |

返回示例

```
{
    "code": 200,
    "message": null,
    "accessToken": "5cb089d6eafd49caa68c41b9be9af6f6",
    "expiresIn": -1
}
```

#### [第三步：使用凭证（AccessToken）访问 API](https://developers.effilink.co/api-reference/v5/integrating-oauth-20-to-your-solution.html#%E7%AC%AC%E4%B8%89%E6%AD%A5-%E4%BD%BF%E7%94%A8%E5%87%AD%E8%AF%81-accesstoken-%E8%AE%BF%E9%97%AE-api)

请求时请添加以下Header来身份验证：

| Header名称 | 必填 | 描述 | 示例值 |
| --- | --- | --- | --- |
| OAuth | **是** | OAuth认证的accessToken | 5cb089d6eafd49caa68c41b9be9af6f6 |

示例

```
curl --request POST \
  --url https://api.effilink.co/v5/transactional/mail/sends_customised \
  --header 'OAuth: 5cb089d6eafd49caa68c41b9be9af6f6'
  --data ...
```