---
title: 旧版支付服务配置
description: 安装后，您可以在商店配置管理员中配置 [!DNL Payment Services] 。
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration
exl-id: a4da36e2-4316-42d5-ae30-cf078f440444
source-git-commit: 24622b8a20b8cd95e13a68df6e0929206ffbb06b
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 0%

---

# 旧版[!DNL Payment Services]配置

您可以使用“管理员”中有用的配置选项根据您的需求自定义[!DNL Payment Services]。

当您在管理员中为[!DNL Adobe Commerce]和[!DNL Magento Open Source]配置[!DNL Payment Services]时，这些配置仅适用于&#x200B;_[!UICONTROL General Configuration]_&#x200B;的_[!UICONTROL Method]_&#x200B;字段中设置的环境。 您在配置字段中所做的任何更改与切换&#x200B;_[!UICONTROL Method]_&#x200B;选项无关 — 如果切换方法，您的选择不会重置。

## 常规配置

您可以为存储区和&#x200B;_[!UICONTROL Merchant Location]_&#x200B;启用[!DNL Payment Services]，并在&#x200B;_[!UICONTROL General Configuration]_&#x200B;分区中启用沙盒测试或实时付款。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 在&#x200B;_[!UICONTROL Merchant Location]_&#x200B;中设置&#x200B;_[!UICONTROL Merchant Country]_&#x200B;字段。 如果未指定&#x200B;_[!UICONTROL Merchant Country]_，则使用常规配置中的&#x200B;_[!UICONTROL Default Country]_。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;部分以访问&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;部分。
1. 在&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;部分中，展开&#x200B;_[!UICONTROL General Configuration]_&#x200B;部分。
1. 对于&#x200B;**启用**，将其设置为`Yes`以启用存储区的[!DNL Payment Services]。
1. 对于&#x200B;**方法**，如果您仍在为存储测试[!DNL Payment Services]，请将其设置为`Sandbox`；或者，如果您准备好启用实时付款，请将其设置为`Production`。
1. 在设置[Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas){target=_blank}并首次访问[!DNL Payment Services]仪表板后，**[!UICONTROL Payment Services Sandbox ID]**&#x200B;和&#x200B;**[!UICONTROL Payment Services Production ID]**&#x200B;值将自动填充。 这样做以完成沙盒和/或生产环境的入门培训。 这些值将您的SaaS ID关联到[!DNL Payment Services]。

   >[!WARNING]
   >
   > 如果您需要在Commerce Services Connector中更改数据空间ID，则需要重置[!DNL Payment Services] ID。 单击&#x200B;**重置付款服务ID**&#x200B;以重置沙盒或生产ID。 如果重置[!DNL Payment Services] ID，则必须重新载入。

1. 首次访问[!DNL Payment Services]仪表板后，PayPal会自动提供您的&#x200B;**[!UICONTROL PayPal Merchant ID]**&#x200B;和&#x200B;**[!UICONTROL PayPal Merchant Status]**&#x200B;值。
1. 对于&#x200B;**Soft Descriptor**（自定义值，显示在客户交易银行对帐单上，以便在商店/品牌/目录之间进行描述），请在文本字段中添加自定义文本（最多22个字符），替换`Soft descriptor`或现有值。
1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;保存更改。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

![特色的Adobe解决方案视图](assets/featured-adobe-solution-view.png){width="700" zoomable="yes"}

### 配置选项

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Enable] | 网站 | 为您的网站启用或禁用[!DNL Payment Services]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | 商店视图 | 为存储设置方法或环境。 选项： [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | 商店视图 | 您的沙盒商家ID，在沙盒载入期间自动生成。 |
| [!UICONTROL Payment Services Production ID] | 商店视图 | 您的生产商家ID，在生产（实时）载入期间自动生成。 |
| [!UICONTROL PayPal Merchant ID] | 商店视图 | 您在创建PayPal帐户时生成的唯一PayPal商家帐户ID。 |
| [!UICONTROL PayPal Merchant Status] | 商店视图 | 您的PayPal商家ID的状态。 |
| [!UICONTROL Soft Descriptor] | 网站或商店视图 | 向您的网站和商店视图添加软描述符，以将信息添加到描述品牌、商店或产品线的客户交易。 |

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields]付款选项为信用卡或借记卡付款方式提供简单安全的结帐。

