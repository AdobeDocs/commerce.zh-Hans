---
title: 文档RAG服务
description: 了解如何使用AI支持的文档搜索服务进行Adobe Commerce开发。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 28396828516645abec3b42a2c6874afe9134dfb8
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 文档RAG服务(Beta)

>[!NOTE]
>
>文档RAG服务当前位于Beta中，并且体验可能会发生更改。

文档RAG（检索 — 增强生成）服务在相关Adobe Commerce和App Builder文档中提供AI支持的语义搜索功能。

此RAG提供了一个IDE界面来询问有关Adobe Commerce的问题，并可为您提供有关开发应用程序和其他迁移任务的最佳实践的建议。

RAG服务是[Commerce可扩展性工具](./coding-tools.md) MCP（模型上下文协议）服务器的一部分，该服务器与Cursor和其他与MCP兼容的AI助理集成。

## 可用文档

下表描述了RAG服务当前索引的文档，以及可用于触发搜索关联索引的关键字。 随着我们开发RAG服务，包含的文档将继续扩展。

| 类别 | 索引 | 包含的内容 | 关键字 |
|-------|---------|---------|------------------------|
| [店面](https://experienceleague.adobe.com/developer/commerce/storefront/) | commerce-storefront-docs | Edge Delivery Services、插件、店面组件 | 店面、插件、EDS、产品列表、结账 |
| [可扩展性](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhook、活动、扩展、集成 | webhook，事件，扩展， API网格， GraphQL |
| [Commerce](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview) | commerce-core-docs | 核心Commerce（目录、客户、订单） | 目录，产品，客户，订单，库存 |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder，运行时操作， UI扩展 | app Builder，运行时操作， React Spectrum |

有关索引选择的详细信息，请参阅[自动索引选择](#automatic-index-selection-recommended)和[显式索引选择](#explicit-index-selection)。

有关每个索引中包含的文档的详细信息，请参阅[摄取的源列表](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md)。

## 安全性和隐私

* **IMS身份验证** — 所有API调用都使用Adobe IMS OAuth2令牌。
* **无数据存储** - MCP服务器不存储任何凭据或数据。
* **本地执行** — 所有工具都在您的计算机上本地运行。
* **安全通信** — 文档搜索使用带有令牌验证的HTTPS。

生产终结点受[Azure前门](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview)保护，包括以下保护：

* 包含Microsoft默认规则集2.1和机器人管理器规则集1.0的Web应用程序防火墙(WAF)
* 美国禁运地区（古巴、伊朗、朝鲜、叙利亚、克里米亚、卢甘斯克、顿涅茨克）的地域封锁
* 边缘的DDoS保护
* API管理后端被锁定为仅接受来自前门的流量

对于不同的安全要求，您可以使用自定义端点。 有关详细信息，请参阅[自定义前门端点](#custom-front-door-endpoint)。

## 先决条件

安装之前，请确保您拥有：

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+（建议使用LTS）
* [Cursor IDE](https://cursor.com/download){target="_blank"} （推荐）或其他与MCP兼容的IDE

  >[!NOTE]
  >
  >虽然支持其他MCP兼容的IDE，但为获得最佳体验，建议使用Cursor。 如果您使用的是其他IDE，则需要修改该文档中的提示和其他步骤才能使用选定的IDE。

## 安装

1. 全局安装[Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/)：

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. 使用Adobe IMS进行身份验证：

   ```bash
   aio auth login
   ```

1. 克隆Commerce可扩展性工具存储库并导航到目录：

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. 安装依赖项：

   ```bash
   npm install
   ```

1. 在Commerce项目目录中创建或更新`.cursor/mcp.json`（非全局）以包含`commerce-extensibility-tools` MCP服务器：

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   请确保将`<your-project-directory>`替换为您克隆存储库的实际路径。

   >[!NOTE]
   >
   >在Windows上，如果您在提供项目目录的路径时遇到问题，请参阅[路径问题疑难解答](#path-issues-windows)。

1. 重新启动Cursor IDE以加载MCP服务器。

1. 通过询问AI助手来验证安装：

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## 使用情况

安装后，您可以自动调用索引[&#128279;](#automatic-index-selection-recommended)或[显式调用](#explicit-index-selection)。 您还可以使用[`/search-commerce-docs`命令](#command-based-search)。

>[!NOTE]
>
>RAG服务会返回前5个最相关的结果。

### 自动索引选择（推荐）

通过询问有关Commerce项目的自然语言问题，该工具将自动搜索相应的文档索引并提供相关信息：

>[!BEGINSHADEBOX]

以下提示将自动选择`commerce-storefront-docs`索引：

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

以下提示将自动选择`commerce-extensibility-docs`索引：

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

以下提示将自动选择`commerce-core-docs`索引：

```shell-session
"How to configure product catalog settings?"
```

以下提示将自动选择`app-builder-docs`索引：

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### 显式索引选择

或者，您可以指定要在提示中使用的索引。

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### 基于命令的搜索

如果要确保使用RAG服务，可以手动调用`/search-commerce-docs` Cursor命令以搜索带有提示的文档：

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## 自定义前门端点

默认情况下，文档搜索使用具有WAF保护的生产[Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview)端点。 出于测试或开发目的，您可以使用`FRONT_DOOR_URL`环境变量覆盖此设置。

要使用自定义端点，请将其添加到您的光标MCP配置：

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>大多数开发人员应使用默认的生产端点，而无需设置`FRONT_DOOR_URL`变量。

## 故障排除

以下部分提供了有关在使用文档RAG服务时可能遇到的常见问题的故障排除提示。

### 身份验证错误

文档搜索工具要求使用Adobe IMS身份验证。 如果遇到身份验证错误，请使用以下步骤对问题进行疑难解答和解决。

1. 验证您已登录：

   ```bash
   aio where
   ```

1. 验证您是否能够看到您的IMS令牌：

   ```bash
   aio auth login --bare
   ```

1. 如果仍存在身份验证错误，请尝试注销并重新登录：

   ```bash
   aio auth logout
   aio auth login
   ```

### MCP服务器未加载

如果MCP服务器未连接，或代理程序指出无法连接到RAG，请使用以下步骤进行故障排除并解决问题。

1. 使用&#x200B;**Cmd 、** (macOS)或&#x200B;**Ctrl 、** （Windows和Linux）打开光标设置。

1. 搜索“MCP”并验证`commerce-extensibility-tools`是否已列出并启用。

1. 在MCP设置面板中检查错误消息。

1. 验证项目中是否存在`mcp.json`文件：

   ```bash
   cat .cursor/mcp.json
   ```

1. 验证路径正确且绝对：

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### 未找到工具

1. 退出Cursor并将其重新打开。

1. 通过使用&#x200B;**Cmd+Shift+P** (macOS)或&#x200B;**Ctrl+Shift+P** (Windows/Linux)并搜索“开发人员：打开日志文件夹”，在Cursor的开发人员控制台中检查MCP服务器日志。

1. 验证安装：

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   服务器应该可以启动，并且没有错误。

### 路径问题(Windows)

在Windows上，使用正斜杠`/`或转义的反斜杠`\\`：

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## 其他资源

* [Adobe Commerce开发人员文档](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [App Builder文档](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [模型上下文协议](https://modelcontextprotocol.io/){target="_blank"}
* [游标IDE](https://cursor.sh/docs){target="_blank"}
