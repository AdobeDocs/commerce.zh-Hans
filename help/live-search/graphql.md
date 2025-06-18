---
title: GraphQL
description: ' [!DNL Live Search] GraphQL工作区允许您使用实时数据构建查询。'
exl-id: d32edf42-1fb0-40f9-89e5-798b39521b77
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

*GraphQL*&#x200B;工作区允许管理员使用自己的数据构建和测试GraphQL查询。

此工作区支持[`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/)和[`attributeMetadata`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/attribute-metadata/)查询。

![GraphQL工作区](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
        name
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
