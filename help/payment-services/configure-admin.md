---
title: '[!DNL Payment Services]配置'
description: 安装后，您可以在商店配置管理员中配置 [!DNL Payment Services] 。
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 0%

---

# [!DNL Payment Services]配置

您可以使用“管理员”中有用的配置选项根据您的需求自定义[!DNL Payment Services]。

当您在管理员中为[!DNL Payment Services]和[!DNL Adobe Commerce]配置[!DNL Magento Open Source]时，这些配置仅适用于&#x200B;_[!UICONTROL Method]_&#x200B;的&#x200B;_[!UICONTROL General Configuration]_&#x200B;字段中设置的环境。 您在配置字段中所做的任何更改与切换&#x200B;_[!UICONTROL Method]_&#x200B;选项无关 — 如果切换方法，您的选择不会重置。

## 常规配置

您可以为存储区和[!DNL Payment Services]启用&#x200B;_[!UICONTROL Merchant Location]_，并在&#x200B;_[!UICONTROL General Configuration]_&#x200B;分区中启用沙盒测试或实时付款。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 在&#x200B;_[!UICONTROL Merchant Country]_&#x200B;中设置&#x200B;_[!UICONTROL Merchant Location]_&#x200B;字段。 如果未指定&#x200B;_[!UICONTROL Merchant Country]_，则使用常规配置中的&#x200B;_[!UICONTROL Default Country]_。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;部分以访问&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;部分。
1. 在&#x200B;_[!UICONTROL [!DNL Payment Services]]_&#x200B;部分中，展开&#x200B;_[!UICONTROL General Configuration]_&#x200B;部分。
1. 对于&#x200B;**启用**，将其设置为`Yes`以启用存储区的[!DNL Payment Services]。
1. 对于&#x200B;**方法**，如果您仍在为存储测试`Sandbox`，请将其设置为[!DNL Payment Services]；或者，如果您准备好启用实时付款，请将其设置为`Production`。
1. 在设置&#x200B;**[!UICONTROL Payment Services Sandbox ID]** Commerce服务连接器&#x200B;**[!UICONTROL Payment Services Production ID]**&#x200B;并首次访问[仪表板后，](https://experienceleague.adobe.com/zh-hans/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank}和[!DNL Payment Services]值将自动填充。 这样做以完成沙盒和/或生产环境的入门培训。 这些值将您的SaaS ID关联到[!DNL Payment Services]。

   >[!WARNING]
   >
   > 如果您需要在Commerce Services Connector中更改数据空间ID，则需要重置[!DNL Payment Services] ID。 单击&#x200B;**重置付款服务ID**&#x200B;以重置沙盒ID。 如果重置[!DNL Payment Services]沙盒ID，则必须重新载入。

1. 首次访问&#x200B;**[!UICONTROL PayPal Merchant ID]**&#x200B;仪表板后，PayPal会自动提供您的&#x200B;**[!UICONTROL PayPal Merchant Status]**&#x200B;和[!DNL Payment Services]值。
1. 对于&#x200B;**Soft Descriptor**（自定义值，显示在客户交易银行对帐单上，以便在商店/品牌/目录之间进行描述），请在文本字段中添加自定义文本（最多22个字符），替换`Soft descriptor`或现有值。
1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;保存更改。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

