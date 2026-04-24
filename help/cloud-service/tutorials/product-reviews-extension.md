---
title: 产品审核扩展教程
description: 了解如何使用App Builder、Edge Delivery Services和AI辅助开发工具为Adobe Commerce as a Cloud Service构建产品审查和问答扩展。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '2533'
ht-degree: 0%

---

# 产品审核扩展教程

本教程将指导您完成构建一个扩展，该扩展允许客户使用[!DNL Adobe App Builder]和AI辅助开发工具为具有[!DNL Adobe Commerce as a Cloud Service]后端的店面提交产品审查和问答(Q&amp;A)内容。 该扩展为购物者提供了REST API端点，用于查看和提交产品审查和问答(Q&amp;A)内容，并将其显示在产品详细信息页面(PDP)上。

您可以构建两个部分：

- **App Builder扩展** — 一个REST API，它具有GET和POST操作，用于在`aio-lib-state`中创建和查看产品审核和问答内容，并具有验证、分页和持久性。
- **店面集成** — PDP上的产品评论块，显示评论和问答，其中包含供购物者提交评论、问题和答案的表单。

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

如果前面任何命令未返回预期结果，请参阅[先决条件](./tutorial-prerequisites.md)获取指导。

此外，请验证以下各项：

- 您有一个包含产品数据的[!DNL Adobe Commerce as a Cloud Service]实例。 查看[Commerce Cloud服务实例](https://experienceleague.adobe.com/zh-hans/docs/commerce/cloud-service/overview){target="_blank"}。
- 您有一个店面项目连接到您的[!DNL Commerce]实例。 如果没有店面，请按照[创建店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=zh-Hans){target="_blank"}中的步骤操作。
- 已安装`aem` CLI：

  ```bash
  npm install -g @adobe/aem-cli
  ```

## 扩展开发

此部分将指导您开发扩展，以使用人工智能辅助开发工具提交和查看具有[!DNL Adobe Commerce as a Cloud Service]后端的店面的产品审核和问答内容。 扩展提供了一个REST API，用于提交和查看产品审查和问答内容并在PDP上显示它。

1. 导航到编码代理中的MCP设置。 例如，在光标中，转到&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**。 验证是否已启用`commerce-extensibility`工具集且未出现错误。 如果看到错误，请关闭和打开工具集。

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
I want to build an Adobe Commerce as a Cloud Service extension that allows shoppers to submit and view product review and question and answer (Q&A) content that displays on product detail pages (PDP).

## Product Reviews
The application has REST API endpoints that can be called by a storefront to retrieve and submit product reviews for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch reviews for
- limit (integer, optional): The maximum number of reviews to return (default: 10)
- offset (integer, optional): The number of reviews to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a review for
- rating (integer, required): The rating for the product (1-5)
- review (string, optional): The text of the review
- user (string, optional): The name of the user submitting the review

The POST endpoint validates the input and returns appropriate error responses for invalid data. The reviews are stored and associated with the corresponding product SKU.

## Questions and Answers
The application has REST API endpoints that can be called by a storefront to retrieve and submit questions and answers for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch questions and answers for
- limit (integer, optional): The maximum number of questions and answers to return (default: 10)
- offset (integer, optional): The number of questions and answers to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a question or answer for
- type (string, required): The type of submission ("question" or "answer")
- questionId (string, required if type is "answer"): The ID of the question being answered
- content (string, required): The text of the question or answer
- user (string, optional): The name of the user submitting the question or answer

The POST endpoint validates the input and returns appropriate error responses for invalid data. The questions and answers are stored and associated with the corresponding product SKU. Answers are also associated with the corresponding question.

Do not require Adobe IMS authentication for these endpoints. They will be called directly from the storefront.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>在继续操作之前告知代理停止操作并询问相关问题，这有助于尽早指导实施。 这可确保尽早识别关键假设和缺失要求，以及启动本教程中的引导式工作流所需的条件。

### 第2步：回答座席的问题

代理返回时会显示一系列需要回答的问题，然后才能开始形成解决方案。 以下示例显示了典型的问题和答案。 您的代理可能会问不同的问题，但主题通常相同。

**代理问题示例：**

1. **REST API — 主机和使用者** - CRUD REST API是否应包含在商店前端调用的此App Builder应用程序（Adobe I/O Runtime上的Web操作）中？ 谁将调用它（EDS Storefront、自定义/Headless店面，或同时调用两者）？ 您需要CORS、公共（未经身份验证）访问，还是呼叫方将使用API密钥或OAuth？
1. **数据模型** — 一个“审阅”或“问题”应该代表什么？ 客户标识符（仅限电子邮件还是客户ID）？ 产品标识符（仅限SKU或SKU +商店视图）？ 同一客户是否可以针对同一个SKU提交多个审核？
1. **持久性** — `aio-lib-state`是保留审阅和问答的正确位置，还是您有外部存储？ 设计应采用多租户还是单租户？
1. **分页语义** — 对于Q&amp;A GET，`limit`是否仅适用于问题（包含嵌套答案），还是适用于问题加答案的总数？

**示例答案：**

```shell-session
1. The REST API should be part of this App Builder app. It will be called by the EDS Storefront. No authentication — public access for both GET and POST.
2. For reviews: sku, rating (1-5), optional review text, optional user name. For Q&A: sku, type (question or answer), content, optional user. Answers linked to questions via questionId. Allow multiple reviews per SKU from the same user.
3. Use aio-lib-state. Single tenant for now.
4. Pagination by question — limit and offset apply to questions; each question includes its nested answers.
```

>[!NOTE]
>
>您的代理可能会问不同的问题。 使用这些答案作为指导，引导代理实现相同的功能结果：具有审阅和问答的公共REST API、`aio-lib-state`持久性并且无身份验证。

### 第3步：审查要求和体系结构

代理程序会生成需求和体系结构文档供您审查。 验证要求与您提供的答案是否匹配，以及体系结构是否涵盖：

- 四个Web操作：`reviews-get`、`reviews-post`、`qa-get`、`qa-post`
- 使用键符合允许模式（`[a-zA-Z0-9-_.]` — 无冒号）的`aio-lib-state`的持久性
- 以JSON字符串形式存储的状态值（不是原始对象或数组）
- 自包含包 — `product-reviews`包内的共享代码（util、常量），而不是通过转义包的`../../`路径进行

>[!NOTE]
>
>AI代理是不确定的，其行为因模型和IDE而异。 您可能会收到一组不同的问题，这些问题会产生一组不同的要求和体系结构。 如果是这样的话，在继续之前，请尝试将代理引导至正确的方向，以使实施根据本教程中的说明进行密切匹配。

### 步骤4：选择实施计划

该代理为您提供了创建详细实施计划或完成直接实施的选项。

- 如果希望可复查计划能够以更多控制分阶段执行，请选择第一个选项。
- 如果您希望代理以最小的干预完成整个实施，请选择第二个选项。

### 第5步：部署扩展

代理完成实施后，部署扩展：

```bash
aio app deploy
```

如果代理已将`require-adobe-auth: true`添加到操作，请要求它删除身份验证，以便直接从店面调用端点：

```shell-session
Remove the requirement to provide a valid Adobe IMS access token from all product-reviews actions.
```

然后重新部署：

```bash
aio app deploy
```

### 步骤6：创建模拟数据并预填充以进行测试

创建一个模拟数据文件，并使用curl预填充API，以便您具有用于在CLI和店面中进行测试的示例审阅和问答内容。

1. 创建包含示例数据的文件`docs/mock-product-reviews-data.json`（或类似文件）。 例如：

   ```json
   {
     "reviews": [
       { "sku": "ADB153", "rating": 5, "review": "Great product, highly recommend!", "user": "shopper@example.com" },
       { "sku": "ADB153", "rating": 4, "review": "Good value for money.", "user": "buyer@example.com" }
     ],
     "questions": [
       { "sku": "ADB153", "type": "question", "content": "Does this come in other colors?", "user": "curious@example.com" }
     ]
   }
   ```

1. 使用curl将数据发布到您部署的API。

   将`<your-runtime-url>`替换为您的实际App Builder运行时URL（例如，`https://1172492-prodreviewqa135-stage.adobeioruntime.net`）：

   ```bash
   API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
   
   # Submit reviews
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":5,"review":"Great product, highly recommend!","user":"shopper@example.com"}'
   
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":4,"review":"Good value for money.","user":"buyer@example.com"}'
   
   # Submit a question (save the returned id for the answer)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"question","content":"Does this come in other colors?","user":"curious@example.com"}'
   
   # Submit an answer (replace <QUESTION-UUID> with the id from the question response)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it comes in blue and red.","user":"seller@example.com"}'
   ```

1. 通过GET请求验证数据：

   ```bash
   curl -s "$API_URL/reviews-get?sku=ADB153"
   curl -s "$API_URL/qa-get?sku=ADB153"
   ```

>[!TIP]
>
>将SKU `ADB153`用于包含审阅和问答内容的产品，将`ADB152`用于没有审阅的产品。 此数据配置允许测试店面中的填充和空状态。

### 步骤7：测试扩展

要求代理提供测试步骤，或使用上一步中的curl示例。 以下示例显示了典型的测试命令。

**提交审核：**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
curl -s -X POST "$API_URL/reviews-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","rating":5,"review":"Excellent!","user":"test@example.com"}'
```

**列出审核：**

```bash
curl -s "$API_URL/reviews-get?sku=ADB153"
```

**提交问题：**

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"question","content":"Is this dishwasher safe?","user":"test@example.com"}'
```

