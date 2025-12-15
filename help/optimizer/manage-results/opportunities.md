---
title: 机会
description: 通过与Adobe Sites Optimizer集成以实现智能的数据驱动型网站改进，发现增加流量、参与度和转化率的机会。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 7f7b4a3c866c453d9722b708a0ed4e1b601c8e8e
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---

# 机会

**机会**&#x200B;页面可帮助您识别并实施优化，以便通过与Adobe Sites Optimizer集成来提高网站流量、用户参与度和转化率。

![个机会](../assets/opportunities.png)

## 什么是机会？

[机会](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-sites-optimizer/content/documentation/opportunities/overview)是AI支持的推荐，可帮助商家识别并解决影响其商业网站性能的问题。 这些建议由[Adobe Experience Manager Sites Optimizer](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-sites-optimizer/content/home)提供支持，这是一项基于云的服务，可分析和改进网站性能。

## 主要功能

- **自动问题检测** — Sites Optimizer不断扫描产品目录、搜索日志和推荐数据，以识别影响发现的问题。
- **AI驱动的建议** — 接收智能建议以解决检测到的问题。
- **影响分类** — 问题按业务影响（搜索、推荐、浏览/导航、产品数据质量）进行分类。
- **功能板报告** — 查看问题趋势、最受影响的产品或查询，以及随时间推移的改进情况。

## 快速入门

要在Commerce Optimizer中启用机会，请联系您的客户成功经理(CSM)。 **Ultima** Adobe Sites Optimizer许可证提供了相关机会。

## 快速导览

“机会”页面分为三个选项卡，可帮助您管理优化推荐：

- **当前（活动）** — 显示新检测到的需要审核和操作的机会。 这些是可能会影响站点性能的活动问题。
- **跳过** — 包含您已选择取消或推迟的机会。 如果销售机会与您当前的业务目标无关，您可以在此处进行移动。
- **已优化（完成）** — 显示已通过自动修复部署成功解决的商机。 任何手动处理的机会都不会显示在此选项卡上。 此选项卡可帮助您在一段时间内跟踪您的自动修复机会。

![当前机会](../assets/current-opportunities.png)

## 自动检测工作流

自动检测工作流使用AI支持的分析自动识别整个产品目录中的优化机会。 此自动扫描过程会持续监视您的产品数据、搜索日志和推荐性能，以检测可能影响站点性能、SEO和客户参与度的问题。

### 工作原理

自动检测利用Adobe Experience Manager Sites Optimizer来：

- **分析产品页面** — 系统会检查产品详细信息页面的前200个页面和过滤器，以确定优化目标。
- **提取元数据** — 将从每个页面提取Meta标记（标题、描述、H1标题）以供分析。
- **生成AI推荐** — 通过Adobe的AI工作流处理提取的数据，以创建可操作的优化建议。
- **填充机会** — 自动检测到的建议显示在&#x200B;**当前（活动）**&#x200B;选项卡中，供您审阅。

### 先决条件

在自动检测可以生成推荐之前，您的目录数据必须同步并处于最新状态以确保推荐准确无误。

### 接下来会发生什么

自动检测识别优化机会后，您可以：

