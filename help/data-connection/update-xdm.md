---
title: 更新Commerce数据摄取的时间序列事件架构
description: 了解如何创建架构、数据集和数据流，以收集和发送用于Commerce数据引入的时间序列事件数据。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# 更新Commerce数据摄取的时间序列事件架构

使用[!DNL Data Connection]扩展的[载入步骤](overview.md#onboarding-steps)之一是访问数据流工作区并[创建特定于Adobe Commerce的数据流](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hans)。 在创建该数据流时，还必须选择描述您计划摄取的数据的架构。 该架构必须包含特定于商务的字段组。

本文为您提供了架构必须包含的字段组，以便成功收集由Adobe Commerce事件提供的以下时间序列数据：

- [行为](events.md) — 包括店面、个人资料、搜索和B2B事件。
- [后台](events-backoffice.md) — 包括订单状态和配置文件事件。

了解有关[时间序列数据](data-ingestion.md)的详细信息。

了解有关[架构组合的基础知识](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hans)的更多信息。

## 使用时间序列行为和后台事件数据更新模式

在此部分中，您将了解如何更新现有模式或创建模式以包含行为和后台事件数据。

>[!NOTE]
>
>请参阅[时间序列配置文件事件数据](#time-series-profile-event-data)，了解如何添加配置文件特定的字段。

1. 如果您还没有架构，请[创建](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hans#create)架构，并将类设置为&#x200B;**体验事件**。

1. [添加](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hans#add-field-groups)以下特定于Commerce的字段组（或者编辑现有架构并添加这些字段组）：

   - 站点搜索
   - 访问网页
   - 用户登录过程
   - 引用键
   - 个人联系人详细信息
   - 渠道详细信息
   - Commerce详细信息
   - Adobe Analytics ExperienceEvent Commerce(如果要将数据发送到Adobe Analytics)

   >[!NOTE]
   >
   > 不要将任何特定于Commerce的字段组设置为`Primary identity`。 这样做会将字段标识为必填字段，Experience Platform希望在每个事件中都使用该字段。 如果该字段不存在，则数据摄取失败。

   您的架构现在包含特定于Commerce的字段组，以便在架构中表示从Commerce [行为](events.md)和[后台](events-backoffice.md)事件收集的时间系列数据。

1. [为配置文件启用](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hans#profile)架构。

   为配置文件启用某个架构后，从该架构创建的任何数据集都将参与Real-Time CDP，后者将合并来自不同源的数据，以构建每个客户的完整视图。

1. [根据您创建或更新的架构创建数据集](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=zh-Hans#create-a-dataset)。

   数据集是用于数据集合的存储和管理结构，通常是包含架构（列）和字段（行）的表。 数据集还包含描述其存储的数据的各个方面的元数据。

1. [创建数据流](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hans)并选择包含Commerce特定字段组和相应数据集的架构。

   数据流将收集的数据转发到数据集。 数据根据所选架构在数据集中表示。

为行为数据和后台数据配置架构、数据集和数据流后，您可以[配置](connect-data.md#data-collection)您的Commerce实例以收集这些数据并将其发送到Experience Platform。

要包含购物者的配置文件信息，请参阅[时间序列配置文件事件数据](#time-series-profile-event-data)。

## 时间序列配置文件事件数据

时间序列配置文件事件数据由以下事件生成：

- [&#39;帐户已创建&#39;](events-backoffice.md#accountcreated)
- [&#39;帐户已更新&#39;](events-backoffice.md#accountupdated)
- [&#39;帐户已删除&#39;](events-backoffice.md#accountdeleted)

如果要将客户的配置文件事件数据摄取到Experience Platform，您可以更新现有的Commerce架构并使用已配置的相同数据流，也可以创建特定于配置文件的数据流和架构。 该决策基于贵公司的数据治理。 下面两个部分将介绍这两种情况。

### 使用现有数据流将时间序列配置文件事件数据发送到Experience Platform

如果要将时间序列[服务器端配置文件事件数据](events-backoffice.md#customer-profile-events-server-side)添加到您现有的Commerce数据流，请将`Demographic Details`字段组添加到您的架构中。 您的架构现在包含以下特定于Commerce的字段组：

- 站点搜索
- 访问网页
- 用户登录过程
- 引用键
- 个人联系人详细信息
- 渠道详细信息
- Commerce详细信息
- Adobe Analytics ExperienceEvent Commerce(如果要将数据发送到Adobe Analytics)
- 新：**人口统计详细信息**

在现有Commerce架构中添加`Demographic Details`字段组后，已与Commerce架构关联的数据集和数据流将用于此时间序列配置文件数据。

### 在单独的数据流中将时间序列配置文件事件数据发送到Experience Platform

如果要将[服务器端配置文件事件数据](events-backoffice.md#customer-profile-events-server-side)添加到新的特定于配置文件的数据流和架构，请完成以下步骤。

1. [创建](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hans#create)架构并将类设置为&#x200B;**体验事件**。

1. [添加](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hans#add-field-groups)以下特定于配置文件的字段组：

   - 人口统计详细信息
   - 个人联系人详细信息
   - 渠道详细信息
   - Commerce详细信息

1. [为配置文件启用](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hans#profile)架构。

   为配置文件启用某个架构后，从该架构创建的任何数据集都将参与Real-Time CDP，后者将合并来自不同源的数据，以构建每个客户的完整视图。

1. [根据您创建的架构创建数据集](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=zh-Hans#create-a-dataset)。

   数据集是用于数据集合的存储和管理结构，通常是包含架构（列）和字段（行）的表。 数据集还包含描述其存储的数据的各个方面的元数据。

1. [创建数据流](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=zh-Hans)并选择包含特定于Commerce的字段组和相应数据集的XDM架构。

   数据流将收集的数据转发到数据集。 数据根据所选架构在数据集中表示。

为客户个人资料数据配置架构、数据集和数据流后，您可以[配置](connect-data.md#data-collection)您的Commerce实例以收集这些数据并将其发送到Experience Platform。

要为配置文件记录数据创建架构、数据集和数据流，请参阅[将配置文件记录数据发送到Experience Platform](profile-data.md)。
