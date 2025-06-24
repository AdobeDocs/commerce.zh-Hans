---
title: Facet最佳实践
description: 了解在商店中实施Facet的最佳实践。
role: Admin, Developer
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Facet最佳实践

过滤器和彩块化功能是[!DNL Adobe Commerce Optimizer]网站的关键组件，旨在通过允许购物者缩小搜索结果范围并更有效地查找产品来增强购物者体验。 此功能通过应用特定标准来帮助购物者对数量庞大的商品目录进行排序，从而使购物过程更快、更容易、更令人满意。 通过实施有效、对购物者友好的过滤器和彩块化，您可以帮助客户快速高效地找到他们所需的内容，最终提高满意度和转化率。

## 优化彩块化的提示

- 确定产品最相关且最有用的属性，如标题、类别、品牌、价格范围、颜色和大小，并将它们设置为[动态Facet](type.md)。 
- 设置和排序在您的目录范围内一致且与您的产品高度相关的产品属性，以提高关联性和过滤功能，从而帮助购物者。
- 确保Facet标签易于理解并在整个站点中以一致的方式命名。 例如，使用“价格范围”而不是“成本”。
- 避免让购物者不知所措，将小面的数量限制在最重要的方面。 太多选项可能会导致决策疲劳。 默认情况下，[!DNL Adobe Commerce Optimizer]限制为最多100个配置为Facet的属性，并在每个Facet中返回30个存储段。 了解有关[方面限制](../../boundaries-limits.md#catalog-views-and-policies)的更多信息。 
- 允许购物者同时选择多个筛选条件以优化结果。 例如，允许购物者同时选择“红色”和“蓝色”颜色。
- 在每个Facet选项旁边显示可用产品的数量，以便让购物者了解他们可期待的搜索结果。
- 实施可折叠的Facet部分以保持接口干净且可管理，尤其是在移动设备上。
- 允许购物者轻松重置单个Facet或所有选定的过滤器以启动新搜索。
- 如果要与大量属性冲突，请考虑将属性组合到单个“meta-attribute”中。 例如，鞋的尺寸通常为数字，而衬衫的尺寸通常为“S/M/L/XL”。 这两种类型的大小可以合并为一个可搜索属性。
