---
title: 设置您的店面
description: 了解如何设置 [!DNL Adobe Commerce Optimizer] 店面。
role: Developer
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目(Adobe管理的SaaS基础架构)。"
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: d6d559728361f4421829f34818aa368eac407225
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 0%

---

# 设置您的店面

本指南将指导您使用Adobe Edge Delivery Services为[!DNL Adobe Commerce Optimizer]实例设置店面。 您的店面包括样板代码、示例内容，以及对产品详细信息页面和产品发现（搜索和筛选）的支持。

**预计完成时间：** 30-45分钟

## 先决条件

* 可以创建存储库并配置为本地开发的&#x200B;**GitHub帐户** (github.com)
* **[!DNL Adobe Commerce Optimizer]实例**&#x200B;包含示例数据以及配置的目录视图和策略
   * 有关安装说明，请参阅[添加示例数据](get-started.md#add-sample-data)。

### 所需的实例数据

在开始之前，请从[!DNL Adobe Commerce Optimizer]实例收集以下信息：

* **租户ID** （也称为实例ID）
   * 可从[实例详细信息页面](get-started.md#manage-instances)获得
* 您实例的&#x200B;**GraphQL端点**
   * 可从[实例详细信息页面](get-started.md#manage-instances)获得
* 全局目录视图的&#x200B;**目录视图ID**
   * 可从[目录详细信息页面](./setup/catalog-view.md#manage-catalog-view)获得
* 目录视图的&#x200B;**Source区域设置**
   * 样本数据的默认值为`en_US`

>[!NOTE]
>
>试用版访问客户可以在创建实例时收到的欢迎电子邮件中找到GraphQL端点。 试用实例预配置了示例数据、目录视图和策略。

## 设置步骤

1. **[创建店面项目](#create-your-storefront-project)** — 使用[站点创建者工具](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)创建一个新的店面项目，该项目包含样板代码、示例内容和配置文件。

1. **[自定义店面配置](#customize-the-storefront-configuration)** — 更新存储库中的`config.json`文件以连接到[!DNL Adobe Commerce Optimizer]实例。

1. **[验证您的设置](#verify-your-setup)** （10分钟）
   * 预览您的店面网站
   * 测试产品详细信息页面和搜索功能

## 创建店面项目

站点创建者工具创建一个包含以下组件的完整店面项目：

* **站点**：包含样板内容的店面登陆页面
* **代码**：包含样板源文件的存储库
* **内容**：包含站点内容文件的文档创作环境
* **Commerce配置**：实例特定配置的`config.json`文件

### 步骤1：生成项目

1. 打开[站点创建者工具](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. 选择&#x200B;**创建新站点（代码和内容）**。

1. 完成站点配置：

   * **GitHub组织/用户名**：输入您的GitHub用户名或组织名称
   * **网站名称**：为您的店面选择一个描述性名称
   * **Commerce GraphQL端点（可选）**：输入[!DNL Adobe Commerce Optimizer]实例的GraphQL端点

1. 单击&#x200B;**创建站点**&#x200B;以使用店面样板代码创建GitHub存储库。

   创建存储库后，站点创建者会更新并提示您安装代码同步应用程序。

### 步骤2：安装代码同步应用程序

1. 单击&#x200B;**[!UICONTROL Install AEM Code Sync App]**&#x200B;以在新选项卡中打开代码同步安装程序。

1. 配置代码同步应用程序：
   * 选择您的GitHub组织，然后单击&#x200B;**[!UICONTROL Configure]**。
   * 在代码同步界面中，单击&#x200B;**[!UICONTROL Only select repositories]**。
   * 单击&#x200B;**[!UICONTROL Select repositories]**&#x200B;菜单，然后选择您创建的店面代码存储库。
   * 单击&#x200B;**[!UICONTROL Save]**&#x200B;注册存储库。

1. 返回打开站点创建器的浏览器窗口，然后单击&#x200B;**创建站点**。

   站点创建者将店面样板内容复制到文档创作环境。 此过程需要1-2分钟。

### 步骤3：保存项目链接

1. 在网站详细信息部分，查看店面项目的链接：

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   使用这些链接管理您的店面代码、内容和配置。

1. 复制并保存这些链接以供将来引用：单击**[!UICONTROL Copy]。

## 配置您的店面

更新storefront配置以连接到[!DNL Adobe Commerce Optimizer]实例。

1. 在样板代码存储库中打开`config.json`文件。

   `https://github.com/<username or org>/<repo name>/config.json`

1. 在配置中找到`cs` （目录服务）部分。

1. 将占位符值替换为实例的值。 请参阅[先决条件](#prerequisites)。

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Source-Locale": "en_US",
      "AC-Price-Book-ID": "{priceBookId}"
   }
   ```

   >[!NOTE]
   >
   >要查找价格手册ID，请检查Adobe Commerce Optimizer中的[目录视图配置详细信息](./setup/catalog-view.md)，以查看分配的价格手册。 如果未分配任何价格手册，则可以从配置文件中删除此标头。 将价格手册分配给目录视图后，将其添加回来。

1. 保存配置文件。

   配置更改可能需要几分钟才能传播。 如果您没有立即看到数据，请等待2-3分钟再进行故障排除。

## 验证设置

测试您的店面以确保它已正确连接到您的[!DNL Adobe Commerce Optimizer]实例。

### 步骤1：查看店面主页

1. 导航到实时预览URL：

   `https://main--{SITE}--{ORG}.aem.live`

   将`{ORG}`和`{SITE}`替换为您的GitHub组织和站点名称。

1. **成功标准**：您应该会看到包含样板内容的店面主页。

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### 第2步：测试产品详细信息页面

查看默认的产品详细信息页面，以验证产品数据是否正确加载。

1. 导航到示例产品页面：
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   使用示例数据中的任意SKU，例如：
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   对于默认店面，您可以使用工艺路线中的`placeholder`值查看产品。 开始自定义店面时，您可以自定义店面代码，以根据目录中定义的产品路线设置产品详细信息页面的路径。

   >[!TIP]
   >
   >从[实例中的](./setup/data-sync.md)数据同步[!DNL Adobe Commerce Optimizer]页面查看可用的SKU。

1. **成功标准**：页面应显示：
   * 产品名称、说明和定价
   * 产品图像
   * 添加到购物车功能
   * 从[!DNL Adobe Commerce Optimizer]实例检索的数据

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### 步骤3：测试默认搜索功能

测试默认的产品功能，包括搜索和筛选。

1. 在店面主页上，单击标题中的放大镜图标。

1. 键入搜索字符串`tires`并按&#x200B;**Enter**。

1. **成功标准**：您应会看到：
   * 包含轮胎产品的搜索结果页面
   * 侧栏中的筛选选项
   * 包含图像和定价的产品列表

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. 单击任何轮胎产品以查看其详细信息页面。

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## 故障排除

如果在设置过程中遇到问题，请使用网页检查器控制台检查错误。 此外，请尝试清除浏览器缓存或使用其他浏览器。

使用以下指南检查常见问题：

### 常见问题

| 问题 | 症状 | 解决方案 |
|-------|----------|----------|
| **代码同步安装失败** | 无法完成代码同步设置 | <ul><li>确保您拥有GitHub组织的管理员访问权限。</li><li>尝试使用个人存储库而不是组织。</li><li>请检查GitHub权限并重试。</li></ul> |
| **站点未加载** | 404或连接错误 | <ul><li>验证您的网站URL格式： `https://main--{SITE}--{ORG}.aem.live`</li><li>检查代码同步应用程序是否已正确安装。</li><li>确保存储库为公共或已正确配置。</li></ul> |
| **未显示产品数据** | 产品页面显示占位符或错误 | <ul><li>验证`config.json`中的配置值</li><li>在[!DNL Adobe Commerce Optimizer]实例中，检查“数据同步”页面以验证是否已加载样例产品。 如果没有可用的产品，请使用[数据摄取API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request)重新加载示例数据或添加产品。 请等待几分钟，以便配置更改能够传播。</li><li>尝试使用在[文件中配置的相同标头，通过Merchandising Service ](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details)products查询`config.json`检索产品详细信息。 如果可以检索数据，则可能是目录视图配置存在问题或索引错误。</li></ul> |
| **搜索未返回任何结果** | 搜索结果页面为空 | <ul><li>验证您是否可以使用[文件中配置的相同标头，通过Merchandising Services ](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search)productSearch查询`config.json`检索产品搜索结果。 如果可以检索数据，则可能是目录视图配置存在问题或索引错误。</li><li>确认`config.json`文件中的目录视图ID与[!DNL Adobe Commerce Optimizer]中的目录视图ID匹配。</li><li>在Adobe Commerce Optimizer中，验证您在店面页眉配置中使用的策略、区域设置和价格手册的配置。</li><li>验证是否已正确设置用于搜索的[属性元数据设置](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata)。</li></ul> |

### 验证核对清单

在继续后续步骤之前，请验证以下各项，确保您的店面运行正常：

![清单](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)配置值与您的实例设置匹配<br>
![检查清单](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)店面主页加载无错误<br>
![清单](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)至少一个产品详细信息页面显示完整信息<br>
![清单](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)搜索功能返回相关结果<br>
![清单](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)产品图像正在正确加载<br>
![清单](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)配置值与您的实例设置匹配<br>

### 获取帮助

如果问题仍然存在：

* 查看[Adobe Commerce Storefront文档](https://experienceleague.adobe.com/developer/commerce/storefront/)
* 查看[Adobe Commerce Optimizer开发人员指南](https://developer.adobe.com/commerce/services/optimizer/)
* 访问[Adobe Commerce支持资源](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)

## 后续步骤

设置并验证店面后，您可以：

1. **[安装Sidekick](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#install-and-configure-sidekick)** — 用于直接从您的网站编辑、预览和发布内容的浏览器扩展

2. **[设置本地开发环境](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment)** — 创建本地环境以自定义店面代码和内容

### 学习和探索

* **[完成端到端用例](./use-case/admin-use-case.md)** — 使用[!DNL Adobe Commerce Optimizer]了解有关店面设置和目录管理的更多信息

* **[探索店面自定义](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)** — 了解高级设置和配置选项

* **[使用Commerce下拉列表自定义店面体验](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/)** — 添加预建组件以增强您的店面体验

>[!MORELIKETHIS]
>
> 请参阅[Adobe Commerce Storefront文档](https://experienceleague.adobe.com/developer/commerce/storefront/)，了解有关更新网站内容以及与Commerce前端组件和后端数据集成的更多信息。
