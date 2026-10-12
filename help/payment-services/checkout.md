---
title: 在[!DNL Payment Services]中签出
description: 自定义[!DNL Payment Services]签出以符合客户的需求。
feature: Payments, Checkout, Paas, Saas
exl-id: 47df165f-2145-4e0e-b272-54b8e768cf19
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%
---

# 在[!DNL Payment Services]中签出

您可以配置Adobe Commerce [!DNL Payment Services]的结账功能，以最适合您的购物者。 [订单自动失效](#order-auto-voided-if-error)和[信用卡保险存储](#credit-card-vaulting)等功能可确保您的购物者获得流畅的用户体验。

## 出错时自动撤消的订单

如果在结账过程中发生错误，[!DNL Payment Services]会自动使订单失效/取消订单。

购物者的结帐页面上会显示一条错误消息。 消息可能有所不同。

![签出时出错](assets/user-checkout-error.png "签出时出错"){width="600" zoomable="yes"}

针对特定[订单](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/order-management/orders/orders?lang=en)，管理员中还会显示有关已取消订单的评论。

![已取消订单管理员中的订单注释](assets/admin-checkout-error.png "已取消订单管理员中的订单注释"){width="600" zoomable="yes"}

如果购物者获得了订单授权，但该订单未创建并转换为`Capture`，则该订单将自动失效。 此过程确保购物者的信用卡上不会预留任何信用，并避免在标准29天期限结束时授权失效时产生的支付提供商费用。

>[!NOTE]
>
>仅当客户使用设置为`Authorize`模式（而不是`Authorize and Capture`模式）的付款方法时，才会发生订单自动失效。

## 从产品页面中结帐

当客户使用PayPal或[!DNL Pay Later]按钮直接从产品页面签出时，只会购买当前产品页面上显示的项目。 已存在于客户购物车中的商品不会添加到结账流程中，也不会被购买。

此功能允许客户快速购买他们当前正在查看的项目，同时保留以前添加到购物车的项目。
如果客户取消订单，则当前产品页面中的项目将添加到客户的购物车。

当客户从产品页面进入结账流程时，结账页面得到简化，该视图仅显示与订单相关的数据和选项。

## 信用卡保险存储

购物者可以将其信用卡信息保存或“保存”，以便将来在网站级别（同一商家帐户内的任何商店）进行购买。

有关详细信息，请参阅[信用卡保险存储](vaulting.md)
