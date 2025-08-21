---
title: 行为事件
description: 了解每个行为事件捕获的数据。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 631dfacd26a333e70a70f354d191d256d90d946f
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Data Connection]行为事件

下面列出了安装[!DNL Data Connection]扩展时可用的Commerce行为事件。 这些事件收集的数据将发送到Adobe Experience Platform。 您还可以创建[自定义事件](custom-events.md)以收集未开箱即用的其他数据。

除了以下事件收集的数据之外，您还会获得由Adobe Experience Platform Web SDK提供的[其他数据](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=zh-Hans)。

行为事件在购物者浏览您的网站时收集来自他们的匿名行为数据。 您可以使用这些事件收集的数据创建针对特定购物者集的促销和促销活动。

>[!NOTE]
>
>所有行为事件都包含[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=zh-Hans)字段，其中包括购物者的电子邮件地址（可用时）和ECID。

## 店面活动

店面事件从购物者在网站上的交互中捕获数据，并包括`addToCart`、`pageView`、`createAccount`、`editAccount`、`startCheckout`、`completeCheckout`、`signIn`、`signOut`等事件。 店面事件仅适用于简单且可配置的产品。

请参阅[开发人员文档](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)，了解有关店面活动的更多信息。

## 客户个人资料事件

从店面捕获的配置文件事件包括帐户信息，如`signIn`、`signOut`、`createAccount`和`editAccount`。 此数据用于帮助填充更好地定义区段或执行营销活动所需的关键客户详细信息，例如发送注册折扣优惠、帐户更改确认等。

请参阅[开发人员文档](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)以了解有关客户个人资料事件的更多信息。

## 搜索事件

搜索事件会提供与购物者意图相关的数据。 insight迎合购物者的意图，有助于商家了解购物者如何搜索商品、点击什么，最终购买或放弃。 例如，如果您希望定位现有购物者，这些购物者搜索您的热门产品，但从未购买该产品，您可能会如何使用此数据。 您必须安装[[!DNL Live Search]](../live-search/install.md)扩展才能访问这些事件。

使用在`searchRequest.id`和`searchResponse.id`事件中找到的`searchRequestSent`和`searchResponseReceived`字段交叉引用搜索请求到相应的搜索响应。

请参阅[开发人员文档](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)，了解有关搜索事件的更多信息。

## B2B事件

Adobe Commerce的![B2B](../assets/b2b.svg)对于B2B商家，您必须[安装](install.md#install-the-b2b-extension) `experience-platform-connector-b2b`扩展才能访问这些事件。

B2B事件包含[申请列表](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=zh-Hans)信息，例如，是否创建、添加或删除了申请列表。 通过跟踪特定于申请列表的事件，您可以查看客户经常购买的产品，并根据这些数据创建营销活动。

请参阅[开发人员文档](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)以了解有关B2B事件的更多信息。
