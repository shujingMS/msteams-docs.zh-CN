---
title: 清单架构参考
description: 在本文中，你将拥有适用于 Microsoft Teams 参考、架构和示例完整清单的最新版本的公共清单架构。
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 2638c668bf1363a0f997786bcb958689626c70c6
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499172"
---
# <a name="app-manifest-schema-for-teams"></a>Teams 的应用清单架构

Microsoft Teams 应用清单介绍了应用如何集成到 Microsoft Teams 产品中。 应用清单必须符合托管在 [`https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json) 的架构。 以前的版本 1.0、1.1、...、1.13 和当前版本 1.14 均受支持（在 URL 中使用“v1.x”）。
有关每个版本中所做的更改的详细信息，请参阅[管理更改日志](https://github.com/OfficeDev/microsoft-teams-app-schema/releases)。

根据不同的应用方案，下表列出了 TeamsJS 版本和应用清单版本：

[!INCLUDE [pre-release-label](~/includes/teamjs-version-details.md)]

以下架构示例显示所有扩展性选项：

## <a name="sample-full-manifest"></a>示例完整清单

```json
{
    "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.14/MicrosoftTeams.schema.json",
    "manifestVersion": "1.14",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "localizationInfo": {
        "defaultLanguageTag": "en-us",
        "additionalLanguages": [
            {
                "languageTag": "es-es",
                "file": "en-us.json"
            }
        ]
    },
    "developer": {
        "name": "Publisher Name",
        "websiteUrl": "https://website.com/",
        "privacyUrl": "https://website.com/privacy",
        "termsOfUseUrl": "https://website.com/app-tos",
        "mpnId": "1234567890"
    },
    "name": {
        "short": "Name of your app (<=30 chars)",
        "full": "Full name of app, if longer than 30 characters (<=100 chars)"
    },
    "description": {
        "short": "Short description of your app (<= 80 chars)",
        "full": "Full description of your app (<= 4000 chars)"
    },
    "icons": {
        "outline": "A relative path to a transparent .png icon — 32px X 32px",
        "color": "A relative path to a full color .png icon — 192px X 192px"
    },
    "accentColor": "A valid HTML color code.",
    "configurableTabs": [
        {
            "configurationUrl": "https://contoso.com/teamstab/configure",
            "scopes": [
                "team",
                "groupchat"
            ],
            "canUpdateConfiguration": true,
            "context": [
                "channelTab",
                "privateChatTab",
                "meetingChatTab",
                "meetingDetailsTab",
                "meetingSidePanel",
                "meetingStage"
            ],
            "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
            "supportedSharePointHosts": [
                "sharePointFullPage",
                "sharePointWebPart"
            ]
        }
    ],
    "staticTabs": [
        {
            "entityId": "unique Id for the page entity",
            "scopes": [
                "personal"
            ],
            "context": [
                "personalTab",
                "channelTab"
            ],
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
            "websiteUrl": "https://contoso.com/content (displayed in web browser)",
            "searchUrl": "https://contoso.com/content (displayed in web browser)"
        }
    ],
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "scopes": [
                "team",
                "personal",
                "groupchat"
            ],
            "needsChannelSelector": false,
            "isNotificationOnly": false,
            "supportsFiles": true,
            "supportsCalling": false,
            "supportsVideo": true,
            "commandLists": [
                {
                    "scopes": [
                        "team",
                        "groupchat"
                    ],
                    "commands": [
                        {
                            "title": "Command 1",
                            "description": "Description of Command 1"
                        },
                        {
                            "title": "Command 2",
                            "description": "Description of Command 2"
                        }
                    ]
                },
                {
                    "scopes": [
                        "personal",
                        "groupchat"
                    ],
                    "commands": [
                        {
                            "title": "Personal command 1",
                            "description": "Description of Personal command 1"
                        },
                        {
                            "title": "Personal command N",
                            "description": "Description of Personal command N"
                        }
                    ]
                }
            ]
        }
    ],
    "connectors": [
        {
            "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
            "scopes": [
                "team"
            ],
            "configurationUrl": "https://contoso.com/teamsconnector/configure"
        }
    ],
    "composeExtensions": [
        {
            "canUpdateConfiguration": true,
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "commands": [
                {
                    "id": "exampleCmd1",
                    "title": "Example Command",
                    "type": "query",
                    "context": [
                        "compose",
                        "commandBox"
                    ],
                    "description": "Command Description; e.g., Search on the web",
                    "initialRun": true,
                    "fetchTask": false,
                    "parameters": [
                        {
                            "name": "keyword",
                            "title": "Search keywords",
                            "inputType": "text",
                            "description": "Enter the keywords to search for",
                            "value": "Initial value for the parameter",
                            "choices": [
                                {
                                    "title": "Title of the choice",
                                    "value": "Value of the choice"
                                }
                            ]
                        }
                    ]
                },
                {
                    "id": "exampleCmd2",
                    "title": "Example Command 2",
                    "type": "action",
                    "context": [
                        "message"
                    ],
                    "description": "Command Description; e.g., Add a customer",
                    "initialRun": true,
                    "fetchTask": false ,
                    "parameters": [
                        {
                            "name": "custinfo",
                            "title": "Customer name",
                            "description": "Enter a customer name",
                            "inputType": "text"
                        }
                    ]
                },
                {
                    "id": "exampleCmd3",
                    "title": "Example Command 3",
                    "type": "action",
                    "context": [
                        "compose",
                        "commandBox",
                        "message"
                    ],
                    "description": "Command Description; e.g., Add a customer",
                    "fetchTask": false,
                    "taskInfo": {
                        "title": "Initial dialog title",
                        "width": "Dialog width",
                        "height": "Dialog height",
                        "url": "Initial webview URL"
                    }
                }
            ],
            "messageHandlers": [
                {
                    "type": "link",
                    "value": {
                        "domains": [
                            "mysite.someplace.com",
                            "othersite.someplace.com"
                        ]
                    }
                }
            ]
        }
    ],
    "permissions": [
        "identity",
        "messageTeamMembers"
    ],
    "devicePermissions": [
        "geolocation",
        "media",
        "notifications",
        "midi",
        "openExternal"
    ],
    "validDomains": [
        "contoso.com",
        "mysite.someplace.com",
        "othersite.someplace.com"
    ],
    "webApplicationInfo": {
        "id": "AAD App ID",
        "resource": "Resource URL for acquiring auth token for SSO"
    },
    "authorization": {
        "permissions": {
            "resourceSpecific": [
                {
                    "type": "Application",
                    "name": "ChannelSettings.Read.Group"
                },
                {
                    "type": "Delegated",
                    "name": "ChannelMeetingParticipant.Read.Group"
                }
            ]
        }
    },
    "showLoadingIndicator": false,
    "isFullScreen": false,
    "activities": {
        "activityTypes": [
            {
                "type": "taskCreated",
                "description": "Task created activity",
                "templateText": "<team member> created task <taskId> for you"
            },
            {
                "type": "userMention",
                "description": "Personal mention activity",
                "templateText": "<team member> mentioned you"
            }
        ]
    },
    "defaultBlockUntilAdminAction": true,
    "publisherDocsUrl": "https://website.com/app-info",
    "defaultInstallScope": "meetings",
    "defaultGroupCapability": {
        "meetings": "tab",
        "team": "bot",
        "groupchat": "bot"
    },
    "configurableProperties": [
        "name",
        "shortDescription",
        "longDescription",
        "smallImageUrl",
        "largeImageUrl",
        "accentColor",
        "developerUrl",
        "privacyUrl",
        "termsOfUseUrl"
    ],
    "subscriptionOffer": {
        "offerId": "publisherId.offerId"
    },
    "meetingExtensionDefinition": {
        "scenes": [
            {
                "id": "9082c811-7e6a-4174-8173-6ccd57d377e6",
                "name": "Getting started sample",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 0
            },
            {
                "id": "afeaed22-f89b-48e1-98b4-46a514344e4a",
                "name": "Sample-1",
                "file": "scenes/sceneMetadata.json",
                "preview": "scenes/scenePreview.png",
                "maxAudience": 15,
                "seatsReservedForOrganizersOrPresenters": 3
            }
        ]
    }
}
```

架构定义以下属性：

## <a name="schema"></a>$schema

可选，但建议 — 的字符串

引用清单的 JSON 架构的 https:// URL。

## <a name="manifestversion"></a>manifestVersion

**必需**— 字符串

此清单使用的清单架构版本。 使用 `1.13` 在 Outlook 和 Office 中启用 Teams 应用支持；对仅限 Teams 的应用使用 `1.12`（或更早版本）。

## <a name="version"></a>version

**必需**— 字符串

特定应用的版本。 更新清单中的内容时，版本也必须递增。 这样，当安装新清单时，它将覆盖现有清单，并且用户会收到新功能。 将此应用提交到应用商店时，必须重新提交并重新验证新清单。 应用用户会在清单获得批准后几小时内自动收到新的更新清单。

如果应用请求权限更改，系统会提示用户升级并重新进入应用。

此版本字符串必须遵循[semver](http://semver.org/)标准 (MAJOR.MINOR.PATCH)。

## <a name="id"></a>ID

**必需**—Microsoft 应用 ID

ID 是 Microsoft 为应用生成的唯一标识符。 如果机器人是通过Microsoft Bot Framework注册的，则有一个 ID。 如果你的选项卡的 Web 应用已使用 Microsoft 登录，则你有一个 ID。 必须在此处输入 ID。 否则，必须在 [Microsoft 应用程序注册门户](https://aka.ms/appregistrations)生成新 ID。 如果添加机器人，请使用相同的 ID。

> [!NOTE]
> 如果要将更新提交到 AppSource 中的现有应用，则不得修改清单中的 ID。

## <a name="developer"></a>developer

**必需**— 对象

指定有关公司的信息。 对于提交到 Teams 应用商店的应用，这些值必须与应用商店一览中的信息匹配。 有关详细信息，请参阅 [Teams Store 发布指南](~/concepts/deploy-and-publish/appsource/publish.md)。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`name`|32 个字符|✔️|开发人员的显示名称。|
|`websiteUrl`|2048 个字符|✔️|开发人员网站的 https:// URL。 此链接必须将用户转到公司或产品特定的登陆页面。|
|`privacyUrl`|2048 个字符|✔️|开发人员隐私策略的 https:// URL。|
|`termsOfUseUrl`|2048 个字符|✔️|开发人员使用条款的 https:// URL。|
|`mpnId`|10 个字符| |**可选** 标识生成应用的合作伙伴组织的Microsoft 合作伙伴网络 ID。|

## <a name="name"></a>name

**必需**— 对象

应用体验的名称，在 Teams 体验中向用户显示。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。 `short`和`full`的值必须不同。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`short`|30 个字符|✔️|应用的短显示名称。|
|`full`|100 个字符||如果完整应用名称超过 30 个字符，则使用应用的全名。|

## <a name="description"></a>说明

**必需**— 对象

向用户描述应用。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。

确保说明描述你的体验，并帮助潜在客户了解你的体验。 如果需要使用外部帐户，则必须在完整说明中进行说明。 `short`和`full`的值必须不同。 不能在长说明中重复简短说明，也不得包含任何其他应用名称。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`short`|80 个字符|✔️|应用体验的简短说明，在空间受限时使用。|
|`full`|4000 个字符|✔️|应用的完整说明。|

## <a name="localizationinfo"></a>localizationInfo

**可选**— 对象

Allows the specification of a default language and provides pointers to more language files. For more information, see [localization](~/concepts/build-and-test/apps-localization.md).

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`defaultLanguageTag`||✔️|此顶级清单文件中字符串的语言标记。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

指定更多语言翻译的对象数组。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`languageTag`||✔️|所提供文件中字符串的语言标记。|
|`file`||✔️|包含已翻译字符串的 .json 文件的相对文件路径。|

## <a name="icons"></a>图标

**必需**— 对象

Teams 应用中使用的图标。 图标文件必须作为上传包的一部分包含在内。 有关详细信息，请参阅 [图标](../../concepts/build-and-test/apps-package.md#app-icons)。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`outline`|32 x 32 像素|✔️|透明 32x32 PNG 大纲图标的相对文件路径。|
|`color`|192 x 192 像素|✔️|完整颜色 192x192 PNG 图标的相对文件路径。|

## <a name="accentcolor"></a>accentColor

**必需**— HTML 十六进制颜色代码

要使用的颜色和大纲图标的背景。

该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee`。

