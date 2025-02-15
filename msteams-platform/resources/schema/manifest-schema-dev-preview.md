---
title: 公共开发人员预览清单架构参考
description: 了解如何启用开发人员预览版。 Microsoft Teams 的公共开发人员预览清单架构示例。
ms.topic: reference
ms.localizationpriority: medium
ms.date: 11/15/2021
ms.openlocfilehash: 2278b2f500ce89f239cae59ffab7f432a8d170f5
ms.sourcegitcommit: 176bbca74ba46b7ac298899d19a2d75087fb37c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2022
ms.locfileid: "68376597"
---
# <a name="public-developer-preview-manifest-schema-for-teams"></a>Teams 的公共开发人员预览清单架构

有关如何启用开发人员预览的信息，请参阅 [Microsoft Teams 的公共开发人员预览](~/resources/dev-preview/developer-preview-intro.md)。

> [!NOTE]
> 如果不使用开发人员预览功能（包括运行 [Outlook 和 Office 中的 Teams 个人选项卡和消息扩展](../../m365-apps/overview.md)），请改用 [正式发布功能的应用清单](~/resources/schema/manifest-schema.md)。

Microsoft Teams 清单介绍应用如何集成到 Microsoft Teams 平台中。 清单必须符合托管在 [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json)的架构。

## <a name="sample-full-manifest"></a>示例完整清单

```json
{
    "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion": "devPreview",
    "version": "1.0.0",
    "id": "%MICROSOFT-APP-ID%",
    "devicePermissions": [
        "geolocation",
        "media"
    ],
    "developer": {
        "name": "Publisher Name",
        "websiteUrl": "https://website.com/",
        "privacyUrl": "https://website.com/privacy",
        "termsOfUseUrl": "https://website.com/app-tos",
        "mpnId": "1234567890"
    },
    "localizationInfo": {
        "defaultLanguageTag": "es-es",
        "additionalLanguages": [
            {
                "languageTag": "en-us",
                "file": "en-us.json"
            }
        ]
    },
    "name": {
        "short": "Name of your app (<=30 chars)",
        "full": "Full name of app, if longer than 30 characters"
    },
    "description": {
        "short": "Short description of your app",
        "full": "Full description of your app"
    },
    "icons": {
        "outline": "%FILENAME-32x32px%",
        "color": "%FILENAME-192x192px"
    },
    "accentColor": "%HEX-COLOR%",
    "configurableTabs": [
        {
            "configurationUrl": "https://contoso.com/teamstab/configure",
            "canUpdateConfiguration": true,
            "scopes": [
                "team",
                "groupchat"
            ],
            "context": []
        }
    ],
    "staticTabs": [
        {
            "entityId": "idForPage",
            "name": "Display name of tab",
            "contentUrl": "https://contoso.com/content?host=msteams",
            "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
            "websiteUrl": "https://contoso.com/content",
            "scopes": [
                "personal"
            ]
        }
    ],
    "bots": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "needsChannelSelector": false,
            "isNotificationOnly": false,
            "scopes": [
                "team",
                "personal",
                "groupchat"
            ],
            "supportsFiles": true,
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
                            "title": "Command N",
                            "description": "Description of Command N"
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
            "configurationUrl": "https://contoso.com/teamsconnector/configure",
            "scopes": [
                "team"
            ]
        }
    ],
    "composeExtensions": [
        {
            "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
            "canUpdateConfiguration": true,
            "commands": [
                {
                    "id": "exampleCmd1",
                    "title": "Example Command",
                    "description": "Command Description; e.g., Search on the web",
                    "initialRun": true,
                    "type": "search",
                    "context": [
                        "compose",
                        "commandBox"
                    ],
                    "parameters": [
                        {
                            "name": "keyword",
                            "title": "Search keywords",
                            "description": "Enter the keywords to search for"
                        }
                    ]
                },
                {
                    "id": "exampleCmd2",
                    "title": "Example Command 2",
                    "description": "Command Description; e.g., Search for a customer",
                    "initialRun": true,
                    "type": "action",
                    "fetchTask": true,
                    "context": [
                        "message"
                    ],
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
                    "id": "exampleMessageHandler",
                    "title": "Message Handler",
                    "description": "Domains that will create a preview when pasted into the compose box",
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
            ]
        }
    ],
    "permissions": [
        "identity",
        "messageTeamMembers"
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
    "defaultInstallScope": "meetings",
    "defaultGroupCapability": {
        "meetings": "tab",
        "team": "bot",
        "groupchat": "bot"
    },
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

*可选，但建议采用* &ndash; 字符串

引用清单的 JSON 架构的 `https://` URL。

