---
title: 在本地调试 Teams 应用
author: surbhigupta
description: 在本模块中，了解如何在 Teams 工具包中本地调试 Teams 应用以及 Teams 工具包的主要功能
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 65eb9599bb60b35448aaf1b6239fc155b7d397d5
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791571"
---
# <a name="debug-your-teams-app-locally"></a>在本地调试 Teams 应用

Teams 工具包可帮助你在本地调试和预览 Microsoft Teams 应用。 在调试过程中，Teams 工具包会自动启动应用服务、启动调试器并旁加载 Teams 应用。 调试后，可以在 Teams Web 客户端本地预览 Teams 应用。

::: zone pivot="visual-studio-code"

## <a name="debug-your-microsoft-teams-app-locally-for-visual-studio-code"></a>在本地调试 Microsoft Teams 应用以Visual Studio Code

Visual Studio Code 中的 Teams 工具包提供了在本地自动调试 Teams 应用的功能。 Visual Studio 允许调试选项卡、机器人和消息扩展。 在调试应用之前，需要设置 Teams 工具包。

> [!NOTE]
>
> 可以升级旧的 Teams 工具包项目以使用新任务，有关详细信息，请参阅 [调试设置文档](https://aka.ms/teamsfx-debug-upgrade-new-tasks)

## <a name="set-up-your-teams-toolkit-for-debugging"></a>设置 Teams 工具包进行调试

以下步骤可帮助你在启动调试过程之前设置 Teams 工具包：

# <a name="windows"></a>[Windows](#tab/Windows)

1. 从“**运行****和调试”下拉列表中选择“调试 (Edge)**”或“**调试 (Chrome)**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="浏览器选项":::

1. 选择 **“运行** > **启动调试” (F5)**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="开始调试":::

3. 选择“**登录**”到 Microsoft 365 帐户。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="登录":::

   > [!TIP]
   > 可以选择“**阅读更多**”，以了解Microsoft 365 开发人员计划。 默认 Web 浏览器随即打开，让你使用凭据登录 Microsoft 365 帐户。

4. 选择“**安装**”，以安装本地主机的开发证书。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="证书":::

   > [!TIP]
   > 可以选择“**了解**”有关开发证书的详细。

5. 在“**安全警告**”对话框中选择“**是**”：

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="证书颁发机构":::：

工具包根据所选内容启动新的 Edge 或 Chrome 浏览器实例，并打开网页以加载 Teams 客户端。  

# <a name="macos"></a>[macOS](#tab/macOS)

1. 从 **“** 运行和 **调试** ”下拉列表中选择“调试边缘”或 **“调试** Chrome”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="浏览器列表":::

1. 选择“**开始调试(F5)**”或“**运行**”，以在调试模式下运行 Teams 应用。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="调试应用":::

3. 选择“**登录**”到 Microsoft 365 帐户。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="登录到 Microsoft 365 帐户":::

   > [!TIP]
   > 可以选择“**阅读更多**”，以了解Microsoft 365 开发人员计划。 打开默认 Web 浏览器，使用凭据登录到 Microsoft 365 帐户。

4. 选择“**安装**”，以安装本地主机的开发证书。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="证书":::

   > [!TIP]
   > 可以选择“**了解**”有关开发证书的详细。

5. 输入 **“用户名”** 和“ **密码”**，然后选择“ **更新设置**”。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="mac 登录":::

Teams 工具包启动浏览器实例并打开一个网页来加载 Teams 客户端。

---

## <a name="debug-your-app"></a>调试应用

完成初始设置过程后，Teams 工具包将启动以下过程：

* [启动应用服务](#starts-app-services)
* [启动调试配置](#launches-debug-configurations)
* [旁加载 Teams 应用程序](#sideloads-the-teams-app)

### <a name="starts-app-services"></a>启动应用服务

运行 中 `.vscode/tasks.json`定义的任务。

|  组件 |  任务名称  | Folder |
| --- | --- | --- |
|  Tab |  **启动前端** |  选项卡 |
|  自动程序或邮件扩展 |  **启动自动程序** |  自动程序 |
|  Azure Functions |  **启动后端** |  API |

下图显示了运行选项卡、机器人或消息扩展以及Azure Functions时Visual Studio Code的 **“输出**”和“**终端**”选项卡中的任务名称。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal1.png" alt-text="启动应用服务" lightbox="../assets/images/teams-toolkit-v2/debug/Terminal1.png":::

### <a name="launches-debug-configurations"></a>启动调试配置

启动中 `.vscode/launch.json`定义的调试配置。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="启动调试程序":::

下表列出了使用选项卡、机器人或消息扩展应用以及Azure Functions的项目的调试配置名称和类型：

|  组件 |  调试配置名称  | 调试配置类型 |
| --- | --- | --- |
|  Tab |  **连接到前端 (Edge)** 或  **连接到前端 (Chrome)**  |  pwa-msedge 或 pwa-chrome  |
|  自动程序或邮件扩展 |   **连接到自动程序** |  pwa 节点 |
| Azure Functions |   **连接到后端** |  pwa 节点 |

下表列出了具有机器人应用、Azure Functions和不带选项卡应用的项目的调试配置名称和类型：

|  组件 |  调试配置名称  | 调试配置类型  |
| --- | --- | --- |
|  自动程序或邮件扩展  | **启动自动程序 (Edge)** 或 **启动自动程序 (Chrome)**  |   pwa-msedge 或 pwa-chrome  |
|  自动程序或邮件扩展  |   **连接到自动程序** |  pwa 节点  |
|  Azure Functions |  **连接到后端** |  pwa 节点 |

### <a name="sideloads-the-teams-app"></a>旁加载 Teams 应用

“ **附加到前端”** 或 **“启动机器人”** 配置启动 Edge 或 Chrome 浏览器实例，以在网页中加载 Teams 客户端。 加载 Teams 客户端后，Teams 会旁加载由 Microsoft Teams 启动配置中定义的旁加载 URL 控制的 [Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}) 应用。 当 Teams 客户端在 Web 浏览器中加载时，选择“ **添加** ”或根据你的要求从下拉列表中选择一个选项。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="添加本地调试" lightbox="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png":::

   你的应用已添加到 Teams！

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [调试后台进程](debug-background-process.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-teams-app-locally-using-visual-studio"></a>使用 Visual Studio 在本地调试 Teams 应用

Teams 工具包可帮助你在本地调试和预览 Microsoft Teams 应用。 Visual Studio 允许调试选项卡、机器人和消息扩展。 可以通过执行以下操作，使用 Teams 工具包在 Visual Studio 中本地调试应用：

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>为机器人和消息扩展应用设置 ngrok () 

使用命令提示符运行此命令：

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>设置 Teams 工具包

创建项目后，使用 Teams 工具包调试应用，执行以下步骤：

1. 右键单击 **项目**。
1. 选择“ **Teams 工具包** > **准备 Teams 应用依赖项**”。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="用于本地调试的 Teams 应用依赖项" lightbox="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png":::

   > [!NOTE]
   > 在此方案中，项目名称为 MyTeamsApp1

   在登录之前，Microsoft 365 帐户需要具有旁加载权限。  确保 Teams 应用可以上传到租户，否则 Teams 应用可能无法在 Teams 客户端中运行。

1. 登录到 **Microsoft 365 帐户**，然后选择“**继续**”

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="登录到 Microsoft 365 帐户":::

   > [!Note]
   > 访问 <https://aka.ms/teamsfx-sideloading-option>详细了解旁加载权限。

1. 选择“ **调试** > **”“开始调试**”，或直接选择“ **F5**”。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="启动调试":::

   Visual Studio 在浏览器中的 Microsoft Teams 客户端内启动 Teams 应用。

   > [!Note]
   > 请访问 <https://aka.ms/teamsfx-vs-debug>了解详细信息。

1. 加载 Microsoft Teams 后，选择“ **添加** ”以在 Teams 中安装应用。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="选择“添加”以加载应用":::

   > [!TIP]
   > 还可以在调试期间使用 Visual Studio 的热重载函数。 请访问 <https://aka.ms/teamsfx-vs-hotreload>了解详细信息。

   > [!NOTE]
   > 在调试通知机器人应用时，请确保将 HTTP 请求 `http://localhost:5130/api/notification` 发布到 以触发通知。 如果在创建项目时选择了 HTTP 触发器，则可以使用任何 API 工具，例如 curl (Windows 命令提示符) 、Postman 等。

   > [!TIP]
   > 如果对 /templates/appPackage/manifest.template.json)  (Teams 应用清单文件进行任何更改，请确保执行“准备 Teams 应用依赖项”命令。 尝试再次在本地运行 Teams 应用之前。

::: zone-end

## <a name="see-also"></a>另请参阅

* [使用 Teams 工具包预配云资源](provision.md)
* [将功能添加到 Teams 应用](add-capability.md)
* [部署到云](deploy.md)
* [在 Teams 工具包中管理多个环境](TeamsFx-multi-env.md)
