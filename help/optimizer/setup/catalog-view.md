---
title: 目录视图
description: 了解目录视图是什么以及如何创建它们以按业务结构、策略和定价整理产品目录。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和[!DNL Adobe Commerce Optimizer]项目（Adobe管理的SaaS基础结构）。"
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
source-git-commit: d081e975b03805a0f46d5194f8c3cd46e3c86839
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
# Merchanding Services的目录视图

{{$include /help/_includes/ccdm-shared/setup/catalog-view.md}}

## 管理目录视图

按照以下说明管理目录视图：

- [创建目录视图](#create-a-catalog-view) — 设置名称、目录源、策略和价格手册。 然后[为推荐和产品发现规则指定目录视图](#specify-catalog-views-for-recommendations-and-product-discovery-rules)，查看覆盖产品属性的[目录层](#catalog-layers)，或[使目录视图专用](#make-a-catalog-view-private)。
- [编辑目录视图](#edit-a-catalog-view) — 更新其源、策略、价格手册和保护设置。
- [删除目录视图](#delete-a-catalog-view) — 删除不再需要的目录视图。
- [查看目录视图详细信息](#view-catalog-view-details) — 从目录视图表中查看目录视图的配置。

### 创建目录视图

在创建目录视图之前，根据需要准备以下项目：

- [目录源](catalog-sources.md)
- 定义产品筛选器的[策略](policies.md)
- 如果需要覆盖产品属性，请[目录层](catalog-layer.md)
- 视图中显示的[价格手册](pricebooks.md)
- 如果要创建专用目录视图，请[受限访问密钥](restricted-access-keys.md)

#### 配置

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

#### 指定推荐和产品发现规则的目录视图

您可以在[创建推荐单位](../merchandising/recommendations/create.md)或[促销规则](../merchandising/rules/add.md)时指定目录视图。

#### 目录层

目录层允许您覆盖选定的产品属性，而无需更改源目录数据。 使用图层可以自定义目录视图的名称、描述、图像、链接或元数据。

查看[目录层](catalog-layer.md)。

#### 将目录视图设为私有

默认情况下，目录视图对可以访问GraphQL促销API的客户端应用程序是公用的。 要限制访问，请启用&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;以配置专用目录视图。

要了解如何保护目录视图并验证是否强制访问，请参阅[私有目录视图](private-catalog-view.md)。

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

在&#x200B;**[!UICONTROL Catalog views]**&#x200B;工作区中，为目录视图选择![信息图标](/help/assets/ccdm-shared/recommendations/info-icon.png)以查看其配置详细信息。

![目录视图详细信息](../assets/catalog-view-details.png)

在此处，您可以查看目录视图配置详细信息，例如：

- 视图ID
- 名称
- 目录源
- 支持
- 创建日期
- 数据已修改

在设置店面或使用数据摄取API时，需要其中的一些配置设置。
