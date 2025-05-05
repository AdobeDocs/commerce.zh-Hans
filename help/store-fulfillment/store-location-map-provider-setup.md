---
title: 存储位置和映射系统配置
description: 配置距离提供商以支持店面UI中的商店位置映射。 “商店履行”解决方案要求距离提供商为端到端履行工作流启用零售商店搜索以及其他映射和计划功能。
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 存储位置和映射设置

通过配置[距离提供程序](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/configuration/distance-priority-algorithm)来搜索零售商店位置，为商店完成启用商店位置和映射功能。

**要求**

在配置过程中，您会为Google Maps平台提供一个Google API密钥。 如果您没有，请[从Google地图平台](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/configuration/distance-priority-algorithm#configure-google-maps)生成一个。

要配置距离提供器，请执行以下操作：

1. 从管理员的&#x200B;**[!UICONTROL Stores > General]**&#x200B;配置中，为映射内容类型添加Google映射集成。

   - 转到&#x200B;**[!UICONTROL Stores > Configuration  > General > Content Management]**。

   - 将您的Google API密钥添加到&#x200B;**[!UICONTROL Google Maps API Key]**&#x200B;字段。

1. 从“管理员”的&#x200B;**[!UICONTROL Stores > Inventory]**&#x200B;配置中，为“商店履行”选择距离提供程序。

   - 转到&#x200B;**[!UICONTROL Stores > Configuration > Catalog > Inventory]**。

   - 展开&#x200B;**[!UICONTROL Distance Provider for Distance Based SSA]**&#x200B;部分。

   - 将&#x200B;**提供程序**&#x200B;设置为&#x200B;**Google映射**。

1. 配置&#x200B;**[!UICONTROL Google Distance Provider]**&#x200B;的设置。

   - 添加您的&#x200B;**Google API密钥**。

   - 将&#x200B;**[!UICONTROL Computation Mode]**&#x200B;设置为`Driving`并将&#x200B;**[!UICONTROL Value]**&#x200B;设置为`Distance`
