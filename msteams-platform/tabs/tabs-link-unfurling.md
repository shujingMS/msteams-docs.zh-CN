---
title: 选项卡链接展开和阶段视图
author: Rajeshwari-v
description: 了解舞台视图，这是一个为显示 Web 内容而调用的全屏 UI 组件。 链接展开用于使用自适应卡片将 URL 转换为选项卡。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 2563cfd266b967bd8c55c24491165c9979bad145
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820085"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>选项卡链接展开和阶段视图

阶段视图是一个新的用户界面 (UI) 组件。 它允许呈现在 Teams 中全屏打开并固定为选项卡的内容。

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="stage-view"></a>阶段视图

阶段视图是一个全屏 UI 组件，可以调用它来显示 Web 内容。 现有链接展开服务已更新，以便使用自适应卡片和聊天服务将 URL 转换为选项卡。 当用户在聊天或频道中发送 URL 时，URL 将展开为自适应卡片。 用户可以在卡片中选择“**视图**”，并直接从阶段视图中将内容固定为选项卡。

## <a name="advantage-of-stage-view"></a>阶段视图的优点

Stage View helps provide a more seamless experience of viewing content in Teams. Users can open and view the content provided by your app without leaving the context, and they can pin the content to the chat or channel for future quick access leading to a higher user engagement with your app.

## <a name="stage-view-vs-task-module"></a>阶段视图与任务模块

|阶段视图|任务模块|
|:-----------|:-----------|
|当要向用户显示丰富的内容（例如页面、仪表板、文件等）时，阶段视图非常有用。 它提供了丰富的功能，有助于在全屏画布中呈现内容。|[任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md)对于显示需要用户注意的消息或收集移动到下一步所需的信息特别有用。|
  
## <a name="invoke-stage-view"></a>调用阶段视图

可以通过以下方式调用阶段视图：

* [从自适应卡片调用阶段视图](#invoke-stage-view-from-adaptive-card)
* [通过深层链接调用阶段视图](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>从自适应卡片调用阶段视图

当用户在 Teams 桌面客户端上输入 URL 时，将调用机器人并返回[自适应卡片](../task-modules-and-cards/cards/cards-actions.md)，并提供在阶段中打开 URL 的选项。 启动阶段并提供 `tabInfo` 后，可以添加将阶段固定为选项卡的功能。  

下图显示了从自适应卡片打开的阶段：

:::image type="content" source="../assets/images/tab-images/open-stage-from-adaptive-card1.png" alt-text="屏幕截图显示了自适应卡片中的打开阶段。"lightbox="~/assets/images/tab-images/open-stage-from-adaptive-card1.png":::

:::image type="content" source="../assets/images/tab-images/open-stage-from-adaptive-card2.png" alt-text="屏幕截图显示卡片中的打开阶段。"lightbox="~/assets/images/tab-images/open-stage-from-adaptive-card2.png":::

### <a name="example"></a>示例

下面是用于从自适应卡片打开阶段的代码：

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

`invoke` 请求类型必须为 `composeExtension/queryLink`。

> [!NOTE]
>
> * `invoke` 工作流类似于当前 `appLinking` 工作流。
> * 为了保持一致性，建议将 `Action.Submit` 命名为 `View`。
> * `websiteUrl` 是要在 `TabInfo` 对象中传递的必需属性。

下面是调用阶段视图的过程：

* When the user selects **View**, the bot receives an `invoke` request. The request type is `composeExtension/queryLink`.
* 来自机器人的 `invoke` 响应包含类型为 `tab/tabInfoAction` 的自适应卡片。
* 机器人使用 `200` 代码进行响应。

> [!NOTE]
>
> 在 Teams 移动客户端上，为通过 [Teams 应用商店](~/concepts/deploy-and-publish/apps-publish-overview.md) 分发的应用调用阶段视图，并且没有移动优化体验会打开设备的默认 Web 浏览器。 浏览器将打开 `TabInfo` 对象的 `websiteUrl` 参数中指定的 URL。

## <a name="invoke-stage-view-through-deep-link"></a>通过深层链接调用阶段视图

若要通过选项卡中的深层链接调用阶段视图，必须在 `app.openLink(url)` API 中包装深层链接 URL。 也可以通过卡片中的 `OpenURL` 操作传递深层链接。

### <a name="syntax"></a>语法

下面是深层链接语法：

`<https://teams.microsoft.com/l/stage/{appId}/0?context>={"contentUrl":"contentUrl","websiteUrl":"websiteUrl","name":"Contoso"}`

### <a name="examples"></a>示例

当用户输入 URL 时，该 URL 会展开到自适应卡片中。

下面是用于调用阶段视图的深层链接示例：

**示例 1：具有 threadId 的 URL**

未编码的 URL：

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous","threadId":"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2"}`

已编码的 URL：

`<https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D>`

**示例 2：没有 threadId 的 URL**

未编码的 URL：

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context>={"contentUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191","websiteUrl":"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true","title":"Quotes: Miscellaneous"}`

已编码

`<https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D>`

> [!NOTE]
> 粘贴 URL 之前，必须对所有深层链接进行编码。 我们不支持未编码的 URL。
>
> * `name` 在深层链接中是可选的。 如果未包含，应用名称将替换它。
> * 也可以通过 `OpenURL` 操作传递深层链接。
> * 从特定上下文启动阶段时，请确保应用在该上下文中正常工作。 例如，如果阶段视图是从个人应用启动的，则必须确保应用具有个人范围。

## <a name="tab-information-property"></a>选项卡信息属性

| 属性名称 | 类型 | 字符数 | 说明 |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | 字符串 | 64 | 此属性是选项卡所显示实体的唯一标识符。 这是必填字段。|
| `name` | String | 128 | 此属性是频道界面中选项卡的显示名称。 这是一个可选字段。|
| `contentUrl` | String | 2048 | This property is the https:// URL that points to the entity UI to be displayed in the Teams canvas. This is a required field.|
| `websiteUrl?` | String | 2048 | This property is the https:// URL to point at, if a user selects to view in a browser. This is a required field.|
| `removeUrl?` | String | 2048 | 此属性是指向用户删除选项卡时要显示的 UI 的 https:// URL。这是一个可选字段。|

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | C# |Node.js|
|-------------|-------------|------|----|
|阶段视图中的选项卡 |Microsoft Teams 选项卡示例应用，用于在阶段视图中演示选项卡。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建对话选项卡](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>另请参阅

* [Teams 的生成选项卡](what-are-tabs.md)
* [添加链接展开](../messaging-extensions/how-to/link-unfurling.md)
* [composeExtensions](../resources/schema/manifest-schema.md#composeextensions)
* [具有自适应卡片的生成选项卡](how-to/build-adaptive-card-tabs.md)
* [创建深层链接](../concepts/build-and-test/deep-links.md)
