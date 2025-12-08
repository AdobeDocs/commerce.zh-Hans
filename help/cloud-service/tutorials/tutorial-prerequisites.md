---
title: 评级扩展教程先决条件
description: 了解评级扩展实验室的先决条件。
role: Developer
hide: true
hidefromtoc: true
source-git-commit: e153e974be1dc5ec8ff2eff8d699ce87ef6708dc
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 评级扩展教程先决条件(Beta)

>[!NOTE]
>
>本教程中使用的AI工具当前位于Beta中，可能包含错误或其他问题。

本页列出了使用[!DNL Adobe Commerce as a Cloud Service]的教程的先决条件和设置步骤，如[评级扩展教程](./ratings-extension.md)。

## Adobe Commerce as a Cloud Service先决条件

* 安装[!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* 安装Commerce插件

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* 下载AI辅助的IDE，如[Cursor](https://cursor.com/download)（推荐），其他IDE，如Claude Code、Gemini CLI或Copilot也受支持，但可能需要修改提示和教程中的其他步骤。

### Adobe Developer Console先决条件

1. 导航到[Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}。
1. 使用您的电子邮件和密码登录。

#### 创建新项目

1. 导航到[Adobe Developer Console](https://developer.adobe.com/)。
1. 单击&#x200B;[!UICONTROL **从模板创建项目**]。
1. 选择&#x200B;[!UICONTROL **App Builder**]&#x200B;模板。
1. 输入&#x200B;[!UICONTROL **项目标题**]&#x200B;和&#x200B;[!UICONTROL **应用程序名称**]。
1. 确保选中&#x200B;**[!UICONTROL Include Runtime]**&#x200B;复选框。

   ![使用App Builder模板创建项目](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. 单击&#x200B;**保存**。

#### 将API添加到工作区

1. 单击&#x200B;[!UICONTROL **阶段**]&#x200B;工作区，然后对每个API重复以下步骤。

   ![个API已添加到工作区](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. 单击&#x200B;[!UICONTROL **添加服务**]&#x200B;并选择&#x200B;[!UICONTROL **API**]。

1. 选择以下API之一。 您需要为下面列出的每个API重复此过程：

   * [!UICONTROL **Adobe服务**]&#x200B;筛选器：
      * [!UICONTROL **I/O管理API**]
      * [!UICONTROL **I/O事件**] API
   * [!UICONTROL **Experience Cloud**]&#x200B;筛选器：
      * 适用于Adobe Commerce的&#x200B;[!UICONTROL **Adobe I/O Events**] API

1. 单击&#x200B;[!UICONTROL **下一步**]。

1. 单击&#x200B;[!UICONTROL **保存配置的API**]。

1. 重复上述步骤，直到将所有API添加到工作区为止。

   ![个API已添加到工作区](../assets/apis-added.png){width="600" zoomable="yes"}

### 配置Adobe I/O CLI

1. 清除任何现有配置：

   ```bash
   aio config clear
   ```

   使用[!DNL Adobe I/O CLI]登录：

   ```bash
   aio auth login -f
   ```

1. 使用以下每个命令选择您的组织、项目和工作区：

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![CLI配置](../assets/cli-configuration.png){width="600" zoomable="yes"}

### 克隆集成入门工具包

克隆Commerce集成入门套件存储库并准备项目：

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![克隆入门工具包](../assets/clone-starter-kit.png){width="600" zoomable="yes"}

### 创建.env文件

创建环境配置文件：

```bash
cp env.dist .env
```

在文本编辑器中打开`.env`文件并添加以下OAuth凭据：

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

您可以通过单击工作区上的&#x200B;**[!UICONTROL Credential details]**&#x200B;选项卡，从[Developer Console](https://developer.adobe.com/)中的&#x200B;**[!UICONTROL OAuth Server-to-Server]**&#x200B;页面复制这些值。

![OAuth凭据](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### 添加Commerce配置

将以下Commerce实例详细信息添加到您的`.env`文件：

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

要查找这些值，请执行以下操作：

1. 导航到[Commerce Cloud服务实例](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances)。
1. 单击实例旁边的信息图标。
1. 将REST终结点复制为`COMMERCE_BASE_URL`。
1. 将GraphQL端点复制为`COMMERCE_GRAPHQL_ENDPOINT`。

#### 设置事件前缀

为事件前缀设置临时值：

```text
EVENT_PREFIX=test
```

### 下载工作区配置

运行以下命令下载工作区配置文件：

```bash
aio console workspace download workspace.json
```

### 将本地工作区连接到远程工作区

将本地项目链接到远程工作区：

```bash
aio app use workspace.json -m
```

![连接到工作区](../assets/connect-workspace.png){width="600" zoomable="yes"}

### 安装可扩展性人工智能工具

更新游标规则文件和MCP配置以包含`commerce-extensibility-tools`包。

1. 使用以下命令在`extension`文件夹中设置AI辅助开发工具：

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![安装AI工具](../assets/install-ai-tools.png){width="600" zoomable="yes"}
<!--
## Storefront prerequisites

The following items are required to complete the [storefront](./ratings-extension.md#connect-to-the-storefront) section of [this tutorial](./ratings-extension.md) and see the product ratings in your store.

* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com) (Optional) - Required only if [cloning the repository directly](#option-a-clone-the-repository-recommended)(recommended), not needed if you [download the zip file](#option-b-download-the-zip-file). Verify your installation:

  ```bash
  git --version
  ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront

### Get the project files

You can obtain the project files using one of the following methods:

#### Option A: Clone the repository (recommended)

If you have [!DNL Git] installed, open your terminal and clone the repository:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

#### Option B: Download the zip file

If you do not have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ```

### Install root dependencies

Install the main project dependencies:

```bash
npm install
```

This will install all the necessary packages for the storefront application.

### Install MCP server dependencies

Navigate to the MCP server directory and install its dependencies:

```bash
cd mcp-server
npm install
cd ..
```

### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create an `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values:

```env
RAG_MODE=worker
WORKER_RAG_URL=
```

### Enable MCP in Cursor

The Model Context Protocol (MCP) server provides AI agents with access to [!DNL Adobe Commerce] Storefront documentation.

#### Open Cursor MCP settings

![Open Cursor MCP Settings](../assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Open [!DNL Cursor].
1. Navigate to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

#### Enable and configure MCP features

The project includes an MCP configuration file at `.cursor/mcp.json`. This file should already be configured to use the local MCP server.

Verify the MCP configuration:

1. Ensure the "commerce-documentation-rag" server is listed and enabled

The configuration should look similar to this:

![MCP Configuration](../assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>The `start-mcp.sh` script will automatically load the environment variables from your `.env` file in the `mcp-server` directory.

#### Restart Cursor

After enabling MCP and configuring the server:

1. Quit [!DNL Cursor] completely.
1. Reopen [!DNL Cursor] and open the `aem-boilerplate-commerce` project.

#### Verify MCP connection

Check that the MCP server is running correctly:

1. Open a new chat in [!DNL Cursor].
1. Look for an indicator showing the MCP server is connected. This indicator is typically located in the chat interface.
1. Try entering a prompt like the following:

   ```text
   Search the storefront docs for information about slots
   ```

If the MCP server is working, you should see relevant documentation results.

![MCP Connection Verified](../assets/mcp-connection-verified.png){width="600" zoomable="yes"}

If this works, you are ready to continue with the [tutorial](./ratings-extension.md).
 -->