**提交答案** （使用问题响应中的`id`作为`questionId`）：

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it is.","user":"support@example.com"}'
```

### 创建服务合同

现在，服务实施已经完成，请要求代理创建店面工作的服务合同：

```shell-session
Create a service contract for the Product Review and Q&A application that defines the API endpoints, request and response formats, and any necessary data models. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront integration without needing to ask additional questions about the API. Name this file PRODUCT_REVIEW_QA_CONTRACT.md
```

将此文件复制到您的店面项目中，以便店面代理可以引用它。

## 连接到店面

此部分将指导您使用[!DNL Edge Delivery Services]和AI辅助开发工具实施产品审查和问答扩展的店面部分。 您将一个产品审核块添加到PDP中，该PDP同时显示审核和问答内容，并允许购物者提交新内容。

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
- 使用CLI安装的Commerce storefront AI工具[&#128279;](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- `PRODUCT_REVIEW_QA_CONTRACT.md`文件已复制到您的店面项目中

### 步骤1：验证环境

打开`config.json`文件并验证`commerce-core-endpoint`和`commerce-endpoint`的值是否指向您的[!DNL Adobe Commerce as a Cloud Service] GraphQL终结点。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 第2步：提供初始提示

当服务合同已存在于您的项目中时，提示工程师实施产品审查块。 使用&#x200B;**计划**&#x200B;模式（如果代理中可用），以防止代理在没有计划的情况下继续。

```shell-session
Analyze @PRODUCT_REVIEW_QA_CONTRACT.md and build a product review block using the API specified in the contract. The block displays both reviews and Q&A content on the product detail page, with forms for shoppers to submit reviews, questions, and answers. Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>专门请求使用项目经理技能会触发分阶段工作流，帮助您指导实施。 这将确保在此过程的早期发现关键假设和缺失要求。

