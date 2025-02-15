---
title: 使用 Microsoft Graph 权限扩展选项卡应用
description: 使用 Microsoft Graph 配置其他权限和范围，以启用单一登录 (SSO) 。
ms.topic: how-to
ms.localizationpriority: high
keywords: Microsoft Azure Active Directory (Azure AD) 图形 API 委派权限访问令牌范围的 Teams 身份验证选项卡
ms.openlocfilehash: 11620e10ed736ce9fe88e3bb755acfbabfec3f47
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791718"
---
# <a name="extend-tab-app-with-microsoft-graph-permissions-and-scope"></a>使用 Microsoft Graph 权限和范围扩展选项卡应用

可以使用 Microsoft Graph 扩展选项卡应用，以允许用户使用其他权限（例如查看应用用户配置文件、读取邮件等）。 应用必须请求特定的权限范围才能在应用用户同意时获取访问令牌。

图形范围（如 `User.Read` 或 `Mail.Read`）允许指定应用访问 Teams 用户帐户的方式。 需要在授权请求中指定范围。

此部分将介绍如何：

- [在 Azure AD 中配置 API 权限](#configure-api-permissions-in-azure-ad)
- [为不同平台配置身份验证](#configure-authentication-for-different-platforms)
- [获取 MS Graph 的访问令牌](#acquire-access-token-for-ms-graph)

## <a name="configure-api-permissions-in-azure-ad"></a>在 Azure AD 中配置 API 权限

可以在 Azure AD 中为应用配置其他 Graph 范围。 这些是委派权限，由需要登录访问的应用使用。 已登录的应用用户或管理员必须同意委托的权限。 在调用 Microsoft Graph 时，选项卡应用可以代表已登录用户同意。

### <a name="to-configure-api-permissions"></a>配置 API 权限

1. 打开在 [Azure 门户](https://ms.portal.azure.com/)中注册的应用。

2. 从左窗格中选择 **管理** > **API权限**。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/api-permission-menu.png" alt-text="应用权限菜单选项。":::

    将显示 **API 权限** 页面。

3. 选择 **+添加权限**，以添加 Microsoft 图形 API权限。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-permission.png" alt-text="应用权限页。":::

    将显示“**请求 API 权限**”页。

4. 选择 **Microsoft Graph**。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/request-api-permission.png" alt-text="“请求 API 权限”页。":::

    显示 Graph 权限的选项。

5. 选择 **委派权限** 以查看权限列表。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/delegated-permission.png" alt-text="委派权限":::

6. 选择应用的相关权限，然后选择“**添加权限**”。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-permission.png" alt-text="选择权限。":::

    还可以在搜索框中输入权限名称来查找。

    浏览器上弹出一条消息，指出权限已更新。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/updated-permission-msg.png" alt-text="权限已更新消息。":::

    添加的权限显示在 **API 权限** 页中。

   :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configured-permissions.png" alt-text="配置 API 权限。":::

    你已使用 Microsoft Graph 权限配置了应用。

## <a name="configure-authentication-for-different-platforms"></a>为不同平台配置身份验证

根据要面向应用的平台或设备，可能需要其他配置，例如重定向 URI、特定的身份验证设置或特定于平台的详细信息。

> [!NOTE]
>
> - 如果选项卡应用尚未获得 IT 管理员同意，则应用用户必须在其他平台上首次使用应用时获得同意。
> - 如果在选项卡应用上启用了 SSO，则不需要隐式授予。

只要 URL 唯一，就可以为多个平台配置身份验证。

### <a name="to-configure-authentication-for-a-platform"></a>为平台配置身份验证

1. 打开在 [Azure 门户](https://ms.portal.azure.com/)中注册的应用。

1. 从左窗格中选择“**管理** > **身份验证**”。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-portal-platform.png" alt-text="平台身份验证":::

    将显示 **平台配置** 页。

1. 选择 **+ 添加平台**。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-platform.png" alt-text="添加平台":::

    将显示“**配置平台**”页。

1. 选择要为选项卡应用配置的平台。 可以从 Web 或 SPA 中选择平台类型。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/configure-platform.png" alt-text="选择 Web 平台":::

    可以为特定平台类型配置多个平台。 确保重定向 URI 对于你配置的每个平台是唯一的。

    将显示“配置 Web”网页。

    > [!NOTE]
    > 根据所选平台，配置将有所不同。

1. 输入平台的配置详细信息。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-web-platform.png" alt-text="配置 Web 平台":::

    1. 输入重定向 URI。 URI 应是唯一的。
    2. 输入前通道注销 URL。
    3. 选择希望 Azure AD 为应用发送的令牌。

1. 选择“**配置**”。

    平台已配置并显示在“**平台配置**”页中。

## <a name="acquire-access-token-for-ms-graph"></a>获取 MS Graph 的访问令牌

需要获取 Microsoft Graph 的访问令牌。 可以使用 Azure AD OBO 流来执行此操作。

SSO 当前仅对无法进行 Graph 调用的用户级权限授予许可。 若要获取 Graph 调用所需的权限（范围），SSO 解决方案必须执行自定义 Web 服务，交换从 Teams JavaScript SDK 收到的令牌，以获取包含所需范围的令牌。 可以使用 Microsoft 身份验证库 (MSAL) 从客户端提取令牌。

在 Azure AD 中配置 Graph 权限后：

- [配置客户端代码以使用 MSAL 提取访问令牌](#configure-code-to-fetch-access-token-using-msal)
- [将访问令牌传递到服务器端代码](#pass-the-access-token-to-server-side-code)

### <a name="configure-code-to-fetch-access-token-using-msal"></a>配置代码以使用 MSAL 提取访问令牌

以下代码提供了使用 MSAL 从 Teams 客户端提取访问令牌的 OBO 流示例。

### <a name="c"></a>[C#](#tab/dotnet)

```csharp

IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(<"Client id">)
                                                .WithClientSecret(<"Client secret">)
                                                .WithAuthority($"https://login.microsoftonline.com/<"Tenant id">")
                                                .Build();
 
            try
            {
                var idToken = <"Client side token">;
                UserAssertion assert = new UserAssertion(idToken);
                List<string> scopes = new List<string>();
                scopes.Add("https://graph.microsoft.com/User.Read");
                var responseToken = await app.AcquireTokenOnBehalfOf(scopes, assert).ExecuteAsync();
                return responseToken.AccessToken.ToString();
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
        }
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```Node.js

// Exchange client Id side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenant id" >
    var token = < "Client side token" >
    var scopes = ["https://graph.microsoft.com/User.Read"];

        // Creating MSAL client
        const msalClient = new msal.ConfidentialClientApplication({
            auth: {
                clientId: < "Client ID" >,
                clientSecret: < "Client Secret" >
      }
        });

        var oboPromise = new Promise((resolve, reject) => {
            msalClient.acquireTokenOnBehalfOf({
                authority: `https://login.microsoftonline.com/${tid}`,
                oboAssertion: token,
                scopes: scopes,
                skipCache: true
            }).then(result => {
                console.log("Token is: " + result.accessToken);
            }).catch(error => {
                reject({ "error": error.errorCode });
            });
        });
```

---

### <a name="pass-the-access-token-to-server-side-code"></a>将访问令牌传递到服务器端代码

如果需要访问 Microsoft Graph 数据，请将服务器端代码配置为：

1. 验证访问令牌。 有关详细信息，请参阅[验证访问令牌](tab-sso-code.md#validate-the-access-token)。
1. 通过调用 Microsoft 标识平台来启动 OAuth 2.0 代理流，该平台包括访问令牌、有关用户的一些元数据，以及选项卡应用的凭据（其应用 ID 和客户端密码）。 Microsoft 标识平台将返回可用于访问 Microsoft Graph 的新访问令牌。
1. 使用新的令牌从 Microsoft Graph 获取数据。
1. 如果需要，请在 MSAL.NET 中使用令牌缓存序列化来缓存多个新访问令牌。

> [!IMPORTANT]
> 作为最佳安全做法，请始终使用服务器端代码进行 Microsoft Graph 调用或需要传递访问令牌的其他调用。 从不将 OBO 令牌返回到客户端，以允许客户端直接调用 Microsoft Graph。 这有助于保护令牌免受截获或泄露的侵害。

## <a name="known-limitations"></a>已知限制

租户管理员同意：[代表组织作为租户管理员进行许可的一](/azure/active-directory/manage-apps/consent-and-permissions-overview#admin-consent) 种简单方法是获得[管理员的同意](/azure/active-directory/manage-apps/grant-admin-consent)。

使用身份验证 API 请求其他许可。 获取 Graph 范围的另一种方法是使用现有的 [第三方 OAuth 提供程序身份验证方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page) 来呈现同意对话框。 此方法涉及弹出 Azure AD 同意对话框。

<details>
<summary>若要使用身份验证 API 请求其他同意，请执行以下步骤：</summary>

1. 使用 `getAuthToken()` 检索到的令牌必须在服务器端使用 Azure AD [代表流](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) 进行交换，以获取对这些其他图形 API 的访问权限。 请确保为此交换使用 v2 Graph 终结点。
2. 如果交换失败，Azure AD 将返回无效的授权异常。 它通常使用 `invalid_grant` 或 `interaction_required` 中的一条错误消息进行响应。
3. 交换失败时，必须请求同意。 使用用户界面 (UI) 要求应用用户授予其他许可。 此 UI 必须包含一个按钮，该按钮使用 [无提示身份验证](~/concepts/authentication/auth-silent-aad.md)触发 Azure AD 同意对话框。
4. 请求 Azure AD 的更多同意时，必须在给 Azure AD 发送的 [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) 中包含 `prompt=consent`，否则 Azure AD 不会要求其他范围。
    - 使用 `?prompt=consent&scope={scopes}` 而不是 `?scope={scopes}`
    - 确保 `{scopes}` 包括你提示用户的所有范围，例如， `Mail.Read` 或 `User.Read`。

    若要处理选项卡应用的增量同意，请参阅 [增量和动态用户同意](/azure/active-directory/develop/v2-permissions-and-consent)。
5. 应用用户授予更多权限后，重试 OBO 流以获取对这些其他 API 的访问权限。
    </details>

## <a name="see-also"></a>另请参阅

- [OAuth 2.0 代理流](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
- [获取 MS Graph 的访问权限](/graph/auth-v2-user)
- [MSAL.NET 中的令牌缓存序列化](/azure/active-directory/develop/msal-net-token-cache-serialization?tabs=aspnet)
- [Microsoft Teams MSAL2 提供程序](/graph/toolkit/providers/teams-msal2)
