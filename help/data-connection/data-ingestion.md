---
title: Commerce数据类型
description: 了解您可以收集并发送到Experience Platform的数据类型。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Commerce数据类型

[Data Connection扩展](overview.md)将您的Commerce数据连接到Experience Platform。 要在Experience Platform中使用的数据将分组为两种行为类型：属于&#x200B;**Experience Event**&#x200B;类的时间系列数据和属于&#x200B;**个人资料**&#x200B;类的记录数据。

了解有关Experience Platform中[数据行为](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#data-behaviors)和[类](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#class)的更多信息。

## 时间序列数据

时序数据提供记录主体直接或间接执行操作时的系统快照。 例如，当购物者浏览您网站上的产品、将产品添加到购物车、下订单时，等等。 使用将类设置为&#x200B;**Experience Event**&#x200B;的架构将时序数据摄取到Experience Platform中。

### 捕获的时间序列数据

查看[行为事件](events.md)和[后台事件](events-backoffice.md)，以了解在生成时间序列事件时捕获了哪些数据。

### 摄取时间序列事件数据所需的架构

了解如何[创建可摄取行为和后台时间序列事件数据的架构](update-xdm.md)。

## 记录数据

记录数据提供有关主题属性的信息。 主体可以是组织，也可以是个人。 例如，您网站上的购物者创建一个帐户并生成记录数据。 此数据是使用类设置为&#x200B;**个人资料**&#x200B;的架构摄取到Experience Platform中的。 您可以将该记录数据发送到Adobe的配置文件管理和分段服务：[Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#)。

### 捕获的配置文件记录数据

查看[客户个人资料记录数据](events-profilerecord.md)，了解生成个人资料记录时捕获了哪些数据。

### 摄取配置文件记录数据所需的架构

了解如何[创建可摄取配置文件记录数据的架构](profile-data.md)。
