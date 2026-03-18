---
title: 库存通知扩展教程
description: 了解如何使用App Builder、Edge Delivery Services和人工智能辅助开发工具为Adobe Commerce as a Cloud Service构建库存通知扩展。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ce8882b8af21198a7bc57bc58124e8a2d1491a50
workflow-type: tm+mt
source-wordcount: '2599'
ht-degree: 0%

---

# 库存通知扩展教程

本教程将指导您使用[!DNL Adobe Commerce as a Cloud Service]和AI辅助开发工具为[!DNL Adobe App Builder]构建库存通知扩展。 该扩展允许购物者订阅缺货产品，并在产品重新上架时收到通知。

您可以构建两个部分：

- **App Builder扩展** — 用于通过事件驱动和计划的缺货检测来管理缺货订阅（创建、读取、删除）的REST API。
- **店面集成** — 产品详细信息页面(PDP)上的订阅表单，仅在所选产品或变体缺货时显示。

>[!NOTE]
>
>AI代理是不确定的。 本教程中的提示、问题和输出是示例。 您的代理可能会提出不同的问题、要求或体系结构建议。 使用本教程中的示例引导代理获得相似的结果。

在开始之前，请完成[先决条件](./tutorial-prerequisites.md)。 本教程使用&#x200B;**集成入门工具包**。 验证是否已克隆该扩展，并完成先决条件页面上描述的设置步骤。

## 验证先决条件

验证是否安装了以下必备组件：

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

如果前面的任何命令未返回预期结果，请参阅[先决条件](./tutorial-prerequisites.md)获取指导。

此外，请验证以下各项：

- 您有一个包含产品数据的[!DNL Adobe Commerce as a Cloud Service]实例。 查看[Commerce Cloud服务实例](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}。
- 您有一个店面项目连接到您的[!DNL Commerce]实例。 如果没有店面，请按照[创建店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}中的步骤操作。
- 已安装`aem` CLI：

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 扩展开发

此部分将指导您使用人工智能辅助开发工具为[!DNL Adobe Commerce as a Cloud Service]开发库存通知扩展。 该扩展提供了用于订阅管理的REST API，并检测产品何时通过Commerce事件和计划检查重新上架。

1. 导航到编码代理中的MCP设置。

   例如，在光标中，转到&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**。 验证是否已启用`commerce-extensibility`工具集且未出现错误。 如果看到错误，请关闭和打开工具集。

   >[!NOTE]
   >
   >使用人工智能辅助开发工具时，预期代码和代理生成的响应会发生自然变化。
   >如果您遇到任何代码问题，请要求代理帮助您对其进行调试。

1. 如果有任何文档添加到光标上下文中，请禁用它。

   导航到&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**&#x200B;并删除列出的任何文档。

### 步骤1：提供初始提示

提示AI代理开始实施。 告诉代理停止操作并提问可帮助您尽早指导实施。

在座席的聊天窗口中输入以下提示：

