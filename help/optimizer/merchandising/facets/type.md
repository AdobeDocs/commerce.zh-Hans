---
title: Facet类型
description: 了解 [!DNL Adobe Commerce Optimizer]中不同类型的方面。
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: f4ab1f27-b393-45e0-94bf-c77d46e3f994
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 彩块化的类型

[!DNL Adobe Commerce Optimizer]使用各种Facet类型，只有在相关时它们才会出现在&#x200B;*筛选器*&#x200B;列表中。 可用Facet的列表会根据返回的产品而发生更改。 以下特征会影响其呈现方式和行为：

- 固定Facet — 最常用的Facet可以固定到列表顶部。 其余Facet在固定的Facet之后以&#x200B;*排序类型*&#x200B;顺序列出。
- 动态Facet - [Adobe AI](https://business.adobe.com/cn/ai.html)发现与产品集和查询最相关的产品属性。 该计算会考虑整个目录的属性元数据，并在查询时确定与查询最相关的Facet。
- 价格Facet — 按价格范围返回产品。 您可以在&#x200B;[*设置*](../../settings.md)&#x200B;工作区中指定选择的数量和价格范围间隔。

## Facet标签

您可以从[彩块化工作区](workspace.md)中编辑彩块化标签。

## 排序类型

为店面呈现的所有Facet按字母顺序或计数排序。

| 排序类型 | 描述 |
|--- |--- |
| 字母 | 在店面&#x200B;*筛选器*&#x200B;列表中，Facet按字母顺序排序。 |
| 计数 | Facet也可以按在当前返回的产品集中每个Facet找到的值数排序。 |
