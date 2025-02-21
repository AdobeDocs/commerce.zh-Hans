---
title: 2级和3级处理
description: ' [!DNL Payment Services] 交易记录中的卡付款处理级别。'
role: Admin
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# 2级和3级处理

通过[!DNL Payment Services]提供三个级别的卡片处理：

* 级别1是最常见的，需要的信息较少，因此与级别2或级别3数据处理的交易相比，通常会产生较高的交换费用，这些数据通常与企业和购买信用卡有关。

* 对于级别2和级别3的客户，如果采用交换加(IC++)定价，且接受大量购买卡或公司卡交易的[!DNL Payment Services]客户可以通过允许[!DNL Payment Services]发送有关交易的更多信息而获得较低的处理速率。 如果该交易符合条件，则根据卡网络要求，商家可以接收针对特定交易的较低处理速率。

>[!NOTE]
>
>2级和3级定价仅适用于Visa和MasterCard交易。 American Express只提供第2级定价。 Discover不提供2级或3级定价。 有关详细信息，请参阅PayPal开发人员文档中的[付款处理](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank}。

查看[什么是IC++?PayPal开发人员文档中的](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank}以了解更多信息。

第2级和第3级处理数据使商家能够降低其IC++定价，前提是他们提供了关于购买的一些附加详细信息，这些细节降低了处理器风险并提供了有益方面：

* 提供这种处理数据，大型客户将支付更少的费用。

* 由于订单包含更多信息，因此客户不太可能遇到欺诈情况。

但是，Visa和万事达卡等卡网络最终会确定交易是否符合第2级或第3级处理的条件：

* 级别2数据包含附加信息，例如订单的税额、客户代码或PO编号。

* 第3层数据是有关销售的更详细信息，这有助于获得比第2层更低的交换率。 级别3数据包含的信息包括已购买项目的说明、已购买件数、已订购项目的单位以及其他特定详细信息。

[!DNL Payment Services]收集此数据并提供付款交易的详细报告。

## [!DNL Payment Services]中的级别2和级别3卡付款交易记录

要获得第2级或第3级处理的资格，商家必须发送以前的信息，不过最终决定交易在处理时符合哪个级别的卡网络。

有关详细信息，请参阅PayPal开发人员文档中的[付款处理常见问题解答](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank}。

默认情况下，[!DNL Payment Services]商家在存储级别禁用级别2和级别3处理。

如果您已经在使用IC++定价，则可以使用2级和3级处理。 要启用此功能，可以通过[命令行界面(CLI](configure-cli.md))执行此操作。

>[!IMPORTANT]
>
>如果您有任何问题，请联系您的[!DNL Payment Services]客户经理。
