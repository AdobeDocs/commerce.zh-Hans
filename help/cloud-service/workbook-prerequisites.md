---
title: ADL Commerce实验室先决条件
description: 了解评级扩展实验室的先决条件。
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ba4d096bcb99420c029d0b0674fc00f1f1445cea
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Adobe Developers Live - Adobe Commerce实验室先决条件

本页列出了[评级扩展实验室](./workbook.md)的先决条件和其他手动设置步骤。 本实验还包含一个脚本，可自动完成这些步骤中的大部分步骤。

## 扩展先决条件

在开始之前，请完成以下先决条件：

* 安装[!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* 安装Commerce插件

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* 下载AI辅助的IDE，如[Cursor](https://cursor.com/download)（推荐），其他IDE，如Claude Code、Gemini CLI或Copilot也受支持，但可能需要修改本教程中的提示和其他步骤。
<!-- 
### Create a new project on Adobe Developer Console

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Create project with App Builder template](./assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click **Save**.

### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![APIs added to workspace](./assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select the [!UICONTROL **Adobe Services**] filter and select one of the following APIs:

   * [!UICONTROL **I/O Management API**]
   * [!UICONTROL **I/O Events**]

1. Select the [!UICONTROL **Experience Cloud**] filter and select one of the following APIs:

   * [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![APIs added to workspace](./assets/apis-added.png){width="600" zoomable="yes"} -->

### 配置AIO CLI

1. 清除现有配置：

   ```bash
   aio config clear
   ```

   使用AIO CLI登录：

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

   ![CLI配置](./assets/cli-configuration.png){width="600" zoomable="yes"}

### 克隆集成入门工具包

克隆Commerce集成入门套件存储库并准备项目：

```bash
git clone --branch adl https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![克隆入门工具包](./assets/clone-starter-kit.png){width="600" zoomable="yes"}

### 创建.env文件

创建环境配置文件：

```bash
cp env.dist .env
```

<!-- Open the `.env` file in a text editor and add the following OAuth credentials:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth credentials](./assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Go to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your assigned seat.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL Endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```text
EVENT_PREFIX=test
```
 -->

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

![连接到工作区](./assets/connect-workspace.png){width="600" zoomable="yes"}

## 店面先决条件

完成本教程的[storefront](#connect-to-the-storefront)部分并查看商店中的产品评级需要以下项目。
<!-- 
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
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront -->

### 获取项目文件

您可以通过以下两种方式之一获取项目文件：

<!-- 
#### Option A: Clone the repository (recommended) -->

如果已安装[!DNL Git]，请打开终端并克隆存储库：

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

<!-- #### Option B: Download the zip file

If you don't have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ``` -->

### 安装根依赖项

安装主项目依赖项：

```bash
npm install
```

这将安装店面应用程序所需的所有软件包。

### 安装MCP服务器依赖项

导航到MCP服务器目录并安装其依赖项：

```bash
cd mcp-server
npm install
cd ..
```

<!-- ### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create a `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values (we'll provide the actual URL during the lab):

```env
RAG_MODE=worker
WORKER_RAG_URL=<provided-during-lab>
```

>[!NOTE]
>
>The actual value for `WORKER_RAG_URL` will be provided by the lab facilitator at the start of the session. -->

### 在光标中启用MCP

模型上下文协议(MCP)服务器为AI代理提供了对[!DNL Adobe Commerce] Storefront文档的访问权限。

#### 打开光标MCP设置

![打开游标MCP设置](./assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. 打开[!DNL Cursor]
1. 转到&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**

#### 启用和配置MCP功能

项目在`.cursor/mcp.json`处包含MCP配置文件。 此文件应已配置为使用本地MCP服务器。

验证MCP配置：

1. 确保列出并启用“commerce-documentation-rag”服务器

配置应类似于以下内容：

![MCP配置](./assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>`start-mcp.sh`脚本将自动从`.env`目录中的`mcp-server`文件加载环境变量。

#### 重新启动光标

启用MCP并配置服务器后：

1. 完全退出[!DNL Cursor]
1. 重新打开[!DNL Cursor]并打开`aem-boilerplate-commerce`项目

#### 验证MCP连接

检查MCP服务器是否正确运行：

1. 在[!DNL Cursor]中打开新聊天
1. 查找显示MCP服务器已连接的指示器（通常在聊天界面中）
1. 尝试提出如下问题：“搜索店面文档以了解有关版块的信息”

如果MCP服务器正在工作，您应该会看到相关的文档结果。

已验证![MCP连接](./assets/mcp-connection-verified.png){width="600" zoomable="yes"}

### 启动开发服务器

启动本地开发服务器：

```bash
npm run start
```

开发服务器将在`http://localhost:3000`启动。

导航到`http://localhost:3000/apparel`上的服装页面。

![开发服务器正在运行](./assets/development-server-running.png){width="600" zoomable="yes"}
