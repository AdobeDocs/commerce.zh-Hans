---
title: 目录视图
description: 了解目录视图是什么以及如何创建它们以按业务结构、策略和定价整理产品目录。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
source-git-commit: f67a5327b742338655b0f7ffa4076a174219f711
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---


# Merchanding Services的目录视图

目录视图是Adobe Commerce Optimizer促销服务的基础，它使您能够按业务结构、策略和定价整理产品目录。 此灵活的数据模型支持多品牌、多业务单元和多语言方案，同时保持运营效率。

## 什么是目录视图？

目录视图定义产品目录的组织和显示方式。 它们充当过滤器，用于确定：

- 根据业务结构（品牌、地区、经销商）**哪些产品可见**
- **通过链接的价格手册显示什么定价**
- **如何使用策略（品牌、模型、类别等属性）过滤产品**
- **根据区域设置等属性，使用了什么目录源**

将目录视图视为不同的“镜头”，客户可通过这些镜头查看您的目录。 例如：

- 经销商目录视图可能只显示对该特定经销商可用的产品
- 区域目录视图可能会显示特定于某个地理区域的产品和定价
- 品牌目录视图可能只显示特定品牌的产品

## 创建目录视图

在此部分中，您创建目录视图，选择[策略](policies.md)和[价格手册](pricebooks.md)。

在创建目录视图之前，请确保您具有：

- [已创建策略](policies.md)以定义产品筛选器

- [设置价格手册](pricebooks.md)以进行定价

1. 从左侧菜单中，转到&#x200B;_商店设置_，然后单击&#x200B;**[!UICONTROL Catalog views]**。

1. 单击&#x200B;**[!UICONTROL Create catalog view]**&#x200B;。

1. 配置目录视图详细信息：

   - **名称** — 输入目录视图的名称，例如`Celport`&#x200B;。
   - **目录源** — 添加目录源（区域设置），例如`en-US`。 按&#x200B;**Enter**。
   - **策略** — 使用下拉菜单选择相关策略。 例如，“品牌”、“型号”。&#x200B;AEM确保您已[创建策略](policies.md)。

1. 选择要链接到目录视图的价格手册。

1. 单击&#x200B;**[!UICONTROL Add]**&#x200B;以创建包含链接的价格手册和策略的目录视图。

   如果&#x200B;**[!UICONTROL Add]**&#x200B;按钮未处于活动状态，请通过将光标置于“目录源”字段并按&#x200B;**Enter**&#x200B;键，确保正确添加了目录源&#x200B;。

目录视图页面将更新以显示新的目录视图&#x200B;。

完成这些步骤后，目录视图现在配置为根据您选择的来源和策略显示产品和定价。

## 架构概述

目录视图是Merchandising Services框架的一部分，该框架将Adobe Commerce基础中使用的网站、商店、商店审核框架替换为更灵活的模型：

![[!DNL Merchandising Services]架构](../assets/merchandising-svcs-architecture.png)

### 工作原理

**1. 数据摄取**
来自PIM、ERP和其他系统的目录数据被引入到Merchandising Services框架。 每个SKU都包含映射到目录视图、策略和区域设置的区域设置信息和产品属性。 有关数据摄取的更多信息，请参阅[开发人员文档](https://developer-stage.adobe.com/commerce/services/composable-catalog)。

**2。 统一的基本目录**
引入的数据在目录服务数据管道中创建统一的基本目录。 此单一来源可消除跨业务部门的数据重复。

**3。 目录视图**
多个目录视图代表不同的业务单位（例如，“Texas Retail”、“Texas Retail Secondural”）。 可以在目录视图之间共享区域设置、策略和价格手册，以实现灵活性。

**4。 多渠道投放**
过滤的目录数据会传送到各种目标，包括Edge Delivery Services店面、市场、广告平台和自定义微型店面。 有关目录数据投放的详细信息，请参阅[开发人员文档](https://developer-stage.adobe.com/commerce/services/composable-catalog)。

### 关键组件

| 组件 | 用途 | 示例 |
|---|---|---|
| **目录视图** | 业务单位或分发渠道 | 经销商网络、地区商店 |
| **策略** | 基于属性的产品过滤器 | 品牌、型号、类别 |
| **区域设置** | 语言/区域设置 | en-US、fr-CA、es-MX |
| **价格手册** | 定价结构 | 零售、批发、员工 |

### 数据流

1. **摄取** - PIM/ERP系统中的产品数据
2. **进程** — 应用目录视图、策略和定价
3. **交付** — 将过滤的目录提供给店面、市场等。

## 主要功能

| 功能 | 收益 |
|---|---|
| **单基目录** | 消除跨业务部门的重复数据 |
| **灵活的定价** | 针对不同客户区段，每个SKU有多个价格手册 |
| **可缩放** | 高效地管理2亿多个SKU |
| **多渠道** | 将目录提供给店面、市场和广告平台 |
| **实时更新** | 快速更新促销和营销活动的目录数据 |

## 用例

### 多品牌企业集团

**挑战**：管理多个品牌、国家和语言<br>
**解决方案**：每个品牌/区域组合只有一个目录，其中具有目录视图

### 汽车零部件经销商

**挑战**： 3,000个产品相同但定价不同的经销商<br>
**解决方案**：一个目录，其中包含经销商特定的目录视图和价格手册

### 多位置Retailer

**挑战**：每个位置的定价和库存不同<br>
**解决方案**：基于位置的目录视图和特定于区域的策略

>[!INFO]
>
>有关目录数据摄取和投放的详细信息，请参阅[开发人员文档](https://developer-stage.adobe.com/commerce/services/composable-catalog)。
