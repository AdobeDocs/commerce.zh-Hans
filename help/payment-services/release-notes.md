---
title: '[!DNL Payment Services]发行说明'
description: 查看发行说明，了解所有 [!DNL Payment Services] 发行版本的信息。
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '4184'
ht-degree: 0%

---


# 发行说明

这些发行说明描述了[!DNL Payment Services]的初始版本，其中包括：

![新](../assets/new.svg)新功能
![已修复问题](../assets/fix.svg)修复和改进
![已知问题](../assets/bug.svg)已知问题

有关在常规功能发布版本之外发布的功能更改和修复，请查看&#x200B;_托管服务更新_&#x200B;部分。

有关即将发行的版本、产品支持以及哪些Adobe Commerce版本支持[!DNL Payment Services]扩展的详细信息，请参阅Adobe Commerce [发行计划](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/release/planning/schedule)和[产品可用性](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/release/product-availability)主题。

## 托管服务更新

这些发行说明描述了所发生以及发行的功能更改和修复，这些更改和修复超出了托管服务的常规功能发行版本。

+++托管服务更新

_2025年4月25日_

![新问题](../assets/new.svg)<!-- Issue PAY-6051 -->现在，[!DNL Payment Services]仪表板显示当前扩展版本和仪表板版本。

_2024年8月30日_

![新问题](../assets/new.svg)<!-- Issue PAY-5658 -->现在，商家可以按[交易报表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=zh-Hans)中的付款详细信息筛选交易，以获得更详细和准确的付款方式数据。

_2024年7月15日_

![新问题](../assets/new.svg)<!-- Issue PAY-5571 -->现在，商户可以在[交易报表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=zh-Hans)中按Commerce客户电子邮件筛选交易。 输入客户电子邮件以筛选该特定电子邮件的交易记录。

_2024年7月9日_

![新问题](../assets/new.svg)<!-- Issue PAY-5488 -->现在，商家可以在[交易报表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=zh-Hans)中将Commerce客户ID作为列查看，以帮助识别特定客户已进行的交易。 此外，商家还可以按此Commerce客户ID筛选关联订单的交易报表。

_2024年3月5日_

![已修复问题](../assets/fix.svg)<!-- Issue PAY-5252 -->现在，商家可以通过选择单个单元格的内容，从功能板网格中复制数据。

_2023年10月10日_

![新发行](../assets/fix.svg)<!-- Issue PAY-4888 -->现在，商家可以按[交易报表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=zh-Hans)中卡号的最后四位数筛选信用卡和借记卡交易。

_2023年7月12日_

![修复了问题](../assets/fix.svg)<!-- Issue PAY-4587 --> [!DNL Payment Services] 2.1.0版本中引入的一个问题现已得到解决，该问题阻止以前的扩展版本设置授权void。 使用任何版本[!DNL Payment Services]的商家都可以使授权无效。

_2023年6月9日_

