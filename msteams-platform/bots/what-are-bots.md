---
title: " Microsoft Teams 中的自动程序"
author: surbhigupta
description: 在本文中，使用 Microsoft Teams 中的对话机器人共享文件、发送主动通知、交互式卡片、拨打电话、调用机器人命令、IVR。
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 4f421c5bcc8251976a54bf5f94b7dafbcc50c64c
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791578"
---
# <a name="build-bots-for-teams"></a>为 Teams 生成机器人

机器人也称为聊天机器人或对话机器人。 它是一个应用，可由客户服务或支持人员等用户运行简单且重复的任务。 机器人的日常使用包括提供天气信息、预订餐食或提供旅行信息。 与机器人的交互可以是快速问答或复杂的对话。

> [!NOTE]
> 建议首先 [使用 JavaScript 生成第一个机器人应用](../sbs-gs-bot.yml) ，或使用适用于 Teams 的新一代开发工具 [使用 JavaScript 生成通知机器人](../sbs-gs-notificationbot.yml) 。 有关详细信息，请参阅 [Teams 工具包概述](../toolkit/teams-toolkit-fundamentals.md)。

> [!IMPORTANT]
>
> * 目前，机器人在政府社区云（GCC）和 GCC-High 中可用，但在国防部（DOD）中不可用。
>
> * Microsoft Teams 中的机器人应用程序通过 [Azure 机器人服务](/azure/bot-service/how-to-deploy-gov-cloud-high)提供，机器人通道注册必须在 Azure 政府门户中完成。
>
> * GCCH 中的应用程序最多仅支持清单版本 v1.10。 GCCH 环境中不支持自适应卡片中的图像 URL。 可以将图像 URL 替换为 Base64 编码的 DataUri。

会话机器人允许用户通过文本、交互卡和任务模块与 web 服务进行交互。

:::image type="content" source="../assets/images/invokebotwithtext.png" alt-text="屏幕截图是一个示例，其中显示了使用文本的 Web 服务。"lightbox="../assets/images/invokebotwithtext.png":::

:::image type="content" source="../assets/images/invokebotwithcard.png" alt-text="屏幕截图是一个示例，其中显示了使用交互式卡片的 Web 服务。"lightbox="../assets/images/invokebotwithcard.png"border="true":::

:::image type="content" source="../assets/images/task-module-example.png" alt-text="屏幕截图是一个示例，显示了使用任务模块的 Web 服务。" lightbox="../assets/images/task-module-example-expanded.png":::

对话机器人非常灵活。 机器人可以处理涉及人工智能和自然语言处理的一些基本命令或复杂任务。 机器人可以是较大应用程序的一部分，也可以是独立的。

使用卡片、文本和任务模块的正确组合创建有用的机器人。 下图显示了用户在使用文本和交互式卡片的一对一聊天中与机器人交谈。

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="屏幕截图是一个示例，显示了示例常见问题解答机器人。":::

用户与机器人之间的每次交互都表示为活动。 机器人收到活动时，会将其传递给其活动处理程序。 参阅[机器人活动处理程序](~/bots/bot-basics.md)。

机器人是具有对话界面的应用。 可以使用文本、交互式卡片和语音与机器人交互。 机器人在频道或群组聊天对话和一对一对话中的行为不同。 会话通过 Bot Framework 连接器进行处理。 请参阅[对话基础知识](~/bots/how-to/conversations/conversation-basics.md)。

机器人需要上下文信息（例如用户配置文件详细信息）来访问相关内容并增强机器人体验。 请参阅[获取 Teams 上下文](~/bots/how-to/get-teams-context.md)。

可以使用 Graph API 或 Teams 机器人 API 通过机器人发送和接收文件。 请参阅[通过机器人发送和接收文件](~/bots/how-to/bots-filesv4.md)。

速率限制用于优化用于 Teams 应用程序的机器人。 为了保护 Teams 及其用户，机器人 API 为传入请求提供速率限制。 请参阅[通过团队中的速率限制来优化你的智能机器人](~/bots/how-to/rate-limit.md)。

通过 Microsoft Graph 用于通话和联机会议的 API，Teams 应用现在可以使用语音和视频与用户进行交互。 请参阅[通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。

可以使用 Teams 机器人 API 获取聊天或团队成员的信息。 请参阅[Teams 机器人 API 在提取团队或聊天成员方面的更改](~/resources/team-chat-member-api-changes.md)。

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="code-samples"></a>代码示例

|示例名称 | Description | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| 机器人每日任务提醒| 演示如何计划定期任务并在计划的时间获取提醒。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |
| Hello World机器人 | 这是一个简单的 hello world 应用程序，具有机器人和消息扩展功能。 | 不适用 | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/hello-world-bot) |
| 自适应卡片通知 | 此示例演示如何使用机器人发送具有不同自适应卡片的通知。 | 不适用 | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/adaptive-card-notification) |
| 传入 Webhook 通知 | 这是一个示例，演示如何在 Microsoft Teams 频道中通过传入 Webhook 发送通知。 | 不适用 | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/v1.0.0/incoming-webhook-notification) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [智能机器人和 SDK](~/bots/bot-features.md)

## <a name="see-also"></a>另请参阅

* [创建适合 Teams 的机器人](../resources/bot-v3/bots-create.md)
* [Microsoft Teams 机器人的工作原理](/azure/bot-service/bot-builder-basics-teams)
* [注册 Microsoft Teams 的通话和会议机器人](~/bots/calls-and-meetings/registering-calling-bot.md)
* [向 Teams 机器人添加身份验证](~/bots/how-to/authentication/add-authentication.md)
* [智能机器人活动处理程序](~/bots/bot-basics.md)
* [Teams 智能机器人中的对话活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [使用 JavaScript 生成第一个机器人应用](../sbs-gs-bot.yml)
* [使用 JavaScript 生成通知机器人](../sbs-gs-notificationbot.yml)