## <a name="configurabletabs"></a>configurableTabs

**可选**— 数组

当应用体验具有团队频道选项卡体验时使用，该体验需要在添加之前进行额外的配置。 只能在 `team` 和 `groupchat` 作用域中使用可配置的选项卡，并且可以多次配置相同的选项卡。 但是，只能在清单中定义一次。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔️|配置选项卡时要使用的 https:// URL。|
|`scopes`|枚举数组|1|✔️|目前，可配置选项卡仅支持 `team` 和 `groupchat` 范围。 |
|`canUpdateConfiguration`|Boolean|||A value indicating whether an instance of the tab's configuration can be updated by the user after creation. Default: **true**.|
|`context` |枚举数组|6||[支持选项卡](../../tabs/how-to/access-teams-context.md)的 `contextItem` 范围的集合。 默认值：**[channelTab， privateChatTab， meetingChatTab， meetingDetailsTab]**。|
|`sharePointPreviewImage`|string|2048||A relative file path to a tab preview image for use in SharePoint. Size 1024x768. |
|`supportedSharePointHosts`|枚举数组|1||Defines how your tab is made available in SharePoint. Options are `sharePointFullPage` and `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

**可选**— 数组

定义默认情况下可以"固定"的一组选项卡，而无需用户手动添加它们。 在 `personal` 范围内声明的静态选项卡始终固定到应用的个人体验。 当前不支持在 `team` 作用域中声明的静态选项卡。

此项是一个数组（最多 16 个元素），其类型的所有元素 `object`。 只有提供静态选项卡解决方案的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`entityId`|string|64 个字符|✔️|选项卡显示的实体的唯一标识符。|
|`name`|string|128 个字符|✔️|通道接口中选项卡的显示名称。|
|`contentUrl`|string||✔️|指向要在 Teams 画布中显示的实体 UI 的 https:// URL。|
|`websiteUrl`|string|||要指向用户是否选择在浏览器中查看的 https:// URL。|
|`searchUrl`|string|||要指向用户搜索查询的 https:// URL。|
|`scopes`|枚举数组|1|✔️|目前，静态选项卡仅支持 `personal` 范围，这意味着只能将其预配为个人体验的一部分。|
|`context` | 枚举数组| 2|| 支持选项卡的 `contextItem` 范围集。|

> [!NOTE]
> The searchUrl feature is not available for the third-party developers.
> If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, For more information, see [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).

## <a name="bots"></a>机器人

**可选**— 数组

定义机器人解决方案以及可选信息（如默认命令属性）。

该项是一个数组（目前每个应用仅允许一个机器人&mdash;最多一个元素），类型为 `object`的所有元素。 只有提供机器人体验的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64 个字符|✔️|使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 ID 可以与整体[应用 ID](#id)相同。|
|`scopes`|枚举数组|3|✔️|Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`). These options are non-exclusive.|
|`needsChannelSelector`|Boolean|||Describes whether or not the bot uses a user hint to add the bot to a specific channel. Default: **`false`**|
|`isNotificationOnly`|布尔值|||Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot. Default: **`false`**|
|`supportsFiles`|布尔值|||Indicates whether the bot supports the ability to upload/download files in personal chat. Default: **`false`**|
|`supportsCalling`|Boolean|||一个值，该值指示机器人支持音频调用的位置。 **IMPORTANT**： 此属性当前为实验性属性。 实验性属性可能无法完成，并且在完全可用之前可能会进行更改。  该属性仅用于测试和探索目的，不得在生产应用程序中使用。 默认值：**`false`**|
|`supportsVideo`|Boolean|||一个值，该值指示机器人支持视频通话的位置。 **IMPORTANT**： 此属性当前为实验性属性。 实验性属性可能无法完成，并且在完全可用之前可能会进行更改。  该属性仅用于测试和探索目的，不得在生产应用程序中使用。 默认值：**`false`**|