### 步骤3：回答澄清问题

代理返回时会显示一系列需要回答的问题，然后才能开始形成解决方案。 以下示例显示了典型的问题和答案。 您的代理可能会问不同的问题，但主题通常相同。

**代理问题示例：**

1. **API基本URL** — 店面应如何获取产品审核API基本URL？ 选项可能包括配置块（例如，具有`apiBaseUrl`的表）、全局占位符或其他方法。
1. **SKU源** — 块应该从PDP上下文（当前产品）还是块配置中读取SKU？
1. **表单行为** — 成功提交后，表单应该隐藏、显示成功消息还是保持可见状态但处于禁用状态？

**示例答案：**

```shell-session
1. Block table config with apiBaseUrl (required). Each block instance can point to its own deployment.
2. From block table if set; otherwise use getProductSku() so it works on PDP without authoring a SKU.
3. Show a success message above the form; keep the form visible but disabled.
```

>[!NOTE]
>
>将块配置中的占位符替换为实际的App Builder运行时URL（例如，`https://1172492-prodreviewqa135-stage.adobeioruntime.net`）。
>
>您的代理可能会问不同的问题。 请将这些答案用作指导：
>
>- API基本URL应来自块表，以便可以在不修改代码的情况下对其进行更改。
>- 块表中的SKU（如果已设置）；否则来自PDP上的当前产品。
>- 成功提交后，显示成功消息并禁用表单。

