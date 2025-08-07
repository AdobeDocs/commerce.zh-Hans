---
title: 后台事件
description: 了解每个后台事件捕获哪些数据。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 65cf8150-1a14-4d4c-aa0c-1545109e4fe7
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '3618'
ht-degree: 0%

---

# [!DNL Data Connection]个后台事件

下面列出了安装[!DNL Data Connection]扩展时可用的Commerce后台事件。 这些事件收集的数据将发送到Adobe Experience Platform。 您还可以创建[自定义事件](custom-events.md)以收集未开箱即用的其他数据。

除了以下事件收集的数据之外，您还会获得由Adobe Experience Platform Web SDK提供的[其他数据](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=zh-Hans)。

后台事件包含服务器端数据。 此数据包含[订单状态](#order-status)信息，例如订单是否已下达、取消、退款、已发运或已完成。 服务器端数据还包含[客户配置文件事件](#customer-profile-events)信息，例如帐户是否已创建、更新或删除。

>[!NOTE]
>
>所有后台事件都包含[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=zh-Hans)字段，其中包括购物者的电子邮件地址（如果可用）和ECID。

## 订单状态

订单状态数据显示购物者订单的360视图。 此视图可帮助商家在开发营销活动时更好地定位或分析整个订单状态。 例如，您可以发现特定产品类别中在一年中的不同时间表现出色的趋势。 例如，在较冷的月份销售较好的冬装或购物者多年来感兴趣的某些产品颜色。 此外，订单状态数据可帮助您通过了解购物者基于先前订单的转化倾向来计算存留期客户价值。

### orderPlaced

| 描述 | XDM事件名称 |
|---|---|
| 购物者下订单时触发。 | `commerce.backofficeOrderPlaced` |

#### 从orderPlaced收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `commerce.order` | 包含有关订单的信息。 |
| `commerce.order.purchaseID` | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的。 |
| `commerce.order.payments` | 此订单的付款清单。 |
| `commerce.order.payments.paymentTransactionID` | 此付款交易记录的唯一标识符。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.order.payments.paymentType` | 此订单的付款方式。 计数，允许自定义值。 |
| `commerce.order.payments.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `commerce.order.taxAmount` | 买方作为最终付款的一部分所支付的税额。 |
| `commerce.order.discountAmount` | 指示应用于整个订单的折扣金额。 |
| `commerce.order.createdDate` | 在商业系统中创建新订单的时间和日期。 例如，`2022-10-15T20:20:39+00:00`。 |
| `commerce.order.currencyCode` | 用于订单总额的ISO 4217货币代码。 |
| `commerce.shipping` | 一个或多个产品的运输详细信息。 |
| `commerce.shipping.shippingMethod` | 客户选择的配送方式，如标准配送、加急配送、店内提货等。 |
| `commerce.shipping.shippingAmount` | 客户必须支付的运费。 |
| `commerce.shipping.currencyCode` | 用于装运总额的ISO 4217货币代码。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `commerce.billing.address` | 帐单邮寄地址。 |
| `commerce.billing.address.street1` | 主要街道级别信息、公寓号、街道号和街道名称 |
| `commerce.billing.address.street2` | 街道级别信息的附加字段。 |
| `commerce.billing.address.city` | 城市的名称。 |
| `commerce.billing.address.state` | 省/市/自治区名称。 这是自由格式字段。 |
| `commerce.billing.address.postalCode` | 位置的邮政编码。 并非所有国家/地区都提供邮政编码。 在一些国家/地区，这将仅包含邮政编码的一部分。 |
| `commerce.billing.address.country` | 政府管辖地区的名称。 除`xdm:countryCode`之外，这是一个自由形式的字段，可以包含任何语言的国家/地区名称。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `productListItems` | 订单中的一系列产品。 |
| `productListItems.id` | 此产品条目的行项目标识符。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |
| `productListItems.categories` | 包含有关产品类别的信息。 |
| `productListItems.categories.id` | 类别的唯一标识符。 |
| `productListItems.categories.name` | 类别的名称。 |
| `productListItems.categories.path` | 类别的路径。 |
| `productListItems.productImageUrl` | 产品的主图像URL。 |

### orderInvoiced

| 描述 | XDM事件名称 |
|---|---|
| 当商家提交发票以请求付款时触发。 | `commerce.backofficeOrderInvoiced` |

#### 从orderInvoiced收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `commerce.order` | 包含有关订单的信息。 |
| `commerce.order.purchaseID` | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的。 |
| `commerce.order.priceTotal` | 应用所有折扣和税费后此订单的总价。 |
| `commerce.order.currencyCode` | 用于订单总额的ISO 4217货币代码。 |
| `commerce.order.purchaseOrderNumber` | 购买者为此购买或合同分配的唯一标识符。 |
| `commerce.order.payments` | 此订单的付款清单。 |
| `commerce.order.payments.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `commerce.order.payments.paymentType` | 此订单的付款方式。 计数，允许自定义值。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.shipping` | 一个或多个产品的运输详细信息。 |
| `commerce.shipping.shippingMethod` | 客户选择的配送方式，如标准配送、加急配送、店内提货等。 |
| `commerce.shipping.shippingAmount` | 客户必须支付的运费。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `productListItems` | 订单中的一系列产品。 |
| `productListItems.id` | 此产品条目的行项目标识符。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.categories` | 包含有关产品类别的信息。 |
| `productListItems.categories.id` | 类别的唯一标识符。 |
| `productListItems.categories.name` | 类别的名称。 |
| `productListItems.categories.path` | 类别的路径。 |

### orderItemsShipped

| 描述 | XDM事件名称 |
|---|---|
| 在发运订单时触发。 | `commerce.backofficeOrderItemsShipped` |

#### 从orderItemsShipped收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `commerce.order` | 包含有关订单的信息。 |
| `commerce.order.purchaseID` | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的。 |
| `commerce.order.payments` | 此订单的付款清单。 |
| `commerce.order.payments.paymentTransactionID` | 此付款交易记录的唯一标识符。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.order.payments.paymentType` | 此订单的付款方式。 计数，允许自定义值。 |
| `commerce.order.payments.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `commerce.order.priceTotal` | 应用所有折扣和税费后此订单的总价。 |
| `commerce.order.purchaseOrderNumber` | 购买者为此购买或合同分配的唯一标识符。 |
| `commerce.order.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `commerce.order.lastUpdatedDate` | 在商业系统中上次更新特定订单记录的时间。 |
| `commerce.shipping` | 一个或多个产品的运输详细信息。 |
| `commerce.shipping.shippingMethod` | 客户选择的配送方式，如标准配送、加急配送、店内提货等。 |
| `commerce.shipping.shippingAmount` | 客户必须支付的运费。 |
| `commerce.shipping.address` | 实际配送地址。 |
| `commerce.shipping.address.street1` | 主要街道级别信息、公寓号、街道号和街道名称。 |
| `commerce.shipping.address.street2` | 可选街道信息第二行。 |
| `commerce.shipping.address.city` | 城市的名称。 |
| `commerce.shipping.address.state` | 国家的名称。 这是自由格式字段。 |
| `commerce.shipping.address.postalCode` | 位置的邮政编码。 并非所有国家/地区都提供邮政编码。 在一些国家/地区，这将仅包含邮政编码的一部分。 |
| `commerce.shipping.address.country` | 政府管辖地区的名称。 除`xdm:countryCode`之外，这是一个自由形式的字段，可以包含任何语言的国家/地区名称。 |
| `commerce.shipping.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `commerce.shipping.trackingNumber` | 装运承运人为订单项目装运提供的跟踪编号。 |
| `commerce.shipping.trackingURL` | 用于跟踪订单项目的装运状态的URL。 |
| `commerce.shipping.shipDate` | 订单中的一个或多个项目发运的日期。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `commerce.billing.address` | 帐单邮寄地址。 |
| `commerce.billing.address.street1` | 主要街道级别信息、公寓号、街道号和街道名称 |
| `commerce.billing.address.street2` | 街道级别信息的附加字段。 |
| `commerce.billing.address.city` | 城市的名称。 |
| `commerce.billing.address.state` | 省/市/自治区名称。 这是自由格式字段。 |
| `commerce.billing.address.postalCode` | 位置的邮政编码。 并非所有国家/地区都提供邮政编码。 在一些国家/地区，这将仅包含邮政编码的一部分。 |
| `commerce.billing.address.country` | 政府管辖地区的名称。 除`xdm:countryCode`之外，这是一个自由形式的字段，可以包含任何语言的国家/地区名称。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `productListItems` | 订单中的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |
| `productListItems.categories` | 包含有关产品类别的信息。 |
| `productListItems.categories.id` | 类别的唯一标识符。 |
| `productListItems.categories.name` | 类别的名称。 |
| `productListItems.categories.path` | 类别的路径。 |

### orderCanceled

| 描述 | XDM事件名称 |
|---|---|
| 购物者取消订单时触发。 | `commerce.backofficeOrderCancelled` |

#### 从orderCanceled收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `commerce.order` | 包含有关订单的信息。 |
| `commerce.order.purchaseID` | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的。 |
| `commerce.order.purchaseOrderNumber` | 购买者为此购买或合同分配的唯一标识符。 |
| `commerce.order.cancelDate` | 购物者取消订单的日期和时间。 |
| `commerce.order.lastUpdatedDate` | 在商业系统中上次更新特定订单记录的时间。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |

### orderLineItemRefreaded

| 描述 | XDM事件名称 |
|---|---|
| 当购物者为退货退款时触发。 | `commerce.backofficeCreditMemoIssued` |

#### 从orderLineItemRefreaded收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `commerce.order` | 包含有关订单的信息。 |
| `commerce.order.purchaseID` | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的。 |
| `commerce.order.lastUpdatedDate` | 在商业系统中上次更新特定订单记录的时间。 |
| `commerce.order.purchaseOrderNumber` | 购买者为此购买或合同分配的唯一标识符。 |
| `commerce.refunds` | 此订单的退款列表。 |
| `commerce.refunds.transactionID` | 此退款的唯一标识符。 |
| `commerce.refunds.refundAmount` | 退款的值。 |
| `commerce.refunds.refundPaymentType` | 此订单的付款方式。 计数，允许自定义值。 |
| `commerce.refunds.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `productListItems` | 订单中的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |
| `productListItems.categories` | 包含有关产品类别的信息。 |
| `productListItems.categories.id` | 类别的唯一标识符。 |
| `productListItems.categories.name` | 类别的名称。 |
| `productListItems.categories.path` | 类别的路径。 |

### orderItemsReturnInitiated

| 描述 | XDM事件名称 |
|---|---|
| 购物者请求返回项目时触发。 | `commerce.backofficeOrderItemsReturnInitiated` |

#### 从orderItemsReturnInitiated收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `commerce.order` | 包含有关订单的信息。 |
| `commerce.order.purchaseID` | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的。 |
| `commerce.order.returns` | 此订单的RMA（退货授权）信息。 |
| `commerce.order.returns.returnID` | 此RMA（退货授权）的唯一标识符。 |
| `commerce.order.returns.returnStatus` | RMA（退货授权）的状态，如“待定”、“已关闭”等。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `productListItems` | 订单中的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |
| `productListItems.categories` | 包含有关产品类别的信息。 |
| `productListItems.categories.id` | 类别的唯一标识符。 |
| `productListItems.categories.name` | 类别的名称。 |
| `productListItems.categories.path` | 类别的路径。 |
| `productListItems.returnItem` | 此物料的RMA（退货授权）信息。 |
| `productListItems.returnItem.returnStatus` | 返回项目的状态，如“待定”、“已批准”等。 |
| `productListItems.returnItem.returnReason` | 要求返回此项目的原因。 |
| `productListItems.returnItem.returnItemCondition` | 请求返回的项目的条件。 |
| `productListItems.returnItem.returnResolution` | 返回项目的请求解决方法，如退款、交换等。 |
| `productListItems.returnItem.returnQuantityRequested` | 购物者请求返回的此项目的编号。 |
| `productListItems.returnItem.returnQuantityAuthorized` | 授权退回的此项目的编号。 |
| `productListItems.returnItem.eturnQuantityReceived` | 收到的返回项目数。 |
| `productListItems.returnItem.returnQuantityApproved` | 返回完全完成并批准的此项目的编号。 |

### orderItemReturnCompleted

| 描述 | XDM事件名称 |
|---|---|
| 当购物者请求返回的项完成时触发。 | `commerce.backofficeOrderItemsReturnCompleted` |

#### 从orderItemReturnCompleted收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `commerce.order` | 包含有关订单的信息。 |
| `commerce.order.purchaseID` | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的。 |
| `commerce.order.returns` | 此订单的RMA（退货授权）信息。 |
| `commerce.order.returns.returnID` | 此RMA（退货授权）的唯一标识符。 |
| `commerce.order.returns.returnStatus` | RMA（退货授权）的状态，如“待定”、“已关闭”等。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `productListItems` | 订单中的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |
| `productListItems.categories` | 包含有关产品类别的信息。 |
| `productListItems.categories.id` | 类别的唯一标识符。 |
| `productListItems.categories.name` | 类别的名称。 |
| `productListItems.categories.path` | 类别的路径。 |
| `productListItems.returnItem` | 此物料的RMA（退货授权）信息。 |
| `productListItems.returnItem.returnStatus` | 返回项目的状态，如“待定”、“已批准”等。 |
| `productListItems.returnItem.returnReason` | 要求返回此项目的原因。 |
| `productListItems.returnItem.returnItemCondition` | 请求返回的项目的条件。 |
| `productListItems.returnItem.returnResolution` | 返回项目的请求解决方法，如退款、交换等。 |
| `productListItems.returnItem.returnQuantityRequested` | 购物者请求返回的此项目的编号。 |
| `productListItems.returnItem.returnQuantityAuthorized` | 授权退回的此项目的编号。 |
| `productListItems.returnItem.eturnQuantityReceived` | 收到的返回项目数。 |
| `productListItems.returnItem.returnQuantityApproved` | 返回完全完成并批准的此项目的编号。 |

### orderShipmentCompleted

| 描述 | XDM事件名称 |
|---|---|
| 在发运完成时触发。 | `commerce.backofficeOrderShipmentCompleted` |

#### 从orderShipmentCompleted收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `commerce.order` | 包含有关订单的信息。 |
| `commerce.order.purchaseID` | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的。 |
| `commerce.order.payments` | 此订单的付款清单。 |
| `commerce.order.payments.paymentTransactionID` | 此付款交易记录的唯一标识符。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.order.payments.paymentType` | 此订单的付款方式。 计数，允许自定义值。 |
| `commerce.order.payments.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `commerce.order.taxAmount` | 买方作为最终付款的一部分所支付的税额。 |
| `commerce.order.createdDate` | 在商业系统中创建新订单的时间和日期。 例如，`2022-10-15T20:20:39+00:00`。 |
| `commerce.shipping` | 一个或多个产品的运输详细信息。 |
| `commerce.shipping.shippingMethod` | 客户选择的配送方式，如标准配送、加急配送、店内提货等。 |
| `commerce.shipping.shippingAmount` | 客户必须支付的运费。 |
| `commerce.shipping.shipDate` | 订单中的一个或多个项目发运的日期。 |
| `commerce.shipping.address` | 实际配送地址。 |
| `commerce.shipping.address.street1` | 主要街道级别信息、公寓号、街道号和街道名称。 |
| `commerce.shipping.address.street2` | 可选街道信息第二行。 |
| `commerce.shipping.address.city` | 城市的名称。 |
| `commerce.shipping.address.state` | 国家的名称。 这是自由格式字段。 |
| `commerce.shipping.address.postalCode` | 位置的邮政编码。 并非所有国家/地区都提供邮政编码。 在一些国家/地区，这将仅包含邮政编码的一部分。 |
| `commerce.shipping.address.country` | 政府管辖地区的名称。 除`xdm:countryCode`之外，这是一个自由形式的字段，可以包含任何语言的国家/地区名称。 |
| `commerce.billing.address` | 帐单邮寄地址。 |
| `commerce.billing.address.street1` | 主要街道级别信息、公寓号、街道号和街道名称 |
| `commerce.billing.address.street2` | 街道级别信息的附加字段。 |
| `commerce.billing.address.city` | 城市的名称。 |
| `commerce.billing.address.state` | 省/市/自治区名称。 这是自由格式字段。 |
| `commerce.billing.address.postalCode` | 位置的邮政编码。 并非所有国家/地区都提供邮政编码。 在一些国家/地区，这将仅包含邮政编码的一部分。 |
| `commerce.billing.address.country` | 政府管辖地区的名称。 除`xdm:countryCode`之外，这是一个自由形式的字段，可以包含任何语言的国家/地区名称。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `productListItems` | 订单中的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |
| `productListItems.categories` | 包含有关产品类别的信息。 |
| `productListItems.categories.id` | 类别的唯一标识符。 |
| `productListItems.categories.name` | 类别的名称。 |
| `productListItems.categories.path` | 类别的路径。 |

## 客户个人资料事件

从服务器端捕获的配置文件事件包括帐户信息，如`accountCreated`、`accountUpdated`和`accountDeleted`。 此数据用于帮助填充更好地定义区段或执行营销活动所需的关键客户详细信息，例如发送注册折扣优惠、帐户更改确认等。 从[店面](events.md#customer-profile-events)捕获到类似的配置文件事件。

>[!NOTE]
>
>每个客户个人资料事件还包括[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=zh-Hans)字段，其中包括系统生成的Commerce客户ID作为个人资料的主要标识符，以及用作辅助标识符的电子邮件ID。 [了解](custom-identities.md)如何创建自定义身份属性以增强客户配置文件识别。

### 帐户已创建

| 描述 | XDM事件名称 |
|---|---|
| 购物者尝试创建帐户时触发。 | `userAccount.backofficeCreateProfile` |

#### 从accountCreated

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `person` | 包含有关客户的信息。 |
| `person.name` | 包含有关客户名称的信息。 |
| `person.name.firstName` | 包含客户的名字。 |
| `person.name.lastName` | 包含客户的姓氏。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

### 帐户已更新

| 描述 | XDM事件名称 |
|---|---|
| 购物者尝试编辑帐户时触发。 | `userAccount.backofficeUpdateProfile` |

#### 从帐户收集的数据已更新

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `person` | 包含有关客户的信息。 |
| `person.name` | 包含有关客户名称的信息。 |
| `person.name.firstName` | 包含客户的名字。 |
| `person.name.lastName` | 包含客户的姓氏。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

### 帐户已删除

| 描述 | XDM事件名称 |
|---|---|
| 购物者尝试删除帐户时触发。 | `userAccount.backofficeDeleteProfile` |

#### 从帐户收集的数据已删除

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `person` | 包含有关客户的信息。 |
| `person.name` | 包含有关客户名称的信息。 |
| `person.name.firstName` | 包含客户的名字。 |
| `person.name.lastName` | 包含客户的姓氏。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
