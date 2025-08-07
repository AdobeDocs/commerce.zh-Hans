---
title: 发行说明
description: 来自Adobe Commerce的 [!DNL Data Connection] 扩展的最新发行信息。
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: 43020e33ce57861cf586ace12a0832b24c23872d
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 1%

---

# 发行说明

>[!IMPORTANT]
>
>Experience Platform连接器已重命名为[!DNL Data Connection]。

这些发行说明包含对[!DNL Data Connection]扩展的更新，其中包括：

![新](../assets/new.svg) — 新功能
![修复](../assets/fix.svg) — 修复和改进
![错误](../assets/bug.svg) — 已知问题

有关[!DNL Data Connection]扩展使用的扩展的功能更改和修复，请参阅&#x200B;**支持的服务更新**。

请参阅[即将发布的版本](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule)，了解版本计划和支持。

请参阅开发人员文档，以[了解哪些Commerce版本支持此模块](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)。

## 支持的服务更新

以下发行说明介绍了与[!DNL Data Connection]扩展使用的扩展相关的功能更改和修复。

+++支持的服务更新

_2025年8月7日_

![新](../assets/new.svg) — 在3.3.0版本中，您现在可以将[自定义属性添加到用户档案](custom-identities.md)。

_2024年8月2日_

![固定](../assets/fix.svg) — 固定将订单总额配置为含税时的付款总额。
![新](../assets/new.svg) — 添加了`taxAmount`字段以订购购买事件。
![新](../assets/new.svg) — 添加了向事件添加自定义数据的功能。 有关[示例](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md)，请参阅以下内容。

_2024年1月24日_

