---
title: '[!DNL Adobe Commerce Optimizer Connector] Headless Storefront集成'
description: 了解如何将Headless店面与 [!DNL Adobe Commerce Optimizer Connector] GraphQL API、价格手册ID和捆绑包添加到购物车编码集成。
feature: Storefront, Integration, GraphQL
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
autotag-review: '2026-06-09T16:27:30.102Z'
TQID: 'https://experienceleague.adobe.com/Orif1rROglTQ-3ZkRj5LMF90Y-AdpfTnOgPmJXQjYgc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 13c9dae2f2f8442f2d5c7be5f6e3317b94956cf0
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 0%

---

# Headless店面集成

`CommerceAdapter`模块延伸[!DNL Adobe Commerce]以弥合Headless店面和[!DNL Adobe Commerce Optimizer]之间的间隙。 它提供了用于解析客户价格手册上下文的GraphQL查询，并强制实施[!DNL Adobe Commerce Optimizer] GraphQL API所需的捆绑包产品编码。

有关高级店面设置说明，请参阅[!DNL Adobe Commerce Optimizer Connector]概述中的[配置推销和店面](./overview.md#merchandising-storefronts)。

## GraphQL： `commerceOptimizer`查询 {#graphql-commerceoptimizer-query}

Headless店面调用`commerceOptimizer` GraphQL查询来检索当前客户会话的`priceBookId`。 在获取价格时将此值传递给[[!DNL Adobe Commerce Optimizer] GraphQL API](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api){target="_blank"}。

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

示例响应：

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

如何解析`priceBookId`：

| 会话状态 | `priceBookId` |
|-----------------------|---------------------------------------------------------------------|
| 来宾（未登录） | `websiteCode::sha1(0)`，其中`0`是来宾客户组ID |
| 已登录的客户 | `websiteCode::sha1(customerGroupId)` |

`Store`请求标头确定了网站范围，因此决定了`websiteCode`组件。 `sha1(customerGroupId)`组件与数据同步期间使用的价格簿ID公式匹配。 查看[价格手册](reference/field-mapping.md#price-books)。

>[!NOTE]
>
>如果目标目录视图启用了[!UICONTROL Catalog Protection]，请在促销API请求中与`AC-View-ID`和`AC-Price-Book-ID`一起包含签名的`AC-Catalog-View-Access-Token`标头，或者请求被拒绝。 查看[专用目录视图](../optimizer/setup/private-catalog-view.md)。

## 捆绑产品：添加到购物车格式 {#bundle-products-add-to-cart-format}

允许购物者将捆绑产品从Headless店面添加到购物车，每个所选捆绑选项仅具有`SKU`和`qty`。

每个选定或输入的选项值都必须采用base64编码，格式如下：

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

同一子SKU在所有选项中只能出现一次。

示例([!DNL JavaScript])：

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
