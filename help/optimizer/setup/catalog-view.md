---
title: 目录视图
description: 了解目录视图是什么以及如何创建它们以按业务结构、策略和定价整理产品目录。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 42c252f70f6ed1d7a5c1fd2832324308294da264
workflow-type: tm+mt
source-wordcount: 1317
ht-degree: 0%

---

# Merchanding Services的目录视图

目录视图定义客户端可以检索的产品和定价。 它结合了目录源、目录层、策略和价格手册以支持不同的品牌、地区、业务部门或渠道。

## 什么是目录视图？

目录视图定义产品目录的组织和显示方式。 它们充当过滤器，用于确定：

- 根据业务结构（品牌、地区、经销商）**哪些产品可见**
- **通过链接的价格手册显示什么定价**
- **如何使用策略（品牌、模型、类别等属性）过滤产品**
- **使用什么[目录源](catalog-sources.md)**&#x200B;基于区域设置等属性
- **谁可以通过[目录保护](private-catalog-view.md)和[受限访问密钥](restricted-access-keys.md)访问视图的数据**

例如，您可以为以下对象创建单独的目录视图：

- 品牌或业务部门
- 地理区域
- 经销商或合作伙伴渠道
- 具有特定定价的客户区段

## 创建目录视图

在创建目录视图之前，根据需要准备以下项目：

- [目录源](catalog-sources.md)
- 定义产品筛选器的[策略](policies.md)
- 如果需要覆盖产品属性，请[目录层](catalog-layer.md)
- 视图中显示的[价格手册](pricebooks.md)
- 如果要创建专用目录视图，请[受限访问密钥](restricted-access-keys.md)

### 配置

在此部分中，您创建目录视图，选择[策略](policies.md)和[价格手册](pricebooks.md)。

1. 从左侧菜单中，转到&#x200B;**[!UICONTROL Store setup]**，然后单击&#x200B;**[!UICONTROL Catalog views]**。

1. 单击&#x200B;**[!UICONTROL Create catalog view]**。 &#x200B;

1. 配置目录视图详细信息：

   - **名称** — 输入目录视图的名称，例如`Celport`。 &#x200B;
   - **目录源** — 选择[目录源](catalog-sources.md)，例如`en-US`。
   - **目录层** — 查看摄取的层和优先级。
   - **策略** — 使用下拉菜单选择相关策略。 例如，“品牌”、“型号”。 请&#x200B;确保您已[创建策略](policies.md)。

