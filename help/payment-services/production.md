---
title: '为生产启用 [!DNL Payment Services] '
description: 通过启用 [!DNL Payment Services] 以进行生产，完成载入流程。
exl-id: 3b1269e8-127b-47f8-9738-9722a5737c63
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 0f2e9c3a7d990a46bafc5f3b8a083436d42643b5
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# 为生产启用[!DNL Payment Services]

在执行以下操作后，您可以按照本主题中的步骤，将服务投入生产并完成[载入流程](onboard.md)：

* 仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"} [安装](install.md)付款服务扩展
* 仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"} [配置并连接](connect.md)您的实例
* [设置](sandbox.md)和[测试](test-validate.md)您的沙盒

## 将[!DNL Payment Services]设置为付款方式

在您[配置您的Commerce服务](connect.md#configure-commerce-services)并启用[沙盒测试](sandbox.md#enable-sandbox-testing)或[实时付款](#enable-live-payments)之后，您必须将[!DNL Payment Services]设置为您的付款方式。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 单击&#x200B;**[!UICONTROL Enable Payment Services]**。

   如果您尚未将[!DNL Payment Services]配置为一个或多个网站的付款方式，则此选项可见。

   您被定向到“主页”视图中的设置区域，相关选项已展开(**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Settings]_)，您可以在其中启用[!DNL Payment Services]选项作为[付款方式](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods){target="_blank"}。

1. 在&#x200B;_[!UICONTROL General Configuration]_中，将&#x200B;**[!UICONTROL Enable]**设置为`Yes`。
1. 将&#x200B;_[!UICONTROL Credit Card Fields]_和_[!UICONTROL PayPal payment buttons]_&#x200B;的&#x200B;**[!UICONTROL Payment Action]**&#x200B;设置为以下任一项：

   | 设置 | 描述 |
   |---|---|
   | `Authorize` | 批准购买并暂停资金。 该金额在商户将该金额“扣押”前不予提取。 |
   | `Authorize and Capture` | 批准购买，商家则“捕获”资金。 |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services]支持部分捕获。 商家可以部分捕获（开票）订单部分。 例如，您可以单独捕获每个项目，或者现在捕获一个项目，稍后捕获其余项目。

1. 单击&#x200B;**[!UICONTROL Save]**。
1. 单击&#x200B;**[!UICONTROL Go to Payment Services]**&#x200B;以定向回[!DNL Payment Services]主页。
1. [清除您的缓存](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html)。

   应在每次配置更改后进行清除。

有关配置信用卡字段和PayPal付款按钮的详细信息，请参阅[配置付款服务](settings.md)。

## 完成商户入门

使您的商店启用Payment Services的下一步是完成实时上线。

根据您运营的国家/地区和首选付款体验，Payment Services提供&#x200B;[**高级**（完全支持）和&#x200B;**标准**（快速结帐）付款选项](../payment-services/payments-options.md#standard-vs-advanced-payments-experience)和登录流程。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 单击&#x200B;**[!UICONTROL Live onboarding]**。

   如果您尚未完成[!DNL Payment Services]的实时载入，则此选项可见。

