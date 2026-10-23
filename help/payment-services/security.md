---
title: 安全性和合规性
description: 查看您站点的安全性和合规性要求。
exl-id: 083c5a12-1d78-48b5-b9e3-612b104ce7e0
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security.html
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: d2bcc58f34af50f26d4a4f082e5b3fc30089ab58
workflow-type: tm+mt
source-wordcount: '729'
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

商家可以完成[自我评估问卷(SAQ)](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"}，这是一种自我验证工具，用于评估持卡人数据的安全性。

### 信用卡字段

使用信用卡字段，您的服务中不会传递PCI管制的数据。 您不必存储或维护这些数据，这大大减少了PCI法规遵从性顾虑。

### 3DS

PCI 3-D Secure (3DS)支持在线购买信用卡时购买者与其信用卡发行商进行身份验证。 此额外的安全层有助于防止在线欺诈，并且是欧盟(EU)合规法规要求的一部分。

[!UICONTROL Payment Services]提供3DS功能，使商家能够遵守欧盟法规，并保护客户和商家免受其商店中的欺诈活动。

如果您是欧盟或英国境内需要3DS合规性的商家，则必须在[配置管理员](configure-admin.md#credit-card-fields)中手动启用3DS（默认为`Off`）。

**[信用卡字段](configure-admin.md#credit-card-fields)**&#x200B;和&#x200B;**[[!DNL Google Pay]](configure-admin.md#google-pay)**&#x200B;均支持3DS。 每个付款方法在Admin中都有自己的3D安全身份验证设置，可以将其设置为`Always`、`When required`或`Off`。

在[!DNL Payment Services] 2.17.0或更高版本中，使用[保存的信用卡](vaulting.md)付款的购物者还可以完成需要颁发者的3DS身份验证挑战。 保存的卡不会免除发卡机构要求的身份验证的付款。

>[!IMPORTANT]
>
>3DS要求适用于企业和持卡人银行位于[欧洲经济区](https://www.efta.int/eea) (EEA)和英国的交易记录。 美国商家不需要3DS，但可以根据需要为其交易启用3DS。

商户或店员为买方下达的订单未配置3DS合规措施。 但是，如果发卡机构需要3DS，则无论[!UICONTROL Payment Services]配置如何，都无法绕过此步骤。

>[!MORELIKETHIS]
>
> * 有关详细信息，请参阅设置[&#128279;](configure-admin.md#3ds)中的3DS。
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
