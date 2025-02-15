---
title: 从个人应用或选项卡共享到 Teams
description: 了解如何在个人应用或选项卡、限制和最终用户体验上启用“共享到 Teams”按钮。
ms.topic: reference
ms.localizationpriority: medium
ms.openlocfilehash: cd4de40fdb557300ad957df03f463a0879f44b0e
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2022
ms.locfileid: "67605059"
---
# <a name="share-to-teams-from-personal-app-or-tab"></a>从个人应用或选项卡共享到 Teams

共享到 Teams 允许用户将内容从个人应用或选项卡共享到 Teams 中的其他用户、组或频道。 用户可以选择“共享到 Teams”以在弹出窗口中启动“共享到 Teams”体验。 弹出窗口允许用户添加其他用户、组或频道来共享内容。

下图显示了“共享到 Teams”弹出窗口：

:::image type="content" source="../../assets/images/share-to-teams/share-to-teams.PNG" alt-text="share-to-teams-pop-up":::

## <a name="enable-share-to-teams-button"></a>“启用共享到 Teams”按钮

> [!NOTE]
> 确保拥有 [Microsoft Teams JavaScript 客户端 SDK](../../tabs/how-to/using-teams-client-sdk.md) 或 [Microsoft Teams JavaScript 客户端 SDK v2 预览](../../tabs/how-to/using-teams-client-sdk.md) 版 (或更高版本) `@microsoft/teams-js@1.11.0-beta.7` 为个人应用或选项卡启用“共享到 Teams”。

若要启用“共享到 Teams”，请执行以下操作：

1. 使用 **Teams Javascript 客户端 SDK** 创建个人应用或选项卡。

2. 创建 **“共享到 Teams”** 按钮。

3. 在“共享到 Teams”按钮上，使用内容有效负载调用 `microsoftTeams.sharing.shareWebContent` 。

以下示例说明如何创建内容有效负载：

```json
microsoftTeams.sharing.shareWebContent({
        content: [
          {
            type: 'URL',
            url: '<URL to be shared>',
            message: 'Default message to be loaded in the compose box',
            preview: true
          }
        ]
      });
```

有效负载包含以下参数：

| 属性名称 | 用途 |
|---|---|
| `type` | 类型必须为 `URL` |
| `url` | `URL` 要共享 |
|`message`| 要在撰写框中加载的默认消息 |
| `preview` | 设置为 `true` 启用 URL 预览 |

下图显示了“共享到 Teams”选项：

:::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="“共享到团队”按钮":::

## <a name="response-codes"></a>响应代码

下表列出了响应代码：

|响应代码|说明|
|---|---|
| **100** | 当前平台不支持 API。 |
| **404** | 未在给定位置找到指定的文件。 |
| **500** | 执行所需操作时遇到内部错误。 |
| **501** | 当前上下文不支持 API。 |
| **1000** | 用户拒绝的权限。 |
| **2000** | 网络问题。 |
| **3000** | 基础硬件不支持此功能。 |
| **4000** | 一个或多个参数无效。 |
| **5000** | 用户未获得此操作的授权。 |
| **6000** | 由于资源不足，无法完成操作。 |
| **7000** | 由于 API 调用太频繁，平台限制了请求。 |
| **8000** | 用户中止了该操作。 |
| **9000** | 平台代码为旧代码，不实现此 API。 |
| **10000** | 返回值太大，已超出我们的大小边界。 |

## <a name="limitations"></a>限制

将“共享”添加到 Teams 按钮的限制：

* 可以在 Teams 内部运行的应用中托管或嵌入“共享到 Teams”按钮。
* 可以使用 **Teams Javascript 客户端 SDK** 将“共享”按钮添加到创建的应用。

## <a name="end-user-share-to-teams-experience"></a>最终用户共享到 Teams 体验

在个人应用或选项卡上启用“共享到团队”按钮后，可以共享内容。 若要访问，请执行以下步骤：

1. 打开个人应用或选项卡，然后选择 **“共享到 Teams**”。

    :::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="“共享到团队”按钮":::

2. 添加其他用户、组或频道以共享内容。

    :::image type="content" source="../../assets/images/share-to-teams/add-recepient.PNG" alt-text="add-recipient":::

3. 选择“**共享**”。

   :::image type="content" source="../../assets/images/share-to-teams/add-notes.PNG" alt-text="add-note":::

4. 选择 **“视图** ”以访问共享链接的对话。

   :::image type="content" source="../../assets/images/share-to-teams/link-shared.PNG" alt-text="share-to-teams-link-shared":::

## <a name="see-also"></a>另请参阅

* [从 Web 应用共享到 Teams](share-to-teams-from-web-apps.md)
* [创建个人选项卡](../../tabs/how-to/create-personal-tab.md)