1. 在&#x200B;_选择国家/地区_&#x200B;模式中，选择您运营的国家/地区。

   付款服务目前为[5个国家/地区](../payment-services/introduction.md#availability)的所有付款选项提供全面支持。 Payment Services为国家/地区列表中表示的所有其他国家/地区提供快速结账功能（付款选项的子集）。

   您从列表中选择的国家/地区将决定您可用的付款选项和登录流程 — [高级](#advanced-onboarding)（完全支持）或[标准](#standard-onboarding)（快速结帐）。

>[!TIP]
>
> 选择并继续载入选项（“标准”或“高级”）后，您必须重新完成入门，才能从初始选择进行升级或降级。

### 高级入门

此入门培训流程适用于[完全支持的国家/地区](../payment-services/introduction.md#availability)的商家。

选择国家/地区后：

1. 在出现的模式窗口中，选择&#x200B;**高级**。

   对于&#x200B;**标准**&#x200B;选项，请转到[标准载入流程](#standard-onboarding)。

1. 单击&#x200B;**继续**。
1. 使用您的PayPal帐户凭据（不是沙盒帐户凭据）_或_&#x200B;注册新的PayPal帐户，继续进行PayPal流程以获得完全支持的高级入门培训。

>[!IMPORTANT]
>
>**高级入门培训**&#x200B;要求商家[申请付款权利](#request-payments-entitlement-from-adobe)以启用实时入门培训。

### 标准载入

此标准登录流程适用于仅提供[快速结帐支持](../payment-services/introduction.md#availability)的可用国家/地区的商家。

选择国家/地区后：

1. 在出现的&#x200B;_付款服务协议_&#x200B;模式中，单击&#x200B;**付款服务协议**&#x200B;链接以查看Adobe Commerce付款服务协议。
1. 在&#x200B;_付款服务协议_&#x200B;模式中，单击&#x200B;**我接受**。
1. 继续使用PayPal流程进行快速结帐，使用您的PayPal帐户凭据（不是沙盒帐户凭据）或注册新的PayPal帐户。

>[!IMPORTANT]
>
>[Apple支付和信用卡字段](../payment-services/payments-options.md)不适用于&#x200B;**标准入门**。

## 确认电子邮件地址

1. 在管理员侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**

   _[!UICONTROL Live onboarding]_按钮不再可见，并且您看到“[!UICONTROL Live payments pending]”文本框。

   在该文本框中，系统可能还会要求您通过PayPal确认您的电子邮件地址以完成入门。

1. 如果系统提示您确认电子邮件地址，请检查从PayPal发送的确认消息的电子邮件，然后单击确认您的电子邮件地址。
1. 在管理员侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 刷新浏览器窗口。

   当您的PayPal商家注册被批准时，您应该会看到一则通知，声明您的支付系统处于沙盒模式并且不处理实时支付。

   >[!IMPORTANT]
   >
   >如果您撤销了对[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]的同意，以处理您的付款（在您的PayPal帐户设置中），则[!DNL Payment Services]无法处理您商店中的订单。 在您的Payment Services主页上，会显示有关撤销同意的警报。

## 从Adobe请求付款权利

要启用您的商店，请从Adobe请求付款权利（仅适用于[高级入门](#advanced-onboarding)）：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 单击[!DNL Payment Services]主页中的&#x200B;**[!UICONTROL Get Live Payments]**。

   ![请求授权](assets/request-entitlements.png){width="500" zoomable="yes"}

1. 完成表单。
1. 销售团队的成员将与您联系。

或者，您可以通过[business.adobe.com](https://business.adobe.com/resources/payment-services.html)向Adobe请求付款权利。

>[!IMPORTANT]
>
>在批准付款权利之前，无法访问&#x200B;**实时上线**。

## 配置定价层

获取您的[!DNL Payment Services] _商家ID_：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 在“主页”视图中，单击&#x200B;**[!UICONTROL Settings]**。 有关详细信息，请参阅[主页](payments-home.md)。
1. 选择所需的&#x200B;_商家ID_&#x200B;并将其提交给您的销售代表，销售代表将配置正确的定价层。

有关付款交易的详细信息，请参阅[第2级和第3级处理](levels-card-payment-transactions.md)。

## 启用实时支付

_生产商家ID_&#x200B;是自动生成的，并在[配置](configure-admin.md)中填充。 请勿更改或更改此ID。

启用实时支付：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。
1. 在主页上，单击页面右上角的&#x200B;**[!UICONTROL Settings]**。 有关详细信息，请参阅[主页](payments-home.md)。
1. 在&#x200B;_[!UICONTROL General Configuration]_分区中，将&#x200B;**[!UICONTROL Payment mode]**设置为`Production`。
1. 单击&#x200B;**[!UICONTROL Save]**。
1. [清除您的缓存](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management){target="_blank"}。

   >[!IMPORTANT]
   >
   >如果不清除缓存，客户在结账期间将无法看到PayPal付款选项。

如果您导航回[!DNL Payment Services]主页，沙盒支付模式消息将不再显示，因为您现在正在处理实时支付。

有关旧版配置选项，请参阅[在管理员中配置](configure-admin.md)。

>[!IMPORTANT]
>
>如果您撤销对[!DNL Payment Services]处理付款（在您的PayPal帐户设置中）的同意，[!DNL Payment Services]无法处理您商店中的订单。 如果您希望重新启用支付处理，则必须重新完成入门培训。 在您的Payment Services主页上，会显示有关撤销同意的警报。

## 在生产环境中测试

强烈建议您在向购物者公开此功能之前，使用真正的信用卡和银行在生产环境中测试支付。

有关详细信息，请参阅[测试和验证](test-validate.md)。