![新](../assets/new.svg)<!-- Issue PAY-4288 -->现在，商家可以[仅配置&#x200B;_个_ PayPal付款按钮](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=zh-Hans#use-only-paypal-payment-buttons)，而&#x200B;_不能_&#x200B;使用PayPal信用卡付款选项。 这允许商家提供各种支付选项，包括Venmo和PayPal支付按钮，并使用现有的信用卡提供商而不是PayPal信用卡支付选项。

![New](../assets/new.svg)<!-- Issue PAY-4050 -->为订单付款状态报告添加了[数据可视化视图](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#order-payment-status-data-visualization-view)，该视图显示在付款服务主页上。

![修复了问题](../assets/fix.svg)<!-- Issue PAY-4486-->之前，PayPal PayLater按钮未出现在英国商家的结帐中。 该问题已得到解决。

![修复了问题](../assets/fix.svg)<!-- Issue PAY-4485-->当[!DNL Payment Services]被禁用时，[!DNL Payment Services]主页现在将显示报表数据可视化视图。

_2023年1月25日_

![已知问题](../assets/bug.svg)<!-- Issue PAY-4102 --> [!DNL Payment Services]的新安装无法配置Commerce服务，导致[!DNL Payment Services]无法操作。 要解决此问题，请将[!DNL Payment Services]扩展更新到1.5.3版本。

_2022年9月12日_

![新](../assets/new.svg)<!-- Issue PAY-3705 --> `increment_id`现在可用于协调外部ERP系统中的付款。 它传播到[`custom_id` _和_ `invoice_id`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/data.html#reconcile-with-erp-system)，在PayPal webhook和付款的商家活动详细信息中均可见。

_2022年8月31日_

![修复了问题](../assets/fix.svg)<!-- Issue PAY-3629 -->当新商家首次访问[!DNL Payment Services]主页时，页面现在会立即加载以显示内容，而无需刷新页面。

_2021年8月9日_

![新](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay现已作为PayPal智能按钮提供。 此[付款选项](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-options.html?lang=zh-Hans#apple-pay-button)允许客户在其iOS或macOS设备上使用Touch ID功能选择Apple Pay。 Apple Pay使用存储在设备上的信用卡和借记卡支付凭据处理支付。

_2021年6月28日_

![新的](../assets/new.svg)<!-- Issue PAY-1720 -->商店订单争议现已在[订单付款状态报表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#view-disputes)中可用。 您可以直接从[!DNL Payment Services]导航到PayPal解决中心来解决争议。

![来自](../assets/new.svg)<!-- Issue PAY-2854 -->主页的[!DNL Payment Services]新用户体验改进包括能够在当前继承级别修改配置，以及改进了标题和导航的显示。

![新](../assets/new.svg)<!-- Issue PAY-2854 -->现在，当您从沙盒模式切换到生产模式，并尝试离开包含尚未保存的更新的视图时，您会看到警告。

![新](../assets/new.svg)<!-- Issue PAY-2761 -->您现在可以通过使用“列”设置控件显示或隐藏列，自定义在[订单付款状态报表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#show-and-hide-columns)和[付款报表](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/payouts.html#show-and-hide-columns)中显示的数据。

+++

>[!NOTE]
>
> 经常发行版本以根据需要提供新功能和修复。 发布计划未修复。

## v2.12.2

_2025年9月23日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![已修复问题](../assets/fix.svg)<!-- PAY-6275 -->已拒绝在捕获模式下不再在Commerce中创建订单的[!DNL Fastlane]个事务。

## v2.12.1

_2025年9月18日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![已修复问题](../assets/fix.svg)<!-- PAY-6164 -->现在，[!DNL Payment Services]在&#x200B;**PayPal服务器端送货回拨(SSSC)**&#x200B;中使用了可用送货方法的基本货币。

![已修复问题](../assets/fix.svg)<!-- PAY-6267 -->选择&#x200B;**店内接送(ISPU)**&#x200B;时，**收货地址**&#x200B;块在签出页面上隐藏。

![已修复问题](../assets/fix.svg)<!-- PAY-6271 -->现在，[!DNL Payment Services]在&#x200B;**客户帐户** > **存储支付方式**&#x200B;部分中显示从PayPal PayFlow保存的信用卡详细信息。

## v2.12.0

_2025年8月20日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新建](../assets/new.svg)<!-- PAY-6022 --> [Fastlane](https://experienceleague.adobe.com/zh-hans/docs/commerce/payment-services/payments-checkout/payments-options)在访客结帐期间提供更快的购买速度。

![New](../assets/new.svg)<!-- PAY-6168 -->已将[`addProductsToNewCart`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/)突变添加到[!DNL Payment Services]，以便实现更平稳的过渡和更好的购物车重用。

![新](../assets/new.svg)<!-- PAY-6169 -->已将[`setCartAsInactive`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/)突变添加到[!DNL Payment Services]以改进报价生命周期管理。

![新](../assets/new.svg)<!-- PAY-6227 -->使用PayPal结帐时，[!DNL Payment Services]将跳过订单确认弹出窗口，以加快购买流程。

![新](../assets/new.svg)<!-- PAY-6234 -->已为[稍后付款](https://experienceleague.adobe.com/zh-hans/docs/commerce/payment-services/payments-checkout/payments-options)付款选项添加了一项新功能。 现在，BNPL消息配置器提供了更大的灵活性，可以在客户结账页面上显示“稍后付款”BNPL消息。

![已修复问题](../assets/fix.svg)<!-- PAY-5505 -->现在，在产品页面中关闭Google Pay或PayPal弹出窗口时，[!DNL Payment Services]将报价设置为非活动。

![已修复问题](../assets/fix.svg)<!-- PAY-5754 --> [!DNL Payment Services]不再允许从空引号创建订单。

## v2.11.1

_2025年3月14日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复了问题](../assets/fix.svg)<!-- PAY-5849 -->修复了签出期间影响[行项目](line-items.md)的问题。 现在，[!DNL Payment Services]已改进&#x200B;**行项目**&#x200B;的结账过程可靠性。 如果您遇到类似问题，请联系您的[!DNL Payment Services]销售代表寻求帮助。

## v2.11.0

_2025年3月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本


![新](../assets/new.svg)<!-- PAY-5938 -->现在，[!DNL Payment Services]允许商家管理付款设置，以最大程度地提高业务的灵活性。 此版本改进了为商家支持的地区和品牌附加[多个PayPal帐户](https://experienceleague.adobe.com/zh-hans/docs/commerce/payment-services/configure/settings#use-multiple-paypal-accounts)的功能。 我们的销售团队可以提供入门链接，以设置您的网站和商店视图范围。

![新](../assets/new.svg)<!-- PAY-5968 -->现在，[!DNL Payment Services]使用&#x200B;**PayPal商家标识**&#x200B;和&#x200B;**PayPal商家状态**&#x200B;值更新管理员配置。 这些值使商家能够更好地了解其PayPal帐户状态。

![修复了问题](../assets/fix.svg)<!-- PAY-5816 -->通过解决在v2.9.0版本的所有订单投放中导致错误的问题，恢复了[!DNL Payment Services]中的正常订单功能。

![修复了问题](../assets/fix.svg)<!-- PAY-5825 -->修复了Apple Pay迷你购物车为登录客户使用的估计总计URL不正确的问题。 现在，[!DNL Payment Services]可确保准确的总数计算。

![修复了问题](../assets/fix.svg)<!-- PAY-5826 -->通过解决在将报价状态更改为`inactive`时导致HTTP 500错误的问题，提高了订单管理的可靠性。

![修复了问题](../assets/fix.svg)<!-- PAY-5849 -->修复了`LineItemProvider`引发的小数数量低于1的异常的问题。 现在，[!DNL Payment Services]为小数数量提供了更好的支持。

![修复了问题](../assets/fix.svg)<!-- PAY-5868 -->修复了结账过程中的礼品卡金额错误。 [!DNL Payment Services]现在可以确保在结账过程中获得准确的值。

![修复了问题](../assets/fix.svg)<!-- PAY-5911 -->解决了使用非[!DNL Payment Services]联机付款方式下订单的发货创建过程中出现的错误，提高了整体可靠性。

![已修复问题](../assets/fix.svg)<!-- PAY-5954 --> [!DNL Payment Services]现在通过解决在钱包中选择其他信用卡时Apple Pay无法下订单的问题，提供了更顺畅的结账体验。

![已修复问题](../assets/fix.svg)<!-- PAY-5971 --> 当Apple Pay失败时，[!DNL Payment Services]不再将客户重定向到订单审核页面，从而防止不必要的结账中断。

## v2.10.3

_2025年2月24日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![已修复问题](../assets/fix.svg)<!-- PAY-xxxx -->已改进整体稳定性和性能。

![已修复问题](../assets/fix.svg)<!-- PAY-xxxx -->一般改进和优化。 修复了v2.10.2中的关键错误。

## v2.10.2

_2025年2月21日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![已知问题](../assets/bug.svg)<!-- PAY-xxxx -->包含可能影响稳定性和性能的严重错误。 Adobe建议升级到v2.10.3而不是使用此版本(v2.10.2)。

## v2.10.1

_2025年2月5日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)<!-- PAY-5813 -->添加了对Adobe Commerce 2.4.8和PHP 8.4的支持。

## v2.10.0

_2024年12月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新建](../assets/new.svg)<!-- PAY-5702 --> [!DNL Payment Services]现在支持GraphQL端点以便在不购买的情况下进行保险存储，从而允许客户保存其付款方式而不完成交易。

![新建](../assets/fix.svg)<!-- PAY-5789 --> [!DNL Payment Services]现在支持[使用Google Pay的3D安全身份验证](https://experienceleague.adobe.com/zh-hans/docs/commerce-merchant-services/payment-services/security-compliance/security#3ds)，增强了商家和客户在付款交易过程中的安全性。

![修复](../assets/fix.svg)<!-- PAY-5703 --> [!DNL Payment Services]添加了[客户直接在其&#x200B;**我的帐户**](https://experienceleague.adobe.com/zh-hans/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting)中保存卡片的功能，从而改善了便利性并简化了未来的结账流程。`Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms`](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/)。

![修复](../assets/fix.svg)<!-- PAY-5762 -->修复了从产品详细信息页面(PDP)启动订单时，未在订单审核页面上应用优惠券代码的问题。

![修复](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services]现在在结账页面[上显示](https://experienceleague.adobe.com/zh-hans/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting)保险存储卡的说明和帐单地址，使客户更清楚地了解他们保存的付款方式。

![修复](../assets/fix.svg)<!-- PAY-5793 --> [!DNL Payment Services]允许商家直接从结帐页面存储存储存储电子仓库卡的帐单地址，以确保准确和完整的付款信息。

## v2.9.0

_2024年11月7日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新建](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services]现在支持Apple Pay的&#x200B;**升级SDK URL**，从而改进了使用Apple Pay的商户的集成。 此功能与macOS 14及更高版本兼容，运行早期版本的macOS的设备将不会显示此功能。

![新](../assets/new.svg)<!-- PAY-5630 -->已更新&#x200B;**结帐**、**产品**、**购物车**&#x200B;和&#x200B;**迷你购物车**&#x200B;页面，以支持Apple Pay的&#x200B;**升级SDK URL**，从而增强将Apple Pay作为付款选项提供的商户的用户体验。

![新增](../assets/new.svg)<!-- PAY-5635 -->基于Apple支付地址&#x200B;**改进了估计运费**，允许客户在结账时查看准确的运费。

![修复](../assets/fix.svg)<!-- PAY-5661 -->修复了结账时出现的各种&#x200B;**[!DNL Payment Services]问题**，提高了商家和购物者付款流程的可靠性。

![修复](../assets/fix.svg)<!-- PAY-5692 -->修复了在使用&#x200B;**智能按钮进行快速结帐**&#x200B;时，**客户的名字和姓氏**&#x200B;未添加到订单中的问题。

![修复](../assets/fix.svg)<!-- PAY-5712 -->解决了总金额为空时，商户无法&#x200B;**使用“零小计结帐”付款选项**&#x200B;完成结帐的问题。

## v2.8.1

_2024年9月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)<!-- PAY-5644 -->修复了在[!DNL Payment Services]中使用多个作用域时，SDK参数的缓存问题。 现在，每个范围的SDK配置都是单独缓存的，而不是通过单个键缓存。 这可以确保每个作用域的缓存都独立失效，从而提高管理多个作用域时的可靠性。

## v2.8.0

_2024年9月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新建](../assets/new.svg)<!-- PAY-5499 --> 在Adobe Commerce中输入[!DNL Payment Services]跟踪号码[时，](track-shipment.md)现在支持向PayPal发送跟踪号码信息。

![修复](../assets/fix.svg)<!-- PAY-5626 --> 当客户访问Commerce结帐页面时，[!DNL Payment Services]已优化商家注册表的请求流程。 以前，会针对每种支付方式(托管字段、Google Pay、Apple Pay和智能按钮)分别发出请求。 这项改进减少了调用次数，提高了结账过程中的性能和效率。

![修复](../assets/fix.svg)<!-- PAY-5645 --> 如果购物者不同意商家在结帐页面上创建自定义条款和条件，[!DNL Payment Services]现在阻止打开PayPal/Google Pay弹出窗口。

![修复](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services]已解决与PayPal门户上的行项目税细分相关的问题。 如果订单的配送成本具有与其关联的税，则该税将包含在配送成本中，并将以这种方式显示在PayPal门户网站中显示的行项目详细信息中。

## v2.7.0

_2024年8月2日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新建](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services]现在支持订单级别[的](https://experienceleague.adobe.com/zh-hans/docs/commerce-merchant-services/payment-services/payments-checkout/manage/line-items)行项数据。 此功能允许商家查看有关订单中项目的详细信息，如产品详细信息、数量和价格（包括销售税、折扣和其他相关信息）。

![新建](../assets/new.svg)<!-- PAY-5380 --> [!DNL Payment Services]改进了Admin[体验中的](https://experienceleague.adobe.com/zh-hans/docs/commerce-merchant-services/payment-services/configure/configure-admin#general-configuration)配置，让商家可以更轻松、更直观地完成入门流程。 此功能允许商家重置其[!DNL Payment Services] ID。

![新建](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services]包含[付款失败通知](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails)。 此功能会近乎实时地通知商家付款失败，因此可以通过联系购物者并潜在改进问题解决来保存订单。

![修复](../assets/fix.svg)<!-- PAY-5469 -->修复了Safari阻止&#x200B;**Google支付弹出窗口**&#x200B;的问题。 购物者现在可以在Safari上完成其Google Pay支付交易。

![修复](../assets/fix.svg)<!-- PAY-5492 -->修复了商家将自定义条款和条件添加到结账页面时出现的问题。 在[快速结帐](https://experienceleague.adobe.com/zh-hans/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options#standard-vs-advanced-payments-experience)期间，购物者现在可以接受这些条款和条件来完成结帐，而不会出现任何问题。

![修复](../assets/fix.svg)<!-- PAY-5532 -->通过&#x200B;**InstantPurchase**&#x200B;改进了店内接送(ISPU)功能。 当购物者使用&#x200B;**InstantPurchase**&#x200B;下订单时，**ISPU交付方法**&#x200B;不再显示。

![修复](../assets/fix.svg)<!-- PAY-5606 -->修复了将商人的国家/地区设置为&#x200B;**德国**&#x200B;时，**配置页面**&#x200B;国家/地区选择器中发生的问题。

## v2.6.0

_2024年6月4日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)<!-- PAY-4877 -->现在，[!DNL Payment Services]支持[L2/L3定价功能](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/levels-card-payment-transactions.html)。 此功能仅适用于已启用IC++定价的[!DNL Payment Services]客户。 如果要使用L2/L3处理[!DNL Payment Services]的数据，请与您的[!DNL Payment Services]帐户管理员联系。

![修复](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services]允许您直接从扩展启用Apple Pay，而无需下载和托管[域关联文件](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)。

## v2.5.0

_2024年4月23日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

对于Adobe Commerce版本2.4.7及更高版本，![修复](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services]现在支持[参数`--db-prefix`的](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line)Adobe Commerce准则。

## v2.4.3

_2024年4月16日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)<!-- Issue PAY-5106 -->修复了在PayPal和Adobe Commerce之间结帐时错误填充订单金额合计的问题。 现在，商家可以在下订单时确保订单金额合计正确。

## v2.4.2

_2024年4月11日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)<!-- Issue xxx -->添加了对Adobe Commerce 2.4.7的支持。

## v2.4.1

_2024年4月4日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)<!-- PAY-5322 -->修复了较新的Adobe Commerce版本存在的PCI兼容性问题。 现在，[!DNL Payment Services]适用于在Adobe Commerce中作为付款选项结帐要求。

在Adobe Commerce中正确显示![Fix](../assets/fix.svg)<!-- PAY-5323 --> PayLater和Venmo。 修复了导致管理员无法显示PayLater和Venmo切换选项的错误。

## v2.4.0

_2024年3月20日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)<!-- PAY-4868 -->商家可以通过管理员成功[在整个购买体验](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=zh-Hans)中配置Google Pay，类似于[!DNL Payment Services]中的其他付款按钮。

![新建](../assets/new.svg)<!-- PAY-4381 --> [Payment Services支持通过GraphQL进行Google Pay](https://developer.adobe.com/commerce/webapi/graphql/payment-services/)，从而允许商家在使用Google Pay付款方式时体验Headless Commerce。

![新](../assets/new.svg)<!-- PAY-4878 -->现在，已为Adobe Commerce和Magento Open Source商家捆绑了[!DNL Payment Services]基本签出功能。[!DNL Payment Services]现在可以支持在全球200个地理区域内开展业务的商家。[!DNL Payment Services]基本签出在自助服务入门中提供借记/贷记、PayPal、Venmo（如果可用）和PayLater（如果可用）选项。

![修复](../assets/fix.svg)<!-- PAY-5291 -->某些交易记录的接收付款确认可能延迟。 在这种情况下，商家现在可以获得订单的更新付款状态。 [付款服务通过检测待定交易并主动监视这些交易并在捕获待定状态时进行更新，来检测订单中付款交易](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html)的待定状态。

## v2.3.4

_2024年3月1日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)<!-- PAY-5244 -->修复了异步签出兼容性。

![修复](../assets/fix.svg)<!-- PAY-5253 -->修复了无法删除不属于[!DNL Payment Services]的保管库令牌的错误。

## v2.3.3

_2024年2月14日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)<!-- PAY-5048 -->添加了对PHP 8.3的支持

![修复](../assets/fix.svg)<!-- PAY-5048 -->修复了`is_deleted`标志的错误。 现在，订单不会由于从扩展发送的`Rejected`状态而失败。

## v2.3.2

_2024年1月26日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)<!-- PAY-5183 -->修复了REST/GraphQL性能问题。 现在，通过API获取时，信用卡按钮呈现。

## v2.3.1

_2023年12月7日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)<!-- PAY-5047 -->现在可以从以下位置获得信用卡/借记卡品牌或付款方式类型：

