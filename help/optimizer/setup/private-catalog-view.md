---
title: 专用目录视图
description: 了解如何通过启用目录保护来创建专用目录视图，以便只有具有有效签名令牌的请求才能检索其产品和定价数据。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 38fa0734562a631fdcdd7510580571c5d37cb598
workflow-type: tm+mt
source-wordcount: 467
ht-degree: 0%

---

# 专用目录视图

默认情况下，[目录视图](catalog-view.md)是公用的。 在目录视图上启用目录保护以限制对包含有效签名令牌的请求的访问。

目录保护仅适用于选定的目录视图。 它不会更改视图的政策、图层或价格手册。

有关何时保护目录视图的示例，请参阅[受限访问密钥用例](restricted-access-keys.md#restricted-access-key-use-cases)。

## 了解保护边界

目录保护仅适用于启用了目录保护的目录视图。 它保护目录和搜索请求，但不更改视图的策略或价格手册，保护其他目录视图，或保护购物车、结账或订单操作。

连接的商务后端必须独立强制实施购买资格。

## 保护目录视图

开始之前，请从客户端应用程序生成的公共密钥[创建一个受限访问密钥](restricted-access-keys.md)。

1. 在目录视图创建或编辑表单上，将&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;切换到&#x200B;**[!UICONTROL Enabled]**。

1. 在&#x200B;**[!UICONTROL Restricted Access Keys]**&#x200B;下，选择最多三个[受限访问密钥](restricted-access-keys.md)以分配给此目录视图。

   ![目录视图编辑表单上启用了目录保护，并分配了受限访问密钥](../assets/catalog-view-protected.png){width="70%" zoomable="yes"}

1. 单击&#x200B;**[!UICONTROL Save catalog view]**。

   目录视图现在已受保护。 只有具有来自已分配密钥的有效签名令牌的请求才能检索其数据。

   >[!NOTE]
   >
   >最多允许五分钟以使目录保护配置更改生效。

## 验证是否强制访问

要确认专用目录视图拒绝未授权请求，请使用以下标头调用其[GraphQL端点](../get-started.md#get-instance-details)，其中带和不带签名令牌：

| 页眉 | 用途 |
| --- | --- |
| `AC-View-ID` | 要查询的目录视图。 |
| `AC-Price-Book-ID` | 要申请的价格手册。 |
| `AC-Catalog-View-Access-Token` | 已签名的JWT证明对目录视图的授权。 |

不带有效令牌的请求会返回GraphQL错误，而不是目录数据，例如：

```json
{
  "errors": [
    {
      "message": "Access key validation failed: Missing token",
      "extensions": { "x-commerce-exception": "access-key-invalid" }
    }
  ]
}
```

如果请求中带有由分配的未过期密钥签名的令牌，则会按预期返回目录数据。 有关签署JWT和调用促销API的详细信息，请参阅[开发人员文档](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication)。

## 管理受限制的访问密钥

如果[!UICONTROL Catalog Protection]已启用，并且所有分配的键都已过期，则目录视图将变得不可访问 — 依赖此目录视图的店面无法从中提供数据。 分配新的未过期密钥以恢复访问权限。 有关说明，请参阅[旋转键](restricted-access-keys.md#rotate-a-key)。

>[!IMPORTANT]
>
>通过Adobe Commerce和Adobe Commerce Optimizer Connector自动创建和管理密钥的功能尚不可用。

## 更多此类内容

- [目录视图](catalog-view.md) — 了解目录视图如何按业务结构、策略和定价组织您的产品目录。
- [受限访问密钥](restricted-access-keys.md) — 创建、分配和旋转用于为目录保护签名令牌的密钥。
