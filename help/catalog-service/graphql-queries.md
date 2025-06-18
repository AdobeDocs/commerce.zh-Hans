---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: 使用GraphQL查询检索目录数据以提升Commerce体验。
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 使用GraphQL检索目录数据 {#graphql-queries}

使用GraphQL查询从Adobe Commerce Catalog SaaS数据空间检索产品、价格和其他数据，并使用它比本机Commerce GraphQL查询更快地呈现Adobe Commerce体验。

目录服务提供以下查询：

| 查询 | 描述 | 使用情况 |
|-------|-------------|-------|
| `categories` | 返回类别数据。 如果指定了子树输入对象，查询将返回有关子类别的详细信息。 | 用于呈现店面导航和类别页面。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | 返回有关指定为输入的SKU的详细信息。 | 主要用于呈现产品详细信息和产品比较页面上的内容。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | 返回符合搜索条件的产品列表。 | 用于根据搜索输入呈现搜索结果和产品列表页面。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | 缩小针对复杂产品运行的产品查询的结果以返回有关产品变型的特定信息。 | 当购物者选择产品选项时，用于呈现更新的产品详细信息页面。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | 返回有关产品所有变体的详细信息。 | 用于在不提交多个API请求的情况下在产品详细信息或列表页面上显示变体图像。 [查看示例。](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

有关使用这些查询的详细信息，请参阅[目录服务API指南](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