- 在&#x200B;**当前（活动）**&#x200B;选项卡中查看建议的优化。
- 使用[自动修复工作流](#auto-fix-workflow)自动部署修复（对于支持的[机会类型](#supported-opportunity-types)）。
- 在Commerce管理员中手动实施更改。
- 忽略不符合您的业务目标的机会。

## 自动修复工作流

自动修复工作流允许您通过单击快速部署AI生成的优化。 应用自动修复时，系统会创建一个覆盖特定产品属性的目录优化层，而不修改原始产品数据。 您的原始产品数据将保持不变，使您能够安全地应用优化并随时恢复更改。 请参阅[目录层如何与自动修复一起使用](#how-catalog-layers-work-with-auto-fix)以了解详细信息。

### 支持的机会类型

下面列出了支持的机会类型：

- 标题过长
- 标题太短
- 重复标题
- 缺少标题
- 空标题
- 描述太长
- 描述太短
- 缺少描述
- 描述为空
- 复制描述
- 缺少H1
- 复制H1
- H1过长

>[!NOTE]
>
>当前不支持页面上的多个H1。

### 先决条件

在使用自动修复之前，请确保：

- 您的产品目录已完全摄取到Commerce Optimizer。
- 机会类型支持自动修复（某些优化类型需要手动实施）。
- 您具有创建和管理目录层的相应权限。

>[!IMPORTANT]
>
>自动修复功能需要完全摄取的产品目录。 如果尚未摄取您的目录，您仍然可以使用提供的CSV文件查看机会并手动实施修复。 请注意，不会在&#x200B;**已优化（完成）**&#x200B;选项卡中跟踪手动实施。

### 部署自动修复优化

按照以下步骤实施AI建议的优化：

1. 导航到&#x200B;**管理结果** > **机会**。

1. 在&#x200B;**当前（活动）**&#x200B;选项卡中，查看可用的优化建议。

1. 选择一个机会。

   ![选择机会](../assets/autofix-opportunity.png)

   >[!NOTE]
   >
   >**部署优化**&#x200B;按钮仅适用于[支持的建议类型](#supported-opportunity-types)。 对于不支持的类型，该复选框处于禁用状态，您必须在目录中手动应用修复。

1. 单击&#x200B;**部署优化**，然后单击&#x200B;**部署**&#x200B;以触发自动修复进程。

   ![部署优化](../assets/deploy-autofix.png)

   系统在后台执行以下操作：

   - 为产品创建新的目录层（如果尚不存在）。
   - 根据AI推荐更新相关属性（例如元标题、描述或H1）。
   - 将新图层指定为目录视图中的最高优先级（顺序1）。
   - 通过目录店面服务验证更改。

1. 监视部署状态。 验证完成后，系统会自动更新建议状态。

1. 优化后，建议将移至带有状态指示器的&#x200B;**已优化（完成）**&#x200B;选项卡：

   - **绿色复选标记** — 优化层设置为第一优先级并主动应用于您的店面。
   - **警告图标** — 该层存在，但不是最高优先级，这意味着它可能被其他层覆盖。

   ![已完成的机会](../assets/done-opportunities.png)

>[!NOTE]
>
>自动修复支持为任何语言的站点优化元数据。 Sites Optimizer会以其原始语言分析产品详细信息页面，生成本地化的AI推荐，并根据在目录视图中配置的源区域设置创建目录层。

### 目录层如何使用自动修复

如果目录视图中不存在Adobe Sites Optimizer层，则自动修复会自动创建一个图层，并为其分配顺序1（最高优先级）。 如果删除此图层，则会在下次自动修复运行时重新创建此图层，并将现有图层移至更低顺序编号。 如果Adobe Sites Optimizer Layer在其他订单号中已存在，则自动修复不会更改其优先级。 如果要保留自动修复层，但不立即使用它，则可以禁用该层。 了解有关如何管理[目录层](../setup/catalog-layer.md#activate-or-deactivate-layers)的详细信息。

![目录层](../assets/catalog-layers.png)

该图显示了名为&#x200B;**ASO优化**&#x200B;的单个行。 此条目表示您选择自动修复的所有业务机会。 无论您是自动修复单个业务机会还是多个业务机会，它们都显示在这个&#x200B;**ASO优化**&#x200B;行中。 图层特定于每个目录视图，因此此处显示的&#x200B;**洛杉矶**&#x200B;目录视图仅在该视图处于活动状态时应用其&#x200B;**ASO优化**&#x200B;图层。

### 重要注意事项

使用自动修复时，请牢记以下几点：

- 为每个建议显示的状态反映了自动修复工作程序运行时的状态。 如果以后手动重新排序目录层，则状态不会动态更新。

- 为了确保您的优化保持活动状态，请避免在部署自动修复推荐后手动更改目录层优先级。

### 故障排除

如果优化似乎未应用于您的店面：

1. 检查&#x200B;**已优化（完成）**&#x200B;选项卡中的状态指示器。
1. 如果看到警告图标，请验证目录层优先级设置。
1. 确保在目录视图中将优化层设置为顺序1（最高优先级）。
1. 确认目录数据同步处于活动状态且是最新的。
1. 留出时间让更改传播。 即使在订单1上有正确配置的层，更改也可能需要一段时间才能显示在店面上，类似于发布新产品时的延迟。

## Sites Optimizer和成功量度如何协作

成功量度可监控关键性能指标，如产品发现和目录业务效率，而Sites Optimizer中的机会则可让您了解如何提高SEO、加载速度、可访问性和参与度。 商家和营销人员可以携手提高运营效率，以最少的IT支持实现更快的端到端性能和转化收益。 要了解如何利用这两种技术改善店面性能和体验，请参阅[将成功量度和Sites Optimizer结合使用](./success-metrics.md#using-success-metrics-and-sites-optimizer-together)。

## 了解有关Sites Optimizer的更多信息

有关Sites Optimizer功能和特征的详细信息，请参阅[Adobe Experience Manager Sites Optimizer文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-sites-optimizer/content/home)。

其他资源：

- [机会类型](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/opportunities) — 了解可用的优化机会。
- [Sites Optimizer功能](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/capabilities) — 探索Sites Optimizer的功能。

## 更多此类内容

- [成功量度](success-metrics.md) — 监视关键绩效指标。
- [搜索性能](search-performance.md) — 分析搜索词并优化相关性。
- [推荐性能](recommendation-performance.md) — 监视推荐有效性。
