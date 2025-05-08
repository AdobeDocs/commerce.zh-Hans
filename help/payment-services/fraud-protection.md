---
title: 重要的防欺诈功能
description: 为 [!DNL Payment Services] 启用Signifyd的自动欺诈防护。
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security, Paas, Saas
exl-id: 440296bb-a6ff-408b-8195-3027916e4f84
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 有效保护欺诈行为

您可以使用[Signifyd扩展](https://commercemarketplace.adobe.com/signifyd-module-connect.html)为[!DNL Payment Services]启用自动欺诈防护。

Adobe Commerce支持Signifyd版本5.4.0及更高版本。 [!DNL Payment Services]支持身份验证前和身份验证后签名流程。

Signifyd/[!DNL Payment Services]集成提供信用卡、借记卡、保险存储卡、通过管理员结账以及PayPal和Apple Pay支付方式的覆盖范围。 虽然部分交易细节未在支付服务与Signifyd之间共享，但Signifyd为所有支付方法提供了全面的风险覆盖，确保最大程度地保护。

请参阅[Signifyd文档](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension)，了解有关安装和配置扩展的信息。

## 入门

您必须直接与Signifyd通信以将扩展载入以与[!DNL Payment Services]一起使用 — 不需要[!DNL Payment Services]配置。 安装后，您可以在Admin中配置Signifyd扩展。 与此扩展相关的任何支持都将由Signifyd管理。

使用Signfyd登录时，您必须：

1. 联系Signid以设置新帐户。
1. 列入允许列表默认情况下，Signifyd为[](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md)，以确保Signifyd不会为其当前不支持的其他付款选项触发。 如果要禁止特定付款方式，则必须进行更改。
1. 通过Signifyd确认贝宝不会拒绝可能由Signifyd批准的订单，具体方式是通过Paypal中的商家欺诈保护设置。
1. 启用Signifyd扩展以与[!DNL Payment Services]兼容：
   * 在&#x200B;_Live_&#x200B;模式下使用[!DNL Payment Services]时，Signifyd必须处于“生产”模式。
   * 在&#x200B;_沙盒_&#x200B;模式下使用[!DNL Payment Services]时，Signifyd必须处于“测试”模式。

## 配置

由于Signifyd对您的订单执行了某些操作，因此必须配置该扩展，使其根据您为[!DNL Payment Services]设置的付款操作执行适当的操作。

这些配置选项与Payment Services和Signifyd集成不兼容：

* 当[!DNL Payment Services]配置有`Authorize`付款操作&#x200B;_且_ Signifyd处于`PostAuth`模式且&#x200B;_[!UICONTROL Decline Guarantees]_选项设置为&#x200B;**创建贷项通知单**时。

  原因： [!DNL Payment Services]创建了一个授权交易记录，表示随后尝试退款。


* [!DNL Payment Services]配置有`Authorize and Capture`付款操作&#x200B;_，且_ Signifyd处于`PostAuth`模式，且&#x200B;_[!UICONTROL Decline Guarantees]_选项设置为&#x200B;**取消订单**。

  原因： [!DNL Payment Services]创建了一个捕获事务，该事务表示Signifyd然后尝试作废。


有关[配置扩展](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension)的信息，请参阅Signifyd文档。

请参阅Signifyd文档以[了解有关订单工作流的更多信息](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works)。
