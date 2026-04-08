---
title: 促销规则最佳实践
description: 了解为搜索、默认列表和类别页面实施促销规则的最佳实践。
role: Admin, Developer
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
exl-id: cc8d0879-c253-4ad4-8e7d-e066dff9112d
source-git-commit: 8abc0593c166a2dd861cfb78674918de1d0744de
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 促销规则最佳实践

为了优化转化和收入，请实施有效的&#x200B;**搜索规则**、强大的&#x200B;**默认列表**&#x200B;规则和&#x200B;**[类别规则](add.md#category-rules)**（测试版）。 使用销售数据、库存、促销活动和[智能排名](add.md#intelligent-ranking)调整排名。

建立精心考虑的&#x200B;**默认规则**&#x200B;至关重要。 您的[默认规则](overview.md#default-rule)确定在没有更具体的搜索规则应用时搜索结果的初始排序方式，这提高了发现和购买的可能性。 请定期检查，以使其与购物者需求和促销活动保持同步。

## 优化搜索规则的提示

- 固定或提升具有高销量或近期销售活动的产品。
- 优先考虑具有高评级和正面评价的产品。
- 确保库存商品排名较高。
- 稍微优先处理利润率较高的产品，而不影响其相关性。
- 突出显示正在销售或属于特殊促销的产品。
- 通过使用促销期间的日期范围，在促销期间或销售期间自动设置搜索规则。
- 使用[智能排名](add.md#intelligent-ranking)（例如“为您推荐”、“查看次数最多”等），根据每位购物者的行为定制搜索结果。
- 始终使用“测试规则”面板来预览您的智能排名策略对不同查询的实际搜索结果有何影响。

## 类别规则的提示

>[!IMPORTANT]
>
>类别规则为测试版。

- 在高流量或高利润的[类别页面](add.md#category-rules)上使用&#x200B;**类别规则**，策划的订单与搜索同样重要 — 例如，季节性系列或特色部门。
- 将&#x200B;**智能排名**（例如，趋势、查看次数最多）与购物者浏览该类别的方式保持一致；类别页面不会像搜索规则那样使用搜索查询文本。 查看[智能排名](add.md#intelligent-ranking)。
- 与您的促销活动计划一致地应用&#x200B;**pin**、**boost**&#x200B;和&#x200B;**bury**；请记住，手动职位通常仅在购物者对列表使用&#x200B;**默认排序**&#x200B;时应用。 请参阅[手动排名](add.md#manual-ranking)。
- 在编辑器中预览&#x200B;**类别**&#x200B;规则流，并在发布后在店面中验证，这与您在搜索中用于“测试您的规则”面板的规则相同。
