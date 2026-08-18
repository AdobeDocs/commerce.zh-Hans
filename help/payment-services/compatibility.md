---
title: ' [!DNL Payment Services]的兼容性'
description: 了解 [!DNL Payment Services] 是否在您的国家/地区可用，以及它与Adobe Commerce版本是否兼容。
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
exl-id: 4bef8429-5053-424d-806a-9e8b96295b1b
TQID: https://experienceleague.adobe.com/UUD0IiEiwh0sZKMkclOJtoC2bKYcmDN3WAWD16mfad4
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 4235bf48bb5f24a076621ee5985e9e7316fcb1cc
workflow-type: tm+mt
source-wordcount: 498
ht-degree: 0%

---

# [!DNL Payment Services]的兼容性

[!DNL Payment Services]可用于[!DNL Adobe Commerce as a Cloud Service]、[!DNL Adobe Commerce on Cloud]和内部部署的所有受支持版本以及Magento Open Source。 有关特定于版本的信息，请参阅[生命周期策略](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/lifecycle-policy)页面。

## 先决条件

要使用[!DNL Payment Services]，您需要先连接Commerce实例。 **您只执行一次此连接**。

1. 如果不确定实例是否已连接，请导航到&#x200B;**系统** >服务> **Commerce服务连接器**，查看API密钥和SaaS标识符的详细信息。 如果这些值存在，则表示您的实例已连接。

1. 如果您仍需要连接实例，请查看[Commerce Services Connector](../landing/saas.md)页面上的说明。

   >[!TIP]
   >
   > 有关更多信息，请参阅我们的[Adobe Commerce服务连接器](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector)教程视频。

1. 如果您已连接实例，请导航到[入门](onboard.md)页面以了解后续步骤。

>[!IMPORTANT]
>
> 所有有权使用[!DNL Payment Services]的商家都可以使用&#x200B;**一个生产数据空间**&#x200B;和&#x200B;**两个测试数据空间**。

## 标准体验与高级[!DNL Payment Services]体验

[!DNL Payment Services]提供&#x200B;**标准** （快速结帐）和&#x200B;**高级** （完全支持）付款选项和登录流程，具体取决于您运营的国家/地区。

>[!NOTE]
>
> [!DNL Payment Services]在入门培训期间为其他[&#128279;](../payment-services/production.md#complete-merchant-onboarding)可用国家/地区提供[快速签出功能](../payment-services/payments-options.md)（付款选项的子集）。

### 哪个[!DNL Payment Services]选项适合您？

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

有关设置[!DNL Payment Services]扩展的更多信息，请参阅[连接](connect.md)。

>[!BEGINTABS]

>[!TAB 标准（快速签出）]

![支票](assets/icon-check.png) PayPal支票

![支票](assets/icon-check.png) PayPal借记卡或信用卡按钮

![检查](assets/icon-check.png)自定义签出配置

![检查](assets/icon-check.png)标准定价

![检查](assets/icon-check.png) **在200多个国家/地区可用**

[![了解详情](assets/learn-more-button.svg)](onboard.md)

>[!TAB 高级（完全支持）]

![支票](assets/icon-check.png)借记卡

![支票](assets/icon-check.png) PayPal点数

![检查](assets/icon-check.png)信用卡字段

![支票](assets/icon-check.png) Apple支付按钮

![支票](assets/icon-check.png) Google支付按钮

![支票](assets/icon-check.png) PayPal付款按钮

![选中](assets/icon-check.png) Venmo按钮

![支票](assets/icon-check.png) PayPal借记卡或信用卡按钮

![支票](assets/icon-check.png)稍后付款按钮

![检查](assets/icon-check.png)自定义签出配置

![检查](assets/icon-check.png)自定义定价

![检查](assets/icon-check.png)（L2/L3定价功能 — 仅限美国）

![check](assets/icon-check.png)在37个国家/地区可用。 澳大利亚、奥地利、比利时、保加利亚、加拿大、中国、塞浦路斯、捷克共和国、丹麦、爱沙尼亚、芬兰、法国、德国、希腊、香港、匈牙利、爱尔兰、意大利、日本、拉脱维亚、列支敦士登、立陶宛、卢森堡、马耳他、墨西哥、荷兰、挪威、波兰、葡萄牙、罗马尼亚、新加坡、斯洛伐克、斯洛文尼亚、西班牙、瑞典、联合王国、美国。 **美国（美国）、加拿大(CA)、澳大利亚(AU)、法国(FR)、英国(GB)、意大利(IT)、荷兰(NL)、德国(DE)的协议费率可用**

[![了解详情](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

有关特定于发行版和版本的详细信息，请参阅[生命周期策略](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/lifecycle-policy)和[[!DNL Payment Services] 发行说明](release-notes.md)页面。

要获取完整说明并开始入门流程，请参阅[开始使用 [!DNL Payment Services]](onboard.md)。

### 接受的信用卡和货币

[!DNL Payment Services]接受可用国家的货币。 有关设置货币汇率的详细信息，请参阅[货币配置](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration)。

有关PayPal产品和服务可用的货币和支付方法的更多信息，请参阅以下页面：

* [支持的货币文档](https://developer.paypal.com/reports/reference/supported-currencies)。

* [付款方式文档](https://developer.paypal.com/payment-methods)。
