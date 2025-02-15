---
title: 使用 RSC 接收所有频道消息
author: surbhigupta12
description: 允许机器人接收所有通道消息，而无需使用 RSC 权限@mentioned。 阅读清单中的 webApplicationInfo 或授权部分。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: db51bcddaa22a115330129ddc677f0401c8bd523
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586908"
---
# <a name="receive-all-channel-messages-with-rsc"></a>使用 RSC 接收所有频道消息

最初针对 Teams Graph API 开发的资源特定许可 (RSC) 权限模型已扩展到机器人方案。

使用 RSC，现在可以请求团队所有者同意机器人接收团队中标准频道的用户消息，无需提及。 可以通过在已启用 RSC 的 Teams 应用中指定 `ChannelMessage.Read.Group` 权限来启用此功能。 配置后，团队所有者可以在应用安装过程中授予许可。

有关为应用启用 RSC 的详细信息，请参阅 [Teams 中的资源特定许可](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)。

## <a name="enable-bots-to-receive-all-channel-messages"></a>使机器人能够接收所有频道消息

`ChannelMessage.Read.Group` RSC 权限已扩展到机器人。 在用户同意的情况下，此权限允许图形应用程序获取对话和机器人中的所有消息，以接收所有频道消息，而无需提及。

> [!NOTE]
>
> * 需要访问所有 Teams 消息数据的服务必须使用 Graph API，这些 API 还提供对频道和聊天中存档数据的访问权限。
> * 机器人必须使用相应的 `ChannelMessage.Read.Group` RSC 权限来构建和增强团队中用户的参与体验，否则不会通过应用商店批准。 应用说明必须包含机器人如何使用它读取的数据。
> * 机器人可能无法使用 `ChannelMessage.Read.Group` RSC 权限来提取大量客户数据。

## <a name="update-app-manifest"></a>更新应用清单

若要让机器人接收所有频道消息，必须使用 `webApplicationInfo` 属性中指定的 `ChannelMessage.Read.Group` 权限在 Teams 应用清单文件中配置 RSC。

:::image type="content" source="~/bots/how-to/conversations/Media/appmanifest.png" alt-text="应用清单更新的屏幕截图。":::

下面是 `webApplicationInfo` 对象的示例：

* **id**：Microsoft Azure Active Directory (Azure AD) 应用 ID。 它可以与机器人 ID 相同。
* **resource**：任何字符串。 此字段在 RSC 中没有操作，但必须添加并包含值以免出现错误响应。
* **applicationPermissions**：必须指定具有 `ChannelMessage.Read.Group` 的应用的 RSC 权限。 有关详细信息，请参阅[资源特定权限](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)。

以下代码是应用清单示例：

```json
"webApplicationInfo": {
  "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
  "resource": "https://AnyString",
  "applicationPermissions": [
    "ChannelMessage.Read.Group"
  ]
}
```

## <a name="sideload-in-a-team"></a>团队中的旁加载

若要在团队中旁加载以进行测试，不论是否在未被提及的情况下接收团队中具有 RSC 的所有频道消息：

1. 选择或创建团队。
1. 从左侧窗格中选择省略号 &#x25CF;&#x25CF;&#x25CF。 此时将显示下拉菜单。
1. 从下拉菜单中选择“**管理团队**”。 此时将显示详细信息。

   :::image type="content" source="Media/managingteam.png" alt-text="Teams 应用程序中管理团队选项的屏幕截图。":::

1. 选择“**应用**”。 此时将显示多个应用。

1. 从右下角选择 **上传自定义应用**。

      :::image type="content" source="Media/uploadingcustomapp.png" alt-text="上传自定义应用选项的屏幕截图。":::
  
1. 从“**打开**”对话框中选择应用程序包。

1. 选择 **“打开”**。

      :::image type="content" source="Media/selectapppackage.png" alt-text="用于选择应用包的打开对话框的屏幕截图。" lightbox="Media/selectapppackage.png":::

1. 从应用详细信息弹出窗口中选择“**添加**”，以便将机器人添加到选定团队。

      :::image type="content" source="Media/addingbot.png" alt-text="用于向团队添加机器人的“添加”按钮的屏幕截图。" lightbox="Media/addingbot.png":::

1. 选择一个频道并在机器人频道中输入消息。

    机器人可以在未提及的情况下接收消息。

      :::image type="content" source="Media/botreceivingmessage.png" alt-text="机器人在频道中接收消息的屏幕截图。" lightbox="Media/botreceivingmessage.png":::

## <a name="code-snippets"></a>代码段

以下代码提供 RSC 权限示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text("Using RSC the bot can receive messages across channels in team without being @mentioned."));
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
this.onMessage(async (context, next) => {
   await context.sendActivity(MessageFactory.text("Using RSC the bot can receive messages across channles in team without being @mentioned."))
   await next();
});
```

---

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | C# |Node.js|
|-------------|-------------|------|----|
|具有 RSC 权限的频道消息| Microsoft Teams 示例应用演示机器人如何在未被提及的情况下通过 RSC 接收所有频道消息。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>另请参阅

* [智能机器人对话](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [特定于资源的同意](/microsoftteams/resource-specific-consent)
* [测试资源特定许可](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [在 Teams 中上传自定义应用](~/concepts/deploy-and-publish/apps-upload.md)
* [列出频道中对消息的答复](/graph/api/chatmessage-list-replies?view=graph-rest-1.0&tabs=http&preserve-view=true)