![新](../assets/new.svg) — 已更新`data-services-b2b`扩展以包含针对B2B商户的名为[deleteRequisitionList](events.md#deleterequisitionlist)的新申请事件。

_2023年11月16日_

![修复](../assets/fix.svg) — 修复了在您下具有多个送货地址的订单时，错误消息显示不正确的问题。
![修复](../assets/fix.svg) — 修复了[productPageView](events.md#productpageview)事件中的一个问题，即在商店视图上切换货币后，`productListItems.priceTotal`事件字段未转换价格。
![修复](../assets/fix.svg) — 修复了`productListItems`事件字段中货币代码在商家切换商店视图时未更新的问题。

_2023年10月10日_

![新](../assets/new.svg) — 已添加新的订单状态事件：[已开发票的订单](events-backoffice.md#orderinvoiced)、[已初始的订单项退货](events-backoffice.md#orderitemsreturninitiated)以及[已完成订单项退货](events-backoffice.md#orderitemreturncompleted)。
![修复](../assets/fix.svg) — 修复了在刷新缓存后，货币配置更改未反映在事件中的问题。
![Fix](../assets/fix.svg) — 修复了在启用异步订单放置后未显示订单确认消息的错误。
![新](../assets/new.svg) — 已将数据添加到“类别”视图页面上的简单产品的[addToRequisitionList](events.md#addtorequisitionlist)事件中。
![修复](../assets/fix.svg) — 修复了从订单确认页面添加产品时，`selectedOptions`addToRequisitionList[事件中](events.md#addtorequisitionlist)数据的问题。
![新建](../assets/new.svg) — 当产品从“类别”视图页面添加到申请列表时，已将产品数据添加到[addToRequisitionList](events.md#addtorequisitionlist)事件。
![新建](../assets/new.svg) — 将可配置产品从“产品视图”页面添加到申请列表时，添加了[addToRequisitionList](events.md#addtorequisitionlist)事件。
![新建](../assets/new.svg) — 在产品数量增加和/或从申请列表中减少时，添加了[addToRequisitionList](events.md#addtorequisitionlist)和[removeFromRequisitionList](events.md#removefromrequisitionlist)事件。

_2023年6月10日_

![修复](../assets/fix.svg) — 修复了`orderId`由于Commerce订单标识符中的前缀而未传入上下文的问题。
![修复](../assets/fix.svg) — 已更新内容安全策略配置。

_2023年3月30日_

![New](../assets/new.svg) — 添加了名为`data-services-b2b`的扩展，该扩展包括针对B2B商家的[申请列表事件](events.md#b2b-events)。
![新](../assets/new.svg) — 已将`uniqueIdentifier`字段添加到[搜索](events.md#search-events)事件。 此新字段允许商家交叉引用搜索请求和搜索响应。

_2022年10月12日_

![新](../assets/new.svg) — 已将两个[店面活动](events.md)、`openCart`和`removeFromCart`添加到Adobe Commerce店面活动SDK和收集器。
![新](../assets/new.svg) — 已添加对[AEM店面](overview.md#aem-support)的支持。

+++

## 3.3.0

_2025年3月21日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg)添加了PHP 8.4支持。

## 3.2.1

_2025年1月17日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) — 已将[HIPAA就绪扩展](hipaa-readiness.md)添加到[!DNL Data Connection]，以便商家可以与Experience Platform共享[!DNL Commerce]后台事件数据并维护HIPAA合规性。
![修复](../assets/fix.svg) — 修复[!DNL Data Connection]扩展覆盖`eventForwarding`数据并为所有客户设置`HIPAA`标记的问题。 现在，扩展仅为HIPAA客户设置标记。

## 3.2.0

_2024年10月7日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) — 添加了创建[自定义订单属性](custom-attributes.md)以访问后台数据的功能。
![新](../assets/new.svg) — 添加了新[自定义订单属性](connect-data.md#data-customization)表，以帮助您查看[!DNL Commerce]中配置并发送到Experience Platform的任何自定义属性。
![新](../assets/new.svg) — 已添加[收集配置文件记录](connect-data.md#send-customer-profile-data)和数据并将其发送到Experience Platform的功能。

## 3.2.0-beta3

_2024年8月27日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) — 如果您正在参与测试版，请确保您的`composer.json`文件在根级别具有以下内容： ` "minimum-stability": "beta"`。 此外，添加`composer require "magento/customers-connector: ^1.2.0"`以将客户配置文件从Commerce实例发送到SaaS。
![新](../assets/new.svg) — 此版本包含3.1.1、3.1.2、3.1.3和3.1.4中发布的修补程序。

## 3.1.4

_2024年8月9日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg) — 已更新`experience-platform-connector`中继包以删除其他未使用的数据导出器和索引器。

## 3.1.3

_2024年7月22日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg) — 已更新`experience-platform-connector`中继包以删除未使用的数据导出器和索引器。

## 3.1.2

_2024年6月5日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![修复](../assets/fix.svg) — 修复了在启动[历史同步](connect-data.md#specify-order-history-date-range)时使用错误日期格式的问题。
![修复](../assets/fix.svg) — 修复了Adobe Commerce 2.4.7上未发送[startCheckout](events.md#startcheckout)事件的问题。

## 3.1.1

_2024年4月4日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) — 为所有[!DNL Data Connection]扩展添加了对PHP 8.3的支持。
![新](../assets/new.svg) — 添加了有关如何[将](mobile-sdk-epc.md) Adobe Experience Platform Mobile SDK与Commerce集成的文章。

## 3.2.0-beta2

_2024年3月4日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) — 如果您正在参与测试版，请确保您的`composer.json`文件在根级别具有以下内容： ` "minimum-stability": "beta"`。 此外，添加`composer require "magento/customers-connector: ^1.2.0"`以将客户配置文件从Commerce实例发送到SaaS。
![新](../assets/new.svg) — 已添加[添加自定义属性](custom-attributes.md)的功能。
![新](../assets/new.svg) — 已添加[收集配置文件记录](connect-data.md#send-customer-profile-data)和数据并将其发送到Experience Platform的功能。

## 3.1.0

_2023年11月16日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

![新](../assets/new.svg) - Experience Platform连接器已重命名为[!DNL Data Connection]。
![修复](../assets/fix.svg) — 添加了在Adobe IMS无法生成访问令牌时记录错误响应的功能。
![修复](../assets/fix.svg) — 如果您尝试同步历史订单但未指定帐户凭据，则添加了通知消息。

## 3.0.0

_2023年10月10日_

[!BADGE 兼容性]{type=Informative tooltip="兼容性"} Adobe Commerce版本2.4.4及更高版本

这是一个主版本发行版本。 [编辑](install.md#update-the-data-connection)项目的根composer.json文件。

![新](../assets/new.svg) - [向Experience Platform发送历史订单](connect-data.md#send-historical-order-data)数据和状态的常规可用性。
![新](../assets/new.svg) — 在您[配置](connect-data.md#connect-commerce-data-to-adobe-experience-platform) [!DNL Data Connection]扩展时添加了对OAuth 2.0的支持。
![新建](../assets/new.svg) — 已终止对Adobe Commerce 2.4.3的支持。

## 2.3.0

_2023年6月27日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.3及更高版本

![新](../assets/new.svg) — 已添加[关闭向Experience Platform发送店面活动](connect-data.md#data-collection)的功能。
![修复](../assets/fix.svg) — 已更新内容安全策略配置。
![修复](../assets/fix.svg) — 修复了Commerce 2.4.7版本对后台事件的支持。
![新](../assets/new.svg) — 添加了关于将更改保存到[!DNL Data Connection]扩展表单时缓存失效的通知消息。

## 3.0.0-beta1（仅限内部）

_2023年6月13日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.3及更高版本

![新](../assets/new.svg) - (Beta)已添加将[历史订单](connect-data.md#beta-send-historical-order-data)数据和状态发送到Experience Platform的功能。

## 2.2.0

_2023年3月30日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.3及更高版本

![New](../assets/new.svg) — 已捆绑`commerce-data-export`和`saas-export`依赖项以及`experience-platform-connector`扩展。 以前，必须单独安装这些依赖项。 这些依赖项以及商家配置支持服务器端处理[后台事件](events-backoffice.md)。
![新](../assets/new.svg) — 已添加名为[`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted)的新后台事件。

## 2.1.1

_2023年2月28日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.3及更高版本

![新](../assets/new.svg) — 为所有[!DNL Data Connection]扩展添加了对PHP 8.2的支持。

## 2.1.0

_2023年1月17日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.3及更高版本

![新](../assets/new.svg) — 更新了[[!DNL Data Connection] 扩展管理员](connect-data.md)，以便您可以指定自己的AEP Web SDK (alloy)。
![Fix](../assets/fix.svg)在为推送到边缘的任何数据设置主标识时，更改为使用`identityMap`而不是`personID`。

## 2.0.1

_2022年11月10日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.3及更高版本

![修复](../assets/fix.svg) — 现在，仅在成功加载Storefront事件收集器和店面事件SDK之后设置Adobe Experience Platform上下文。

## 2.0.0

_2022年10月12日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.3及更高版本

![新](../assets/new.svg) — 添加了在[将您的AEP实例](connect-data.md)连接到Experience Platform时指定您自己的Adobe Commerce Web SDK的功能。
![修复](../assets/fix.svg) — 更新了数据流作用域要求，以便数据流ID的作用域必须限制在网站中，而不是存储审阅。

## 1.0.0

_2022年8月9日_

[!BADGE 支持]{type=Informative tooltip="支持"} Adobe Commerce版本2.4.3及更高版本

![新](../assets/new.svg) — 一般可用性版本。
