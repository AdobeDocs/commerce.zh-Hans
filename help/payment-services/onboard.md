---
title: 板载 [!DNL Payment Services]
description: 完成几个入门步骤，将您的实例与 [!DNL Payment Services] 功能连接起来。
role: User
level: Intermediate
feature: Payments, Checkout, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 载入[!DNL Payment Services]

要开始为[!DNL Adobe Commerce]和[!DNL Magento Open Source]使用[!DNL Payment Services]，您必须完成一些入门步骤，以便将您的实例与支付功能连接。

## 载入流程

此流程图显示了载入[!DNL Payment Services]的一般流程。

![载入流程](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> 对于Adobe Commerce版本2.4.7或更高版本，您可以跳过Marketplace扩展步骤，因为[!DNL Payment Services]是现成的。

完成沙盒或实时支付的入门培训后，可在Admin中从[!DNL Payment Services]访问Financial Reporting。

如果沙盒和实时支付都已载入并启用，则可以从[!DNL Payment Services]主页轻松地在这些模式之间切换。

## 先决条件

要使用[!DNL Payment Services]，您必须启用所有依赖模块，并且以下模块可用于您的实例：

* 服务连接器模块
* 服务ID模块
* API密钥

服务连接器和服务ID模块在[安装 [!DNL Payment Services]](install.md)期间自动安装。

安装完成后，如果您展开&#x200B;**[!UICONTROL Services]**—**[!UICONTROL Commerce Services Connector]**，则可以在配置设置(**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**)中看到新部分。

要了解如何创建或访问您的API密钥，请参阅[API凭据](#obtain-api-credentials)。

## 载入步骤

1. [安装 [!DNL Payment Services] 扩展](install.md#get-payment-services)。
1. [获取API凭据](connect.md#obtain-api-credentials)。
1. [将您的实例](connect.md#configure-commerce-services)连接到Commerce服务。 每个Commerce实例只能完成一次此连接。
1. [使用测试的PayPal付款处理帐户](sandbox.md#enable-sandbox-testing)设置沙盒服务（或者，如果已在其他环境中测试过功能，请转到[启用实时付款](sandbox.md#enable-live-payments)）。
1. 在沙盒模式下[将 [!DNL Payment Services] 设置为您的付款方式](production.md#set-payment-services-as-payment-method)以开始处理测试付款。
1. [请求支付权利](production.md#request-payments-entitlement-from-adobe)以启用实时上线。
1. [完成商家入门](production.md#complete-merchant-onboarding)以启用您的Commerce网站的实时付款。
1. [获取您的 [!DNL Payment Services] 商家ID](production.md#configure-pricing-tier)并将其交给销售人员以配置正确的定价层。
1. [在实时模式下启用 [!DNL Payment Services] ](production.md#enable-live-payments)以开始处理实时付款。
1. 在[沙盒](sandbox.md#test-in-sandbox-environment)和[生产](production.md#test-in-production)环境中测试付款。

>[!NOTE]
>
>如果您未在管理员（步骤3）中配置Commerce服务，则无法设置沙盒或实时支付。

## 故障排除

* [疑难解答 [!DNL Payment Services] 安装](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=zh-Hans)
* [PayPal沙盒帐户未验证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html?lang=zh-Hans)
* [延迟 [!DNL Payment Services] 报告数据](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html?lang=zh-Hans)
* 在Sandbox环境中处理付款时，[在PayPal中测试信用卡失败](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=zh-Hans)