```shell-session
Implement an Adobe Commerce as a Cloud Service extension to handle out-of-stock notifications for products.

The service should provide REST API endpoints for basic create, read, update, and delete (CRUD) operations on out-of-stock notifications, allowing storefronts to manage notifications for specific product SKUs.

Back-in-stock is detected by an inventory or product event or a scheduled action that checks Commerce API and then calls the REST API to send the notification.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>在继续操作之前告知代理停止操作并询问相关问题，这有助于尽早指导实施。 此过程确保尽早识别关键假设和缺失要求，以及启动本教程中的引导式工作流所必需的。

### 第2步：回答座席的问题

代理返回时提出一系列它需要的问题，然后才能开始形成解决方案。 以下示例显示了典型的问题和答案。 您的代理可能会问不同的问题，但主题通常相同。

**代理问题示例：**

1. **REST API — 主机和使用者** - CRUD REST API是否应该包含在商店前端调用的此App Builder应用程序（例如，Adobe I/O Runtime上的Web操作）中？ 谁将调用它（EDS Storefront、自定义/Headless店面，或同时调用两者）？ 您需要CORS、公共（未经身份验证）访问，还是呼叫方将使用API密钥、OAuth或Commerce令牌？
1. **数据模型** — 一个“通知”应该代表什么？ 客户标识符（仅限电子邮件还是客户ID）？ 产品标识符（仅限SKU或SKU +商店视图）？ 同一客户是否可以多次订阅同一个SKU，或者是否应消除重复的订阅？
1. **重新上架检测 — 事件与已计划的** — 您是希望使用事件驱动检测（对Commerce中的库存/产品事件做出反应）、已计划检测（定期检查库存的计划操作）还是同时使用两者？ “发送通知”是什么意思（调用外部webhook、发送电子邮件或记录它）？
1. **重新上架 — Commerce源** — 您有首选事件名称吗，还是设计应使用Commerce提供的任何库存/库存更新事件？ 对于计划的检查，SKU应使用哪个API获取库存状态？
1. **持久性和多租用** — `aio-lib-state`是保留订阅的正确位置，还是您有外部存储？ 设计应采用多租户还是单租户？
1. **CRUD语义和生命周期** — “删除”是否意味着取消订阅？ 是否需要“更新”？ 发送后备通知后，订阅是否将自动删除或标记为已通知？
1. **无法正常工作** — 要强制实施的任何速率限制或最大订阅数？ 是否有任何合规性需求（双重选择加入、同意标记）？

**示例答案：**

```shell-session
1. The CRUD REST API should be part of thie App Builder app. It will be called by the EDS Storefront. For this implementation there is no need for API keys or security tokens.
2. For this initial implementation the customer identifier will be the email, product is identified by SKU, customer emails should not be able to subscribe to the same SKU multiple times.
3. Implement both. For now instead of sending the notification, log it so I can audit in the Adobe Developer Console.
4. Research and use what the best event to use that commerce already provides. Research the simplest way to get the stock status by SKU.
5. Use the aio-lib-state. Single tenant for now
6. Delete means cancel subscription. Skip Update, it does not apply for this service. After subscription is sent, it should be marked as notified or removed so it won't send again until the user subscribes again.
7. No limits. Implement minimal compliance requirements.
```

>[!NOTE]
>
>您的代理可能会问不同的问题。 使用这些答案作为指导，引导代理实现相同的功能结果：包含电子邮件和SKU订阅的REST API、事件驱动和计划的缺货检测、`aio-lib-state`持久性以及基于日志的通知。

### 第3步：审查要求和体系结构

代理程序会生成需求和体系结构文档供您审查。 验证要求与您提供的答案是否匹配，以及体系结构是否涵盖：

- 用于订阅CRUD（创建、读取、更新和删除）的REST API操作
- 由Commerce库存事件触发的事件驱动型缺货处理程序
- 作为回退的计划支票库存操作
- 使用`aio-lib-state`的持久性

>[!NOTE]
>
>AI代理是不确定的，其行为因模型和IDE而异。 您可能会收到一组不同的问题，这些问题会产生一组不同的要求和体系结构。 如果是这样的话，在继续之前，请尝试将代理引导到某个方向，以便该实施与本教程中介绍的内容非常匹配。

### 步骤4：选择实施计划

该代理为您提供了创建详细实施计划或完成直接实施的选项。

- 如果希望可复查计划能够以更多控制分阶段执行，请选择第一个选项。
- 如果您希望代理以最小的干预完成整个实施，请选择第二个选项。

### 步骤5：部署、载入和订阅事件

代理完成实施后，它会提供以下步骤：部署应用程序、载入Commerce实例，以及使用以下命令订阅事件：

1. 部署扩展：

   ```bash
   aio app deploy
   ```

1. 运行载入脚本以在Commerce中注册事件提供程序：

   ```bash
   npm run onboard
   ```

1. 订阅Commerce活动：

   ```bash
   npm run commerce-event-subscribe
   ```

1. 验证事件订阅。

   导航到您的Commerce实例并打开&#x200B;**[!UICONTROL System]** > **[!UICONTROL Event Subscriptions]**。

   您应该会看到一个事件记录表。

   ![Commerce管理菜单突出显示事件订阅部分](../assets/in-stock-event-subscriptions.png){width="600" zoomable="yes"}

   ![具有已注册事件条目的事件订阅表](../assets/in-stock-event-table.png){width="600" zoomable="yes"}

### 第6步：测试扩展

要求代理提供测试步骤。 由于这是一项API服务，因此您可以请求命令行指令：

```shell-session
Give me step by step instructions to test the API service from the command line.
```

按照代理提供的步骤操作。 以下示例显示了典型的测试命令。

**订阅SKU：**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api"; curl -X POST "$API_URL" \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","sku":"ADB153"}'
```