## <a name="manifestversion"></a>manifestVersion

**必需** &ndash; 字符串

此清单使用的清单架构版本。

## <a name="version"></a>version

**必需** &ndash; 字符串

特定应用的版本。 如果更新清单中某些内容，则版本也必须递增。 这样一来，在安装新的清单时，它将覆盖现有的版本，用户将获得新的功能。 如果将此应用提交到应用商店，则必须重新提交并重新验证新清单。 然后，此应用的用户将在批准后的几个小时内自动获取新更新的清单。

如果应用请求的权限发生了更改，则系统将提示用户对加载项进行升级和重新许可。

此版本字符串必须遵循[semver](http://semver.org/)标准 (MAJOR.MINOR.PATCH)。

## <a name="id"></a>id

**必需** &ndash; Microsoft 应用 ID

此应用的唯一 Microsoft 生成的标识符。 如果已通过Microsoft Bot Framework注册了机器人，或者选项卡的 Web 应用已使用 Microsoft 登录，则应该已有一个 ID，并且必须在此处输入。 否则，必须在 Microsoft 应用程序注册门户 ([“我的应用程序](https://apps.dev.microsoft.com) ”) 生成新 ID，在此处输入该 ID，然后在 [添加机器人](~/bots/how-to/create-a-bot-for-teams.md)时重用它。

## <a name="developer"></a>developer

必需：

指定有关公司的信息。 对于已提交到 AppSource（原 Office Store）的应用，这些值必须与 AppSource 条目中的信息匹配。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`name`|32 个字符|✔️|开发人员的显示名称。|
|`websiteUrl`|2048 个字符|✔️|开发人员网站的 https:// URL。 此链接应将用户转到公司或产品特定的登陆页面。|
|`privacyUrl`|2048 个字符|✔️|开发人员隐私策略的 https:// URL。|
|`termsOfUseUrl`|2048 个字符|✔️|开发人员使用条款的 https:// URL。|
|`mpnId`|10 个字符|✔️|**可选** 标识生成应用的合作伙伴组织的Microsoft 合作伙伴网络 ID。|

## <a name="localizationinfo"></a>localizationInfo

可选：

允许默认语言的规范，以及指向其他语言文件的指针。 参阅 [本地化](~/concepts/build-and-test/apps-localization.md)。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`defaultLanguageTag`|4 个字符|✔️|此顶级清单文件中字符串的语言标记。|

### <a name="localizationinfoadditionallanguages"></a>localizationInfo.additionalLanguages

指定其他语言翻译的对象数组。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`languageTag`|4 个字符|✔️|所提供文件中字符串的语言标记。|
|`file`|4 个字符|✔️|包含已翻译字符串的 .json 文件的相对文件路径。|

## <a name="name"></a>name

必需：

应用体验的名称，在 Teams 体验中向用户显示。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。 `short`值和`full`应该不一样。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`short`|30 个字符|✔️|应用的短显示名称。|
|`full`|100 个字符||如果完整应用名称超过 30 个字符，则使用应用的全名。|

## <a name="description"></a>说明

必需：

向用户描述应用。 对于提交到 AppSource 的应用，这些值必须与 AppSource 条目中的信息匹配。

确保描述可以准确描述你的体验，并提供信息来帮助潜在客户了解你的体验。 如果需要使用外部帐户，则应在完整说明中进行备注。 `short`值和`full`应该不一样。  简短说明不能在长说明中重复，也不能包含任何其他应用名称。

|名称| 最大大小 | 必需 | Description|
|---|---|---|---|
|`short`|80 个字符|✔️|应用体验的简短说明，在空间受限时使用。|
|`full`|4000 个字符|✔️|应用的完整说明。|

## <a name="icons"></a>图标

必需：

Teams 应用中使用的图标。 图标文件必须作为上传包的一部分包含在内。

|名称| 最大大小 | 必需 | 说明|
|---|---|---|---|
|`outline`|2048 个字符|✔️|透明 32x32 PNG 大纲图标的相对文件路径。|
|`color`|2048 个字符|✔️|完整颜色 192x192 PNG 图标的相对文件路径。|

## <a name="accentcolor"></a>accentColor

**必需** &ndash; 字符串

用于大纲图标的颜色和背景。

该值必须是以"#"开头的有效 HTML 颜色代码，例如 `#4464ee`。

## <a name="configurabletabs"></a>configurableTabs

可选：

当应用体验具有团队频道选项卡体验时使用，该体验需要在添加之前进行额外的配置。 可配置选项卡仅在团队范围内受支持，并且目前每个应用仅支持一个选项卡。

对象是一个数组，其中包含类型的所有元素 `object`。 只有提供可配置频道选项卡解决方案的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|字符串|2048 个字符|✔️|配置选项卡时要使用的 https:// URL。|
|`canUpdateConfiguration`|Boolean|||A value indicating whether an instance of the tab's configuration can be updated by the user after creation. Default: `true`|
|`scopes`|枚举数组|1|✔️|目前，可配置选项卡仅支持 `team` 和 `groupchat` 范围。 |
|`context` |枚举数组|6||[支持选项卡](../../tabs/how-to/access-teams-context.md)的 `contextItem` 范围的集合。 默认值：`channelTab`、`privateChatTab`、`meetingChatTab`、`meetingDetailsTab`、`meetingSidePanel` 和 `meetingStage`。|
|`sharePointPreviewImage`|String|2048||A relative file path to a tab preview image for use in SharePoint. Size 1024x768. |
|`supportedSharePointHosts`|枚举数组|1||Defines how your tab will be made available in SharePoint. Options are `sharePointFullPage` and `sharePointWebPart` |

## <a name="statictabs"></a>staticTabs

可选：

定义默认情况下可以"固定"的一组选项卡，而无需用户手动添加它们。 在 `personal` 范围内声明的静态选项卡始终固定到应用的个人体验。 当前不支持在 `team` 作用域中声明的静态选项卡。

通过在 **staticTabs** 块指定 `contentBotId` 而不是 `contentUrl` 来呈现具有自适应卡片的选项卡。

对象是一个所有元素均为类型 `object` 的数组（最多 16 个元素）。 只有提供静态选项卡解决方案的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`entityId`|字符串|64 个字符|✔️|选项卡显示的实体的唯一标识符。|
|`name`|字符串|128 个字符|✔️|通道接口中选项卡的显示名称。|
|`contentUrl`|字符串|2048 个字符|✔️|指向要在 Teams 画布中显示的实体 UI 的 https:// URL。|
|`contentBotId`|   | | | 在 Bot Framework 门户中为机器人指定的 Microsoft Teams 应用 ID。 |
|`websiteUrl`|String|2048 个字符||用户选择在浏览器中查看时要指向的 http:// URL。|
|`scopes`|枚举数组|1|✔️|目前，静态选项卡仅支持 `personal` 范围，这意味着只能将其预配为个人体验的一部分。|

## <a name="bots"></a>机器人

可选：

定义机器人解决方案以及可选信息（如默认命令属性）。

对象是一个数组（目前每个应用仅允许一个机器人&mdash;最多 1 个元素），其所有元素类型均为 `object`。 只有提供机器人体验的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|字符串|64 个字符|✔️|使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 这可能与整个 [应用 ID](#id) 相同。|
|`needsChannelSelector`|Boolean|||Describes whether or not the bot utilizes a user hint to add the bot to a specific channel. Default: `false`|
|`isNotificationOnly`|布尔值|||Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot. Default: `false`|
|`supportsFiles`|Boolean|||Indicates whether the bot supports the ability to upload/download files in personal chat. Default: `false`|
|`scopes`|枚举数组|3|✔️|Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`). These options are non-exclusive.|

### <a name="botscommandlists"></a>bots.commandLists

机器人可以向用户推荐的命令的可选列表。 对象是一个数组（最多 2 个元素），其所有元素类型均为 `object`；必须为机器人支持的每个范围定义一个单独的命令列表。 有关详细信息，请参阅 [机器人菜单](~/bots/how-to/create-a-bot-commands-menu.md)。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`items.scopes`|枚举数组|3|✔️|Specifies the scope for which the command list is valid. Options are `team`, `personal`, and `groupchat`.|
|`items.commands`|对象数组|10|✔️|自动程序支持的命令数组：<br>`title`：自动程序命令名称（字符串，32）<br>`description`：命令语法及其参数的简单说明或示例（字符串，128）。|

## <a name="connectors"></a>连接器

可选：

`connectors`块定义应用的 Office 365 连接器。

对象是一个数组（最多 1 个元素），其所有元素类型均为 `object`。 只有提供连接器的解决方案才需要此块。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`configurationUrl`|字符串|2048 个字符|✔️|配置连接器时要使用的 https:// URL。|
|`connectorId`|字符串|64 个字符|✔️|连接器的唯一标识符，与[Connectors 开发人员仪表板](https://aka.ms/connectorsdashboard)中的 ID 匹配。|
|`scopes`|枚举数组|1|✔️|Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`). Currently, only the `team` scope is supported.|

## <a name="composeextensions"></a>composeExtensions

可选：

定义应用的消息扩展。

> [!NOTE]
> 2017 年 11 月，该功能的名称已从“撰写扩展”更改为“消息扩展”，但清单名称保持不变，以便现有扩展可以继续运行。

对象是一个数组（最多 1 个元素），其所有元素类型均为 `object`。 只有提供消息扩展的解决方案才需要此块。

|名称| 类型 | 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`botId`|字符串|64|✔️|支持消息扩展的机器人的唯一 Microsoft 应用 ID，已向机器人框架注册。 这可能与整个 [应用 ID](#id) 相同。|
|`canUpdateConfiguration`|Boolean|||A value indicating whether the configuration of a message extension can be updated by the user. The default is `false`.|
|`commands`|对象数组|10|✔️|消息扩展支持的命令数组|

### <a name="composeextensionscommands"></a>composeExtensions.commands

消息扩展应声明一个或多个命令。 每个命令在 Teams 中显示为来自基于 UI 的入口点的潜在交互。 最多有 10 个命令。

每个命令项都是具有以下结构的对象：

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|字符串|64 个字符|✔️|命令的 ID。|
|`type`|字符串|64 个字符||命令的类型。 `query`或`action`之一。 默认值：`query`|
|`title`|字符串|32 个字符|✔️|用户友好的命令名称。|
|`description`|字符串|128 个字符||向用户显示以指示此命令用途的说明。|
|`initialRun`|Boolean|||指示命令最初是否应在没有参数时运行的布尔值。 默认值：`false`|
|`context`|Array of Strings|3||定义可以从何处调用消息扩展插件。 `compose`、`commandBox`、`message` 的任何组合。 默认值为 `["compose", "commandBox"]`|
|`fetchTask`|Boolean|||指示它是否应动态提取任务模块的布尔值。|
|`taskInfo`|Object|||指定使用消息扩展命令时要预加载的任务模块。|
|`taskInfo.title`|String|64||初始对话框标题。|
|`taskInfo.width`|字符串|||对话框宽度 - 数字（以像素为单位）或默认布局，如"large"、"medium"或"small"。|
|`taskInfo.height`|String|||对话框高度 - 数字（以像素为单位）或默认布局，如"large"、"medium"或"small"。|
|`taskInfo.url`|String|||初始 Web 视图 URL。|
|`messageHandlers`|对象数组|5||A list of handlers that allow apps to be invoked when certain conditions are met. Domains must also be listed in `validDomains`.|
|`messageHandlers.type`|String|||The type of message handler. Must be `"link"`.|
|`messageHandlers.value.domains`|Array of Strings|||链接消息处理程序可以注册的域数组。|
|`parameters`|对象数组|5|✔️|命令采用的参数列表。 最小值：1；最大值：5。|
|`parameter.name`|字符串|64 个字符|✔️|在客户端中显示的参数的名称。 这包含在用户请求中。|
|`parameter.title`|字符串|32 个字符|✔️|参数的用户友好标题。|
|`parameter.description`|String|128 个字符||描述此参数用途的用户友好字符串。|
|`parameter.inputType`|String|128 个字符||定义在 `fetchTask: true` 的任务模块上显示的控件类型。 `text`、`textarea`、`number`、`date`、`time`、`toggle`、`choiceset` 其中之一。|
|`parameter.choices`|对象数组|10||`choiceset` 的选择选项。 仅当 `parameter.inputType` 为 `choiceset` 时使用。|
|`parameter.choices.title`|String|128||选择的标题。|
|`parameter.choices.value`|String|512||选项的值。|

## <a name="permissions"></a>permissions

可选：

一个数组 `string`，指定应用请求的权限，让最终用户知道扩展将如何执行。 以下选项是非独占的：

* `identity`&emsp;需要用户标识信息。
* `messageTeamMembers`&emsp;请求向团队成员发送直接消息的权限。

更新应用时更改这些权限将导致用户在首次运行更新的应用时重复同意过程。

## <a name="devicepermissions"></a>devicePermissions

**可选** 字符串数组

Specifies the native features on a user's device that your app may request access to. Options are:

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a>validDomains

**可选**，除非备注为 **必需**。

应用需要从中加载任何内容的有效域的列表。 域列表可以包含通配符，例如 `*.example.com`。 这与域的某区段完全匹配；如果需要匹配 `a.b.example.com`，则使用 `*.*.example.com`。 如果选项卡配置或内容 UI 需要转到除选项卡配置之外的任何其他域，则必须在此处指定该域。

但是，**没有** 必要在应用中包含你要支持的标识提供者的域。 例如，若要使用 Google ID 进行身份验证，必须重定向到 accounts.google.com，但不应在 `validDomains[]`其中包含 accounts.google.com。

> [!IMPORTANT]
> 不要直接或通过通配符添加超出控制范围的域。 例如，`yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。

对象是一个数组，其中包含类型的所有元素 `string`。

## <a name="webapplicationinfo"></a>webApplicationInfo

可选：

指定Microsoft Azure Active Directory (Azure AD) 应用 ID 和 Graph 信息，以帮助用户无缝登录到 Azure AD 应用。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`id`|字符串|36 个字符|✔️|应用的 Microsoft Azure Active Directory (Azure AD) 应用程序 ID。 此 ID 必须是 GUID。|
|`resource`|String|2048 个字符|✔️|用于获取 SSO 身份验证令牌的应用的资源 URL。|
|`applicationPermissions`|Array|最多 100 项|✔️|应用程序的资源权限。|

## <a name="graphconnector"></a>graphConnector

**可选**— 对象

指定应用的 Graph 连接器配置。 如果存在，则还必须指定 [webApplicationInfo.id](#webapplicationinfo)。

|名称| 类型| 最大大小 | 必需 | 说明|
|---|---|---|---|---|
|`notificationUrl`|string|2048 个字符|✔️|应在其中发送应用程序的 Graph 连接器通知的 URL。|

## <a name="showloadingindicator"></a>showLoadingIndicator

**可选**— 布尔值

指示是否在加载应用或选项卡时显示加载指示器。 默认为 **false**。
> [!NOTE]
> 如果在应用清单中选择`showLoadingIndicator` 为 true，若要正确加载页面，请修改选项卡和任务模块的内容页，如 [显示本机加载指示器](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) 文档中所述。

## <a name="isfullscreen"></a>isFullScreen

 **可选**— 布尔值

Indicate where a personal app is rendered with or without a tab header bar. Default is **false**.

> [!NOTE]
> `isFullScreen` 仅适用于发布到组织的应用。

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

## <a name="configurableproperties"></a>configurableProperties

**可选** - 数组

`configurableProperties`此块定义管理员可Teams的应用程序属性。 有关详细信息，请参阅启用 [应用自定义](~/concepts/design/enable-app-customization.md)。

> [!NOTE]
> 必须定义至少一个属性。 最多可以在此块中定义九个属性。

可以定义以下任一属性：

* `name`：应用显示名称。
* `shortDescription`：应用的简短说明。
* `longDescription`：应用的详细说明。
* `smallImageUrl`：应用的大纲图标。
* `largeImageUrl`：应用的颜色图标。
* `accentColor`：用于大纲图标的颜色和背景。
* `developerUrl`：开发人员网站的 HTTPS URL。
* `privacyUrl`：开发人员隐私策略的 HTTPS URL。
* `termsOfUseUrl`：开发人员使用条款的 HTTPS URL。

## <a name="supportedchanneltypes"></a>supportedChannelTypes

**可选** - 数组

在非标准频道中启用应用。 如果应用支持团队范围，并且定义了此属性，Teams 会在每个频道类型中相应地启用应用。 当前支持专用频道和共享频道类型。

> [!NOTE]
>
> * 如果应用支持团队范围，则无论在此属性中定义的值如何，它都会在标准频道中运行。
> * 应用可以考虑每个频道类型的唯一属性，以便正常运行。 若要为专用频道和共享频道启用选项卡，请参 [阅在专用通道中检索上下文](~/tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) 并在 [共享通道中获取上下文](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

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

## <a name="subscriptionoffer"></a>subscriptionOffer

**可选** - object

指定与你的应用关联的 SaaS 产品/服务。

|名称| 类型| 最大大小 | 必需 | 说明|
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

**可选** - object

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

## <a name="see-also"></a>另请参阅

* [了解Microsoft Teams结构](~/concepts/design/app-structure.md)
* [启用应用自定义](~/concepts/design/enable-app-customization.md)
* [本地化应用](~/concepts/build-and-test/apps-localization.md)
* [集成媒体功能](~/concepts/device-capabilities/media-capabilities.md)
