---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: 使用GraphQL查询检索目录数据以提升Commerce体验。
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
TQID: https://experienceleague.adobe.com/ahutwotbB6Dxg7Tc3WMFd7S-WBMALvOYIUTmB5JKmyM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: d842311424e76b83a131ada7a2db6e3fb868acd8
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# 使用GraphQL检索目录数据 {#graphql-queries}

使用GraphQL查询从[!DNL Catalog Service]数据空间检索产品、价格和其他目录数据，并比本机产品查询更快地呈现[!DNL Adobe Commerce]店面体验。

{{aco-merchandising-services}}

[!DNL Catalog Service]提供了以下查询：

| 查询 | 描述 | 使用情况 | 限制 |
| --- | --- | --- | --- |
| `categories` | 返回类别数据。 如果指定了`subtree`输入对象，查询将返回有关子类别的详细信息。 | 在渲染店面导航和类别页面时非常有用。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/){target="_blank"} | — |
| `products` | 返回有关指定为输入的SKU的详细信息。 | 主要用于呈现产品详细信息和产品比较页面上的内容。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} | 每个请求100个SKU |
| `productSearch` | 返回符合搜索条件的产品列表。 | 用于根据搜索输入呈现搜索结果和产品列表页面。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/){target="_blank"} | 每个请求100个SKU |
| `refineProduct` | 缩小复杂产品的`products`查询结果以返回有关产品变体的特定信息。 | 当购物者选择产品选项时，可用于呈现更新的产品详细信息页面。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/){target="_blank"} | 每个请求100个SKU |
| `variants` | 返回有关产品所有变体的详细信息。 | 用于在不提交多个API请求的情况下在产品详细信息或列表页面上显示变体图像。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/){target="_blank"} | 每个请求100个SKU |

{style="table-layout:auto"}

有关使用这些查询的详细信息，请参阅[Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/){target="_blank"}。