- 店面的客户订单页面
- 发送给购物者的订单确认电子邮件
- 从Commerce管理员的[订单详细信息视图](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html?lang=zh-Hans#view-an-order)中。

## v2.3.0

_2023年12月1日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新建](../assets/new.svg)<!-- PAY-4381 --> [Payment Services现在支持GraphQL集成](https://developer.adobe.com/commerce/webapi/graphql/payment-services/)。 由于GraphQL支持PayPal支付按钮、托管字段和Apple Pay，因此[!DNL Payment Services]现在支持Headless Commerce设置。

## v2.2.1

_2023年9月27日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复了问题](../assets/fix.svg)<!-- Issue PAY-4870 -->修复了在使用最新版本发送扩展版本时，Storefront中正确填充新标头属性的问题。 以前，在`1.3.0`版本的Commerce Services连接器中，您无法从`User-Agent header`扩展扩展[!DNL Payment Services]。

## v2.2.0

_2023年8月30日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![New](../assets/new.svg)<!-- PAY-4638 -->添加了[与Signifyd](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security-compliance/fraud-protection.html?lang=zh-Hans)的集成，后者提供自动防欺诈服务。

![新建](../assets/new.svg)<!-- PAY-3981 --> [已将Apple Pay提升为单独的付款选项](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=zh-Hans#apple-pay-button)，位于PayPal付款按钮之外，以提高购物者对付款选项的可见性，并允许商家控制Apple Pay的放置和样式。

![新](../assets/new.svg)<!-- PAY-4002 -->改进了信用卡字段结账的用户体验，包括样式改进，如添加付款图标，以降低购物者的认知负荷并提高转化率。

![新](../assets/new.svg)<!-- PAY-4002 -->添加的功能允许商家[对其付款选项排序](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=zh-Hans#payment-buttons)以优先处理某些付款选项。 此功能可提高结帐对话率。

![新](../assets/new.svg)<!-- PAY-4035 -->商家现在可以使用[管理主页上的新](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=zh-Hans)交易报告[!DNL Payment Services]有效地监控其商店的运行状况并识别任何交易问题。 此报表还会提供有关交易授权率和负交易趋势的数据。

## v2.1.0

_2023年6月9日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)<!-- Issue xxx -->添加了对Adobe Commerce 2.4.7-beta1的支持。

![新](../assets/new.svg)<!-- Issue xxx -->在下列国家/地区和相关货币中添加了[可用性](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=zh-Hans#availability)：澳大利亚、法国、英国。

![新](../assets/new.svg)<!-- Issue PAY-4296 -->添加了[针对管理员角色的扩展资源](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=zh-Hans#configure-roles)，以确保管理员用户可以创建和管理客户的订单，并可以在“销售”菜单中看到[!DNL Payment Services]。

![新](../assets/new.svg)<!-- Issue PAY-4236 -->已添加[在结账过程中发生错误的订单的自动失效](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/checkout.html?lang=zh-Hans#order-auto-voided-if-error)。

![新建](../assets/new.svg)<!-- Issue PAY-4183 -->创建了[在结帐页上显示信用卡/借记卡付款选项按钮](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=zh-Hans#debit-or-credit-card-button)的功能。

## v2.0.0

_2023年3月10日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)<!-- Issue PAY-4152 -->添加了对PHP 8.2和Adobe Commerce 2.4.6的支持。与PHP 7.x不兼容。

## v1.6.1

_2023年3月10日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg)<!-- Issue PAY-4226 -->修复了阻止新[!DNL Payment Services]商家在Admin中使用签出功能的问题。[!DNL Payment Services]以前使用过对于新客户不存在的Commerce客户ID。

![修复](../assets/fix.svg)<!-- Issue PAY-4205 -->修复了在使用[PayPal选项](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=zh-Hans#paypal-smart-buttons)结帐时，导致指定的送货地址状态被默认税务设置中的状态替换的问题。 现在，客户可以将他们的订单发往商户税务设置中配置为默认状态的状态以外的其他状态。

![修复](../assets/fix.svg)<!-- Issue PAY-4202 -->修复了阻止客户使用[付款操作`Authorize and Capture`为商店](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html?lang=zh-Hans#set-payment-services-as-payment-method)使用卡保险存储完成购买或删除保险存储付款方法的问题。 以前，当客户尝试使用或修改其保险存储信用卡时，会出现“Provider Vault ID未找到”错误。

## v1.6.0

_2023年2月17日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![新](../assets/new.svg)<!-- Issue PAY-3540 -->已添加针对在欧盟(EU)和英国进行交易的商家的[PCI 3DS合规性功能](security.md#3ds)。 这一额外的安全层要求购买者使用其信用卡发行商进行身份验证，有助于防止在线欺诈，并且是欧盟(EU)合规条例的必备要求。

![新](../assets/new.svg)<!-- Issue PAY-3609 -->添加了[在Admin](vaulting.md#use-vaulting-in-the-admin)中启用卡保险存储的功能。 这允许商家使用他们存储的支付方式在管理员中为客户创建订单。

## v1.5.4

_2023年1月29日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![修复了问题](../assets/fix.svg)<!-- Issue PAY-4110 -->修复了阻止购买者使用产品页面、迷你购物车和购物车上的付款按钮下达订单的问题。 买家现在可以成功完成订单。

## v1.5.3

_2023年1月25日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![已修复问题](../assets/fix.svg)<!-- Issue PAY-4102 -->已发布对向后不兼容的已知问题的修复。 此版本将服务ID扩展版本锁定到最新稳定版本，从而重新启用新的[!DNL Payment Services]安装以配置Commerce服务。

## v1.5.2

_2022年12月22日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![修复了问题](../assets/fix.svg)<!-- Issue PAY-3992 -->在拒绝付款方式时改进了[!DNL Payment Services]中的开票。

![修复了问题](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services]现在可以正确显示商户使用[Fire Checkout的](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank}自定义模板进行结帐页面的PayPal付款按钮。 以前，微型画间歇性地显示按钮。

## v1.5.1

_2022年11月23日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![New](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services]现在在用户代理标头中包含版本号，以便请求可以跟踪、过滤或弃用未使用的端点。

![修复了问题](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services]现在，当使用付款按钮从产品页面下订单时，可以正确显示订单数据。

## v1.5.0

_2022年11月18日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![新](../assets/new.svg)<!-- Issue PAY-3880 -->购物者现在可以在结账时[保管库（保存）其信用卡信息](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html?lang=zh-Hans)，以便稍后为同一商家帐户内的同一商店或其他商店购买时使用。

![新](../assets/new.svg)<!-- Issue PAY-3950 -->商家现在可以为其商店启用[即时购买Commerce功能](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html?lang=zh-Hans)，以便购物者可以（使用[保险存储信用卡信息](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html?lang=zh-Hans)）加快结帐速度。

## v1.4.1

_2022年10月14日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![修复](../assets/fix.svg)<!-- Issue PAY-3766 -->当客户的付款方式被拒绝时，显示的错误消息更具描述性。 它建议客户重新输入付款信息，然后重试，尝试其他付款方式，或就拒绝的交易联系其银行。

## v1.4.0

_2022年9月30日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![新](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services]现在包括设置商家帐户以[使用多个PayPal商业帐户](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=zh-Hans#use-multiple-paypal-accounts)的功能。 这使商家能够使用不同的货币在多个国家/地区经营您的商店，或者将Adobe Commerce用于您的部分业务。

![新](../assets/new.svg)<!-- Issue PAY-3231 -->商家可以[将[!UICONTROL Soft Descriptor]](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=zh-Hans#add-soft-descriptor)添加到客户交易银行对帐单上显示的网站或单个商店视图配置中，以描述品牌、商店或产品线。

![新建](../assets/new.svg)<!-- Issue PAY-3707 --> [启用或禁用信用卡字段和PayPal付款按钮](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=zh-Hans#configure-payment-options)，以便在[!DNL Payment Services]设置中签出。

![修复了问题](../assets/fix.svg)<!-- Issue PAY-3546 -->当客户单击&#x200B;**[!UICONTROL Edit cart]**&#x200B;时，页面将重定向到购物车页面并显示更新的项目，而不是显示空购物车。

## v1.3.1

_2022年9月6日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![已修复问题](../assets/fix.svg)<!-- Issue PAY-3663 -->现在，当商户商店捕获使用非全局货币授权的订单时，捕获进程将完成，并且不显示任何错误。

## v1.3.0

_2022年8月9日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![新](../assets/new.svg)<!-- Issue PAY-XX -->一般可用性版本 — [!DNL Payment Services]现在[和 [!DNL Adobe Commerce] 版本2.4.0到2.4.5 [!DNL Magento Open Source] 支持](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/release/product-availability)。

![已修复问题](../assets/fix.svg)<!-- Issue PAY-x --> Apple Pay现在与移动和桌面上的Safari浏览器v15.5兼容。

## v1.2.0

_2022年6月29日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![已知问题](../assets/bug.svg)<!-- Issue PAY-x --> Apple Pay与移动和桌面上的Safari浏览器v15.5不兼容。 使用Safari版本15.5时，无法使用Apple Pay完成签出。

![已修复问题](../assets/fix.svg)<!-- Issue PAY-3264 -->以前，当登录用户为其帐户选择默认地址以外的账单/送货地址时，签出失败。 现在，将发送选定的账单/运送地址（而不是默认的保存地址），并成功完成结账。

![已修复问题](../assets/fix.svg)<!-- Issue PAY-3314 -->如果您禁用PayPal付款按钮以进行结帐，则不会显示任何错误。

![修复了问题](../assets/fix.svg)<!-- Issue PAY-3330 -->当来宾用户输入包含短划线的电话号码时，结帐期间付款不再失败。

![修复了问题](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 -->当Commerce Services凭据无效时，[!DNL Payment Services]现在通过在Admin的[!DNL Payment Services]主页中显示凭据错误来提醒您。

![已知问题](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services]与`commerce-data-export` v101.20及更高版本不兼容，这会使其与[[!DNL Channel manager] 扩展](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html?lang=zh-Hans)不兼容。

## v1.1.0

_2022年3月31日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![新](../assets/new.svg)<!-- Issue PAY-2127 -->一般可用性版本 — [!DNL Payment Services]现在[和 [!DNL Adobe Commerce] 版本2.4.0到2.4.4 [!DNL Magento Open Source] 支持](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/release/product-availability)。

![新](../assets/new.svg)<!-- Issue PAY-2682 --> [!DNL Payment Services]和[!DNL Adobe Commerce]的[!DNL Magento Open Source]扩展现在适用于加拿大商家。 商家可以使用[法语](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=fr#carte-de-cr%C3%A9dit-et-devises-accept%C3%A9es)或[英语](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=zh-Hans#accepted-credit-cards-and-currencies)查看付款配置。

![新建](../assets/new.svg)<!-- Issue PAY-2681 --> 对于信用卡和PayPal交易，[!DNL Payment Services]支持[加元(CAD)](introduction.md#accepted-credit-cards-and-currencies)。

![新](../assets/new.svg)<!-- Issue PAY-2680 -->商家可以[加入英语或法语的 [!DNL Payment Services]](onboard.md)扩展。

![新](../assets/new.svg)<!-- Issue PAY-2678 -->商家现在可以查看以加元(CAD)表示的[订单付款状态](order-payment-status.md)和[付款报表](payouts.md)的财务报表。

![修复的问题](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services]现在与[PHP 8.1](https://www.php.net/releases/8.1/en.php)兼容。

![修复了问题](../assets/fix.svg)<!-- Issue PAY-3017 -->改进了沙盒模式警报以在多个存储中显示正确的警报。

![已修复问题](../assets/fix.svg)<!-- Issue PAY-2742 -->您现在可以在商店视图级别启用和禁用可用的付款方法，例如Venmo。 以前，您只能为每个网站配置支付方式。

![已修复问题](../assets/fix.svg)<!-- Issue PAY-2277 -->您现在可以选择[启用或禁用单个PayPal付款按钮](configure-admin.md#payment-buttons)。

![已修复问题](../assets/fix.svg)<!-- Issue PAY-2561 -->以前删除的产品未出现在&#x200B;_审阅订单_&#x200B;页面的购物车中。

![已知问题](../assets/bug.svg)<!-- Issue PAY-2842 -->在沙盒环境中处理付款时，使用PayPal[测试信用卡交易记录](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=zh-Hans)可能失败。

## v1.0.0

_2021年11月29日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.0及更高版本

![新](../assets/new.svg)<!-- Issue PAY-2127 -->一般可用性版本 — [[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html)现在由[!DNL Adobe Commerce]和[!DNL Magento Open Source]版本2.4.0到2.4.3-p1支持。

![新](../assets/new.svg)<!-- Issue PAY-124 --> [!DNL Payment Services]和[!DNL Adobe Commerce]的[!DNL Magento Open Source]扩展可以为[[!DNL Adobe Commerce] 在云基础架构](install.md#adobe-commerce-on-cloud-infrastructure)上或[内部部署](install.md#on-premises)实例安装。 这些方法需要使用命令行接口。

![新建](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services]支持[沙盒帐户](sandbox.md)，该帐户允许商家在测试模式下评估扩展。

![新](../assets/new.svg)<!-- Issue PAY-666 -->商家可以[使用基本付款行为配置付款服务](configure-admin.md)扩展，例如利用[`Authorize and Capture`](production.md#set-payment-services-as-payment-method)在沙盒或生产环境之间切换。

![新](../assets/new.svg)<!-- Issue PAY-780 -->您的购物者可以使用[!DNL Payment Services]或通过[手动创建订单](create-order.md)结帐。

![新](../assets/new.svg)<!-- Issue PAY-1856 -->通过[订单付款状态](order-payment-status.md)和[付款报告](payouts.md)提供的综合报告可供[!DNL Payment Services]使用，以便您清楚地了解商店的订单和相关付款。

![新建](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services]支持基于总处理量的灵活分层定价，适用于任何商家。

![新](../assets/new.svg)<!-- Issue PAY-1443 -->您可以轻松[自定义](payments-options.md)扩展的PayPal付款按钮和信用卡字段的外观[!DNL Payment Services]。

![已知问题](../assets/bug.svg)<!-- Issue PAY-2473 -->在安装扩展期间使用[不正确的编辑器键](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=zh-Hans)会阻止用户使用正确的[进行](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)身份验证`MAGEID`。

![已知问题](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services]报告[不能立即同步](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html?lang=zh-Hans)。

![已知问题](../assets/bug.svg)<!-- Issue PAY-2475 -->如果您在新用户引导期间创建了[的](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html?lang=zh-Hans)PayPal沙盒帐户[!DNL Payment Services]，则无法验证该帐户。