### 第4步：审查要求和体系结构

代理程序将更新要求文档供您查看。 验证：

- 块可呈现评论（包括评级、用户、日期、文本）和问答（包含嵌套答案的问题）。
- Forms可用于提交评论、问题和答案。
- 评论和问答内容都支持分页。
- API集成使用块表中的基本URL。
- 成功和错误状态根据合同进行处理。

>[!NOTE]
>
>AI代理是不确定的，其行为因模型和IDE而异。 您可能会收到一组不同的问题，这些问题会产生一组不同的要求和体系结构。 如果是这样的话，在继续之前，请尝试将代理引导至正确的方向，以使实施根据本教程中的说明进行密切匹配。

### 步骤5：选择实施计划

该代理为您提供了创建详细实施计划或完成直接实施的选项。

- 如果希望可复查计划能够以更多控制分阶段执行，请选择第一个选项。
- 如果您希望代理以最小的干预完成整个实施，请选择第二个选项。

在实施过程中，代理会创建和修改块文件。 观察生成的代码并提问或根据需要重定向代理。 如果块未呈现，请要求代理分析节修饰和块发现模式 — 块元素必须是节的直接子级，以便框架可以找到它。

### 步骤6：在文档创作中将块添加到产品页面

将产品审核块添加到产品页面模板，使其显示在所有PDP上。 使用Document Authoring服务(da.live)添加和配置块。

