---
title: 价格手册
description: 了解如何在 [!DNL Adobe Commerce Optimizer]中管理价格手册。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
source-git-commit: 1c720bc3ba755639eff2f17912fb3a3446e367f6
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 价格手册

价格手册允许您在不同的客户层和市场中为目录来源定义产品价格。 价格手册支持分层模型，允许每个基本价格手册下最多三层嵌套子价格手册。 每个价格手册均可以引用父价格手册，从而形成定价目录来源的树结构。

![价格手册层次结构](../assets/price-book-hier.png)

基本价格手册定义了它本身及其所有子价格手册的币种。 子价格帐簿将继承此币种，并且无法覆盖它。

## 向Commerce Optimizer添加价格手册

您可以使用价格手册API将价格手册添加到Commerce Optimizer。 请参阅[开发人员文档](https://developer.adobe.com/commerce/services/reference/rest/)以了解如何创建、更新和删除[!DNL Adobe Commerce Optimizer]的价格手册。

## 在Commerce Optimizer中查看价格手册

将价格手册摄取到Commerce Optimizer后，您可以在&#x200B;**目录视图**&#x200B;页面上看到价格手册的列表及其对应的ID。

1. 转到&#x200B;_存储设置_，然后单击&#x200B;**[!UICONTROL Catalog views]**。

1. 单击&#x200B;**[!UICONTROL Create catalog view]**&#x200B;。

   在配置目录视图详细信息中，选择一个可用的价格手册。

   ![价格簿名称和ID](../assets/price-book-name-ids.png)

## 重要概念

| 术语 | 描述 |
|------|-------------|
| **价格手册** | 逻辑分组，定义目录来源的价格；例如，特定区域或客户层，用于管理产品价格。 |
| **备用价格手册** | 层次结构中最顶层的价格手册。 它没有父级，并且是&#x200B;*仅*&#x200B;价格手册，它定义了自身及其所有子级价格手册的货币。<br/><br/>如果在创建价格手册期间（通过API）未定义任何父项，则会创建一个新的备用价格手册。 |
| **父价格手册** | 一个更高级别的价格手册，如果子价格手册中没有明确设置价格，则子价格手册可以从中继承价格。 |
| **层次结构深度** | 最多三个级别（回退 — >子级 — >孙级）<br/><br/>在摄取时未强制执行。 |
| **货币** | 仅为后备价格手册定义。 由所有子价格手册继承。<br/><br/>如果在创建后备价格手册期间（通过API）未指定货币，则该货币将默认为USD。 |
| **产品价格** | 特定价格手册中分配给产品(SKU)的特定价格。 |
| **折扣** | 折扣在产品价格中定义。 未继承。 |