有关详细信息，请参阅[付款选项](payments-options.md#paypal-smart-buttons)。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;部分。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;部分中，展开&#x200B;_[!UICONTROL Credit Card Fields]_&#x200B;部分。
1. 对于&#x200B;**[!UICONTROL Title]**，输入文本（如果需要）以更改结帐期间显示的付款方式名称。
1. 要[设置付款操作](production.md#set-payment-services-as-payment-method)，请选择&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**授权并捕获**。
1. 要在结账页面上区分付款方法的优先级，请在&#x200B;**[!UICONTROL Sort order]**&#x200B;字段中提供`Numeric Only`值。
1. 对于&#x200B;**[!UICONTROL Show on checkout page]**，选择`Yes`以启用签出页面上的信用卡字段。
1. 对于&#x200B;**[!UICONTROL Vault Enabled]**，选择`Yes`以启用信用卡保险存储以进行签出。
1. 对于&#x200B;**[!UICONTROL Vault Enabled in Admin]**，选择`Yes`以允许商家使用其保险存储信用卡为客户创建订单。
1. 要启用&#x200B;**[!UICONTROL 3D Secure authentication]** （`Off`默认为），请选择`Always`或`When required`。
1. 对于&#x200B;**[!UICONTROL Debug Mode]**，选择`Yes`启用调试模式，或选择`No`禁用调试模式。
1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;保存更改。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

### 配置选项

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Title] | 商店视图 | 在结帐期间，添加要作为此付款选项的标题显示在“付款方式”视图中的文本。 选项： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 网站 | 指定付款方式的[付款操作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 选项： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | 商店视图 | 结账页面上指定支付方式的排序顺序。 `Numeric Only`值 |
| [!UICONTROL Show on checkout page] | 网站 | 启用或禁用结账页面上的信用卡字段。 选项： [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | 商店视图 | 启用或禁用[信用卡保险存储](vaulting.md)。 选项： [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | 商店视图 | 启用或禁用[商家在Admin](vaulting.md)中使用保管式付款方式完成客户订单的功能。 选项： [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | 网站 | 启用或禁用[3DS安全身份验证](security.md#3ds)。 选项： [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | 网站 | 启用或禁用调试模式。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Apple Pay]

[!UICONTROL Apple Pay]付款选项允许商家向其购物者提供使用Touch ID从Safari浏览器进行购买的购买Apple Pay的购物者。 商户在每个商户帐户中最多可以添加99个域。

有关详细信息，请参阅[付款选项](payments-options.md#apple-pay-button)。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;部分。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;部分中，展开&#x200B;_[!UICONTROL Apple Pay]_&#x200B;部分。
1. 对于&#x200B;**[!UICONTROL Title]**，输入文本（如果需要）以更改结帐期间显示的付款方式名称。
1. 要[设置付款操作](production.md#set-payment-services-as-payment-method)，请选择&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**[!UICONTROL Authorize and Capture]**。
1. 根据需要选择以下选项中的`Yes`，指定在Adobe Commerce中启用[!DNL Apple Pay]选项的位置：
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. 要启用调试模式，请为&#x200B;**[!UICONTROL Debug Mode]**&#x200B;选择`Yes` （`No`禁用它）。
1. 要保存更改，请单击&#x200B;**[!UICONTROL Save Config]** 。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

### 配置选项

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Title] | 商店视图 | 在结帐期间，添加要作为此付款选项的标题显示在“付款方式”视图中的文本。 选项： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 网站 | 指定付款方式的[付款操作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 选项： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | 网站 | 在签出页面上启用或禁用[!DNL Apple Pay]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | 商店视图 | 结账页面上指定付款方式的排序顺序。 `Numeric Only`值 |
| [!UICONTROL Show buttons on product detail page] | 商店视图 | 在产品详细信息页面上启用或禁用[!DNL Apple Pay]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | 商店视图 | 在迷你购物车预览中启用或禁用[!DNL Apple Pay]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 商店视图 | 在购物车页面上启用或禁用[!DNL Apple Pay]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | 网站 | 启用或禁用调试模式。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

[!UICONTROL Google Pay]付款选项允许商家向其购物者提供Google Pay，购物者可以在自己的设备上使用Google Wallet进行购买。

有关详细信息，请参阅[付款选项](payments-options.md#google-pay-button)。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;部分。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;部分中，展开&#x200B;_[!UICONTROL Google Pay]_&#x200B;部分。
1. （可选）通过在&#x200B;**[!UICONTROL Title]**&#x200B;字段中输入新名称来更改结账期间显示的付款方法的名称。
1. [通过选择&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**[!UICONTROL Authorize and Capture]**&#x200B;设置付款操作](production.md#set-payment-services-as-payment-method)。
1. 根据需要选择以下选项中的`Yes`，指定在Adobe Commerce中启用[!DNL Google Pay]选项的位置：
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. 要启用&#x200B;**[!UICONTROL 3D Secure authentication]** （`Off`默认为），请选择`Always`或`When required`。
1. 要启用调试模式，请为&#x200B;**[!UICONTROL Debug Mode]**&#x200B;选择`Yes` （`No`禁用它）。
1. 根据需要选择&#x200B;**[!UICONTROL Button Color]**、**[!UICONTROL Button Type]**&#x200B;和&#x200B;**[!UICONTROL Button Style]**，配置&#x200B;_[!UICONTROL Google Pay]_&#x200B;按钮的外观。
1. 要设置高度，请使用&#x200B;**[!UICONTROL Button Style]**&#x200B;中定义的高度默认值。
1. 要保存更改，请单击&#x200B;**[!UICONTROL Save Config]** 。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

### 配置选项

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Title] | 商店视图 | 指定在结帐期间在“付款方式”视图中为此付款选项显示的文本标签。 选项： `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | 网站 | 指定付款方式的[付款操作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html)。 选项： `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show on checkout page] | 网站 | 在签出页面上启用或禁用[!DNL Google Pay]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | 商店视图 | 结账页面上指定付款方式的排序顺序。 `Numeric Only`值 |
| [!UICONTROL Show buttons on product detail page] | 商店视图 | 在产品详细信息页面上启用或禁用[!DNL Google Pay]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | 商店视图 | 在迷你购物车预览中启用或禁用[!DNL Google Pay]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 商店视图 | 在购物车页面上启用或禁用[!DNL Google Pay]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | 商店视图 | 启用或禁用[3D安全身份验证](security.md#3ds)。 选项： [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | 网站 | 启用或禁用调试模式。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | 商店视图 | 定义[!DNL Google Pay]按钮的颜色。 选项： `[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | 商店视图 | 定义[!DNL Google Pay]按钮的类型。 选项： `[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

有关详细信息，请参阅[Google Pay API请求对象选项](https://developers.google.com/pay/api/web/reference/request-objects)文档。

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons]付款选项可为您的客户提供简单、快速和安全的结账过程。

有关详细信息，请参阅[付款选项](payments-options.md#paypal-smart-buttons)。

配置[!DNL PayPal payment buttons]

您可以在管理员中启用和配置PayPal付款按钮付款选项：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;部分。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;部分中，展开&#x200B;_[!UICONTROL PayPal payment buttons]_&#x200B;部分。
1. 若要更改结账期间显示的付款方式名称，请编辑&#x200B;_[!UICONTROL Title]_&#x200B;字段。
1. 要[设置付款操作](production.md#set-payment-services-as-payment-method)，请选择&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**[!UICONTROL Authorize and Capture]**。
1. 要在结账页面上区分付款方法的优先级，请在&#x200B;**[!UICONTROL Sort order]**&#x200B;字段中提供`Numeric Only`值。
1. 要启用/禁用[稍后付费消息](payments-options.md#pay-later-button)，请为&#x200B;**[!UICONTROL Display Pay Later Message]**&#x200B;选择`Yes`/`No`。
1. 根据需要选择以下选项中的`Yes`，指定在Adobe Commerce中启用PayPal付款按钮的位置：
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. 要启用Venmo作为付款选项，请为&#x200B;**[!UICONTROL Venmo Enabled]**&#x200B;选择`Yes`。
1. 要启用信用卡和借记卡作为付款选项（PayPal智能按钮），请为&#x200B;**[!UICONTROL Credit and Debit Card Enabled]**&#x200B;选择`Yes`。
1. 若要启用/禁用[PayPal稍后支付](payments-options.md#pay-later-button)付款选项，请为&#x200B;**[!UICONTROL PayPal Pay Later Enabled]**&#x200B;选择`Yes`/`No`。
1. 要启用调试模式，请为&#x200B;**[!UICONTROL Debug Mode]**&#x200B;选择`Yes` （`No`禁用它）。
1. 要保存更改，请单击&#x200B;**[!UICONTROL Save Config]** 。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

### 配置选项

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Title] | 商店视图 | 在结帐期间，在“付款方式”视图中添加要作为此付款选项的标题显示的文本。 选项：文本字段 |
| [!UICONTROL Payment Action] | 网站 | 指定付款方式的[付款操作](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}。 选项： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | 网站 | 在购物车、产品页面、迷你购物车和结帐流程中启用或禁用“稍后付款”消息。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on checkout page] | 商店视图 | 在签出页面上启用或禁用[!DNL PayPal payment buttons]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on product detail page] | 商店视图 | 在产品详细信息页面上启用或禁用[!DNL PayPal payment buttons]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | 商店视图 | 在迷你购物车预览中启用或禁用[!DNL PayPal payment buttons]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | 商店视图 | 在购物车页面上启用或禁用[!DNL PayPal payment buttons]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | 商店视图 | 启用或禁用显示付款按钮的Venmo付款选项。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | 商店视图 | 启用或禁用显示付款按钮的信用卡和借记卡选项。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | 商店视图 | 启用或禁用显示付款按钮的PayPal Pay Later付款选项外观。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | 网站 | 启用或禁用调试模式。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 按钮样式

您还可以配置付款按钮的&#x200B;_[!UICONTROL Button style]_&#x200B;选项：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;部分。
1. 在&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;部分中，展开&#x200B;_[!UICONTROL PayPal Smart Button Styling]_&#x200B;部分。
1. 要设置布局，请选择&#x200B;**[!UICONTROL Layout]**&#x200B;的`Vertical`或`Horizontal`
1. 要设置颜色，请从&#x200B;**[!UICONTROL Color]**&#x200B;中的可用颜色中选择。
1. 要设置形状，请选择&#x200B;**[!UICONTROL Shape]**&#x200B;的`Rectangular`或`Pill`。
1. 若要使用默认高度，请为&#x200B;**[!UICONTROL Use Default Height]**&#x200B;选择`Yes`或`No`。
1. 要设置自定义高度，请为&#x200B;**[!UICONTROL Height]**&#x200B;添加所需的像素高度。
1. 要设置标语，请为&#x200B;**[!UICONTROL Tagline]**&#x200B;选择`Yes`或`No`。
1. 要保存更改，请单击&#x200B;**[!UICONTROL Save Config]** 。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

您还可以在付款服务主页的“设置”[&#128279;](settings.md#button-style)中配置样式为的付款按钮。

### 配置选项

| 字段 | 范围 | 描述 |
|--- |--- |--- |
| [!UICONTROL Layout] | 商店视图 | 定义Paypal付款按钮的布局样式。 选项： `[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | 商店视图 | 定义Paypal付款按钮的颜色。 选项： [!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | 商店视图 | 定义Paypal付款按钮的形状。 选项： `[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | 商店视图 | 定义PayPal付款按钮是否使用默认高度。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | 商店视图 | 定义PayPal付款按钮的高度。 默认值：无 |
| [!UICONTROL Label] | 商店视图 | 定义显示在PayPal付款按钮中的标签。 选项： `[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | 商店视图 | 启用标语。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## 刷新缓存

如果更改配置，请[手动刷新缓存](/help/payment-services/settings.md#flush-the-cache)，以便您的存储显示最新的配置设置。
