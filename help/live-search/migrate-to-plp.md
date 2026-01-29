---
title: 从搜索适配器迁移到PLP小组件
description: 了解如何从已弃用的搜索适配器迁移到 [!DNL Live Search] 产品列表页面小组件。
source-git-commit: 8811f0f271928fbc827e5a0164542da473c57224
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 0%

---

# 从搜索适配器迁移到PLP小组件

搜索适配器自[ 4.0.0起已](release-notes.md#live-search-400)弃用[!DNL Live Search]，将仅接收安全更新。 [产品列表页面(PLP)小组件](plp-styling.md)是所有[!DNL Live Search]实施都支持的解决方案。 本指南可帮助您了解何时可以直接迁移以及何时需要执行其他工作。

## 先决条件

在开始迁移过程之前，确保您的环境满足这些要求。

开始迁移前：

**技术要求**：

- Adobe Commerce 2.4.4或更高版本。
- 已安装[!DNL Live Search]扩展。
- 访问命令行(CLI)。
- 访问Commerce管理员。
- 用于测试的暂存或QA环境。

**备份和准备**：

1. 备份数据库和代码。
1. 记录当前的自定义项。
1. 查看[边界和限制](boundaries-limits.md)以确保PLP构件满足您的需求。
1. 在低流量期间安排迁移。
1. 通知利益相关者店面行为可能发生更改。

**查看当前实施**：

- 检查当前[!DNL Live Search]版本。
- 记录正在使用哪些Facet及其配置。
- 测试所有搜索功能并记录预期行为。
- 捕获当前搜索结果演示文稿的屏幕截图。

**版本兼容性**：

- 运行Adobe Commerce 2.4.4或更高版本。
- 准备好升级到[!DNL Live Search] 4.0.0或更高版本。

## 迁移方案

### 直接迁移（无需额外工作）

如果您的实施符合以下所有条件，则可以直接迁移到PLP小组件：

**基于Luma的标准店面**：

- 您正在使用Luma主题或从Luma继承的主题，只需进行最少的自定义。
- 您尚未对PLP布局或模板进行自定义修改。
- 您尚未创建与搜索结果交互的自定义JavaScript扩展。

**标准产品目录**：

- 所有产品属性都使用标准源模型（而非自定义源模型）。
- 没有需要特殊渲染逻辑的自定义产品类型。
- 您的目录仅使用标准Facet和筛选。

**标准集成**：

- 您未使用适用于Analytics的Google Tag Manager (GTM)。
- 您未使用可修改搜索行为的第三方扩展。

如果实施符合这些条件，请继续执行[标准迁移步骤](#standard-migration-steps)。

### 需要额外工作的迁移

如果您的实施具有以下任一情况，则需要执行其他工作：

**自定义主题修改**：

- 覆盖Luma模板的自定义PLP布局。
- 用于定位搜索适配器特定元素的自定义CSS或JavaScript。
- PLP或相关文件的自定义模板修改。
- 主题不会从Luma继承（例如，从头开始自定义主题）。

**自定义产品属性**：

- 具有用作Facet的自定义源模型的产品属性。
- 具有特殊显示要求的自定义产品类型。
- 具有`"is_user_defined": false`的编程特性。

**高级集成**：

- Google Tag Manager (GTM)主要用于跟踪。
- 与搜索集成的第三方分析或个性化工具。
- 自定义事件跟踪或数据层实施。
- 与外部搜索或推荐引擎集成。

**Headless或PWA实施**：

- 使用Headless架构(例如，PWA Studio、Vue Storefront)。
- 自定义前端框架(React、Vue、Angular)。
- 专门将GraphQL用于目录查询。
- 自定义店面事件实施。

**自定义构件代码**：

- 之前自定义了搜索适配器代码。
- 将构件的自定义版本托管在您自己的CDN上。
- 用于搜索功能的自定义JavaScript扩展。

如果您的实施具有任何这些方案，请参阅[复杂的迁移方案](#complex-migration-scenarios)。

## 标准迁移步骤

对于没有特殊自定义设置的实施，请执行以下步骤：

### 步骤1：升级[!DNL Live Search]

将您的[!DNL Live Search]扩展升级到版本4.0或更高版本，以访问PLP构件。

**角色**：商家或合作伙伴

1. 检查当前[!DNL Live Search]版本：

   ```bash
   composer show magento/live-search | grep version
   ```

1. 如果使用的是版本3.x或更低版本，请在升级之前启用AdvancedSearch模块：

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

1. 更新`composer.json`以要求[!DNL Live Search] 4.0或更高版本：

   ```json
   "require": {
      "magento/live-search": "^4.0"
   }
   ```

1. 运行升级：

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. 运行安装程序升级并重新编译：

   ```bash
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   ```

1. 部署静态内容（如果需要）：

   ```bash
   bin/magento setup:static-content:deploy
   ```

### 步骤2：启用PLP小组件

在Commerce管理中配置PLP小组件。

**角色**：商家

对于[!DNL Live Search] 4.0.0+的新安装，默认启用PLP小组件。 如果从早期版本升级：

1. 转到&#x200B;**[!UICONTROL Stores]** >设置> **[!UICONTROL Configuration]**。
1. 导航到&#x200B;**[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**。
1. 展开&#x200B;**[!UICONTROL Storefront Features]**&#x200B;部分。
1. 将&#x200B;**[!UICONTROL Enable Product Listing Widgets]**&#x200B;设置为&#x200B;**是**。
1. 单击&#x200B;**[!UICONTROL Save Config]**。
1. 刷新缓存： **[!UICONTROL System]** >工具> **[!UICONTROL Cache Management]** > **[!UICONTROL Flush Magento Cache]**。

### 步骤3：在暂存环境中测试

在上线之前，在非生产环境中验证迁移。

**角色**：商家/合作伙伴

在部署到生产环境之前，请彻底测试搜索功能：

**功能测试**：

- 验证搜索结果是否正确显示。
- 测试所有已配置的Facet。
- 验证类别导航是否有效。
- 通过结果测试分页。
- 验证排序选项是否按预期工作。
- 测试简单产品的添加到购物车功能。

**视觉测试**：

- 确认产品图像是否正确显示。
- 验证产品名称和价格是否正确呈现。
- 测试色板（如果使用）。
- 检查移动设备上的响应式行为。
- 验证样式是否与您的品牌匹配。

**性能测试**：

- 测量页面加载时间。
- 使用真实的目录大小进行测试。
- 监视服务器资源使用情况。
- 检查浏览器控制台中是否存在JavaScript错误。

### 步骤4：部署到生产

将经验证的配置移至您的实时店面。

**角色**：商家/合作伙伴

1. 在维护时段安排部署（如果可能）。
1. 按照标准部署流程操作。
1. 使用[步骤2在生产环境中启用PLP小组件：启用PLP小组件](#step-2-enable-the-plp-widget)。
1. 部署后立即监控任何问题。
1. 如果出现严重问题，请准备好回滚计划。

### 步骤5：验证和监控

迁移后跟踪搜索性能和客户体验。

**角色**：商家

部署后，监视关键量度：

- 零结果搜索率
- 搜索到购物车的转化率
- 页面加载性能
- 客户反馈或支持票证
- 浏览器控制台中的JavaScript错误

## 复杂的迁移方案

以下方案需要在标准迁移步骤之外进行额外的规划、自定义开发或专业化支持。

### 带有布局修改的自定义主题

在此方案中，您具有覆盖默认产品列表行为的自定义模板或布局。

**角色**：开发人员/合作伙伴

1. **审核自定义项**：
   - 在主题中记录所有自定义布局XML文件。
   - 查看对产品列表页面或相关文件所做的任何自定义模板修改。
   - 标识用于样式设置的自定义CSS类。
   - 记录自定义JavaScript交互。

1. **迁移到基于CSS的自定义项**：
   - PLP构件使用特定的CSS类（请参阅[PLP样式指南](plp-styling.md)）。
   - 使用PLP小组件CSS类重新创建可视化自定义项。
   - 测试自定义样式是否正确应用。

1. **删除冲突的自定义项**：
   - 删除修改产品清单结构的布局XML。
   - 清理定位搜索适配器特定元素的JavaScript。
   - 更新模板将覆盖与构件渲染的冲突。

1. **全面测试**：
   - 验证所有可视化自定义是否均可用于PLP小组件。
   - 确保没有布局冲突。
   - 在所有断点和设备上测试。

### 具有自定义源模型的产品属性

在此方案中，您的方面将产品属性与自定义源模型结合使用，而搜索适配器不支持这些自定义源模型，但PLP构件也支持这些自定义源模型。

**角色**：贸易商（管理员配置）

1. **识别受影响的属性**：
   - 查看用作Facet的产品属性。
   - 确定使用自定义源模型的受众。
   - 记录当前彩块化配置。

1. **升级并启用PLP小组件**：
   - 执行[标准迁移步骤](#standard-migration-steps)。
   - PLP小组件支持自定义源模型属性。

1. **重新配置Facet**：
   - 转到&#x200B;**[!UICONTROL Marketing]** > SEO和搜索> **[!UICONTROL Live Search]**。
   - 查看受影响属性的方面配置。
   - 测试Facet可与自定义源模型正常配合使用。

1. **验证**：
   - 使用自定义源模型Facet测试筛选。
   - 验证所有属性值是否正确显示。
   - 确保性能可接受。

### Google Tag Manager (GTM)集成

在此方案中，有一个已知问题，启用PLP构件可能导致GTM失败。

**角色**：开发人员/合作伙伴+客户工程

**选项1：继续使用搜索适配器（仅限临时）**

- 如果GTM对业务至关重要，请保持搜索适配器处于启用状态。
- 了解您只会收到安全更新。
- 计划在解决GTM兼容性时进行迁移。
- 有关GTM兼容性的更新，请联系Adobe支持部门。

**选项2：将GTM跟踪迁移到替代方法**

1. **实施自定义事件集合**：

   - 使用[店面活动SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/)。
   - 捕获搜索和产品交互事件。
   - 手动将事件推送到GTM数据层。

1. **完成以下步骤**：

   - 审核当前GTM跟踪要求。
   - 将GTM事件映射到Storefront事件。
   - 实施自定义事件侦听器。
   - 测试数据流到GTM。
   - 验证Analytics报表。

**选项3：将GTM替换为Adobe Analytics**

- 考虑迁移到[Adobe Analytics](https://business.adobe.com/products/adobe-analytics.html)（如果适用）。
- 请联系客户工程部门以获取指导。

**联系对象**：提交支持票证以获取GTM兼容性更新或客户工程部门帮助。

### 情景：Headless或PWA实施

在此方案中，您有一个需要自定义事件收集的Headless或PWA店面，并且无法使用标准PLP小组件UI。

**角色**：开发人员/合作伙伴

1. **查看引用实施**：
   - 研究[PLP小部件源代码](https://github.com/adobe/storefront-product-listing-page)。
   - 查看[[!DNL Live Search] GraphQL](graphql.md)的API文档。
   - 了解[目录服务查询](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)。

1. **实施自定义用户界面**：
   - 使用[!DNL Live Search] GraphQL API进行查询。
   - 构建自定义产品列表组件。
   - 实施用于分面的UI。
   - 处理分页和排序。

1. **实施事件集合**：
   - 查看[店面活动文档](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)。
   - 实施所需事件：
      - `search-request-sent`
      - `search-response-received`
      - `search-results-view`
      - `product-page-view`
      - `add-to-cart`
   - 测试事件数据流向Adobe Commerce。

1. **配置Facet排序**：
   - 对于Headless实施，Facet可以按计数排序。
   - 在&#x200B;**[!UICONTROL Live Search]** > **[!UICONTROL Facets]**&#x200B;工作区中进行配置。
   - 将&#x200B;**[!UICONTROL Sort Type]**&#x200B;设置为&#x200B;**Count**&#x200B;以获得更好的UX。

1. **测试和验证**：
   - 验证搜索结果的准确性。
   - 测试彩块化功能。
   - 确认正确跟踪了事件。
   - 监控性能指标。
   - 验证智能促销功能是否有效。

### 方案：自定义构件代码修改

在这种情况下，您以前自定义过搜索适配器或构件代码，因此需要迁移自定义项。

**角色**：开发人员/合作伙伴

1. **记录现有自定义项**：
   - 列出对搜索适配器所做的所有自定义设置。
   - 确定推动每次自定义的业务需求。
   - 确定是否仍需要自定义。

1. **检查内置功能是否满足您的需求**：
   - 查看[PLP小部件功能](plp-styling.md#widget-features)。
   - 检查基于CSS的自定是否足够。
   - 测试默认PLP构件行为。

1. **如果仍需要自定义代码**：
   - 克隆[PLP小部件存储库](https://github.com/adobe/storefront-product-listing-page)。
   - 实施您的自定义项。
   - 在您自己的CDN上托管。
   - 更新Commerce配置以使用您的自定义构件。

   >[!WARNING]
   >
   >如果使用存储库中的代码自定义PLP小组件，则由您负责维护和更新。 Adobe中的新PLP构件功能可能与您的自定义不兼容。

1. **全面测试**：
   - 测试所有自定义功能。
   - 确认Commerce更新不会破坏自定义设置。
   - 记录您的自定义实施。
   - 规划日常维护。

## 已知限制和边缘案例

迁移时，请注意以下限制：

**PLP构件限制**：

- **排序顺序方向**：启用PLP构件时，无法更改产品列表页面上的排序顺序方向（升序/降序）。
- **添加到购物车**：“添加到购物车”按钮仅适用于小组件中的简单产品。
- **层定价**：在PLP小部件中不受支持。
- **增值税显示**：价格包含增值税，但增值税不能显示为单独的值。

**与搜索适配器的功能差异**：

- **颜色样本**： `color`属性的拼写必须与`color`完全相同（不是“颜色”或自定义名称），样本才能正常工作。
- **主题样式**：自定义主题类不由构件继承；必须定位特定于构件的CSS类。
- **自定义产品类型**：小部件中不支持。

**性能注意事项**：

- 大型目录（50,000多种产品）的初始页面加载时间可能会较长。
- 具有许多值的多个Facet可能会影响性能。
- 移动设备性能可能会因目录大小而异。

**兼容性问题**：

- Google Tag Manager兼容性问题（请参阅[GTM方案](#google-tag-manager-gtm-integration)）。
- 某些第三方扩展可能会与PLP构件冲突。
- 自定义签出扩展可能需要更新。

## 获取帮助

根据您的特定需求，联系相应的资源。

**Adobe支持**&#x200B;可以协助您：

- 标准Live Search迁移过程
- PLP构件配置问题
- Facet或属性索引问题
- 默认实施的性能问题
- 升级错误

**应该联系开发合作伙伴/系统集成商**：

- 自定义主题修改
- 自定义构件代码实施
- 第三方扩展兼容性
- Headless或PWA实施
- 自定义事件跟踪

要联系Adobe支持，请参阅[帮助中心用户指南](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。

## 常见问题解答

查找有关从搜索适配器迁移到PLP小组件的常见问题解答。

**问：搜索适配器是否会收到错误修复或功能更新？**

答：不行。 搜索适配器已弃用，将只接收安全更新。 错误修复、性能改进和新功能仅在PLP构件中可用。 如果您遇到搜索适配器问题，建议迁移至PLP构件。

**问：迁移是否会破坏我的店面？**

答：如果您在暂存过程中遵循了正确的测试步骤，那么迁移应该是无缝的。 准备生产部署的回滚计划。

**问：迁移需要多长时间？**

答：对于标准实施：1-2个小时。 对于自定义实施：根据复杂性，持续1-4周。

**问：我的搜索促销规则是否仍然有效？**

答：是，在[!DNL Live Search]工作区中配置的所有搜索促销规则、同义词和Facet都可以继续使用PLP小组件。

**问：是否需要重新配置我的Facet？**

答：通常不会，但是如果您受限于带有搜索适配器的自定义源模型属性，那么现在可以将它们与PLP构件一起使用。

**问：我的自定义CSS呢？**

答：您需要更新CSS以定位PLP构件类。 请参阅[CSS类引用](plp-styling.md#css-classes)。

**问：这将影响我的搜索性能吗？**

答：PLP小组件旨在提供高性能。 大多数商家认为业绩相当甚至更好。 大型目录应在暂存环境中进行测试。