### <a name="botscommandlists"></a>bots.commandLists

机器人可以向用户推荐的命令的列表。 对象是一个数组（最多两个元素），其类型为 `object`;必须为机器人支持的每个范围定义一个单独的命令列表。 有关详细信息，请参阅 [机器人菜单](~/bots/how-to/create-a-bot-commands-menu.md)。

|名称| 类型| 最大大小 | 必需 | Description|
|---|---|---|---|---|
|`items.scopes`|枚举数组|3|✔️|Specifies the scope for which the command list is valid. Options are `team`, `personal`, and `groupchat`.|
|`items.commands`|对象数组|10|✔️|自动程序支持的命令数组：<br>`title`：自动程序命令名称（字符串，32）<br>`description`：命令语法及其参数的简单说明或示例（字符串，128）。|

### <a name="botscommandlistscommands"></a>bots.commandLists.commands

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|title|string|12 |✔️|机器人命令名称。|
|description|string|128 个字符|✔️|简单的文本说明或命令语法及其参数的示例。|

## <a name="connectors"></a>连接器

**可选**— 数组

`connectors`块定义应用的 Office 365 连接器。

对象是一个数组（最多一个元素），其中所有元素的类型为 `object`。 只有提供连接器的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|string|2048 个字符|✔️|配置连接器时要使用的 https:// URL。|
|`scopes`|枚举数组|1|✔️|Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`). Currently, only the `team` scope is supported.|
|`connectorId`|string|64 个字符|✔️|连接器的唯一标识符，与[Connectors 开发人员仪表板](https://aka.ms/connectorsdashboard)中的 ID 匹配。|

## <a name="composeextensions"></a>composeExtensions

**可选**— 数组

定义应用的消息扩展。

> [!NOTE]
> 2017 年 11 月，该功能的名称已从“撰写扩展”更改为“消息扩展”，但清单名称保持不变，以便现有扩展可以继续运行。

该项是一个数组（最大值为一个元素），其中所有元素的类型。 `object` 只有提供消息扩展的解决方案才需要此块。

|名称| 类型 | 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|string|64|✔️|支持消息扩展的机器人的唯一 Microsoft 应用 ID，已向机器人框架注册。 ID 可以与整体应用 ID 相同。|
|`commands`|对象数组|10|✔️|消息扩展支持的命令数组。|
|`canUpdateConfiguration`|Boolean|||A value indicating whether the configuration of a message extension can be updated by the user. Default: **false**.|
|`messageHandlers`|对象数组|5||允许在满足特定条件时调用应用的处理程序列表。|
|`messageHandlers.type`|string|||The type of message handler. Must be `"link"`.|
|`messageHandlers.value.domains`|字符串数组|||链接消息处理程序可以注册的域数组。|

### <a name="composeextensionscommands"></a>composeExtensions.commands

消息扩展必须声明一个或多个命令，最多为 10 个命令。 每个命令都显示在 Microsoft Teams 中，作为来自基于 UI 的入口点的潜在交互。

每个命令项都是具有以下结构的对象：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|64 个字符|✔️|命令的 ID。|
|`title`|string|32 个字符|✔️|用户友好的命令名称。|
|`type`|string|64 个字符||命令的类型。 `query`或`action`之一。 默认值： **查询**。|
|`description`|string|128 个字符||向用户显示以指示此命令用途的说明。|
|`initialRun`|Boolean|||A Boolean value indicates whether the command runs initially with no parameters. Default is **false**.|
|`context`|字符串数组|3||定义可以从何处调用消息扩展插件。 `compose`、`commandBox`、`message`的任何组合。 默认值为“`["compose","commandBox"]`”。|
|`fetchTask`|Boolean|||A Boolean value that indicates if it must fetch the task module dynamically. Default is **false**.|
|`taskInfo`|object|||指定使用消息扩展命令时要预加载的任务模块。|
|`taskInfo.title`|string|64 个字符||初始对话框标题。|
|`taskInfo.width`|string|||对话框宽度 - 数字（以像素为单位）或默认布局，如"large"、"medium"或"small"。|
|`taskInfo.height`|string|||对话框高度 - 数字（以像素为单位）或默认布局，如"large"、"medium"或"small"。|
|`taskInfo.url`|string|||初始 Web 视图 URL。|
|`parameters`|对象数组|5 个项目|✔️|命令采用的参数列表。 最小值：1;最大值： 5。|
|`parameters.name`|string|64 个字符|✔️|The name of the parameter as it appears in the client. The parameter name is included in the user request.|
|`parameters.title`|string|32 个字符|✔️|参数的用户友好标题。|
|`parameters.description`|string|128 个字符||描述此参数用途的用户友好字符串。|
|`parameters.value`|string|512 个字符||参数的初始值。 当前不支持该值|
|`parameters.inputType`|string|128 个字符||Defines the type of control displayed on a task module for`fetchTask: false` . One of `text, textarea, number, date, time, toggle, choiceset` .|
|`parameters.choices`|对象数组|10 项||`choiceset`的选择选项。 仅当`parameter.inputType``choiceset`时使用。|
|`parameters.choices.title`|string|128 个字符|✔️|选择的标题。|
|`parameters.choices.value`|string|512 个字符|✔️|选项的值。|

## <a name="permissions"></a>permissions

**Optional**—字符串数组

An array of `string`, which specifies which permissions the app requests, which let end users know how the extension does. The following options are non-exclusive:

* `identity`&emsp;需要用户标识信息。
* `messageTeamMembers`&emsp;请求向团队成员发送直接消息的权限。

Changing these permissions during app update, causes your users to repeat the consent process after they run the updated app. For more information, see [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).

> [!NOTE]
> 现已弃用这些权限。

## <a name="devicepermissions"></a>devicePermissions

**Optional**—字符串数组

Provides the native features on a user's device that your app requests access to. Options are:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**可选**，除非 **所述的必需**。

应用应在 Teams 客户端中加载的网站的有效域列表。 域列表可以包含通配符，例如，`*.example.com`。 有效域与域的一个段完全匹配;如果需要匹配 `a.b.example.com`则使用 `*.*.example.com`。 如果选项卡配置或内容 UI 导航到选项卡配置以外的任何其他域，则必须在此处指定该域。

请 **不要** 包含要在应用中支持的标识提供程序的域。 例如，若要使用 Google ID 进行身份验证，需要重定向到 accounts.google.com，但是，不得在 `validDomains[]`其中包含 accounts.google.com。

需要自己的 SharePoint URL 才能正常运行的 Teams 应用包括 "{teamsitedomain}>在其有效域列表中。

> [!IMPORTANT]
> 不要直接或通过通配符添加超出控制范围的域。 例如， `yourapp.onmicrosoft.com` 有效，但是， `*.onmicrosoft.com` 无效。

对象是一个数组，其中包含类型的所有元素 `string`。

## <a name="webapplicationinfo"></a>webApplicationInfo

**可选**— 对象

提供 Azure Active Directory 应用 ID 和 Microsoft Graph 信息，以帮助用户无缝登录到应用。 如果应用已在 Microsoft Azure Active Directory (Azure AD) 中注册，则必须提供应用 ID。 管理员可以在 Teams 管理中心轻松查看权限并授予同意。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|string|36 个字符|✔️|应用的 Azure AD 应用程序 ID。 此 ID 必须是 GUID。|
|`resource`|string|2048 个字符|✔️|用于获取 SSO 的身份验证令牌的应用的资源 URL。 </br> **注意：** 如果未使用 SSO，请确保在此字段中将虚拟字符串值输入到应用清单，例如， `https://notapplicable` 以避免错误响应。 |

