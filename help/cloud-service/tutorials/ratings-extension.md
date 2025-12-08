---
title: 评级扩展教程
description: 了解如何使用App Builder和AI辅助开发工具为Adobe Commerce as a Cloud Service构建产品评级扩展。
role: Developer
hide: true
hidefromtoc: true
source-git-commit: e153e974be1dc5ec8ff2eff8d699ce87ef6708dc
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 评级扩展教程(Beta)

>[!NOTE]
>
>本教程中使用的AI工具当前位于Beta中，可能包含错误或其他问题。

本教程将指导您使用[!DNL Adobe Commerce as a Cloud Service]和AI辅助开发工具为[!DNL Adobe App Builder]构建产品评级扩展。

在开始之前，请完成[先决条件](./tutorial-prerequisites.md)。

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

如果前面任何命令未返回预期结果，请参阅[先决条件](tutorial-prerequisites.md)获取指导。

## 扩展开发

此部分将指导您使用人工智能辅助开发工具来为Adobe Commerce as a Cloud Service开发评级扩展的过程。

1. 导航到&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**，并验证`commerce-extensibility`工具集是否已启用且未出现错误。 如果看到错误，请关闭和打开工具集。

   ![光标设置](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >在使用人工智能辅助开发工具时，代理生成的代码和响应将发生自然变化。
   >如果您遇到任何代码问题，始终可以请求代理帮助您对其进行调试。

1. 如果有任何文档添加到光标上下文中，请禁用它：

   - 导航到&#x200B;[!UICONTROL **Cursor**] > [!UICONTROL **设置**] > [!UICONTROL **Cursor设置**] > [!UICONTROL **索引和文档**]，并删除列出的任何文档。

   ![禁用文档](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. 为产品评级扩展生成代码：
   - 从光标聊天窗中，选择&#x200B;**代理**&#x200B;模式。
   - 输入以下提示：

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >如果代理请求搜索文档，请允许搜索。

1. 准确地回答座席的问题以帮助其生成最佳代码。

   ![在光标中输入提示](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![代理询问澄清问题](../assets/agent-questions.png){width="600" zoomable="yes"}

1. 使用以下示例文本回答座席的问题，以设置随机评级数据：

   ```text
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension will be called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   代理将创建一个`requirements.md`文件，用作实现的真实来源。

   已创建![要求文件](../assets/requirements-file.png){width="600" zoomable="yes"}

1. 查看`requirements.md`文件并验证计划。

   如果一切看起来都正确，请指示代理移至&#x200B;**阶段2 — 架构计划**。
1. 查看体系结构计划。
1. 指示代理继续生成代码。

   代理程序会生成必要的代码并提供详细的摘要，其中包含后续步骤。

   ![架构计划](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![代码生成摘要](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![后续步骤](../assets/next-steps.png){width="600" zoomable="yes"}

### 本地测试

1. 请求代理帮助您在本地测试代码。

   ```text
   Test the ratings API locally on a dev server using cURL.
   ```

1. 按照代理的说明操作，并确认API在本地工作。

   ![本地测试](../assets/local-testing.png){width="600" zoomable="yes"}

   ![本地测试结果](../assets/local-testing-1.png){width="600" zoomable="yes"}

### 部署扩展

1. 验证生成的代码后，使用以下提示部署扩展：

   ```text
   Deploy the ratings API.
   ```

   代理在部署之前执行部署前就绪性评估。

   ![部署前评估](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. 如果对评估结果有信心，请指示代理继续部署。

   代理使用MCP工具包自动验证、构建和部署。

   ![部署](../assets/deployment-process.png){width="600" zoomable="yes"}

### 部署后

您可以在将API集成到店面之前对其进行测试。 代理应提供新操作的位置和测试策略。

![测试策略](../assets/testing-strategy.png){width="600" zoomable="yes"}

您还可以在终端中使用cURL手动测试API：

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![cURL测试](../assets/curl-test.png){width="600" zoomable="yes"}

### 与Edge Delivery Services集成

要将评级API与由[!DNL Adobe Commerce]提供支持的[!DNL Edge Delivery Services]店面集成，请要求代理创建具有评级API要求的服务合同：

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![服务合同](../assets/create-contract.png){width="600" zoomable="yes"}

![服务合同详细信息](../assets/contract.png){width="600" zoomable="yes"}
<!-- 
Return to the terminal and run the following command in the `extension` folder to copy the file to the `storefront` folder:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
``` -->

### 后续步骤

现在您有了评级API合同，就可以开始构建评级扩展的店面（前端）部分了。

<!-- 
## Connect to the storefront

This section teaches you how to implement real storefront features and communicate effectively with AI agents when working with [!DNL Adobe Commerce] dropins and [!DNL Edge Delivery Services].

>[!NOTE]
>
>The prompts provided are starting points. Although you can use them without modification, consider having a natural conversation with the agent.
>
>When working with AI-assisted development tools, there are always natural variations in the code and responses generated by the agent.
>
>If you encounter any issues with your code, ask the agent to help you debug it.

### Ratings stars and review count implementation

1. Navigate to the `storefront` folder:

   ```bash
   cd storefront
   ```

1. Open the storefront folder in a new Cursor window.

    Alternatively, if you have the [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) installed, open the window by using the following command in your terminal:

   ```bash
   cursor .
   ```

1. Start the local development server:

   ```bash
   npm run start
   ```

1. In a browser, navigate to the Apparel page:

   ```text
   http://localhost:3000/apparel
   ```

1. Observe the boilerplate storefront UI layout and note the lack of visual product ratings.

1. Use the following prompt with your agent:

   ```text
   Implement product ratings in the storefront.

   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.

   Use the dropin slot system where available.

   Use @RATINGS_API_CONTRACT.md to understand how to use the ratings API.
   ```

1. Observe the changes in the codebase, and watch the Apparel page for updates.

   You should see the following changes in your development environment and browser:

   * A product rating "component" is automatically created.
   * The component is integrated into product-details, product-list-page, and product-recommendations blocks using [dropin slots](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots).
   * Stars display with proper fill proportions based on mock rating values.

![Product Ratings Implementation](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Tutorial recap

Here is a summary of the topics covered in this tutorial:

* **Feature implementation**: How to describe new functionality to an AI agent.
* **Iterative changes**: Making quick modifications to existing code.
* **Complex UI components**: Building interactive features with visual references.
* **Dropin integration**: Working with [!DNL Adobe Commerce] dropin containers and slots.
* **Component reusability**: Creating shared components used across multiple blocks.

## Next steps

For further experimentation with this tutorial, use the following suggestions to further customize your ratings extension, or create your own modifications:

### Change the star colors

Use the following prompt to your agent:

```text
Change the star fill color to red.
```

**Expected outcome:**

The stars are changed to red.

![Red Star Colors](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Add rating distribution modal

The following steps show how the agent handles complex UI features with visual references.

1. **Before starting:** Save the following mock image and paste it into the chat with your storefront agent.

   ![Rating Distribution Mockup](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Follow these steps to create the ratings distribution modal using the reference image as a guide:

   * Update the API to return additional data representing the ratings distribution.
   * Update the API Contract.
   * Update the contact in the storefront codebase.
   * Ask the storefront agent to use the reference image and updated API Contract to add the ratings distribution to the PDP page.

1. Observe the following changes in the codebase, and watch the Apparel page for updates:

   * How the agent interprets the visual mockup
   * Whether it uses appropriate HTML structure for accessibility
   * How it handles the positioning and interaction states

#### Troubleshooting

* If the modal does not appear, check the browser console for errors.
* If positioning is off, ask the agent to fix it using the following format:

   ```text
   adjust the modal position to be...
   ```

![Rating Distribution Modal](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
 -->
