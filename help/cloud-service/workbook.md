---
title: 评级扩展教程
description: 了解如何使用App Builder和AI辅助开发工具为Adobe Commerce as a Cloud Service构建产品评级扩展。
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 453b21f89d2024a8d6927fa082affdd5abb6e5cd
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Adobe Developers Live - Adobe Commerce实验室工作簿

本实验将指导您使用[!DNL Adobe Commerce as a Cloud Service]和AI辅助开发工具为[!DNL Adobe App Builder]构建产品评级扩展。

## 验证先决条件

验证是否安装了以下必备组件：

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git
git --version

# Check Bash
bash --version
```

## 登录到Adobe Developer Console

1. 导航到[Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}。
1. 如果您已经登录，请单击右上角的配置文件图标，然后单击&#x200B;**注销**&#x200B;按钮。
1. 使用为您的名额提供的实验室电子邮件ID和密码登录。
1. 如果系统提示您添加辅助电子邮件地址或电话号码，请单击&#x200B;**现在不要**。
1. 当提示您选择组织配置文件时，请选择&#x200B;**Adobe Commerce Labs**。

   ![选择组织](./assets/select-org.png){width="600" zoomable="yes"}

1. 如果提示您接受条款和条件，请单击链接阅读条款，然后单击“**接受并继续**”。

   ![accept-terms](./assets/accept-terms.png){width="600" zoomable="yes"}

## 运行安装脚本

如果已安装[先决条件](#verify-prerequisites)，并且您已登录到Adobe Developer Console，请下载并运行安装脚本。 或者，您可以按照[实验室先决条件](workbook-prerequisites.md)步骤手动设置脚本。

1. 克隆包含安装脚本的存储库：

   ```bash
   git clone https://github.com/adobe-commerce/commerce-adl-2025.git
   ```

   >[!NOTE]
   >
   >如果脚本失败，请参阅[先决条件](workbook-prerequisites.md)并在脚本遇到错误时继续。

1. 导航到存储库：

   ```bash
   cd commerce-adl-2025
   ```

1. 运行安装脚本：

   ```bash
   bash adl-setup.sh
   ```

   脚本运行时，系统将提示您输入用户名和密码，该用户名和密码将在实验期间提供。 您的用户名将反映您的位置和座位号。 例如，如果您在加利福尼亚州圣何塞，123号座位，则您的用户名将为`sjc-adl-123@adobeeventlab.com`。

   此外，您应该选择与名额和&#x200B;**阶段**&#x200B;工作区对应的项目。 您的项目名称将反映您的位置和座位号。 例如，如果您在加利福尼亚州圣何塞，123号座位，则项目名称为`SJC ADL 123`。

## 扩展开发

此部分将指导您使用人工智能辅助开发工具来为Adobe Commerce as a Cloud Service开发评级扩展的过程。

### 安装可扩展性人工智能工具

在`extension`文件夹中设置AI辅助开发工具：

```bash
cd extension
```

```bash
aio commerce extensibility tools-setup
```

![安装AI工具](./assets/install-ai-tools.png){width="600" zoomable="yes"}

### 打开光标

>[!NOTE]
>
>在使用人工智能辅助开发工具时，代理生成的代码和响应将发生自然变化。
>如果您遇到任何代码问题，始终可以请求代理帮助您对其进行调试。

打开[!DNL Cursor]应用程序并导航到`extension`文件夹，或者如果您安装了[Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands)，请在终端中输入以下命令：

```bash
cursor .
```

![打开游标](./assets/open-cursor.png){width="600" zoomable="yes"}

此时，所有[!DNL Cursor]规则都安装在`.cursor/rules`文件夹中。 您可以在&#x200B;**的** MCP设置[!DNL Cursor]中找到MCP工具。 验证是否已启用`commerce-extensibility`工具集且未出现错误。 如果看到错误，请关闭和打开工具集。

![光标设置](./assets/cursor-settings.png){width="600" zoomable="yes"}

如果您将任何文档添加到光标上下文中，则需要禁用它。 导航到&#x200B;[!UICONTROL **Cursor**] > [!UICONTROL **设置**] > [!UICONTROL **Cursor设置**] > [!UICONTROL **索引和文档**]，并删除列出的任何文档。

![禁用文档](./assets/disable-documentation.png){width="600" zoomable="yes"}

### 代码生成

此部分演示如何使用人工智能辅助工具为产品评级扩展生成代码。

#### 定义要求

您将实施一个扩展，以作为API提供产品评级。 [!DNL App Builder]扩展提供了给定SKU的评级详细信息。

**初始提示：**

在[!DNL Cursor]中使用以下提示：

1. 在光标中打开聊天窗口。
1. 选择&#x200B;**代理**&#x200B;模式。
1. 输入以下提示：

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   Implement a REST API to handle GET ratings requests.
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

1. 如果代理请求搜索文档，请允许搜索。

![在光标中输入提示](./assets/enter-prompt.png){width="600" zoomable="yes"}

代理人研究要求并提问明确的问题。 准确地回答座席的问题以帮助其生成最佳代码。

![代理询问澄清问题](./assets/agent-questions.png){width="600" zoomable="yes"}

**响应提示：**

使用以下响应来回答座席的问题：

```text
Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
This extension will be called directly from the storefront,
no async invocation, such as events or webhooks, is required.
Let's start with just the GET API for now,
we will implement other CRUD operations at a later time.
We do not need a DB or storage mechanism right now,
just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
The API should only return the average rating for the product and the total number of ratings.
We do not need to add tests right now.
```

代理将创建一个`requirements.md`文件，用作实现的真实来源。

已创建![要求文件](./assets/requirements-file.png){width="600" zoomable="yes"}

#### 验证要求并规划体系结构

1. 查看`requirements.md`文件。
1. 如果一切看起来都正确，请指示代理移至&#x200B;**阶段2 — 架构计划**。
1. 查看体系结构计划。
1. 指示代理继续生成代码。

![架构计划](./assets/architecture-planning.png){width="600" zoomable="yes"}

#### 生成代码

代理程序会生成必要的代码并提供详细的摘要，其中包含后续步骤。

![代码生成摘要](./assets/code-generation-summary.png){width="600" zoomable="yes"}

![后续步骤](./assets/next-steps.png){width="600" zoomable="yes"}

### 本地测试

请求代理帮助您在本地测试代码。

```text
Test the ratings API locally on a dev server using cURL.
```

按照代理的说明操作，并确认API在本地工作。

![本地测试](./assets/local-testing.png){width="600" zoomable="yes"}

![本地测试结果](./assets/local-testing-1.png){width="600" zoomable="yes"}

### 部署扩展

验证生成的代码后，您可以使用以下提示部署扩展：

```text
Deploy the ratings API.
```

#### 部署前评估

代理在部署之前执行部署前就绪性评估。

![部署前评估](./assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

#### 部署

如果对评估结果有信心，请指示代理继续部署。 代理使用MCP工具包自动验证、构建和部署。

![部署](./assets/deployment-process.png){width="600" zoomable="yes"}

### 测试API

您可以在将API集成到店面之前对其进行测试。

代理提供新操作的位置和测试策略。

![测试策略](./assets/testing-strategy.png){width="600" zoomable="yes"}

#### 使用cURL手动测试

在终端中使用cURL手动测试API：

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![cURL测试](./assets/curl-test.png){width="600" zoomable="yes"}

### 与Edge Delivery Services集成

要将评级API与由[!DNL Adobe Commerce]提供支持的[!DNL Edge Delivery Services]店面集成，请要求代理创建具有评级API要求的服务合同：

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![服务合同](./assets/create-contract.png){width="600" zoomable="yes"}

![服务合同详细信息](./assets/contract.png){width="600" zoomable="yes"}

返回终端并在`extension`文件夹中运行以下命令以将文件复制到`storefront`文件夹：

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## 连接到店面

此部分将帮助您实施真正的店面功能，向您展示在使用[!DNL Adobe Commerce]放置和[!DNL Edge Delivery Services]时如何有效地与AI代理进行通信。

>[!NOTE]
>
>提供的提示是起点，您应该可以随时与座席进行自然对话。 在使用人工智能辅助开发工具时，代理生成的代码和响应将发生自然变化。
>
>如果您遇到任何代码问题，始终可以请求代理帮助您对其进行调试。

### 实施评级星和评论计数

1. 导航到`storefront`文件夹：

   ```bash
   cd storefront
   ```

1. 在新的“光标”窗口中打开店面文件夹。 如果安装了[Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands)，请在终端中输入以下命令：

   ```bash
   cursor .
   ```

1. 启动本地开发服务器：

   ```bash
   npm run start
   ```

1. 在浏览器中，导航到“服饰”页面：

   ```text
   http://localhost:3000/apparel
   ```

1. 观察样板店面UI布局。

1. 对代理使用以下提示：

   ```text
   Implement product ratings to the storefront.
   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.
   Use the dropin slot system where available.
   
   Use the @RATINGS_API_CONTRACT.md to understand how to use the ratings api.
   ```

   >[!NOTE]
   >
   >如果提示您启动本地开发服务器，请通知代理该服务器已在运行。

1. 观察代码库中的变化，并查看“服装”页面以了解更新。

**预期结果：**

* 系统会自动创建产品评级“组件”。
* 该组件使用插槽集成到产品详细信息、产品列表页面和产品推荐块中。
* 星星以基于模拟评级值的适当填充比例显示。

![产品评级实施](./assets/product-ratings-implementation.png){width="600" zoomable="yes"}

### 更改星形颜色

对您的座席使用以下提示：

```text
Change the star fill color to red.
```

**预期结果：**

星星变红了。

![红星颜色](./assets/red-star-colors.png){width="600" zoomable="yes"}

## 店面回顾

在本教程中，我们涵盖了以下主题：

* **功能实现**：如何向AI代理描述新功能。
* **迭代更改**：快速修改现有代码。
* **复杂的UI组件**：正在生成具有可视化引用的交互功能。
* **放置集成**：正在使用[!DNL Adobe Commerce]个放置容器和插槽。
* **组件可重用性**：正在创建跨多个块使用的共享组件。

## 后续步骤

如果时间允许，您可以通过添加以下功能进一步自定义评级扩展：

### 添加评级分布模式（可选）

以下步骤显示了代理如何处理具有可视化引用的复杂UI功能。

1. **开始之前：**&#x200B;保存以下模拟图像并将其粘贴到与店面代理的聊天中。

   ![评级分发模型](./assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. 可按照以下步骤引导您根据参考图像创建评级分布模式：

   * 更新API以返回表示评级分布的附加数据。
   * 更新API合同。
   * 更新店面代码库中的联系人。
   * 要求店面代理使用参考图像并更新API合同以将评级分发添加到PDP页面。

1. 观察代码库中的以下更改，并查看“服装”页面以了解更新：

   * 代理如何解释可视化模型
   * 它是否使用适当的HTML结构来实现辅助功能
   * 如何处理定位和交互状态

**疑难解答：**

* 如果未显示该模式窗口，请检查浏览器控制台中是否有错误。
* 如果定位功能已关闭，您可以要求代理：

  ```text
  adjust the modal position to be...
  ```

![评级分发模式](./assets/rating-distribution-modal.png){width="600" zoomable="yes"}
