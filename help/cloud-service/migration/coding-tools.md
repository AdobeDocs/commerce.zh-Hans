---
title: 扩展的AI编码工具
description: 了解如何使用AI工具创建Commerce App Builder扩展。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
role: Architect
hide: true
hidefromtoc: true
source-git-commit: e032571ba0dd8a2f71813f9e3114afa3f7d617bf
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# 扩展的AI编码工具

迁移到[!DNL Adobe Commerce as a Cloud Service]时，您可以使用AI编码工具将现有[!DNL Adobe Commerce] PHP扩展转换为[!DNL Adobe Developer App Builder]扩展。 它也可用于创建新的[!DNL App Builder]扩展。

使用AI编码工具具有以下优势：

* **增强的开发工作流**：集成的Adobe Commerce开发工具。
* **AI支持的帮助**：上下文感知代码生成和调试。
* **Commerce特定功能**：用于Adobe Commerce App Builder开发的专用工具。
* **自动化工作流**：简化了开发和部署流程。

## 先决条件

* [游标](https://cursor.com/download)
* [Node.js](https://nodejs.org/en/download)： LTS版本
* 包管理器： [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)或[yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git)：用于存储库克隆和版本控制

## 安装

1. 全局安装最新的[Adobe I/O CLI](https://github.com/adobe/aio-cli)：

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. 安装[Adobe I/O CLI Commerce插件](https://github.com/adobe-commerce/aio-cli-plugin-commerce)：

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. 克隆Commerce [集成入门工具包](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)：

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. 导航到starter kit目录：

   ```bash
   cd commerce-integration-starter-kit
   ```

1. 通过运行交互式设置命令安装Commerce AI可扩展性工具：

   ```bash
   aio commerce extensibility tools-setup
   ```

安装过程将为您提示配置选项。 对于安装位置，选择“当前目录”以在当前工作区中安装工具：

```terminal
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

选择包管理器时，Adobe建议使用`npm`来保持一致性：

```terminal
? Which package manager would you like to use?
❯ npm
  yarn
```

1. 成功安装编码工具后，安装过程将配置：

   * 用于Adobe Commerce开发的MCP服务器集成
   * 用于增强开发体验的光标IDE规则
   * 特定于Commerce的开发工具和工作流

   以下文件将添加到您的工作区：

   * MCP配置： `.cursor/mcp.json`
   * Rules目录： `.cursor/rules/`

## 安装后配置

1. 重新启动光标IDE以加载新的MCP工具和配置。

1. 通过确认规则存在于`.cursor/rules/`文件夹下来验证安装。

1. 启用MCP服务器：

   * 使用&#x200B;**Cmd+Shift+P** (macOS)或&#x200B;**Ctrl+Shift+P** （Windows和Linux）打开光标MCP设置。
   * 类型&#x200B;**视图：打开MCP设置**
   * 在列表中找到&#x200B;**commerce-extensibility MCP服务器**
   * 切换服务器&#x200B;**ON**&#x200B;以启用编码工具

1. 验证服务器状态 — Commerce可扩展性MCP服务器应显示为：

   ```terminal
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

## 示例提示

以下示例提示创建一个扩展，用于在下订单时发送通知。

```terminal
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## 最佳实践

Adobe建议在使用人工智能编码工具时遵循以下最佳实践：

### 清单

在开始任何开发会话之前：

* 检查`REQUIREMENTS.md`
* 验证MCP工具是否正常工作
* 审查当前阶段和目标
* 从示例代码或基架项目开始

在开发过程中：

* 信任四阶段[协议](#protocol)
* 为复杂开发请求实施计划
* 在可用时使用MCP工具
* 实施后测试每个功能
* 首先在本地测试，然后再次部署和测试
* 利用编码工具测试支持
* 问题不必要的复杂性
* 增量部署以实现更快的开发

开始新聊天时：

* 提供正确的会话切换
* 使用`@`的引用密钥文件
* 为会话设置明确的目标
* 使用基于阶段的边界

### 工作流

使用AI编码工具进行开发时，请从示例代码或基架项目开始。 此方法可确保您基于坚实的基础进行构建，而不是从零开始，同时还可优化您的AI开发工作流。

这还允许您利用Adobe的模板并基于经验证的模式和体系结构进行构建，同时保留已建立的目录结构和约定。

请查阅以下资源以开始使用：

* [集成入门工具包](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [Adobe Commerce入门套件模板](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Adobe I/O Events入门模板](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [App Builder示例应用程序](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### 为什么应使用这些资源

* **经验证的模式**：入门套件体现了Adobe的最佳实践和体系结构决策
* **加快开发**：减少花在样板和配置上的时间
* **一致性**：确保扩展遵循已建立的约定
* **可维护性**：遵循标准模式时，更容易维护和更新
* **文档**：入门套件随附示例和文档
* **社区支持**：使用标准方法时更容易获得帮助
* **AI上下文效率**：使用熟悉的模式和结构进行处理，从而减少大量解释的需要，并提高代码生成准确性
* **减少了令牌使用量**：引用现有模式，而不是从头开始生成所有内容，从而提高对话效率和减少上下文摘要

### 协议

规则系统会自动实施以下四阶段协议。 在开发扩展时，工具应自动遵循此协议：

* 第1阶段：需求分析和说明
   * 当被问及澄清问题时，请提供完整的答案。
* 第2阶段：架构规划和用户批准
   * 提交计划时，请在批准之前仔细审查计划。
* 阶段3：代码生成和实施
* 第4阶段：文档和验证

### 为复杂开发请求实施计划

对于涉及多个运行时操作、接触点或集成的复杂开发，明确要求AI工具创建详细的实施计划。 当您在[阶段2](#protocol)中看到涉及多个组件的高级计划时，请要求提供详细的实施计划以将其划分为可管理的任务：

```terminal
Create a detailed implementation plan for this complex development.
```

复杂的Adobe Commerce扩展通常涉及：

* 多个运行时操作
* 跨多个接触点的事件配置
* 与外部系统集成
* 状态管理要求
* 跨多个组件测试

### 使用MCP工具

该工具默认为MCP工具，但在某些情况下，它可以改用CLI命令。 如果要确保MCP工具的使用情况，请在提示符下明确请求使用。

如果您看到正在使用的CLI命令并希望改用MCP工具，请使用以下提示：

```terminal
Use only MCP tools and not CLI commands
```

* MCP工具：aio-app-deploy、aio-app-dev、aio-dev-invoke
* CLI命令：aio应用程序部署、aio应用程序开发

CLI命令可用于以下情况：

* 复杂的部署方案
* 调试特定问题
* 当MCP工具具有限制时
* 无法从MCP集成中受益的一次性操作

### 开发

重要的是，要质疑人工智能工具所造成的不必要的复杂性。

为简单只读端点添加不必要的文件(`validator.js`、`transformer.js`、`sender.js`)时，请使用以下提示：

```terminal
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### 测试

测试时请遵循以下最佳实践：

#### 实施后测试每个功能

完成实施计划中的功能开发后，请立即对其进行测试。 早期测试可避免复合问题，并使调试更容易。

* 不要等到所有功能都完成
* 增量测试以及早发现问题
* 在移到下一个功能之前验证功能

#### 首先在本地测试

始终首先使用`aio-app-dev`工具在本地测试。 这提供了即时反馈，并允许更快的迭代周期、更轻松的调试以及无部署开销。

1. 启动本地开发服务器：

   ```bash
   aio-app-dev
   ```

1. 本地测试操作：

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### 再次部署和测试

本地测试成功后，在运行时环境中部署和测试。 运行时环境的行为可能与本地开发不同。

1. 部署到运行时：

   ```bash
   aio-app-deploy
   ```

1. 测试已部署的操作

1. 使用Web浏览器或直接HTTP请求

1. 检查激活日志以进行调试

#### 利用编码工具测试支持

请求有关测试的帮助。 这些工具可帮助调试、日志分析和为特定运行时操作创建适当的测试数据。

**测试运行时操作**：

```terminal
Help me test the customer-created runtime action running locally
```

**调试失败**：

```terminal
Why did the subscription-updated runtime action activation fail?
```

**检查日志**：

```terminal
Help me check the logs for the last stock-monitoring runtime action invocation
```

**创建测试负载**：

```terminal
Generate test data for this Commerce event
```

```terminal
Create a test payload for the customer_save_after event
```

**查找运行时终结点**：

```terminal
What's the URL for this deployed action?
```

**处理身份验证**：

```terminal
How do I authenticate with this external API?
```

**疑难解答**：

```terminal
Help me debug why this action is returning 500 errors
```

### 调试

停止并评估何时出现问题。 如果您遇到问题：

* 停止并评估 — 不要在中断状态下继续
* 检查日志 — 使用激活日志识别问题
* 简化 — 消除复杂性以隔离问题
* 增量测试 — 一次修复一个问题
* 验证 — 在继续操作之前测试每个修复

### 部署

部署时请遵循以下最佳实践：

#### 增量部署

仅部署已修改的操作，以加快开发。 这将降低中断现有功能的风险，并加快提供更改的反馈。 它还降低了中断现有功能的风险。

* 使用MCP工具部署特定操作

  ```bash
  aio-app-deploy --actions action-name
  ```

* 在本地测试后部署单个操作
* 以增量方式部署，避免在开发期间进行完整的应用程序部署

#### 运行时清理

在进行重大更改后，请利用这些工具来清理孤立的操作。 AI工具可以系统地处理清除过程，高效地识别孤立的操作，验证其状态，并且无需手动干预即可安全移除孤立的操作。

```terminal
Help me identify and clean up orphaned runtime actions
```

请求人工智能工具列出已部署的操作并识别未使用的操作

```terminal
List all deployed actions and identify which ones are no longer needed
```

让AI工具使用适当的命令删除孤立的操作

```terminal
Remove the orphaned actions that are no longer part of the current implementation
```

### 监控

在监视应用程序时，请使用以下最佳实践：

#### 查看上下文质量指示器

* **良好的上下文**： AI记住最近的决策，引用正确的文件
* **较差的上下文**： AI会询问以前提供的信息，重复已解决的问题

#### 跟踪开发速度

* **高速**：进度清晰，所需说明最少
* **低速**：重复解释，AI混乱，进度缓慢

#### 监控成本效益

跟踪令牌使用模式：

* **高效**：令牌使用率低，上下文摘要很少
* **效率低下**：令牌利用率高，有多个摘要，重复工作

## 应避免的内容

在使用AI编码工具时，您应该避免以下反模式：

* **不要跳过澄清阶段** — 始终确保在实施之前完成阶段1。
* **在每个功能之后不要跳过测试** — 增量测试，不要等到所有功能都完成。
* **在没有根本原因分析的情况下不要增加复杂性** — 询问不必要的文件添加情况并要求进行适当的调查。
* **没有实际数据测试时不声明成功** — 始终使用实际数据进行测试，而不仅仅是边缘案例。
* **不要忘记运行时清理** — 始终在主要更改后清理孤立的操作。
