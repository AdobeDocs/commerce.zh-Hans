---
source-git-commit: e3be9274ca8db80d3559b24a5c8be36f5d61b2ba
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.zh-Hans/blob/main/help/_includes/ccdm-shared/merchandising/rules/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# 促销规则最佳实践

为了优化转化和收入，请实施有效的&#x200B;**搜索规则**、强大的&#x200B;**默认列表**&#x200B;规则和&#x200B;**[类别规则](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/add#rule-types)**。 使用销售数据、库存、促销活动和[智能排名](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)调整排名。

仅在匹配的购物者查询必须返回零个产品时才使用[搜索禁止显示规则](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/overview#search-suppression-rules)，而不是在产品需要不同的排名时使用。

建立精心考虑的&#x200B;**默认规则**&#x200B;至关重要。 您的[默认规则](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/overview#default-rule)确定在没有更具体的搜索规则应用时搜索结果的初始排序方式，这提高了发现和购买的可能性。 请定期检查，以使其与购物者需求和促销活动保持同步。

## 优化搜索规则的提示

- 固定或提升具有高销量或近期销售活动的产品。
- 优先考虑具有高评级和正面评价的产品。
- 确保库存商品排名较高。
- 稍微优先处理利润率较高的产品，而不影响其相关性。
- 突出显示正在销售或属于特殊促销的产品。
- 通过使用促销期间的日期范围，在促销期间或销售期间自动设置搜索规则。
- 使用[智能排名](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)（例如“为您推荐”、“查看次数最多”等），根据每位购物者的行为定制搜索结果。
- 选择非&#x200B;**无**&#x200B;的智能策略时，针对每个规则调整&#x200B;**[智能排名提升](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)**，并在发布之前在&#x200B;**测试您的规则**&#x200B;中进行验证。
- 始终使用“测试规则”面板来预览您的智能排名策略对不同查询的实际搜索结果有何影响。

## 类别规则的提示

- 在高流量或高利润的&#x200B;**类别页面**&#x200B;上使用[类别规则](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/add#rule-types)，策划的订单与搜索同样重要 — 例如，季节性系列或特色部门。
- 将&#x200B;**智能排名**（例如，趋势、查看次数最多）与购物者浏览该类别的方式保持一致；类别页面不会像搜索规则那样使用搜索查询文本。 查看[智能排名](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking)。 对于非&#x200B;**无**&#x200B;的智能方法，请使用&#x200B;**[智能排名提升](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)**&#x200B;和类别预览来调整该类别规则的行为强度。
- 与您的促销活动计划一致地应用&#x200B;**pin**、**boost**&#x200B;和&#x200B;**bury**；请记住，手动职位通常仅在购物者对列表使用&#x200B;**默认排序**&#x200B;时应用。 请参阅[手动排名](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/add#manual-ranking)。
- 在编辑器中预览&#x200B;**类别**&#x200B;规则流，并在发布后在店面中验证，这与您在搜索中用于“测试您的规则”面板的规则相同。

## 搜索禁止显示最佳实践和用例 {#search-suppression-best-practices}

搜索隐藏规则会阻止符合其条件的查询结果，因此店面会显示一个搜索结果页面，其中不含任何产品。 规则编辑器不提供禁止显示规则的预览。 使用满足该限制的最窄条件，然后遵循[创建和管理搜索禁止显示规则](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules)。 规则变为活动状态后，验证店面中的匹配搜索和非匹配搜索。 检查店面的实际无结果演示。

| 用例 | 建议的配置 | 检查内容 |
| --- | --- | --- |
| 针对搜索的管理合规性 | 将规则范围设置为受影响的目录视图，并匹配受限的搜索词。 | 与合规性团队确认条款。 仅使用“搜索抑制”不会阻止通过类别导航、促销页面、推荐或直接产品URL进行访问。 |
| 品牌限制 | 在较长的查询中必须阻止受限品牌名称时，使用&#x200B;**查询包含**。 | 在规则变为活动状态后，检查包含类似文本的不相关的店面查询，以避免隐藏合法的搜索。 |
| 阻止特定搜索词返回结果 | 使用&#x200B;**查询is**&#x200B;获取不应返回任何产品的精确短语。 | 请单独检查相关短语。 完全匹配条件不会阻止每个包含该短语的查询。 |
| 查询前缀或后缀的限制 | 当受限文本的位置重要时，使用&#x200B;**查询开始于**&#x200B;或&#x200B;**查询结束于**。 | 在规则变为活动状态后，检查店面查询，并在开头、中间和结尾显示文本，以确认预定范围。 |
| 临时搜索限制 | 设置时间限制限制的开始和结束日期。 | 确认计划和启用状态，并查看限制结束后是否仍需要规则。 |

- 为每个规则提供一个描述性名称，并在其描述中记录限制的原因。
- 在发布更改之前查看查询条件。 规则变为活动状态后，检查应阻止的店面查询以及仍应返回产品的查询。 缓存的查询结果可能需要长达15分钟才能刷新。
- 查看店面的无结果状态，并确保购物者有有用的方式来继续浏览，例如修改查询或导航到店面支持的类别。
- 请勿使用查询隐藏作为产品级别排除的替代项。 要跨搜索结果、搜索建议以及自动完成排除产品，请在&#x200B;**默认搜索规则**&#x200B;中使用手动排除项或具有&#x200B;**隐藏**&#x200B;操作的&#x200B;**基于属性的促销事件**。
- 定期查看活动禁止显示规则。 禁用不再需要的规则，或在限制更改时编辑和发布这些规则。
