---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.zh-Hans/blob/main/help/_includes/ccdm-shared/merchandising/facets/type.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# 彩块化的类型

Facet有多种类型，只有在相关时才会显示在&#x200B;*筛选器*&#x200B;列表中。 可用Facet的列表会根据返回的产品而发生更改。 以下特征会影响其呈现方式和行为：

- 固定多面 — 最常用的多面可以固定到列表顶部。 其余Facet在固定的Facet之后以&#x200B;*排序类型*&#x200B;顺序列出。
- 动态Facet - [Adobe AI](https://business.adobe.com/cn/ai.html)发现与产品集和查询最相关的产品属性。 该计算会考虑整个目录的属性元数据，并在查询时确定与查询最相关的Facet。
- 价格Facet — 按价格范围返回产品。 您可以在&#x200B;[*设置*](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/settings)工作区中指定选择的数量和价格范围间隔。

## Facet标签

您可以从[彩块化工作区](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/merchandising/facets/workspace)中编辑彩块化标签。

## 排序类型

为店面呈现的所有Facet按字母顺序或计数排序。

| 排序类型 | 描述 |
|--- |--- |
| 字母 | 在店面&#x200B;*筛选器*&#x200B;列表中，Facet按字母顺序排序。 |
| 计数 | Facet也可以按在当前返回的产品集中每个Facet找到的值数排序。 |
