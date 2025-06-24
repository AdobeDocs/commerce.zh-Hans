---
title: 价格手册
description: 了解如何在 [!DNL Adobe Commerce Optimizer]中管理价格手册。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# 价格手册

本文介绍了如何通过适当的数据治理控制来定义价格手册并将其分配给目录视图。

请参阅[开发人员文档](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books)，了解如何使用价格手册API将价格手册信息从第三方系统摄取到[!DNL Adobe Commerce Optimizer]。

通过价格手册，您可以定义定价目录来源，以管理不同客户层和市场之间的产品价格。 价格手册支持分层模型，允许每个基本价格手册下最多三层嵌套子价格手册。 每个价格手册均可以引用父价格手册，从而形成定价目录来源的树结构。

基本价格手册定义了它本身及其所有子价格手册的币种。 子价格帐簿将继承此币种，并且无法覆盖它。

## 重要概念

| 术语 | 描述 |
|------|-------------|
| **价格手册** | 定义价格目录来源的逻辑分组；例如，特定区域或客户层，用于管理产品价格。 |
| **备用价格手册** | 层次结构中最顶层的价格手册。 它没有父级，并且是&#x200B;*仅*&#x200B;价格手册，它定义了自身及其所有子级价格手册的货币。<br/><br/>如果在创建价格手册期间（通过API）未定义任何父项，则会创建一个新的备用价格手册。 |
| **父价格手册** | 一个更高级别的价格手册，如果子价格手册中没有明确设置价格，则子价格手册可以从中继承价格。 |
| **层次结构深度** | 最多3个级别(回退→子级→孙级)<br/><br/>在摄取时未强制执行。 |
| **货币** | 仅在后备价格手册中定义。 由所有孩子继承，价格手册。<br/><br/>如果在创建后备价格手册期间（通过API）未指定货币，则该货币将默认为USD。 |
| **产品价格** | 特定价格手册中分配给产品(SKU)的特定价格。 |
| **折扣** | 折扣在产品价格中定义。 未继承。 |
