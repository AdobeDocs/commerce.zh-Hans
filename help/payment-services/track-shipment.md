---
title: 在[!DNL Payment Services]中跟踪您的装运
description: 自定义Paypal商家仪表板中显示的[!DNL Payment Services]装运和跟踪信息。
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
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
source-wordcount: '228'
ht-degree: 0%
---
# 在[!DNL Payment Services]中跟踪您的装运

[!DNL Payment Services]允许商家在其PayPal商家信息板中查看装运的跟踪信息。

有关Adobe Commerce的装运网格的详细信息，请参阅[装运](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank}主题。

## 如何跟踪您的装运

此功能取决于是否已对订单开票，因为PayPal必须接收`capture_id`才能处理跟踪信息。 如果商家在捕获前发运其产品，则跟踪信息不会发送到PayPal。

>[!NOTE]
>
> 建议为每个跟踪编号创建一个发运，将正确的物料与发运关联。

## 添加跟踪编号

以下说明将指导您完成使用[!DNL Payment Services]在Adobe Commerce中创建装运的过程：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Orders]**。

1. 在选定订单的&#x200B;**[!UICONTROL Action]**&#x200B;列中，单击&#x200B;**[!UICONTROL View]**。

1. 单击&#x200B;**[!UICONTROL Ship]**。

1. 向下滚动到&#x200B;**[!UICONTROL Payment & Shipping Method]**&#x200B;块并单击&#x200B;**[!UICONTROL Shipping Information]**&#x200B;中的&#x200B;**[!UICONTROL Add Tracking Number]**。

1. 设置&#x200B;**[!UICONTROL Carrier]**。

1. 要跟踪装运，请输入&#x200B;**[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Number]** 。

1. 单击&#x200B;**[!UICONTROL Submit Shipment]**。

>[!NOTE]
>
> 或者，您可以使用送货模块输入跟踪编号信息。 确保送货模块在`tracking_number`字段中保存跟踪编号信息。

### 与第三方的兼容性

通过[Commerce API](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}创建装运实体时，任何第三方扩展都与功能兼容。
