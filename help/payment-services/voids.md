---
title: 空洞
description: 通过撤消，您可以释放信用卡或借记卡账户中的资金，该账户已通过授权被阻止或保留，金额为购买金额。
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
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
source-wordcount: '244'
ht-degree: 0%
---
# 空洞

[!DNL Payment Services]支持Commerce现有的使事务失效的功能。 撤消释放由采购额授权持有的信用卡或借记卡帐户中的资金。 仅当尚未获取付款时，才能使事务处理失效。

* 如果您的商店[配置为](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}，则在销售点仅授权（不捕获）资金，则从您的商店购买会导致订单在Commerce管理中具有`Processing`状态。

* 您也可以[取消未开票的订单](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"}。 作为取消过程的一部分，任何未捕获的授权也会失效。

>[!NOTE]
>
>取消订单也会产生作废，但撤消订单不会触发取消。

要了解有关订单所经历的基本步骤的更多信息，请参阅核心用户指南中的[订单工作流](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"}主题。

要了解撤消功能以及如何撤消订单交易记录，请参阅核心用户指南中的[处理订单](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"}。
