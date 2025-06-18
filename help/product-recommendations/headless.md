---
title: Headless
description: 了解如何在headless店面中集成 [!DNL Product Recommendations] 。
exl-id: c40dac31-f87e-402a-ba50-e8aa4c1d66aa
source-git-commit: fe5f864262478d1f9e205f2cd275452594cf4675
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Headless

您可以使用[PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)或自定义前端技术（如React或Vue JS）将[!DNL Product Recommendations]集成到Headless店面。

自定义和Headless集成商应该参考这些Luma和PWA说明作为建议的实施。 可通过多种方法将产品推荐实施到Headless解决方案中，本文档并未涵盖所有场景。 集成商必须为其实施提供事件、设计和测试服务。

[!DNL Product Recommendations]需要[行为和目录数据](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html)才能运行。 在Headless实施中，目录数据同步过程保持不变，但行为数据收集需要更改。

>[!NOTE]
>
>Headless实例必须实施事件才能为产品推荐仪表板提供支持。

要将[!DNL Product Recommendations]集成到Headless店面，您必须：

1. 将行为数据发送到Adobe Sensei以分析和计算产品推荐结果。 您还可以发送其他数据以启用产品推荐[量度报告](workspace.md)。

1. 获取产品推荐结果并在页面上呈现这些结果。

您可以使用可用的SDK执行这两项操作，如下面的工作流中所述。

1. [安装](install-configure.md) [!DNL Product Recommendations]模块。

1. 安装并使用[Adobe Commerce Storefront活动SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)以触发[行为事件](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html)。

   返回[!DNL Product Recommendations]结果所需的最小事件数：

   | 事件 | 类别 |
   |--- | ---|
   | `view` | 产品 |
   | `add-to-cart` | 产品 |
   | `place-order` | 结账 |

   要启用[量度报告](workspace.md)，需要以下附加事件：

   | 事件 | 类别 |
   |--- | ---|
   | `impression-render` | 推荐单元 |
   | `view` | 推荐单元 |
   | `rec-click` | 推荐单元 |
   | `rec-add-to-cart-click` | 推荐单元（如果推荐模板中存在“添加到购物车”按钮） |

1. 触发事件时，请使用[Adobe Commerce Storefront事件收集器](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)处理事件并将它们发送到Adobe Sensei。

1. 收集行为数据后，您可以[在“管理员”中创建](create.md) [!DNL Product Recommendations]。

1. 使用[推荐SDK](https://developer.adobe.com/commerce/services/product-recommendations/)获取店面上的推荐单位。 SDK会返回必要的产品数据以呈现页面上的推荐单元。

1. 了解如何使用[`recommendations` GraphQL查询](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)返回有关给定SKU的产品推荐块的信息等。
