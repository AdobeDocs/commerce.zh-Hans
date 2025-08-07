---
title: 行为事件
description: 了解每个行为事件捕获的数据。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '4528'
ht-degree: 0%

---

# [!DNL Data Connection]行为事件

下面列出了安装[!DNL Data Connection]扩展时可用的Commerce行为事件。 这些事件收集的数据将发送到Adobe Experience Platform。 您还可以创建[自定义事件](custom-events.md)以收集未开箱即用的其他数据。

除了以下事件收集的数据之外，您还会获得由Adobe Experience Platform Web SDK提供的[其他数据](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html)。

行为事件在购物者浏览您的网站时收集来自他们的匿名行为数据。 您可以使用这些事件收集的数据创建针对特定购物者集的促销和促销活动。

>[!NOTE]
>
>所有行为事件都包含[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html)字段，其中包括购物者的电子邮件地址（可用时）和ECID。

## 店面活动

店面事件从购物者在网站上的交互中捕获数据，并包括[`addToCart`](#addtocart)、[`pageView`](#pageview)、[`createAccount`](#createaccount)、[`editAccount`](#editaccount)、[`startCheckout`](#startcheckout)、[`completeCheckout`](#completecheckout)、[`signIn`](#signin)、[`signOut`](#signout)等事件。 店面事件仅适用于简单且可配置的产品。

### addToCart

| 描述 | XDM事件名称 |
|---|---|
| 将产品添加到购物车时或购物车中的产品数量增加时触发。 | `commerce.productListAdds` |

#### 从addToCart收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productListAdds` | 指示是否将产品添加到购物车。 值为`1`表示已添加产品。 |
| `commerce.cart.cartID` | 标识客户购物车的唯一ID。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `productListItems` | 添加到购物车的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 产品的主图像URL。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |

### openCart

| 描述 | XDM事件名称 |
|---|---|
| 在创建新购物车时触发，即在将产品添加到空购物车时。 | `commerce.productListOpens` |

#### 从openCart收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productListOpens` | 指示是否已创建购物车。 值为`1`表示已创建购物车。 |
| `commerce.cart.cartID` | 标识客户购物车的唯一ID。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `productListItems` | 添加到购物车的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 产品的主图像URL。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |

### removeFromCart

| 描述 | XDM事件名称 |
|---|---|
| 每次删除产品或购物车中的产品数量减少时触发。 | `commerce.productListRemovals` |

#### 从removeFromCart收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productListRemovals` | 指示产品是否已从购物车中删除。 值为`1`表示产品已从购物车中删除。 |
| `commerce.cart.cartID` | 标识客户购物车的唯一ID。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `productListItems` | 添加到购物车的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 产品的主图像URL。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |

### shoppingcartView

| 描述 | XDM事件名称 |
|---|---|
| 任何购物车页面加载时触发。 | `commerce.productListViews` |

#### 从shoppingCartView收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productListViews` | 指示是否已查看产品列表。 |
| `commerce.cart.cartID` | 标识客户购物车的唯一ID。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `commerce.order` | 包含有关一个或多个产品的未决订单的信息。 |
| `commerce.order.discountAmount` | 指示应用于整个订单的折扣金额。 |
| `productListItems` | 添加到购物车的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 产品的主图像URL。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |

### pageView

| 描述 | XDM事件名称 |
|---|---|
| 任何页面加载时触发。 | `web.webpagedetails.pageViews` |

#### 从pageView收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `web.webPageDetails.pageViews` | 指示是否已加载页面。 `value`的`1`表示页面已加载。 |
| `web.webPageDetails.URL` | 网页的规范或常用URL。 这可能是用于访问页面的实际URL，将使用`Web Link`记录该URL。 |
| `web.webPageDetails.name` | 网页的规范名称。 此名称不一定是页面标题或直接与页面内容关联，但用于整理网站页面以进行分类。 |
| `web.webReferrer.URL` | 购物者在单击指向您的网站的链接之前访问过的网页的URL。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

### productPageView

| 描述 | XDM事件名称 |
|---|---|
| 任何产品页面加载时触发。 | `commerce.productViews` |

#### 从productPageView收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.productViews` | 指示是否查看了产品。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `productListItems` | 添加到购物车的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 产品的主图像URL。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |

### startCheckout

| 描述 | XDM事件名称 |
|---|---|
| 购物者单击结帐按钮时触发。 | `commerce.checkouts` |

#### 从startCheckout收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.checkouts` | 指示在结账过程中是否执行了某个操作。 |
| `commerce.cart.cartID` | 标识客户购物车的唯一ID。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `productListItems` | 添加到购物车的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.productImageUrl` | 产品的主图像URL。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |

### completeCheckout

| 描述 | XDM事件名称 |
|---|---|
| 购物者下订单时触发。 | `commerce.purchases` |

#### 从completeCheckout收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.purchases` | 指示是否已接受订单。 |
| `commerce.order` | 包含有关一个或多个产品所下订单的信息。 |
| `commerce.order.purchaseID` | 卖方为此购买或合同分配的唯一标识符。 无法保证ID是唯一的。 |
| `commerce.order.payments` | 此订单的付款清单。 |
| `commerce.order.payments.paymentTransactionID` | 此付款交易记录的唯一标识符。 |
| `commerce.order.payments.paymentAmount` | 付款的值。 |
| `commerce.order.payments.paymentType` | 此订单的付款方式。 选项为：`cash`、`credit_card`、`debit_card`、`gift_card`、`check`、`paypal`、`wire_transfer`、`credit_card_reference`、`other`。 |
| `commerce.order.payments.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `commerce.order.taxAmount` | 买方作为最终付款的一部分所支付的税额。 |
| `commerce.order.discountAmount` | 指示应用于整个订单的折扣金额。 |
| `commerce.order.createdDate` | 在商业系统中创建新订单的时间和日期。 例如，`2022-10-15T20:20:39+00:00`。 |
| `commerce.shipping` | 一个或多个产品的运输详细信息。 |
| `commerce.shipping.shippingMethod` | 客户选择的配送方式，如标准配送、加急配送、店内提货等。 |
| `commerce.shipping.shippingAmount` | 客户必须支付的运费。 |  | `shipping` | 一个或多个产品的运输详细信息。 |
| `commerce.shipping.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `personalEmail` | 个人电子邮件地址。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `productListItems` | 添加到购物车的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.productImageUrl` | 产品的主图像URL。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |

## 客户个人资料事件

从店面捕获的配置文件事件包括帐户信息，如`signIn`、`signOut`、`createAccount`和`editAccount`。 此数据用于帮助填充更好地定义区段或执行营销活动所需的关键客户详细信息，例如发送注册折扣优惠、帐户更改确认等。 从[服务器端](events-backoffice.md#customer-profile-events)捕获到类似的配置文件事件。

>[!NOTE]
>
>[了解](custom-identities.md)如何创建自定义身份属性以增强客户配置文件识别。

### 登录

| 描述 | XDM事件名称 |
|---|---|
| 购物者尝试登录时触发。 | `userAccount.login` |

>[!NOTE]
>
> 此事件在尝试特定操作时触发。 它并不表示操作成功。

#### 从登录收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `person` | 单独的操作者、联系人或所有者。 |
| `person.accountID` | 捕获用户帐户ID。 |
| `person.accountType` | 捕获用户帐户类型，如`Personal`或`Company`（如果适用）。 |
| `person.personalEmailID` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `personalEmail` | 捕获联系人详细信息 — 电子邮件和相关信息。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `userAccount` | 指示任何忠诚度详细信息、偏好设置、登录流程和其他帐户偏好设置。 |
| `userAccount.login` | 指示访客是否尝试登录。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

### 注销

| 描述 | XDM事件名称 |
|---|---|
| 购物者尝试注销时触发。 | `userAccount.logout` |

>[!NOTE]
>
> 此事件在尝试特定操作时触发。 它并不表示操作成功。

#### 从注销收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `userAccount` | 指示任何忠诚度详细信息、偏好设置、登录流程和其他帐户偏好设置。 |
| `userAccount.logout` | 指示访客是否尝试注销。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

### createAccount

| 描述 | XDM事件名称 |
|---|---|
| 购物者尝试创建帐户时触发。 | `userAccount.createProfile` |

>[!NOTE]
>
> 此事件在尝试特定操作时触发。 它并不表示操作成功。

#### 从createAccount收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `person` | 单独的操作者、联系人或所有者。 |
| `person.accountID` | 捕获用户帐户ID。 |
| `person.accountType` | 捕获用户帐户类型，如`Personal`或`Company`（如果适用）。 |
| `person.personalEmailID` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `personalEmail` | 捕获联系人详细信息 — 电子邮件和相关信息。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `userAccount` | 指示任何忠诚度详细信息、偏好设置、登录流程和其他帐户偏好设置。 |
| `userAccount.updateProfile` | 指示用户是否已更新其帐户配置文件。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

### editAccount

| 描述 | XDM事件名称 |
|---|---|
| 购物者尝试编辑帐户时触发。 | `userAccount.updateProfile` |

>[!NOTE]
>
> 此事件在尝试特定操作时触发。 它并不表示操作成功。

#### 从editAccount收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `person` | 单独的操作者、联系人或所有者。 |
| `person.accountID` | 捕获用户帐户ID。 |
| `person.accountType` | 捕获用户帐户类型，如`Personal`或`Company`（如果适用）。 |
| `person.personalEmailID` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `personalEmail` | 捕获联系人详细信息 — 电子邮件和相关信息。 |
| `personalEmail.address` | 技术地址，例如RFC2822和后续标准中通常定义的`name@domain.com`。 |
| `userAccount` | 指示任何忠诚度详细信息、偏好设置、登录流程和其他帐户偏好设置。 |
| `userAccount.updateProfile` | 指示用户是否已更新其帐户配置文件。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

## 搜索事件

搜索事件会提供与购物者意图相关的数据。 insight迎合购物者的意图，有助于商家了解购物者如何搜索商品、点击什么，最终购买或放弃。 例如，如果您希望定位现有购物者，这些购物者搜索您的热门产品，但从未购买该产品，您可能会如何使用此数据。 您必须安装[[!DNL Live Search]](../live-search/install.md)扩展才能访问这些事件。

使用在`searchRequest.id`和`searchResponse.id`事件中找到的`searchRequestSent`和`searchResponseReceived`字段交叉引用搜索请求到相应的搜索响应。

### searchRequestSent

| 描述 | XDM事件名称 |
|---|---|
| 由“键入时搜索”弹出框中的以下事件触发：<br><br>按Enter，单击&#x200B;_查看全部_<br><br>&#x200B;由搜索结果页面上的以下事件触发：<br><br>选择过滤器，更改排序顺序（_排序依据_），更改排序方向（升序或降序），更改每页的结果数（_每页显示次数_），导航到下一页，导航到上一页，导航到其他页面 | `searchRequest` |

>[!NOTE]
>
>安装了B2B扩展的Adobe Commerce Enterprise Edition不支持搜索事件。

#### 从searchRequestSent收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `searchRequest` | 指示是否发送了搜索请求。 |
| `searchRequest.id` | 此特定搜索请求的唯一ID。 |
| `searchRequest.value` | 请求的可量化值。 |
| `siteSearch` | 包含有关搜索的信息。 |
| `siteSearch.filter` | 指示是否应用了任何过滤器来限制搜索结果。 |
| `siteSearch.filter.attribute` （筛选器） | 用于确定是否将其包含在搜索结果中的项目的方面。 |
| `siteSearch.filter.isRange` | 如果为true，则值表示值的可接受范围的端点。 |
| `siteSearch.filter.value` | 用于确定搜索结果中包含哪些项目的属性值。 |
| `siteSearch.sort` | 指示应如何对搜索结果排序。 |
| `siteSearch.sort.attribute` （排序） | 用于对搜索结果中的项目进行排序的属性。 |
| `siteSearch.sort.order` | 返回搜索结果的顺序。 |
| `siteSearch.query` | 搜索的词语。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

### searchResponseReceived

| 描述 | XDM事件名称 |
|---|---|
| 当Live Search返回“键入时搜索”弹出框或搜索结果页面的结果时触发。 | `searchResponse` |

>[!NOTE]
>
>安装了B2B扩展的Adobe Commerce Enterprise Edition不支持搜索事件。

#### 从searchResponseReceived收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `searchResponse` | 指示是否已收到搜索响应。 |
| `searchResponse.id` | 此特定搜索响应的唯一ID。 |
| `searchResponse.value` | 响应的可量化值。 |
| `siteSearch.numberOfResults` | 返回的产品数。 |
| `siteSearch.suggestions` | 一个字符串数组，其中包含目录中存在的与搜索查询类似的产品和类别的名称。 |
| `productListItems` | 添加到购物车的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.productImageUrl` | 产品的主图像URL。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

## B2B事件

Adobe Commerce的![B2B](../assets/b2b.svg)对于B2B商家，您必须[安装](install.md#install-the-b2b-extension) `experience-platform-connector-b2b`扩展才能访问这些事件。

B2B事件包含[申请列表](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html)信息，例如，是否创建、添加或删除了申请列表。 通过跟踪特定于申请列表的事件，您可以查看客户经常购买的产品，并根据这些数据创建营销活动。

### createRequisitionList

| 描述 | XDM事件名称 |
|---|---|
| 购物者创建申购单列表时触发。 | `commerce.requisitionListOpens` |

#### 从createRequisitionList收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.requisitionListOpens` | 指示新申请列表的初始化。 |
| `commerce.requisitionList` | 客户创建的申请列表的属性。 |
| `commerce.requisitionList.ID` | 申购单列表的唯一标识符。 |
| `commerce.requisitionList.name` | 客户指定的申请列表的名称。 |
| `commerce.requisitionList.description` | 客户指定的申请列表的描述。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |

### addToRequisitionList

| 描述 | XDM事件名称 |
|---|---|
| 当购物者将产品添加到现有申请列表或创建列表时触发。 | `commerce.requisitionListAdds` |

#### 从addToRequisitionList收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.requisitionListAdds` | 指示向申请列表添加一个或多个产品。 |
| `commerce.requisitionList` | 客户创建的申请列表的属性。 |
| `commerce.requisitionList.ID` | 申购单列表的唯一标识符。 |
| `commerce.requisitionList.name` | 客户指定的申请列表的名称。 |
| `commerce.requisitionList.description` | 客户指定的申请列表的描述。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `productListItems` | 已添加到申请列表的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |

### removeFromRequisitionList

| 描述 | XDM事件名称 |
|---|---|
| 当购物者从申请列表中删除产品时触发。 | `commerce.requisitionListRemovals` |

#### 从removeFromRequisitionList收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.requsitionListRemovals` | 指示从申请列表中删除一个或多个产品。 |
| `commerce.requisitionList` | 客户创建的申请列表的属性。 |
| `commerce.requisitionList.ID` | 申购单列表的唯一标识符。 |
| `commerce.requisitionList.name` | 客户指定的申请列表的名称。 |
| `commerce.requisitionList.description` | 客户指定的申请列表的描述。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
| `productListItems` | 已添加到申请列表的一系列产品。 |
| `productListItems.SKU` | 库存单位。 产品的唯一标识符。 |
| `productListItems.name` | 产品的显示名称或人类可读的名称。 |
| `productListItems.priceTotal` | 产品行项目的总价。 |
| `productListItems.quantity` | 购物车中的产品件数。 |
| `productListItems.discountAmount` | 指示应用的折扣金额。 |
| `productListItems.currencyCode` | 使用的[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)货币代码，如`USD`或`EUR`。 |
| `productListItems.selectedOptions` | 用于可配置产品的字段。 |
| `productListItems.selectedOptions.attribute` | 标识可配置产品的属性，如`size`或`color`。 |
| `productListItems.selectedOptions.value` | 标识属性的值，如`small`或`black`。 |

### deleteRequisitionList

| 描述 | XDM事件名称 |
|---|---|
| 当购物者删除申请列表时触发。 | `commerce.requisitionListDeletes` |

#### 从deleteRequisitionList收集的数据

下表描述了为此事件收集的数据。

| 字段 | 描述 |
|---|---|
| `channel` | 包含有关数据源的信息。 `_id`和`_type`都包含[命名空间值](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html)。 |
| `channel._id` | 渠道的唯一标识符，如`"https://ns.adobe.com/xdm/channels/web"`。 |
| `channel._type` | 标识渠道数据的来源，如`"https://ns.adobe.com/xdm/channel-types/web"`。 |
| `commerce.requisitionListDeletes` | 指示已删除申请列表。 |
| `commerce.requisitionList` | 客户创建的申请列表的属性。 |
| `commerce.requisitionList.ID` | 申购单列表的唯一标识符。 |
| `commerce.requisitionList.name` | 客户指定的申请列表的名称。 |
| `commerce.requisitionList.description` | 客户指定的申请列表的描述。 |
| `commerce.commerceScope` | 指示事件发生位置（商店视图、商店、网站等）。 |
| `commerce.commerceScope.environmentID` | 环境ID 32位数的字母数字ID，用连字符分隔。 |
| `commerce.commerceScope.storeCode` | 唯一商店代码。 每个网站可以有许多商店。 |
| `commerce.commerceScope.storeViewCode` | 唯一的商店视图代码。 每个商店可以有多个商店视图。 |
| `commerce.commerceScope.websiteCode` | 唯一的网站代码。 在一个环境中可以有许多网站。 |
