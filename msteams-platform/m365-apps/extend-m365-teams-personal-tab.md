---
title: 跨 Microsoft 365 扩展 Teams 个人选项卡应用
description: 了解如何更新个人选项卡应用以在 Outlook 和 Office 中运行，以及 Microsoft Teams。
ms.date: 10/10/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 910a94f34d14c8dbb8a35099d438469fea52155b
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789970"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>跨 Microsoft 365 扩展 Teams 个人选项卡

个人选项卡提供了增强 Microsoft Teams 体验的好方法。 使用个人选项卡，可以在 Teams 中提供用户对其应用程序的访问权限，无需用户离开体验或再次登录。 使用此预览版，个人选项卡可以在其他 Microsoft 365 应用程序中亮起。 本教程演示了采用现有 Teams 个人选项卡并将其更新为在 Outlook 和 Office 桌面和 Web 体验以及 Android 版 Office 应用中运行的过程。

更新个人应用以在 Outlook 和 Office 中运行涉及以下步骤：

> [!div class="checklist"]
>
> * [更新应用清单](#update-the-app-manifest)。
> * [更新 TeamsJS SDK 引用](#update-sdk-references)。
> * [修改内容安全策略标头](#configure-content-security-policy-headers)。
> * [更新单个 Sign-On (SSO) Microsoft Azure Active Directory (Azure AD) 应用注册](#update-azure-ad-app-registration-for-sso)。
> * [在 Teams 中旁加载已更新的应用](#sideload-your-app-in-teams)。

本指南的其余部分将指导你完成这些步骤，并演示如何在其他 Microsoft 365 应用程序中预览你的个人选项卡。

## <a name="prerequisites"></a>先决条件

若要完成本教程，需要：

* Microsoft 365 开发人员计划沙盒租户
* 在 *Office 365 目标版本* 中注册的沙盒租户
* 从 Microsoft 365 应用 *beta 版通道* 安装了 Office 应用的计算机
*  (可选) 在 *beta 计划中* 安装并注册了 Office for Android 应用的 Android 设备或仿真器
* （可选）Microsoft Visual Studio Code 的 [ Teams 工具包 ](https://aka.ms/teams-toolkit) 扩展，用于帮助更新代码

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>准备好个人选项卡进行升级

如果你有现有的个人选项卡应用，请创建生产项目的副本或分支，用于测试应用清单中的应用 ID，以使用与生产应用 ID 不同的新标识符 (，用于测试) 。

若要使用示例代码完成本教程，请按照[待办事项列表示例中](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend)的设置步骤，使用适用于Visual Studio Code的 Teams 工具包扩展生成个人选项卡应用，然后返回本文以更新 Microsoft 365。

或者，可以使用以下 [快速入门](#quickstart)部分中已启用 Microsoft 365 的基本单一登录 *hello world* 应用，然后跳到 [Teams 中旁加载应用](#sideload-your-app-in-teams)。

### <a name="quickstart"></a>快速入门

若要从已启用可在 Outlook 和 Office 中运行[的个人选项卡](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)开始，请使用适用于Visual Studio Code的 Teams 工具包扩展。

1. 从 Visual Studio Code 打开命令面板 (`Ctrl+Shift+P`)，键入 `Teams: Create a new Teams app`。
1. 选择“**新建 Teams 应用**”选项。
1. 选择 **“已启用 SSO 的个人”选项卡**。

    :::image type="content" source="images/toolkit-tab-sample.png" alt-text="屏幕截图是一个示例，其中显示了 Teams 工具包中的待办事项列表示例 (在 Teams、Outlook 和 Office) 中工作。":::
1. 选择首选编程语言。
1. 在本地计算机上为工作区文件夹选择一个位置，然后输入应用程序名称。
1. 打开命令面板 (`Ctrl+Shift+P`) 并键入`Teams: Provision in the cloud`以在 Azure 帐户中创建所需的应用资源， (App 服务计划、存储帐户、函数应用、托管标识) 。
1. 选择订阅和资源组。
1. 选择“ **预配**”。
1. 打开命令面板（`Ctrl+Shift+P`）并键入 `Teams: Deploy to the cloud`，将示例代码部署到 Azure 中预配的资源并启动应用。
1. 选择“部署”。

在此处，你可以跳到 [在 Teams 中旁加载应用](#sideload-your-app-in-teams) ，并在 Outlook 和 Office 中预览应用。  (已针对 Microsoft 365.) 更新应用清单和 TeamsJS API 调用

## <a name="update-the-app-manifest"></a>更新应用清单

你需要使用 [Teams 开发人员清单](../resources/schema/manifest-schema.md) 架构版本 `1.13` ，使 Teams 个人选项卡能够在 Outlook 和 Office 中运行。

可通过两个选项更新应用清单：

# <a name="teams-toolkit"></a>[Teams 工具包](#tab/manifest-teams-toolkit)

1. 打开命令面板：`Ctrl+Shift+P`。
1. 运行该 `Teams: Upgrade Teams manifest` 命令并选择应用清单文件。 将进行更改。

# <a name="manual-steps"></a>[ 手动步骤 ](#tab/manifest-manual)

打开 Teams 应用清单，使用以下值更新 `$schema` 和 `manifestVersion`：

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

如果使用 Teams 工具包创建了个人应用，则还可以使用它来验证清单文件的更改并识别任何错误。 打开命令面板 () `Ctrl+Shift+P` 并查找 **Teams：验证清单文件**。

## <a name="update-sdk-references"></a>更新 SDK 引用

若要在 Outlook 和 Office 中运行，你的应用需要引用 npm 包 `@microsoft/teams-js@2.0.0` (或更高版本) 。 虽然 Outlook 和 Office 支持具有下层版本的代码，但会记录弃用警告，并且最终将停止对 Outlook 和 Office 中 TeamsJS 下层版本的支持。

可以使用 Teams 工具包来帮助识别和自动执行从 1.x TeamsJS 版本升级到 TeamsJS 版本 2.x.x 所需的代码更改。 或者，可以手动执行相同的步骤;有关详细信息，请参阅 [Microsoft Teams JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) 。

1. 打开 *命令面板*： `Ctrl+Shift+P`。
1. 运行命令 `Teams: Upgrade Teams JS SDK and code references`。

完成后，*package.json* 文件将引用`@microsoft/teams-js@2.0.0` (或更高版本) 和`*.js/.ts``*.jsx/.tsx`文件将更新为：

> [!div class="checklist"]
>
> * 导入 teams-js@2.x.x 的语句
> * teams-js@2.x.x 的[函数、枚举和接口调用](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20)
> * `TODO` 注释提醒标记可能受 [上下文](../tabs/how-to/using-teams-client-sdk.md#updates-to-the-context-interface) 接口更改影响的区域
> * `TODO` 注释提醒，[将回调函数转换为 promise](../tabs/how-to/using-teams-client-sdk.md#callbacks-converted-to-promises)

> [!IMPORTANT]
> 升级工具不支持 *.html* 文件内的代码，需要手动更改。

## <a name="configure-content-security-policy-headers"></a>配置内容安全策略标题

与在 Microsoft Teams 中一样，选项卡应用程序托管在 Office 和 Outlook Web 客户端的 [iframe 元素](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) 中。

如果应用使用 [内容安全策略](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) 标头，请确保在 CSP 标头中允许以下所有 [上级帧](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) ：

|Microsoft 365 主机| 框架上级元素权限|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.microsoft365.com`, `*.office.com` |
| Outlook | `outlook.live.com`, `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>更新 SSO 的 Azure AD 应用注册

适用于个人选项卡[的 Azure Active Directory (AD) 单一登录 (SSO) ](../tabs/how-to/authentication/tab-sso-overview.md)在 Office 和 Outlook 中的工作方式与在 Teams 中的工作方式相同。 但是，需要在租户的 *应用注册* 门户中将多个客户端应用程序标识符添加到选项卡应用的 Azure AD 应用注册。

1. 使用沙盒租户帐户登录到 [Microsoft Azure 门户 ](https://portal.azure.com)。
1. 打开 **应用注册** 边栏选项卡。
1. 选择个人选项卡应用程序的名称以打开其应用注册。
1. 在“*管理*”下选择“**公开 API**”。

    :::image type="content" source="images/azure-app-registration-clients.png" alt-text="屏幕截图显示了Azure 门户上“应用注册”边栏选项卡中的授权客户端 ID。":::

1. 在”**授权客户端应用程序**“部分中，确保添加了以下 `Client Id` 所有值：

    |Microsoft 365 客户端应用程序 | 客户端 ID |
    |--|--|
    |Teams 桌面、移动设备 |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
    |Teams Web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
    |Office Web  |4765445b-32c6-49b0-83e6-1d93765276ca|
    |Office 桌面版  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
    |Office 移动版  | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook 桌面版、移动版 | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook Web | bc59ab01-8403-45c6-8796-ac3ef710b3e3|

    > [!NOTE]
    > 某些 Microsoft 365 客户端应用程序共享客户端 ID。

## <a name="sideload-your-app-in-teams"></a>在 Teams 中旁加载应用

在 Office 和 Outlook 中运行应用的最后一步是在 Microsoft Teams 中旁加载已更新的个人选项卡 [应用包](..//concepts/build-and-test/apps-package.md) 。

1. 将 Teams 应用程序打包 ([清单](../resources/schema/manifest-schema.md) 和 [应用图标](/microsoftteams/platform/resources/schema/manifest-schema#icons)) 在 zip 文件中。 如果使用 Teams 工具包创建应用，则可以使用 Teams 工具包的“**部署**”菜单中的“**压缩 Teams 元数据包**”选项轻松完成此操作。

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="“屏幕截图是用于Visual Studio Code的 Teams 工具包扩展中显示 Zip Teams 元数据包”选项的示例。":::

1. 使用沙盒租户帐户登录 Teams，并切换到“*开发者预览版*”模式。 选择用户个人资料旁边的省略号 (**...**) 菜单，然后依次选择：“**关于**” > “**开发者预览版**”。

    :::image type="content" source="images/teams-dev-preview.png" alt-text="屏幕截图介绍如何选择“开发人员预览版”选项。":::

1. 选择“**应用**”以打开“**管理你的应用**”窗格。 然后选择“ **上传应用**”。

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="屏幕截图是显示“管理应用”窗格和“发布应用”选项的示例。":::

1. 选择 **“上传自定义应用** ”选项，然后选择应用包。

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="屏幕截图是一个示例，其中显示了在 Teams 中上传 am 应用的选项。":::

旁加载到 Teams 后，你的个人选项卡可在 Outlook 和 Office 中使用。 必须使用用于将应用旁加载到 Teams 中的相同凭据登录。 运行适用于 Android 的 Office 应用时，需要重启应用才能使用 Office 应用中的个人选项卡应用。

可以固定应用以进行快速访问，也可以在省略号 (**...**) 中找到应用左侧边栏中最近应用程序中的浮出控件。 在 Teams 中固定应用不会将其固定为 Office 或 Outlook 中的应用。

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>在其他 Microsoft 365 体验中预览个人选项卡

下面介绍如何预览 Office 和 Outlook、Web 和 Windows 桌面客户端中运行的应用。

> [!NOTE]
> 如果使用 Teams 工具包示例应用并从 Teams 中卸载它，则会从 Outlook 和 Office 中的 **“更多应用”** 目录中删除它。

### <a name="outlook-on-windows"></a>Windows 版 Outlook

若要在 Windows 桌面上查看在 Outlook 中运行的应用：

1. 启动 Outlook 并使用开发租户帐户登录。
1. 在侧边栏上，选择“  **更多应用**”。 旁加载的应用标题显示在已安装的应用之间。
1. 选择应用图标以在 Outlook 中启动应用。

    :::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="屏幕截图是一个示例，显示 Outlook 桌面客户端侧栏上的省略号 (“更多应用) ”选项，以查看已安装的个人选项卡。":::

### <a name="outlook-on-the-web"></a>Outlook 网页版

若要查看 Outlook 网页版中的应用，请执行以下操作：

1. 转到[Outlook 网页版](https://outlook.office.com)并使用开发租户帐户登录。
1. 在侧边栏上，选择“  **更多应用**”。 旁加载的应用标题显示在已安装的应用之间。
1. 选择应用图标以启动和预览在 Outlook 网页版 中运行的应用。

    :::image type="content" source="images/outlook-web-more-apps.png" alt-text="屏幕截图是一个示例，显示 outlook.com 侧边栏中的省略号 (“更多应用) ”选项，以查看已安装的个人选项卡。":::

### <a name="office-on-windows"></a>Windows 版 Office

若要在 Windows 桌面上查看在 Office 中运行的应用，请执行以下操作：

1. 启动 Office 并使用开发租户帐户登录。
1. 选择侧栏上的 **“应用”** 图标。 旁加载的应用标题显示在已安装的应用之间。
1. 选择应用图标以在 Office 中启动应用。

    :::image type="content" source="images/office-desktop-more-apps.png" alt-text="屏幕截图是一个示例，显示 Office 桌面客户端侧栏上的省略号 (“更多应用) ”选项，以查看已安装的个人选项卡。":::

### <a name="office-on-the-web"></a>Office 网页版

若要预览在 Office 网页版中运行的应用，请执行以下操作：

1. 使用测试租户凭据登录到 **office.com** 。
1. 选择侧栏上的 **“应用”** 图标。 旁加载的应用标题显示在已安装的应用之间。
1. 选择应用图标以在 Office web 版 中启动应用。

    :::image type="content" source="images/office-web-more-apps.png" alt-text="屏幕截图是一个示例，显示 office.com 侧栏上的“ (更多应用) ”选项，以查看已安装的个人选项卡。":::

### <a name="office-app-for-android"></a>适用于 Android 的 Office 应用

> [!NOTE]
> 在安装应用之前，请执行 [安装最新的 Office 应用 beta 版本](prerequisites.md#mobile) 并成为 beta 程序的一部分的步骤。

若要查看在适用于 Android 的 Office 应用中运行的应用，请执行以下操作：

1. 启动 Office 应用并使用开发租户帐户登录。 如果在 Teams 中旁加载应用之前，Android 版 Office 应用已在运行，则需要重启它才能在已安装的应用中查看。
1. 选择 **“应用”** 图标。 旁加载的应用显示在已安装的应用之间。
1. 选择应用图标，在适用于 Android 的 Office 应用中启动应用。

    :::image type="content" source="images/office-mobile-apps.png" alt-text="屏幕截图是一个示例，显示 Office 应用侧栏上的“应用”选项，以查看已安装的个人选项卡。":::

## <a name="troubleshooting"></a>故障排除

目前，Outlook 和 Office 客户端支持一部分 Teams 应用程序类型和功能。 此支持会随着时间的推移而扩展。

有关各种 TeamsJS 功能的主机支持，请参阅 [Microsoft 365 支持](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook) 。

有关 Microsoft 365 主机和 Teams 应用平台支持的总体摘要，请参阅 [跨 Microsoft 365 扩展 Teams 应用](overview.md)。

可以在运行时通过调用 `isSupported()` 该功能上的 函数 (命名空间) ，并根据需要调整应用行为，在运行时检查给定功能的主机支持。 这允许你的应用在支持它的主机中亮起 UI 和功能，并在不支持的主机中提供优美的回退体验。 有关详细信息，请参阅 [区分应用体验](../tabs/how-to/using-teams-client-sdk.md#differentiate-your-app-experience)。

使用 [Microsoft Teams 开发人员社区频道](/microsoftteams/platform/feedback)报告问题并提供反馈。

### <a name="debugging"></a>调试

在 Teams 工具包中，除了 Teams 之外，还可以) Office 和 Outlook 中运行的选项卡应用程序调试 `F5` (。

:::image type="content" source="images/toolkit-debug-targets.png" alt-text="屏幕截图是一个示例，显示了 Teams 工具包中 Teams 中调试的下拉菜单。":::

首次在 Office 或 Outlook 中运行本地调试时，系统会提示登录 Microsoft 365 租户帐户并安装自签名测试证书。 系统还会提示你手动安装 Teams。 选择“ **在 Teams 中安装** ”，打开浏览器窗口并手动安装应用。 然后选择“ **继续** ”以继续在 Office/Outlook 中调试应用。

:::image type="content" source="images/toolkit-dialog-teams-install.png" alt-text="屏幕截图是一个示例，其中显示了要安装在 Teams 中的“工具包”对话框。":::

在 [Microsoft Teams Framework (TeamsFx) ](https://github.com/OfficeDev/TeamsFx/issues)提供反馈并报告 Teams 工具包调试体验的任何问题。

#### <a name="mobile-debugging"></a>移动调试

适用于 Android 的 Office 应用尚不支持 Teams 工具包 `F5` () 调试。 下面介绍如何远程调试在适用于 Android 的 Office 应用中运行的应用：

1. 如果使用物理 Android 设备进行调试，请将其连接到开发计算机，并启用 [USB 调试](https://developer.android.com/studio/debug/dev-options)选项。 默认情况下，这是使用 Android 模拟器启用的。
1. 从 Android 设备启动 Office 应用。
1. 打开配置文件 **“我”>“设置”>“允许调试**”，然后切换 **“启用远程调试**”选项。

    :::image type="content" source="images/office-android-enable-remote-debugging.png" alt-text="屏幕截图是显示“启用远程调试”切换选项的示例。":::

1. 保留 **“设置”。**
1. 离开个人资料屏幕。
1. 选择“ **应用** ”并启动旁加载的应用以在 Office 应用中运行。
1. 确保 Android 设备已连接到开发计算机。 在开发计算机上，打开浏览器到其 DevTools 检查页。 例如，在 Microsoft Edge 中转到 `edge://inspect/#devices` 以显示已启用调试的 Android WebView 的列表。
1. `Microsoft Teams Tab`找到带有选项卡 URL 的 ，然后选择“**检查**”以开始使用 DevTools 调试应用。

    :::image type="content" source="images/office-android-debug.png" alt-text="屏幕截图是一个示例，显示了 devtool 中的 Web 视图列表。":::

1. 在 Android WebView 中调试选项卡应用。 与在 Android 设备上 [远程调试](/microsoft-edge/devtools-guide-chromium/remote-debugging) 常规网站的方式相同。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **Node.js** |
|---------------|--------------|--------|
| 待办事项列表 | 具有使用 React 和 Azure Functions 生成的 SSO 的可编辑待办事项列表。 仅适用于 Teams (使用此示例应用尝试本教程) 中所述的升级过程。 | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend)  |
| 待办事项列表 (Microsoft 365)  | 具有使用 React 和 Azure Functions 生成的 SSO 的可编辑待办事项列表。 在 Teams、Outlook、Office 中工作。 | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)|
|  (Microsoft 365) 的图像编辑器 | 使用 Microsoft 图形 API创建、编辑、打开和保存图像。 在 Teams、Outlook、Office 中工作。 | [View](https://github.com/OfficeDev/m365-extensibility-image-editor) |
| Microsoft 365)  (示例启动页 | 演示不同主机中可用的 SSO 身份验证和 TeamsJS SDK 功能。 在 Teams、Outlook、Office 中工作。 | [View](https://github.com/OfficeDev/microsoft-teams-library-js/tree/main/apps/sample-app) |
| Northwind Orders 应用 | 演示如何使用 Microsoft TeamsJS SDK V2 将 Teams 应用程序扩展到其他 Microsoft 365 主机应用。 在 Teams、Outlook、Office 中工作。 针对移动设备进行优化。| [View](https://github.com/microsoft/app-camp/tree/main/experimental/ExtendTeamsforM365) |

## <a name="next-step"></a>后续步骤

发布应用以便在 Teams、Outlook 和 Office 中可以发现：

> [!div class="nextstepaction"]
> [发布适用于 Outlook 和 Office 的 Teams 应用](publish.md)