![特色的Adobe解决方案视图](assets/config-view-all.png){width="700" zoomable="yes"}

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
1. 要在结账页面上区分付款方法的优先级，请在`Numeric Only`字段中提供&#x200B;**[!UICONTROL Sort order]**&#x200B;值。
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
| [!UICONTROL Payment Action] | 网站 | 指定付款方式的[付款操作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=zh-Hans)。 选项： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | 商店视图 | 结账页面上指定支付方式的排序顺序。 `Numeric Only`值 |
| [!UICONTROL Show on checkout page] | 网站 | 启用或禁用结账页面上的信用卡字段。 选项： [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | 商店视图 | 启用或禁用[信用卡保险存储](vaulting.md)。 选项： [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | 商店视图 | 启用或禁用[商家在Admin](vaulting.md)中使用保管式付款方式完成客户订单的功能。 选项： [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | 网站 | 启用或禁用[3DS安全身份验证](security.md#3ds)。 选项： [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | 网站 | 启用或禁用调试模式。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Fastlane]

[[!DNL Fastlane by PayPal]](https://www.paypal.com/us/cshelp/article/what-is-fastlane-by-paypal-help1096)是一种快速而简便的联机安全付款方式。 在&#x200B;**来宾结帐**&#x200B;期间，您可以安全地存储您的卡和运送详细信息，以便将来更快地进行购买。

有关详细信息，请参阅[付款选项](payments-options.md#fastlane-button)。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;部分。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;部分中，展开&#x200B;_[!UICONTROL Fastlane]_&#x200B;部分。
1. 要启用它，请为`Yes`选择&#x200B;**[!UICONTROL Enable Fastlane]** （`No`禁用它）。

   >[!NOTE]
   >
   > 如果已启用[!UICONTROL Fastlane]，则将禁用[!UICONTROL Credit Card Fields]付款选项。

1. 对于&#x200B;**[!UICONTROL Title]**，输入文本（如果需要）以更改结帐期间显示的付款方式名称。 默认标题为`Credit Card (via Fastlane)`
1. 要[设置付款操作](production.md#set-payment-services-as-payment-method)，请选择&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**授权并捕获**。
1. 要在结账页面上区分付款方法的优先级，请在`Numeric Only`字段中提供&#x200B;**[!UICONTROL Sort order]**&#x200B;值。
1. 通过将[!UICONTROL Fastlane]字段设置为&#x200B;**[!UICONTROL Enable messaging]**，指定在Adobe Commerce中签出期间是否启用`Yes`品牌。
1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;保存更改。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Enable Fastlane] | 商店视图 | 在签出页面上启用或禁用[!DNL Fastlane]。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | 商店视图 | 在结帐期间，添加要作为此付款选项的标题显示在“付款方式”视图中的文本。 默认值为`Credit Card (via Fastlane)`。 选项： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 网站 | 指定付款方式的[付款操作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=zh-Hans)。 选项： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | 商店视图 | 结账页面上指定付款方式的排序顺序。 `Numeric Only`值 |
| [!UICONTROL Enable messaging] | 商店视图 | 指定在Adobe Commerce中签出期间是否启用[!UICONTROL Fastlane]品牌。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |

### 可选。 高级样式设置

这些可选设置可以自定义[!UICONTROL Fastlane]在您网站上的显示方式。

>[!TIP]
>
>不符合辅助功能准则的样式将还原为默认设置。

1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;部分中，导航到&#x200B;_[!UICONTROL Fastlane]_&#x200B;部分。
1. 展开&#x200B;_[!UICONTROL Advanced Style Settings (optional)]_&#x200B;部分。
1. 根据需要修改设置。
1. 单击&#x200B;**[!UICONTROL Save Config]**&#x200B;保存更改。

有关自定义的更多信息，请参阅[PayPal开发人员文档](https://developer.paypal.com/limited-release/accelerated-checkout-bt/)。

#### 根设置

这些可选设置修改了整个[!UICONTROL Fastlane]签出组件。

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Background Color] | 商店视图 | 定义组件的背景颜色。 仅`RGB`个值 |
| [!UICONTROL Border Color] | 商店视图 | 定义组件的边框颜色。 仅`RGB`个值 |
| [!UICONTROL Font Family] | 商店视图 | 设置组件的字体。 仅显示主题中可用的字体 |
| [!UICONTROL Font Size Base] | 商店视图 | 定义字体大小。 仅`px` （像素）值 |
| [!UICONTROL Padding] | 商店视图 | 设置组件中的内边距。 仅`px` （像素）值 |
| [!UICONTROL Primary Color] | 商店视图 | 定义组件的主颜色。 仅`RGB`个值 |
| [!UICONTROL Text Color] | 商店视图 | 定义组件中文本的主颜色。 仅`RGB`个值 |

#### 输入设置

这些可选设置适用于[!UICONTROL Fastlane]组件的客户输入字段。

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Background Color] | 商店视图 | 定义组件的背景颜色。 仅`RGB`个值 |
| [!UICONTROL Border Color] | 商店视图 | 定义组件的边框颜色。 仅`RGB`个值 |
| [!UICONTROL Border Radius] | 商店视图 | 定义边框的半径。 仅`px` （像素）值 |
| [!UICONTROL Border Width] | 商店视图 | 定义边框的宽度。 仅`px` （像素）值 |
| [!UICONTROL Focus Border Color] | 商店视图 | 定义组件的焦点边框颜色。 仅`RGB`个值 |
| [!UICONTROL Text Color Base] | 商店视图 | 定义组件中文本的主颜色。 仅`RGB`个值 |

## [!UICONTROL Apple Pay]

借助[!DNL Apple Pay]，商家可以在Safari中提供安全、快速且无缝的结账体验 — 每个商家帐户最多支持99个域。 “[!DNL Apple Pay]”按钮会自动填充客户的iOS或macOS设备中的付款、联系和送货信息，从而支持通过一次点按即可快速完成购买操作，这有助于提高转化率。

有关详细信息，请参阅[付款选项](payments-options.md#apple-pay-button)。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**。
1. 在左侧面板中，展开&#x200B;**[!UICONTROL Sales]**&#x200B;并选择&#x200B;**[!UICONTROL Payment Methods]**。
1. 展开&#x200B;_[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;部分。
1. 在&#x200B;_[!UICONTROL Payment Services]_&#x200B;部分中，展开&#x200B;_[!UICONTROL Apple Pay]_&#x200B;部分。
1. 对于&#x200B;**[!UICONTROL Title]**，输入文本（如果需要）以更改结帐期间显示的付款方式名称。
1. 要[设置付款操作](production.md#set-payment-services-as-payment-method)，请选择&#x200B;**[!UICONTROL Authorize]**&#x200B;或&#x200B;**[!UICONTROL Authorize and Capture]**。
1. 根据需要选择以下选项中的[!DNL Apple Pay]，指定在Adobe Commerce中启用`Yes`选项的位置：
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. 要启用调试模式，请为`Yes`选择&#x200B;**[!UICONTROL Debug Mode]** （`No`禁用它）。
1. 要保存更改，请单击&#x200B;**[!UICONTROL Save Config]** 。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

### 配置选项

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Title] | 商店视图 | 在结帐期间，添加要作为此付款选项的标题显示在“付款方式”视图中的文本。 选项： [!UICONTROL text field] |
| [!UICONTROL Payment Action] | 网站 | 指定付款方式的[付款操作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=zh-Hans)。 选项： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
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
1. [通过选择](production.md#set-payment-services-as-payment-method)或&#x200B;**[!UICONTROL Authorize]**&#x200B;设置付款操作&#x200B;**[!UICONTROL Authorize and Capture]**。
1. 根据需要选择以下选项中的[!DNL Google Pay]，指定在Adobe Commerce中启用`Yes`选项的位置：
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. 要启用&#x200B;**[!UICONTROL 3D Secure authentication]** （`Off`默认为），请选择`Always`或`When required`。
1. 要启用调试模式，请为`Yes`选择&#x200B;**[!UICONTROL Debug Mode]** （`No`禁用它）。
1. 根据需要选择&#x200B;_[!UICONTROL Google Pay]_、**[!UICONTROL Button Color]**&#x200B;和&#x200B;**[!UICONTROL Button Type]**，配置&#x200B;**[!UICONTROL Button Style]**&#x200B;按钮的外观。
1. 要设置高度，请使用&#x200B;**[!UICONTROL Button Style]**&#x200B;中定义的高度默认值。
1. 要保存更改，请单击&#x200B;**[!UICONTROL Save Config]** 。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

### 配置选项

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Title] | 商店视图 | 指定在结帐期间在“付款方式”视图中为此付款选项显示的文本标签。 选项： `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | 网站 | 指定付款方式的[付款操作](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=zh-Hans)。 选项： `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
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
1. 要在结账页面上区分付款方法的优先级，请在`Numeric Only`字段中提供&#x200B;**[!UICONTROL Sort order]**&#x200B;值。
1. 要启用/禁用[稍后付费消息](payments-options.md#pay-later-button)，请为`Yes`选择`No`/**[!UICONTROL Display Pay Later Message]**。

   * 如果启用[稍后付费消息](payments-options.md#pay-later-button)，则会显示&#x200B;**[!UICONTROL Configure Messaging]**&#x200B;模式按钮，以便您可以设置&#x200B;**[!UICONTROL PayPal Pay Later messaging]**&#x200B;的样式。

1. 根据需要选择以下选项中的`Yes`，指定在Adobe Commerce中启用PayPal付款按钮的位置：
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. 要启用Venmo作为付款选项，请为`Yes`选择&#x200B;**[!UICONTROL Venmo Enabled]**。
1. 要启用信用卡和借记卡作为付款选项（PayPal智能按钮），请为`Yes`选择&#x200B;**[!UICONTROL Credit and Debit Card Enabled]**。
1. 若要启用/禁用[PayPal稍后支付](payments-options.md#pay-later-button)付款选项，请为`Yes`选择`No`/**[!UICONTROL PayPal Pay Later Enabled]**。
1. 要启用调试模式，请为`Yes`选择&#x200B;**[!UICONTROL Debug Mode]** （`No`禁用它）。
1. 要保存更改，请单击&#x200B;**[!UICONTROL Save Config]** 。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

### 配置选项

| 字段 | 范围 | 描述 |
|---|---|---|
| [!UICONTROL Title] | 商店视图 | 在结帐期间，在“付款方式”视图中添加要作为此付款选项的标题显示的文本。 选项：文本字段 |
| [!UICONTROL Payment Action] | 网站 | 指定付款方式的[付款操作](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"}。 选项： [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | 网站 | 在购物车、产品页面、迷你购物车和结帐流程中启用或禁用PayPal Pay Later消息。 选项： `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Configure Messaging] | 商店视图 | 修改PayPal Pay Later消息传递样式。 选项： `[!UICONTROL Product page]` / `[!UICONTROL Cart]` |
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
1. 要设置布局，请选择`Vertical`的`Horizontal`或&#x200B;**[!UICONTROL Layout]**
1. 要设置颜色，请从&#x200B;**[!UICONTROL Color]**&#x200B;中的可用颜色中选择。
1. 要设置形状，请选择`Rectangular`的`Pill`或&#x200B;**[!UICONTROL Shape]**。
1. 若要使用默认高度，请为`Yes`选择`No`或&#x200B;**[!UICONTROL Use Default Height]**。
1. 要设置自定义高度，请为&#x200B;**[!UICONTROL Height]**&#x200B;添加所需的像素高度。
1. 要设置标语，请为`Yes`选择`No`或&#x200B;**[!UICONTROL Tagline]**。
1. 要保存更改，请单击&#x200B;**[!UICONTROL Save Config]** 。
1. 导航到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**，然后单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

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

如果您在&#x200B;_设置_&#x200B;中更改配置，例如切换Apple Pay、Venmo或PayPal PayLater按钮，请手动刷新缓存，以便您的商店显示最新配置。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Cache Management]**。
1. 单击&#x200B;**[!UICONTROL Flush Cache]**&#x200B;以刷新所有无效缓存。

如果缓存管理表中的任何缓存类型具有`INVALIDATED`状态，则存储区可能不会显示该项目的最新配置。 刷新缓存以更新存储以显示最新配置。

为确保您的存储显示正确的配置，请定期[刷新缓存](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/tools/cache-management)。

## 卡保险存储

您可以启用一些功能，使客户能够保存其“我的帐户”中的信用卡信息，以便将来购买时使用。

您也可以在“管理员”中使用卡保险存储来完成现有客户的后续订单。

在[信用卡字段设置](#credit-card-fields)中启用或禁用卡保险存储。

有关详细信息，请参阅[信用卡保险存储](vaulting.md)。

## 3DS

3DS可保护客户和商户免受其商店中的欺诈行为之害，并实现对欧盟(EU)标准的遵守。

在[信用卡字段设置](#credit-card-fields)中启用或禁用3DS。

有关详细信息，请参阅安全性[中的](security.md#3ds)3DS。

## 使用多个PayPal帐户

在[!UICONTROL Payment Services]中，您可以在网站级别的&#x200B;**one**&#x200B;商家帐户中使用多个PayPal帐户。 例如，如果您在多个国家/地区经营您的商店（使用不同的[货币](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/site-store/currency/currency)），或者希望将Adobe Commerce用于业务的某些部分而非&#x200B;_所有_，您可以将商家帐户设置为使用多个PayPal帐户。

有关网站、商店和商店视图层次结构的详细信息，请参阅[网站、商店和视图范围](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=zh-Hans)。

有关通过CLI为多个PayPal帐户配置作用域的详细信息，请参阅[命令行配置](configure-cli.md#configure-scope-via-cli)。

您的销售代表可以为您的商家帐户创建新的[范围](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=zh-Hans#scope-settings)，并使用PayPal载入其他网站，以便您配置的任何PayPal按钮都将显示在您的网站上。 联系您的销售人员
，以获取有关为您的网站使用多个PayPal帐户的帮助。
