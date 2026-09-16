---
title: GraphQL
description: '[!DNL Live Search] GraphQL工作区允许您使用实时数据构建查询。'
exl-id: d32edf42-1fb0-40f9-89e5-798b39521b77
TQID: https://experienceleague.adobe.com/y-aM85yTrJA6JNXlJeacXEOkr8l-Bwij9gdVCgNGEqY
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 438d00c69044818382ffd22ffb68a4061c59ddbd
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%
---
# GraphQL

*GraphQL*&#x200B;工作区允许管理员使用自己的数据构建和测试GraphQL查询。

此工作区支持[`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)和[`attributeMetadata`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/attribute-metadata/)查询。

![GraphQL工作区](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "") {
    total_count
    items {
      productView {
        sku
      }
    }
    facets {
      title
    }
  }
}
```

变量：

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```