## <a name="graphconnector"></a>graphConnector

**可选**— 对象

指定应用的 Graph 连接器配置。 如果存在，则还必须指定 [webApplicationInfo.id](#webapplicationinfo) 。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`notificationUrl`|string|2048 个字符|✔️|应在其中发送应用程序的 Graph 连接器通知的 URL。|

## <a name="showloadingindicator"></a>showLoadingIndicator

**可选**— 布尔值

指示是否在加载应用或选项卡时显示加载指示器。 默认为 **false**。
>[!NOTE]
>如果在应用清单中选择 `showLoadingIndicator` 为 true，若要正确加载页面，请根据 [“显示本机加载指示器](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) ”文档中所述修改选项卡和任务模块的内容页。

## <a name="isfullscreen"></a>isFullScreen

 **可选**— 布尔值

指示是否在没有选项卡标题栏（表示全屏模式）的情况下呈现个人应用。 默认为 **false**。

> [!NOTE]
>
> * `isFullScreen` 仅适用于发布到组织的应用。 旁加载和已发布的第三方应用无法使用此属性（将被忽略）。
>
> * `isFullScreen=true` 将从个人应用和任务模块对话框中删除 Teams 提供的标头栏和标题。

## <a name="activities"></a>activities

**可选**— 对象

定义应用用于发布用户活动源的属性。

|名称| 类型| 最大大小 | 必需 | Description|
|---|---|---|---|---|
|`activityTypes`|对象数组|128 个项目| | 提供应用可以发布到用户活动源的活动类型。|

### <a name="activitiesactivitytypes"></a>activities.activityTypes

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`type`|string|32 个字符|✔️|通知类型。 *请参阅下文*。|
|`description`|string|128 个字符|✔️|A brief description of the notification. *See below*.|
|`templateText`|string|128 个字符|✔️|例如："{actor} 为你创建了任务 {taskId}"|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***

## <a name="defaultinstallscope"></a>defaultInstallScope

**可选** - 字符串

指定默认情况下为此应用定义的安装范围。 定义的范围将是当用户尝试添加应用时按钮上显示的选项。 选项有：

* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a>defaultGroupCapability

**可选** - object

When a group install scope is selected, it will define the default capability when the user installs the app. Options are:

* `team`
* `groupchat`
* `meetings`

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`team`|string|||When the install scope selected is `team`, this field specifies the default capability available. Options: `tab`, `bot`, or `connector`.|
|`groupchat`|string|||When the install scope selected is `groupchat`, this field specifies the default capability available. Options: `tab`, `bot`, or `connector`.|
|`meetings`|string|||When the install scope selected is `meetings`, this field specifies the default capability available. Options: `tab`, `bot`, or `connector`.|

## <a name="configurableproperties"></a>configurableProperties

**可选** - 数组

`configurableProperties`此块定义管理员可Teams的应用程序属性。 有关详细信息，请参阅启用 [应用自定义](~/concepts/design/enable-app-customization.md)。 自定义或 LOB 应用中不支持应用自定义功能。

> [!NOTE]
> 必须定义至少一个属性。 最多可以在此块中定义九个属性。

可以定义以下任一属性：

* [名称](#name)：应用的显示名称。
* [shortDescription](#description)：应用的简短说明。
* [longDescription](#description)：应用的长描述。
* [smallImageUrl](#icons)：应用的大纲图标。
* [largeImageUrl](#icons)：应用的颜色图标。
* [accentColor](#accentcolor)：要使用的颜色和轮廓图标的背景。
* [developerUrl](#developer)：开发人员网站的 HTTPS URL。
* [privacyUrl](#developer)：开发人员隐私策略的 HTTPS URL。
* [termsOfUseUrl](#developer)：开发人员使用条款的 HTTPS URL。

## <a name="supportedchanneltypes"></a>supportedChannelTypes

**可选** - 数组

在非标准频道中启用应用。 如果应用支持团队范围，并且定义了此属性，Teams 会在每个频道类型中相应地启用应用。 当前支持专用频道和共享频道类型。

> [!NOTE]
>
> * 如果应用支持团队范围，则无论在此属性中定义的值如何，它都会在标准频道中运行。
> * 应用可以考虑每个频道类型的唯一属性，以便正常运行。 若要为专用频道和共享频道启用选项卡，请参 [阅在专用通道中检索上下文](~/tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) 并在 [共享通道中获取上下文](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

## <a name="defaultblockuntiladminaction"></a>defaultBlockUntilAdminAction

**可选** - 布尔值

当 `defaultBlockUntilAdminAction` 属性设置为 **true** 时，应用默认向用户隐藏，直到管理员允许它。 如果设置为 **true，** 则应用将隐藏所有租户和最终用户。 租户管理员可以在管理中心内Teams应用，并采取措施以允许或阻止该应用。 默认值为 **false**。 有关默认应用块的详细信息，请 [参阅默认情况下为用户阻止应用，直到管理员批准](../../concepts/design/enable-app-customization.md#block-apps-by-default-for-users-until-an-admin-approves)

## <a name="publisherdocsurl"></a>publisherDocsUrl

**可选** - 字符串

**最大大小** - 128 个字符

是一个指向信息页的 HTTPS URL，供管理员在允许应用之前获取指南， `publisherDocsUrl` 此应用默认被阻止。 它还可用于提供有关对租户管理员有用的应用的任何说明或信息。

## <a name="subscriptionoffer"></a>subscriptionOffer

**可选** - object

指定与你的应用关联的 SaaS 产品/服务。

|名称| 类型|最大大小|必需|说明|
|---|---|---|---|---|
|`offerId`| string | 2048 个字符 | ✔️ | A unique identifier that includes your Publisher ID and Offer ID, which you can find in [Partner Center](https://partner.microsoft.com/dashboard). You must format the string as `publisherId.offerId`.|

## <a name="meetingextensiondefinition"></a>meetingExtensionDefinition

**可选** - object

Specify meeting extension definition. For more information, see [custom Together Mode scenes in Teams](../../apps-in-teams-meetings/teams-together-mode.md).

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`scenes`|对象数组| 5 个项目||会议支持的场景。|
|`supportsStreaming`|Boolean|||指示应用是否可以将会议的音频和视频内容流式传输到实时会议协议 (RTMP) 终结点的值。 默认值为 **false**。|

### <a name="meetingextensiondefinitionscenes"></a>meetingExtensionDefinition.scenes

|名称| 类型|最大大小|必需 |说明|
|---|---|---|---|---|
|`id`|||✔️| 场景的唯一标识符。 此 ID 必须是 GUID。 |
|`name`| string | 128 个字符 |✔️| 场景的名称。 |
|`file`|||✔️| 场景的元数据 json 文件的相对文件路径。 |
|`preview`|||✔️| 场景的 PNG 预览图标的相对文件路径。 |
|`maxAudience`| integer | 50  |✔️| 场景中支持的最大受众数。 |
|`seatsReservedForOrganizersOrPresenters`| integer | 50 |✔️| 为组织者或演示者保留的席位数。|

## <a name="authorization"></a>授权

**可选** - 对象

> [!NOTE]
> If you set the `manifestVersion` property to 1.12, the authorization property is incompatible with the older versions (version 1.11 or earlier) of the manifest. Authorization is supported for manifest version 1.12.

指定并合并应用的授权相关信息。

|名称| 类型|最大大小|必需 |说明|
|---|---|---|---|---|
|`permissions`||||应用运行所需的权限列表。|

### <a name="authorizationpermissions"></a>authorization.permissions

|名称| 类型|最大大小|必需 |说明|
|---|---|---|---|---|
|`resourceSpecific`| 对象数组|16 个项目||在资源实例级别保护数据访问的权限。|

### <a name="authorizationpermissionsresourcespecific"></a>authorization.permissions.resourceSpecific

|名称| 类型|最大大小|必需 |说明|
|---|---|---|---|---|
|`type`|string||✔️| The type of the resource-specific permission. Options: `Application` and `Delegated`.|
|`name`|string|128 个字符|✔️|特定于资源的权限名称。 有关详细信息，请参阅[资源对应的应用程序权限](#resource-specific-application-permissions)和[资源对应的委派权限](#resource-specific-delegated-permissions)|

#### <a name="resource-specific-application-permissions"></a>资源对应的应用程序权限

应用程序权限允许应用在用户未登录的情况下访问数据。 有关应用程序权限的信息，请参阅 [MS Graph 和 MS BotSDK 的资源相应的许可](../../graph-api/rsc/resource-specific-consent.md)。

#### <a name="resource-specific-delegated-permissions"></a>资源对应的委派权限

委派的权限允许应用代表已登录用户访问数据。

* **团队的资源对应的委派权限**

    |**名称**|**说明**|
    |---|---|
    |`ChannelMeetingParticipant.Read.Group`| 允许应用代表已登录用户读取与此团队关联的频道会议的参与者信息，包括姓名、角色、ID、加入和离开时间。|
    |`InAppPurchase.Allow.Group`| 允许应用代表已登录用户向此团队中的用户显示市场产品/服务并在应用中完成购买。|
    |`ChannelMeetingStage.Write.Group`| 允许应用代表已登录用户在与此团队关联的频道会议中显示会议阶段的内容。|
    |`LiveShareSession.ReadWrite.Group`|允许应用为与此团队关联的会议创建和同步 Live Share 会话，并代表登录用户访问有关会议名册的相关信息，例如成员的会议角色。|

* **聊天或会议的资源对应的委派权限**

    |**名称**|**说明**|
    |---|---|
    |`InAppPurchase.Allow.Chat`|允许应用代表已登录用户向此聊天和任何关联会议中的用户显示市场产品/服务，并在应用中完成其购买。|
    |`MeetingStage.Write.Chat`|允许应用代表已登录用户在与此聊天关联的会议中显示会议阶段的内容。|
    |`OnlineMeetingParticipant.Read.Chat`|允许应用代表已登录用户读取与此聊天关联的会议的参与者信息，包括姓名、角色、ID、加入和离开时间。|
    |`OnlineMeetingParticipant.ToggleIncomingAudio.Chat`|允许应用代表登录用户为与此聊天关联的会议中的参与者切换传入音频。|
    |`LiveShareSession.ReadWrite.Chat`|允许应用为与此聊天关联的会议创建和同步 Live Share 会话，并代表登录用户访问有关会议名册的相关信息，例如成员的会议角色。|
   |`OnlineMeetingIncomingAudio.Detect.Chat`|允许应用代表已登录用户检测与此聊天关联的会议中传入音频状态的变化。|

* **用户的资源对应的委派权限**

    |**名称**|**说明**|
    |---|---|
    |`InAppPurchase.Allow.User`|允许应用代表已登录用户显示用户市场产品/服务并完成用户在应用内的购买。|

## <a name="create-a-manifest-file"></a>创建清单文件

如果应用没有 Teams 应用清单文件，则需要创建它。

若要创建 Teams 应用清单文件，请执行以下操作：

1. 使用[示例清单架构](#sample-full-manifest)创建 .json 文件。
1. 将其作为 `manifest.json` 保存在项目文件夹的根目录中。

<br>
<details>
<summary>下面是启用了 SSO 的选项卡应用的清单架构示例：</summary>
<br>

> [!NOTE]
> 此处显示的清单示例内容仅适用于选项卡应用。 它使用子域 URI 的示例值。 有关详细信息，请参阅[示例清单架构](#sample-full-manifest)。

  ```json
{ 
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json", 
 "manifestVersion": "1.12", 
 "version": "1.0.0", 
 "id": "{new GUID for this Teams app - not the Azure AD App ID}", 
 "developer": { 
 "name": "Microsoft", 
 "websiteUrl": "https://www.microsoft.com", 
 "privacyUrl": "https://www.microsoft.com/privacy", 
 "termsOfUseUrl": "https://www.microsoft.com/termsofuse" 
  }, 

  "name": { 
    "short": "Teams Auth SSO", 
    "full": "Teams Auth SSO" 
  }, 


  "description": { 
    "short": "Teams Auth SSO app", 
    "full": "The Teams Auth SSO app" 
  }, 

  "icons": { 
    "outline": "outline.png", 
    "color": "color.png" 
  }, 

  "accentColor": "#60A18E", 
  "staticTabs": [ 
    { 
     "entityId": "auth", 
     "name": "Auth", 
     "contentUrl": "https://https://subdomain.example.com/Home/Index", 
     "scopes": [ "personal" ] 
    } 
  ], 

  "configurableTabs": [ 
    { 
     "configurationUrl": "https://subdomain.example.com/Home/Configure", 
     "canUpdateConfiguration": true, 
     "scopes": [ 
     "team" 
      ] 
    } 
  ], 
  "permissions": [ "identity", "messageTeamMembers" ], 
  "validDomains": [ 
   "{subdomain or ngrok url}" 
  ], 
  "webApplicationInfo": { 
    "id": "{Azure AD AppId}", 
    "resource": "api://subdomain.example.com/{Azure AD AppId}" 
  }
} 
```

</details>

## <a name="see-also"></a>另请参阅

* [了解Microsoft Teams结构](~/concepts/design/app-structure.md)
* [启用应用自定义](~/concepts/design/enable-app-customization.md)
* [本地化应用](~/concepts/build-and-test/apps-localization.md)
* [集成媒体功能](~/concepts/device-capabilities/media-capabilities.md)
* [Microsoft Teams 的公共开发人员预览清单架构](manifest-schema-dev-preview.md)