1. 选择要链接到目录视图的价格手册。

   - **使用所有可用的价格手册** — 此选项从所有可用的价格手册中提取定价数据。
   - **仅允许所选价格手册** — 此选项显示&#x200B;**添加允许的价格手册**&#x200B;对话框。 使用此对话框选择要用于目录视图的特定价格手册。
   - **仅限单一价格手册** — 如果只有一个价格手册，请选择此选项。 如果要配置只能引用一个价格手册的专用目录视图，则必须使用此选项。 查看私有目录视图的[价格簿限制](private-catalog-view.md#price-book-restriction-on-private-catalog-views)。
   - **禁用定价** — 此选项目前不可用。

   >[!NOTE]
   >
   >价格手册ID控制请求哪种定价。 它不会限制对目录视图的访问。 要限制访问，请启用目录保护以创建[专用目录视图](private-catalog-view.md)。

1. （可选）将&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;切换为&#x200B;**[!UICONTROL Enabled]**&#x200B;以将此目录视图的数据限制为仅供具有有效签名令牌的客户端使用。 有关设置步骤，请参阅[保护目录视图](private-catalog-view.md#protect-a-catalog-view)。

1. 单击&#x200B;**[!UICONTROL Add]**&#x200B;以创建包含链接的价格手册和政策的目录视图。

目录视图页面将更新以显示新的目录视图&#x200B;。

完成这些步骤后，目录视图现在配置为根据您选择的来源和策略显示产品和定价。

### 指定推荐和产品发现规则的目录视图

您可以在[创建推荐单位](../merchandising/recommendations/create.md)或[促销规则](../merchandising/rules/add.md)时指定目录视图。

## 目录层

目录层允许您覆盖选定的产品属性，而无需更改源目录数据。 使用图层可以自定义目录视图的名称、描述、图像、链接或元数据。

查看[目录层](catalog-layer.md)。

## 将目录视图设为私有

默认情况下，目录视图对可以访问GraphQL促销API的客户端应用程序是公用的。 要限制访问，请启用&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;以配置专用目录视图。

要了解如何保护目录视图并验证是否强制访问，请参阅[私有目录视图](private-catalog-view.md)。

## 管理目录视图

要更新或查看现有目录视图的属性，请按照以下说明操作。

### 编辑目录视图

1. 在&#x200B;**[!UICONTROL Catalog views]**&#x200B;工作区中，找到目录视图。
1. 要打开操作菜单，请选择(**[!UICONTROL ...]**)。
1. 选择&#x200B;**[!UICONTROL Edit]**&#x200B;以访问目录视图编辑器。
1. 根据需要更新名称、目录源、策略、价格手册信息和&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;设置（包括分配的限制访问密钥）。
1. 单击&#x200B;**[!UICONTROL Save]**。

### 删除目录视图

1. 在&#x200B;**[!UICONTROL Catalog views]**&#x200B;工作区中，找到目录视图。
1. 要打开操作菜单，请选择(**[!UICONTROL ...]**)。
1. 选择&#x200B;**[!UICONTROL Delete]**。
1. 确认删除。

   出现确认对话框时，单击&#x200B;**[!UICONTROL Delete]**。

### 查看目录视图详细信息

此选项提供了一种快速查看所有目录视图参数的方法，同时保留在&#x200B;**[!UICONTROL Catalog views]**&#x200B;表中。

在&#x200B;**[!UICONTROL Catalog views]**&#x200B;工作区中，为目录视图选择![信息图标](../assets/info-icon.png)以查看其配置详细信息。

![目录视图详细信息](../assets/catalog-view-details.png)

在此处，您可以查看目录视图配置详细信息，例如：

- 视图ID
- 名称
- 目录源
- 支持
- 创建日期
- 数据已修改

在设置店面或使用数据摄取API时，需要其中的一些配置设置。

## 架构概述

目录视图是Merchandising Services框架的一部分，该框架将Adobe Commerce基础中使用的网站、商店、商店审核框架替换为更灵活的模型：

![[!DNL Merchandising Services]架构](../assets/merchandising-svcs-architecture.png)

### 工作原理

**1. 数据摄取**
来自PIM、ERP和其他系统的目录数据被引入到Merchandising Services框架。 每个SKU都包含映射到目录视图、策略和区域设置的区域设置信息和产品属性。 有关数据摄取的更多信息，请参阅[开发人员文档](https://developer.adobe.com/commerce/services/optimizer/)。

**2. 统一的基本目录**
引入的数据在目录服务数据管道中创建统一的基本目录。 此单一来源可消除跨业务部门的数据重复。

**3. 目录视图**
多个目录视图代表不同的业务单位（例如，“Texas Retail”、“Texas Retail Secondural”）。 可以在目录视图之间共享区域设置、策略和价格手册，以实现灵活性。

**4. 多渠道交付**
过滤的目录数据会交付到Edge Delivery Services、市场、广告平台和自定义微店面等目标。 有关目录数据投放的详细信息，请参阅[开发人员文档](https://developer.adobe.com/commerce/services/optimizer/)。

当目录视图启用了&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;时，向该目标的投放需要分配的[受限访问密钥](restricted-access-keys.md)中的有效签名令牌；未授权的请求将被拒绝而不是接收目录数据。

### 关键组件

| 组件 | 用途 | 示例 |
|---|---|---|
| **目录视图** | 业务单位或分发渠道 | 经销商网络、地区商店 |
| **策略** | 基于属性的产品过滤器 | 品牌、型号、类别 |
| **区域设置** | 语言/区域设置 | en-US、fr-CA、es-MX |
| **价格手册** | 定价结构 | 零售、批发、员工 |
| **受限访问密钥** | 用于阻止访问受保护目录视图的签名令牌凭据 | 合作伙伴门户密钥、B2B定价密钥 |

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
| **专用目录视图** | 使用签名令牌验证将目录视图限制为授权客户端 |

## 用例

### 多品牌企业集团

**挑战**：管理多个品牌、国家和语言<br>
**解决方案**：每个品牌/区域组合只有一个目录，其中具有目录视图

### 汽车零部件经销商

**挑战**： 3,000个具有相同产品但不同定价的经销商<br>
**解决方案**：一个目录，其中包含经销商特定的目录视图和价格手册

### 多位置retailer

**挑战**：每个位置的定价和库存不同<br>
**解决方案**：基于位置的目录视图以及特定于区域的策略

>[!NOTE]
>
>有关目录数据摄取和投放的详细信息，请参阅[开发人员文档](https://developer.adobe.com/commerce/services/optimizer/)。

## 更多此类内容

- [目录源](catalog-sources.md) — 为搜索、筛选和排序行为定义产品、属性和类别的权威范围
- [目录层](catalog-layer.md) — 了解如何在不更改原始源的情况下修改产品数据
- [专用目录视图](private-catalog-view.md) — 创建专用目录视图以限制对授权客户端的访问
- [受限访问密钥](restricted-access-keys.md) — 创建、分配和旋转用于为目录保护签名令牌的密钥
- [策略](policies.md) — 创建策略以筛选目录视图中的产品
- [价格手册](pricebooks.md) — 管理不同客户区段的定价结构
