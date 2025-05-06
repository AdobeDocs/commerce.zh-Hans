---
title: 设置您的店面
description: 了解如何运行基架工具来设置 [!DNL Adobe Commerce as a Cloud Service] 店面。
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
source-git-commit: 022e3474b8f2839d2501c46def21733a8d4ad9cc
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 设置您的店面

{{accs-early-access}}

以下步骤演示了如何使用`aio commerce init`命令快速设置由Edge Delivery提供支持的Adobe Commerce店面。 此过程将设置以下内容：

* [由Edge Delivery Services提供支持的Commerce店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=zh-Hans) — 由Adobe的Edge Delivery Services提供支持的高性能、可扩展且安全的店面。
* 适用于Adobe Developer App Builder的[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/) — 一个API平台，允许开发人员将多个数据源合并到单个GraphQL端点中。 API Mesh通过单个网关使用Adobe API协调第三方API。 对单个GraphQL端点的一个查询可以返回来自多个源的结果。
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) — 开发人员工具集合，具有对API、事件、运行时函数和插件的访问权限，可用于为Adobe应用程序构建项目。
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) — 用于部署自定义代码的无服务器引擎，该引擎响应云中的事件并执行函数。

## 先决条件

运行`aio commerce init`命令之前，必须完成以下先决条件：

1. 安装节点版本管理器(NVM)。

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. 安装Node.js和NPM。 有关详细信息，请参阅[Node.js](https://nodejs.org/en/)。

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. 安装[Adobe I/O Runtime CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)。

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. 安装Adobe I/O API网格插件。

   ```bash
   aio plugins:install @adobe/aio-cli-plugin-api-mesh
   ```

1. 安装Adobe I/O Commerce插件。

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. 更新任何现有的插件。

   ```bash
   aio plugins:update
   ```

1. 登录到您的Adobe Experience Cloud帐户。

   ```bash
   aio login
   ```

1. 选择IMS组织、项目和工作区。 使用箭头键并按&#x200B;**Enter**&#x200B;进行选择。 有关`aio`命令的详细信息，请参阅[Adobe I/O CLI文档](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands)。

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

1. 如果您尚未这样做，请导航到https://developer.adobe.com/console/home并单击&#x200B;**接受并继续**，以接受Adobe Developer控制台中的开发人员使用条款。

## 运行`aio commerce init`命令

运行以下命令将为您的Commerce店面创建基架。 此基架是构建和了解店面的绝佳起点。 有关使用店面的更多信息，请参阅[Adobe Commerce店面文档](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hans)。


1. 运行`init`命令：

   ```bash
   aio commerce init
   ```

1. 如果您已经登录GitHub，请输入`Y`以在您的用户名下创建存储库。

1. 输入要创建的存储库的名称。

1. 选择以下选项之一：

   * **使用演示Adobe Commerce租户** — 使用演示租户。
      * 如果选择此选项，则系统会提示您在一个浏览器窗口中安装AEM代码同步机器人。 您必须指定您创建的存储库并授权机器人。 返回到CLI并输入`y`以确认AEM代码同步机器人的安装。
   * **选择可用的Adobe Commerce租户** — 在所选组织中选择现有的Commerce租户。
      * 如果选择此选项，则必须选择要在其中创建网格的项目和工作区。
   * **提供您自己的Adobe Commerce租户API URL** — 如果您是提前访问计划参与者，请选择此选项。 输入Adobe入门培训电子邮件中提供的API URL。

   >[!NOTE]
   >
   >如果选择`Pick an available API (Mesh -> SaaS)`选项，则Adobe Developer Console中必须具有现有的项目和Workspace。 [创建模板化项目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/)并选择App Builder将自动创建所需的工作区。

1. 该过程完成后，您可以使用以下方法自定义您的店面：

   * 自定义您的代码： `https://github.com/<username or org>/<repo name>`
   * 编辑您的内容： `https://da.live/#/<username or org>/<repo name>`
   * 管理您的配置： `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * 预览店面： `https://main--<repo name>--<username or org>.aem.page/`
   * 本地运行： `aio commerce:dev`

要自定义您的店面，请参阅[Adobe Commerce店面文档](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=zh-Hans)。