响应类似于：

```json
{
  "createdAt": "2026-03-06T22:11:00.308Z",
  "email": "test@example.com",
  "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
  "sku": "ADB153"
}
```

**列出所有订阅：**

```bash
curl -X GET "$API_URL"
```

响应将返回所有活动订阅的列表：

```json
{
  "subscriptions": [
    {
      "createdAt": "2026-03-06T22:11:00.308Z",
      "email": "test@example.com",
      "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
      "sku": "ADB153"
    }
  ]
}
```

**测试后备流程：**

1. 在Commerce实例中，编辑已为其创建订阅的产品。
1. 将产品库存状态设置为&#x200B;**[!UICONTROL Out of Stock]**。
1. 等待大约一分钟，然后将库存状态切换回&#x200B;**[!UICONTROL In Stock]**。

   ![Commerce管理员产品编辑页面显示“库存状态”下拉列表，其中包含“缺货”和“缺货”选项](../assets/in-stock-product-stock-status-toggle.png){width="600" zoomable="yes"}

1. 等待大约五分钟，以触发事件并将其发送到您的服务。

1. 从[!DNL Adobe Developer Console]，导航到App Builder日志部分。

   ![Adobe Developer Console App Builder日志部分](../assets/in-stock-developer-console-logs.png){width="600" zoomable="yes"}

1. 在日志中，验证是否存在用于确认事件已处理的条目，以及是否已识别正确的电子邮件 — SKU订阅对。

   ![App Builder日志条目显示库存事件正在处理](../assets/in-stock-log-entries.png){width="600" zoomable="yes"}

>[!TIP]
>
>您可以询问代理在日志中查找什么内容，以验证是否已成功记录通知操作。 您还可以复制并粘贴日志条目，以让代理进行验证。

在重新上架事件处理后，请求订阅列表应少返回一个条目，因为已通知的订阅将被删除。

### 创建服务合同

现在，服务实施已经完成，请要求代理创建店面工作的服务合同：

```shell-session
Create an API service contract for the Out of Stock notification service and its endpoints. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront UI integration without needing to ask additional questions about the API. Name this file OUT_OF_STOCK_NOTIFICATION_CONTRACT.md
```

将此文件复制到您的店面项目中，以便店面代理可以引用它。

## 连接到店面

此部分将指导您使用[!DNL Edge Delivery Services]和AI辅助开发工具实施库存通知扩展的店面部分。 将订阅表单添加到产品详细信息页面(PDP)，该页面仅在所选产品或变体缺货时显示。

>[!NOTE]
>
>提供的提示是起点。 虽然您可以不修改这些模板就加以使用，但可以考虑与代理进行自然对话。
>
>在使用人工智能辅助开发工具时，代理生成的代码和响应始终存在自然变化。
>
>如果您遇到任何代码问题，请要求代理帮助您对其进行调试。

### 店面先决条件

在开始店面集成之前，请验证您是否具备以下条件：