1. 打开您的文档创作服务，例如[da.live](https://da.live/)

1. 单击您的项目空间，打开&#x200B;**products**&#x200B;文件夹，然后选择&#x200B;**default** (`products/default`)。

1. 添加新块分区。

   在块表中，添加块名称为&#x200B;**product-review**&#x200B;的行（或代理创建的块名称）。

1. 使用所需的设置配置块：
   - **apiBaseUrl** — 您的App Builder运行时URL（例如，`https://<namespace>-<app-name>-stage.adobeioruntime.net`）。
   - **sku** — 留空将使用PDP上当前产品的SKU，或者输入特定的SKU以仅显示对该产品的评价。

1. 单击&#x200B;**[!UICONTROL Publish]**&#x200B;发布更改。

### 步骤7：启动服务器并测试

在文档创作中将块添加到产品页面后，启动开发服务器并测试块。

1. 启动本地开发服务器：

   ```bash
   npm run start
   ```

1. 在浏览器中，导航到已预填充审核和问答内容的产品页面。 例如：

   ```shell-session
   http://localhost:3000/products/<product-slug>/ADB153
   ```

1. 验证产品审核块是否显示审核和问答内容，以及提交表单是否有效。

您可以手动测试或要求代理使用其浏览器功能为您进行测试：

```shell-session
Run complete browser testing. Use the following product page 'http://localhost:3000/products/<product-slug>/ADB153'
```

### 步骤8：清理

跳过或完成测试后，代理会提示您进入最终的&#x200B;**清理**&#x200B;阶段。 确认后，代理将存档实施期间创建的所有文档工件。

## 故障排除

如果在教程中遇到问题，请使用以下提示。

### 后端(App Builder)

| 症状 | 原因 | 修复 |
|---------|-------|-----|
| GET或POST返回500“无法找到模块” | 产品审阅操作使用`require("../../utils")`或`require("../../constants")`，它们将转义包捆绑。 部署包时，这些文件不包括在内。 | 使产品审阅包自包含。 添加`actions/product-reviews/lib/constants.js`和`actions/product-reviews/lib/utils.js`，并从`../lib/...`而不是`../../`更新所需的全部四个操作。 |
| GET返回500并显示“键必须匹配模式” | 状态键使用冒号（例如，`reviews:ADB153`）。 `aio-lib-state`仅允许`[a-zA-Z0-9-_.]`。 | 将前缀从`reviews:`和`qa:`更改为`reviews.`和`qa.`。 添加可清理SKU的`stateKey(prefix, sku)`帮助程序（将无效字符替换为`_`）。 |
| POST返回500并显示“值必须为字符串” | `aio-lib-state`仅接受字符串值。 代码将数组或对象传递给`state.put()`。 | 写入时与`JSON.stringify()`序列化，读取时与`JSON.parse()`序列化。 更新全部四个操作。 |

{style="table-layout:auto"}

### 店面(Edge Delivery Services)

| 症状 | 原因 | 修复 |
|---------|-------|-----|
| 块未在测试页面上呈现 | 块元素嵌套在额外的`div`中，因此`decorateSections`之后的块选择器(`div.section > div > div`)不匹配。 | 将块设为部分的直接子级。 结构： `section > div.product-review` （或等效的块类）。 避免`section > div > div.product-review`。 |
| CSS令牌无效 | 该块使用`styles/styles.css`中不存在的设计令牌（例如，`--color-error-100`、`--type-detail-font-size`）。 | 要求代理针对项目的`styles/styles.css`验证令牌，并用现有令牌替换无效令牌（例如，`--color-alert-*`、`--type-details-caption-*`）。 |

{style="table-layout:auto"}

## 教程回顾

以下是本教程涵盖的主题摘要：

- **扩展开发：**&#x200B;描述在具有Adobe Commerce as a Cloud Service后端的店面上为AI代理创建和查看产品审核和问答内容的功能，以及如何使用[!DNL App Builder]生成具有四个端点的工作REST API来实施此功能。
- **持久性：**&#x200B;正在使用具有正确键格式和JSON序列化值的`aio-lib-state`。
- **模拟数据和预填充：**&#x200B;创建模拟数据文件并使用curl预填充API以进行CLI和店面测试。
- **服务合同：**&#x200B;正在创建桥接后端扩展和店面实施的API合同。
- **分阶段店面集成：**&#x200B;使用人工智能辅助技能处理需求、架构和实施。
- **PDP块：**&#x200B;将产品审核块添加到显示审核和问答以及提交表单和分页的PDP。

## 后续步骤

请使用以下建议来扩展您的产品审查服务：

- **添加审核：**&#x200B;在发布审核和问答内容之前实施审核工作流。
- **添加身份验证：**&#x200B;要求购物者登录以提交评论或问答内容，并将提交内容与客户帐户关联。
- **添加订阅管理页面：**&#x200B;创建购物者可以查看和编辑其评论的店面页面。
- **支持多租户部署：**&#x200B;扩展状态管理以支持单个Commerce应用程序中的多个App Builder租户。
- **添加速率限制：**&#x200B;在API上实施速率限制以防止滥用。
