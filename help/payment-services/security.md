---
title: 安全性和合规性
description: 查看您站点的安全性和合规性要求。
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce/payment-services/security.html
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# 安全性和合规性

安全性是[!DNL Payment Services]中最为关心的问题，您的[!DNL Payment Services]中没有任何私人或支付卡行业(PCI)监管信息被传递。

## Commerce安全

[!DNL Adobe Commerce]和[!DNL Magento Open Source]包含对多个安全功能的支持。

请参阅核心用户指南中的[安全性](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security){target="_blank"}，以查看安全最佳实践，并了解如何管理管理员会话和凭据、实施验证码以及管理网站限制。

## PCI合规性

支付卡行业(PCI)为通过互联网接受信用卡付款的企业制定了一系列要求。 除了维护安全的环境外，处理客户信用卡信息的商户还需要满足一些标准准则。

有关详细信息，请参阅[PCI合规性指南](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/payments/compliance-pci){target="_blank"}。

商家可以完成[自我评估问卷(SAQ)](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"}，这是用于评估持卡人数据的安全性的自我验证工具。

### 信用卡字段

使用信用卡字段，您的服务中不会传递PCI管制的数据。 您不必存储或维护这些数据，这大大减少了PCI法规遵从性顾虑。

### 3DS

PCI 3-D Secure (3DS)支持在线购买信用卡时购买者与其信用卡发行商进行身份验证。 此额外的安全层有助于防止在线欺诈，并且是欧盟(EU)合规法规要求的一部分。

[!UICONTROL Payment Services]提供3DS功能，使商家能够遵守欧盟法规，并保护客户和商家免受其商店中的欺诈活动。

如果您是欧盟或英国境内需要3DS合规性的商家，则必须在[设置](settings.md#credit-card-fields)中手动启用3DS（默认为`Off`）。

>[!IMPORTANT]
>
>3DS要求适用于企业和持卡人银行位于[欧洲经济区](https://www.efta.int/eea) (EEA)和英国的交易记录。 美国商家不需要3DS，但可以根据需要为其交易启用3DS。

商家/店员为买方下单的订单未配置3DS合规措施。

>[!MORELIKETHIS]
>
> * 有关详细信息，请参阅设置[&#128279;](settings.md#3ds)中的3DS。
> * 有关用于3DS测试的特定信用卡的更多信息，请参阅PayPal开发人员文档中的[测试卡](https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/test/)。

### 卡保险存储

当购物者[存储其信用卡信息](vaulting.md)以便将来在商店中购物时，与购物者共享最少量的信用卡信息（最后四位、卡到期日期和卡品牌）。 信用卡信息存储在支付提供商中。 当卡过期或不再需要保存信息时，可以删除该令牌，以便支付提供商不再存储信息。

有关详细信息，请参阅[信用卡保险存储](vaulting.md)。

### PayPal付款按钮

使用PayPal支付按钮，您的服务中不会传递PCI管制的数据。 您不必存储或维护这些数据，这大大减少了PCI法规遵从性顾虑。

为安全起见，PayPal在结账时不会传递账单地址 — 国家/地区、电子邮件和名称是唯一使用的账单信息。 您可以选择启用网站的PayPal签出，以联系PayPal并完成审查流程来返回完整的帐单地址。

PayPal还集成了防欺诈功能，使用机器学习帮助你打击欺诈。 有关详细信息，请参阅PayPal的[卖方保护文档](https://www.paypal.com/us/webapps/mpp/security/seller-protection)。

## 欺诈防护

您可以使用[Signifyd扩展](https://commercemarketplace.adobe.com/signifyd-module-connect.html)为付款服务启用自动欺诈防护。 有关详细信息，请参阅[表示欺诈保护](fraud-protection.md)。

PayPal在其开发人员文档中为[欺诈保护](https://www.paypal.com/us/cshelp/article/what-is-fraud-protection-help1014){target=_blank}提供了其他选项：

* 有关详细信息，请参阅[高级欺诈防护](https://www.paypal.com/us/enterprise/fraud-protection-advanced#fraud-protection-advanced){target=_blank}。
* 有关详细信息，请参阅[按存储容量使用计费保护](https://www.paypal.com/us/cshelp/article/what-is-chargeback-protection-help608){target=_blank}。
