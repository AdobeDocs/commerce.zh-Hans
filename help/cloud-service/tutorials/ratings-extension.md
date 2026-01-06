---
title: 评级扩展教程
description: 了解如何使用App Builder和AI辅助开发工具为Adobe Commerce as a Cloud Service构建产品评级扩展。
feature: App Builder, Cloud
role: Developer
level: Intermediate
hide: true
hidefromtoc: true
source-git-commit: 4ca909c2f8f95fbc404ce6a745d769958b2c01f4
workflow-type: tm+mt
source-wordcount: '622'
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

如果前面的任何命令未返回预期结果，请参阅[先决条件](tutorial-prerequisites.md)获取指导。

## 扩展开发

此部分将指导您使用AI辅助开发工具为Adobe Commerce as a Cloud Service开发评级扩展。

1. 导航到&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**，并验证`commerce-extensibility`工具集是否已启用且未出现错误。 如果看到错误，请关闭和打开工具集。

   ![Cursor IDE设置显示MCP商务扩展工具集已启用](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >使用人工智能辅助开发工具时，预期代码和代理生成的响应会发生自然变化。
   >如果您遇到任何代码问题，始终可以请求代理帮助您对其进行调试。

1. 如果有任何文档添加到光标上下文中，请禁用它：

   - 导航到&#x200B;[!UICONTROL **Cursor**] > [!UICONTROL **设置**] > [!UICONTROL **Cursor设置**] > [!UICONTROL **索引和文档**]，并删除列出的任何文档。

   ![文档列表为空的游标索引和文档设置](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. 为产品评级扩展生成代码：
   - 在“光标聊天”窗口中，选择&#x200B;[!UICONTROL **代理**]&#x200B;模式。
   - 输入以下提示：

   ```shell-session
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >如果代理请求搜索文档，请允许搜索。

1. 准确地回答座席的问题以帮助其生成最佳代码。

   ![在代理模式下光标聊天窗口，已输入扩展提示](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![AI代理询问有关扩展要求的问题](../assets/agent-questions.png){width="600" zoomable="yes"}

1. 使用以下示例文本回答座席的问题，以设置随机评级数据：

   ```shell-session
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension is called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   代理将创建一个`requirements.md`文件，用作实现的真实来源。

   AI代理创建的![Requirements.md文件及实现详细信息](../assets/requirements-file.png){width="600" zoomable="yes"}

1. 查看`requirements.md`文件并验证计划。

   如果一切看起来都正确，请指示代理移至&#x200B;**阶段2 — 架构计划**。
1. 查看体系结构计划。
1. 指示代理继续生成代码。

   代理程序会生成必要的代码并提供详细的摘要，其中包含后续步骤。

   ![分级API的AI代理2期体系结构计划](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![生成的代码文件和结构的摘要](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![AI代理提供测试和部署的后续步骤](../assets/next-steps.png){width="600" zoomable="yes"}

### 本地测试

1. 请求代理帮助您在本地测试代码。

   ```shell-session
   Test the ratings API locally on a dev server using cURL.
   ```

1. 按照代理的说明操作，并确认API在本地工作。

   用于本地API测试的![AI代理说明](../assets/local-testing.png){width="600" zoomable="yes"}

   ![终端显示成功的本地API测试结果(cURL](../assets/local-testing-1.png){width="600" zoomable="yes"})

### 部署扩展

1. 验证生成的代码后，使用以下提示部署扩展：

   ```shell-session
   Deploy the ratings API.
   ```

   代理在部署之前执行部署前就绪性评估。

   ![AI代理部署前准备情况评估核对清单](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. 如果对评估结果有信心，请指示代理继续部署。

   代理使用MCP工具包自动验证、构建和部署。

   ![MCP工具包验证生成和部署过程](../assets/deployment-process.png){width="600" zoomable="yes"}

### 部署后

您可以在将API集成到店面之前对其进行测试。 代理应提供新操作的位置和测试策略。

具有已部署的操作URL和测试命令的![AI代理测试策略](../assets/testing-strategy.png){width="600" zoomable="yes"}

您还可以在终端中使用cURL手动测试API：

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![终端显示已部署的分级API的cURL测试成功](../assets/curl-test.png){width="600" zoomable="yes"}

### 与Edge Delivery Services集成

要将评级API与由[!DNL Adobe Commerce]提供支持的[!DNL Edge Delivery Services]店面集成，请要求代理创建具有评级API要求的服务合同：

```shell-session
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![AI代理为店面集成创建服务合同文件](../assets/create-contract.png){width="600" zoomable="yes"}

![带有端点和响应详细信息的Rating API合同Markdown文件](../assets/contract.png){width="600" zoomable="yes"}
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

   ```shell-session
   http://localhost:3000/apparel
   ```

1. Observe the boilerplate storefront UI layout and note the lack of visual product ratings.

1. Use the following prompt with your agent:

   ```shell-session
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

```shell-session
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

   ```shell-session
   adjust the modal position to be...
   ```

![Rating Distribution Modal](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
 -->
