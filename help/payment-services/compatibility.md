---
title: ' [!DNL Payment Services]的兼容性'
description: 了解 [!DNL Payment Services] 是否在您的国家/地区可用，以及它与Adobe Commerce版本是否兼容。
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# [!DNL Payment Services]的兼容性

[!DNL Payment Services]可用于Adobe Commerce和Magento Open Source。 [!DNL Payment Services]现在与Adobe Commerce版本2.4.x兼容。

## 先决条件

要使用[!DNL Payment Services]，您需要先连接Commerce实例。 **您只设置一次此连接**。

1. 如果您不确定实例是否已连接，请导航到&#x200B;**系统** >服务> **Commerce服务连接器**，并在“沙盒密钥”和“生产密钥”部分查看公共API密钥值和私有API密钥值，并在“SaaS标识符”部分查看“项目”和“数据空间”字段。 如果这些值存在，则表示您的实例已连接。

1. 如果您仍需要连接实例，请查看[Commerce Services Connector](../landing/saas.md)页面上的说明。

   >[!TIP]
   >
   > 有关更多信息，请参阅我们的[Adobe Commerce服务连接器](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector)教程视频。

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

![检查](assets/icon-check.png) **在XX个国家/地区可用**

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

![check](assets/icon-check.png) **仅适用于美国(US)、加拿大(CA)、澳大利亚(AUS)。 法国(FR)、英国(UK)**

[![了解详情](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

有关特定于发行版和版本的详细信息，请参阅[生命周期策略](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=zh-Hans)和[[!DNL Payment Services] 发行说明](release-notes.md)页面。

要获取完整说明并开始入门流程，请参阅[开始使用 [!DNL Payment Services]](onboard.md)。

### 接受的信用卡和货币

[!DNL Payment Services]接受其可用的国家/地区[的货币](#availability)。 有关设置货币汇率的详细信息，请参阅[货币配置](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=zh-Hans)。

有关PayPal产品和服务可用的货币和支付方法的更多信息，请参阅以下页面：

* [支持的货币文档](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/)。

* [付款方式文档](https://developer.paypal.com/docs/checkout/payment-methods/)。
