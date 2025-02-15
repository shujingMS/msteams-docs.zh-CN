---
title: 创建传入 Webhook
author: laujan
description: 创建 Teams 应用的传入 Webhook 并将外部请求发布到 Teams。 删除传入 Webhook。 示例代码 (C#，Node.js) 使用传入 Webhook 发送卡片。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 5f6aef184805aa4ef7a68eac827b08fa8d4c12f1
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615329"
---
# <a name="create-incoming-webhooks"></a>创建传入 Webhooks

传入 Webhook 允许外部应用程序在 Microsoft Teams 频道中共享内容。 Webhook 用作跟踪和通知的工具。 Webhook 提供唯一的 URL，用于发送 JSON 有效负载，其中包含卡格式的消息。 卡片是包含与单个主题相关的内容和操作的用户界面容器。 可以在以下功能中使用卡片：

* 机器人
* 消息扩展
* 连接器

> [!IMPORTANT]
> 可以选择生成通知机器人 Teams 应用，而不是传入 Webhook。 它们的性能类似，但通知机器人具有更多功能。 有关详细信息，请参阅 [使用 JavaScript](../../sbs-gs-notificationbot.yml) 或 [传入 Webhook 通知示例生成通知](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification)机器人。 若要开始，请立即下载 [Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) 并浏览。 有关详细信息，请参阅 [Teams 工具包文档](../../toolkit/teams-toolkit-fundamentals.md)。

请参阅以下视频，了解如何创建传入 Webhook：
<br>
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4ODcY]

## <a name="key-features-of-an-incoming-webhook"></a>传入 Webhook 的主要功能

下表提供了传入 Webhook 的功能和说明：

| 功能 | Description |
| -------- | ----------- |
|使用传入 webhook 的自适应卡 | 可以通过传入 Webhook 发送自适应卡片。 有关详细信息，请参阅[使用传入 Webhook 发送自适应卡片](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)。|
|可操作消息传递支持|包括 Teams 在内的所有 Office 365 组都支持可操作消息卡片。 如果通过卡片发送消息，则必须使用可操作邮件卡格式。 有关详细信息，请参阅[可操作邮件卡参考](/outlook/actionable-messages/message-card-reference)和[消息卡片操场](https://messagecardplayground.azurewebsites.net)。|
|独立 HTTPS 消息传递支持|Cards provide information clearly and consistently. Any tool or framework that can send HTTPS POST requests can send messages to Teams through an Incoming Webhook.|
|Markdown 支持|在可操作消息传递卡片中的所有文本字段都支持基础 Markdown。 请勿在卡片中使用 HTML 标记。 HTML 会遭忽略并被视为纯文本。|
|作用域配置|传入的 Webhook 在通道级别进行作用域化和配置。|
|保护资源定义|消息的格式设置为 JSON 有效负载。 此声明性消息传送结构阻止插入恶意代码。|

<!--- TBD: A note should be short and eye-catching. No need to put a list item inside a Note or any admonition for that matter. Re-write the below list item.
--->

> [!NOTE]
>
> * Teams 机器人、消息扩展、传入 Webhook 和机器人框架支持自适应卡片。 自适应卡片是可在所有平台（如 Windows、Android、iOS 等）中使用的开放式跨卡平台框架。 目前，[Teams 连接器](../../webhooks-and-connectors/how-to/connectors-creating.md)不支持自适应卡片。 但是，可以创建一个将自适应卡片发布到 Teams 频道的[流](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)。
> * 有关卡片和 Webhook 的详细信息，请参阅[自适应卡片和传入 Webhook](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)。

## <a name="create-an-incoming-webhook"></a>创建传入 Webhook

若要将传入 Webhook 添加到 Teams 频道，请执行以下步骤：

1. 打开要在其中添加 Webhook 的频道，然后选择 &#8226;&#8226;&#8226; **顶部导航栏中** 的更多选项。
1. 从下拉菜单中选择 **连接器**：

   :::image type="content" source="../../assets/images/connectors.png" alt-text="此屏幕截图显示了如何选择连接器。":::

1. 搜索 **传入 Webhook** 并选择 **添加**。
1. 选择 **配置**，提供名称，并在必要时上传 Webhook 的图像：

   :::image type="content" source="../../assets/images/configure.png" alt-text="此屏幕截图显示了如何配置和上传 Webhook 的图像。":::

1. 复制并保存对话框窗口中存在的唯一 Webhook URL。 URL 映射到频道，你可以使用它将信息发送到 Teams。 选择“**完成**”。

   :::image type="content" source="../../assets/images/url.png" alt-text="此屏幕截图显示了唯一的 Webhook URL。":::

Webhook 在 Teams 频道中可用。

可以通过传入 Webhook 或 Office 365 连接器创建和发送可操作邮件。 有关详细信息，请参阅[创建和发送消息](~/webhooks-and-connectors/how-to/connectors-using.md)。

> [!NOTE]
> 在 Teams 中，选择“**设置**” > “**成员权限**” > “**允许成员创建、更新、删除连接器**，以便任何团队成员添加、修改或删除连接器。

## <a name="remove-an-incoming-webhook"></a>删除传入 Webhook

若要从 Teams 频道中删除传入 Webhook，请执行以下步骤：

1. 打开频道并选择&#8226;&#8226;&#8226; **顶部导航栏中** 的更多选项。
1. 从下拉菜单中选择 **连接器**。
1. 选择 **Configured** 下 **Manage** 下。
1. 选择 **<*1*> 已配置** 查看当前连接器的列表：

   :::image type="content" source="../../assets/images/configured.png" alt-text="此屏幕截图显示如何配置为查看当前连接器的列表。":::

1. 选择 **管理要删除的连接器的** ：

   :::image type="content" source="../../assets/images/manage.png" alt-text="此屏幕截图显示了如何管理要删除的连接器。":::

1. 选择 **Remove** 以查看 **"移动配置** 对话框。

   :::image type="content" source="../../assets/images/removeconfiguration.png" alt-text="此屏幕截图显示了如何查看“删除配置”对话框。":::

1. 完成对话框字段和复选框，然后选择 **删除**。

   :::image type="content" source="../../assets/images/finalremove.png" alt-text="此屏幕截图显示了如何从 Teams 频道中删除传入 Webhook。":::

## <a name="code-sample"></a>代码示例

| 示例名称           | 说明 | C#    |  TypeScript |
|:---------------------|:--------------|:---------|:--------|
|传入 Webhook|此示例代码演示如何使用传入 Webhook 发送卡。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/incoming-webhook/csharp)|[View](https://github.com/OfficeDev/TeamsFx-Samples/tree/release/incoming-webhook-notification) |

## <a name="see-also"></a>另请参阅

* [创建传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [创建和发送邮件](~/webhooks-and-connectors/how-to/connectors-using.md)
* [从 Web 应用共享到 Teams](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [集成 web 应用](~/samples/integrate-web-apps-overview.md)
* [保护 Azure 逻辑应用中的访问和数据](/azure/logic-apps/logic-apps-securing-a-logic-app)
* [使用 JavaScript 生成通知机器人](../../sbs-gs-notificationbot.yml)
* [使用 JavaScript 生成第一个机器人应用](../../sbs-gs-bot.yml)