- 店面项目已连接到您的[!DNL Commerce]实例
- 使用CLI安装的Commerce storefront AI工具[](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- `OUT_OF_STOCK_NOTIFICATION_CONTRACT.md`文件已复制到您的店面项目中

### 步骤1：验证环境

打开`config.json`文件并验证`commerce-core-endpoint`和`commerce-endpoint`的值是否指向您的[!DNL Adobe Commerce as a Cloud Service] GraphQL终结点。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 第2步：提供初始提示

当服务合同已存在于您的项目中，提示代理在产品详细信息页面中创建UI。 使用&#x200B;**计划**&#x200B;模式（如果代理中可用），以防止代理在没有计划的情况下继续。

```shell-session
Analyze @OUT_OF_STOCK_NOTIFICATION_CONTRACT.md. Add a form for subscribing to a notification for when a product is back in stock. Place this form on the product details page, underneath the add to cart and wishlist button. The form only displays when a product is out of stock. 

Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>专门请求使用项目经理技能会触发分阶段工作流，帮助您在该过程的早期指导实施。 此过程可确保尽早识别关键假设和缺失的需求，并使代理有机会向您提供您可能在最初提示中从未想过提供的详细信息和需求。

### 步骤3：回答规划问题

代理返回时会显示一系列需要回答的问题，然后才能开始形成解决方案。 以下示例显示了典型的问题和答案。 您的代理可能会问不同的问题，但主题通常相同。

**代理问题示例：**

1. **API基本URL** — 店面应如何获取通知缺货API基本URL？ 选项可能包括配置块（例如，具有`out-of-stock-api-base-url`的表）、全局占位符或环境变量或其他方法。
1. **复制** — 该实施应该使用占位符来显示成功消息和错误消息（例如，本地化），还是使用静态英语来显示此实施？
1. **成功订阅后** — 表单是否应隐藏并仅显示“您已订阅”(A)，保持表单可见但已禁用，并在其上方显示成功消息(B)，还是其他行为(C)？
1. **可配置产品** — 窗体可见性是否应该基于所选变体的`inStock`值，以便该窗体显示所选变体何时缺货？

**示例答案：**

```shell-session
1. Global placeholder with baseurl value of `https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api`
2. Use placeholders with static English fallback
3. B
4. Use selected variant's inStock value
```

>[!NOTE]
>
>将`<your-runtime-url>`替换为App Builder部署中的实际[!DNL Adobe I/O Runtime] URL。
>
>您的代理可能会问不同的问题。 请将这些答案用作指导：
>
>- 为API基本URL使用全局占位符，以便可以在不修改代码的情况下对其进行更改。
>- 对于将静态英语作为回退的面向用户的副本，请使用占位符。
>- 成功订阅后，保持表单可见但已禁用，并在其上方显示成功消息。
>- 对于可配置产品，请使用所选变体的`inStock`值来控制表单可见性。

### 第4步：审查要求和体系结构

代理程序将更新要求文档供您查看。 验证：

- 仅当产品或选定的变型无现货时，该表单才会出现。
- 该表单位于PDP上的添加到购物车和愿望清单按钮的下方。
- API集成使用来自全局占位符的基本URL。
- 成功和错误状态根据合同处理(201、409、400、503/500)。

>[!NOTE]
>
>AI代理是不确定的，其行为因模型和IDE而异。 您可能会收到一组不同的问题，这些问题会产生一组不同的要求和体系结构。 如果是这样的话，在继续之前，请尝试将代理引导到某个方向，以便该实施与本教程中介绍的内容非常匹配。

在&#x200B;**第2阶段（体系结构规划）**&#x200B;期间，代理在建议体系结构之前会研究文档和您的代码库。 希望代理能够：

- 在[!DNL Commerce]文档中搜索PDP放置容器、插槽和事件负载。
- 扫描您的`blocks`目录和`scripts/initializers/`文件夹以查找现有的PDP相关代码。
- 浏览可用容器和槽上下文形状的TypeScript定义。

然后，代理会显示架构选项。 复查计划并指示座席继续。

### 步骤5：选择实施计划

该代理为您提供了创建详细实施计划或完成直接实施的选项。

- 如果希望可复查计划能够以更多控制分阶段执行，请选择第一个选项。
- 如果您希望代理以最小的干预完成整个实施，请选择第二个选项。

在&#x200B;**阶段4（实现）**&#x200B;期间，代理会根据所选架构生成代码。 根据具体方法，工程师会使用多种专业技能：

- **内容建模：**&#x200B;如果需要新块，代理将设计一个作者友好的内容结构。
- **块开发：**&#x200B;代理按照[!DNL Edge Delivery Services]约定创建块文件，包括JavaScript修饰函数、作用域CSS样式、用于辅助功能的ARIA标签以及加载和错误状态处理。
- **插入式自定义：**&#x200B;如果体系结构使用插槽自定义，则代理将导入正确的容器，使用产品标题附近的验证插槽，并订阅当前SKU的产品数据事件。

观察生成的代码并提问或根据需要重定向代理。

### 步骤6：启动服务器并测试

代理完成实施后，启动开发服务器并测试表单。

1. 启动本地开发服务器：

   ```bash
   npm run start
   ```

1. 在浏览器中，导航到缺货的产品页面。 例如：

   ```shell-session
   http://localhost:3000/products/<out-of-stock-product-slug>/<sku>
   ```

1. 验证订阅表单是否显示在添加到购物车和愿望清单按钮的下方。

您可以手动测试或要求代理使用其浏览器功能为您进行测试：

```shell-session
Run complete browser testing. Use the following out of stock product 'http://localhost:3000/products/<out-of-stock-product-slug>/<sku>'
```

![产品详细信息页面显示“添加到购物车”按钮下方的重新上架通知表单](../assets/in-stock-notification-form.png){width="600" zoomable="yes"}

### 步骤7：清理

跳过或完成测试后，代理会提示您进入最终的&#x200B;**清理**&#x200B;阶段。 确认后，代理将存档实施期间创建的所有文档工件。

## 故障排除

如果在教程中遇到问题，请使用以下提示：

- **API错误：**&#x200B;使用CLI直接向API发送请求以验证行为。 例如，使用`curl`单独测试每个端点。
- **代理错误：**&#x200B;将错误消息复制并粘贴到代理聊天会话以帮助您调试问题。 代理可以诊断常见问题，例如缺少环境变量或操作配置错误。
- **事件管道：**&#x200B;如果重新上架事件未触发，请验证您已完成入门和事件订阅步骤。 检查`workspace.json`是否位于正确的位置，以及是否已启用Commerce Events模块。
- **Stock状态有效负载：** Commerce可能会将`is_in_stock`作为字符串(`"1"`)而不是布尔值(`true`)发送。 如果未触发股票回购处理程序，请要求代理检查客户代码是否为严格类型比较并更新以处理这两种格式。

## 教程回顾

以下是本教程涵盖的主题摘要：

- **扩展开发：**&#x200B;描述AI代理的新功能，并使用[!DNL App Builder]生成具有CRUD操作的有效REST API。
- **事件驱动架构：**&#x200B;配置Commerce事件和计划操作以检测产品何时重新上架。
- **本地测试和部署：**&#x200B;使用`curl`测试API并使用[!DNL Adobe I/O CLI]进行部署。
- **服务合同：**&#x200B;正在创建桥接后端扩展和店面实施的API合同。
- **分阶段店面集成：**&#x200B;使用人工智能辅助技能处理需求、架构和实施。
- **插入式集成：**&#x200B;使用[!DNL Adobe Commerce]插入式容器和插槽将订阅表单添加到PDP。

## 后续步骤

使用以下建议来扩展您的库存通知服务：

- **发送实际通知：**&#x200B;使用电子邮件服务（如[!DNL Adobe Campaign]或第三方提供程序）替换基于日志的通知。
- **添加订阅管理页面：**&#x200B;创建一个店面页面，购物者可以在其中查看和取消其有效订阅。
- **支持多租户部署：**&#x200B;扩展状态管理以支持单个Commerce应用程序中的多个App Builder租户。
- **添加速率限制：**&#x200B;对订阅API实施速率限制以防止滥用。
