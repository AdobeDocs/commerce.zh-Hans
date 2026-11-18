---
title: Adobe Commerce as a Cloud Service限制和边界
description: 了解Adobe Commerce as a Cloud Service许可证限制和系统边界。 规划容量、跟踪使用情况，并在超出限制时避免延迟和限制。
role: Admin, Developer
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和[!DNL Adobe Commerce as a Cloud Service]项目（Adobe管理的SaaS基础结构）。"
nudge: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a13aaee57732f27b51a2d2acdd0ca3de364ee6ab
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 1%
---
# 限制和边界

[!DNL Adobe Commerce as a Cloud Service]应用&#x200B;**许可证限制**&#x200B;和&#x200B;**系统边界**，它们定义了您的项目可以使用的容量：

- **许可证限制**&#x200B;基于您购买的容量，可通过购买其他包来扩展。
- **系统边界**&#x200B;是固定的限制，可保护系统资源并确保所有用户的可靠性能。

>[!IMPORTANT]
>
> 您的使用情况必须保持在这些限制之内。 超过这些超时可能会导致延迟增加并请求限制。

## 请求额外容量

您可以通过购买[许可证限制和系统边界](#license-limits-and-system-boundaries)中描述的许可证包，或针对独特用例协商自定义许可证来增加许可证限制。 请联系您的Adobe客户代表以讨论您的要求。

有关系统边界的问题，请联系[Adobe支持](https://experienceleague.adobe.com/home?lang=zh-Hans#support)。

## 防止出现性能问题

遵循这些最佳实践以保持在限制范围内并避免操作问题：

- **查看您的限制** — 在启动新店面或营销活动之前，了解您的[容量限制](#license-limits-and-system-boundaries)。
- **跟踪您的使用情况** — 使用内置量度仪表板或CDN日志。

## 许可证限制和系统边界

下表按功能区域汇总了许可证限制和系统边界，并包含有关使用其他许可证在适用的情况下扩展容量的信息。

### 环境限制

| **环境** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| **沙盒环境** | 包含的沙盒环境数 | 每个实例2个 | 是<p>为每个实例添加一个额外的环境许可证</p> |
| **生产环境** | 包含的生产环境数 | 每个实例1个 | 是<p>为每个实例添加一个额外的环境许可证</p> |

{style="table-layout:auto"}

### 目录

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 产品摄取率 | 创建或更新的产品数 | 每分钟1千次更新<p>每天最多可更新10万次</p> | 是<p>添加一个许可证包：</p><ul><li>每分钟5K更新<br>每天最多500K更新</li><li>每分钟10K更新<br>每天最多更新1M</li></ul><p>每天的最大数据摄取容量为100万次更新。</p> |
| 产品有效负载大小 | 使用API创建、更新或摄取产品信息时允许的最大数据量 | 200 KB | 否 |
| 类别 | 产品可分组到的类别数 | 6,000 | 否 |
| 产品数量 | 目录中支持的SKU数量 | 25万SKU | 是<p>添加100K SKU许可证包</p> |
| 每个产品的变体 | 每个产品允许的产品变体数量（大小、颜色组合） | 1万 | 否 |
| 商店视图 | 存储视图上下文的数量（例如，区域设置） | 50 | 否 |
| SLA ，可在搜索中显示产品更新 | 产品创建/更新显示在店面搜索中的时间 | 10 - 15分钟 | 否 |

{style="table-layout:auto"}

### 结帐

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 购物车中的产品 | 每个购物车允许的产品数 | 650 | 否 |
| 每个帐户的客户地址 | 每个帐户允许的客户地址数 | 2,000 | 否 |
| 购物车价格规则 | 根据一组条件对购物车中的商品应用折扣的购物车价格规则数 | 100,000 | 否 |
| 优惠券 | 与购物车价格规则一起使用的优惠券代码数 | 1,000,000 | 否 |

{style="table-layout:auto"}

<!--
# Price books

# | **Capability** | **Description** | **Base allocation** | **Expandable?** |
# | --- | --- | --- | --- |
# | Price books | The number of price books allowed per instance | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
# | Discounts per price record | The number of discounts that can be applied to a product price within a single price book | 10 | No |

{style="table-layout:auto"}
-->

### [!DNL Product Visuals]限制

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 产品视觉效果高级用户 | 具有完整数字资产管理功能（包括AI工具、[!DNL Adobe Express]/[!DNL Firefly]集成和Content Hub共享）的许可用户，可处理核心DAM任务和高级云原生功能以实现最佳效率。 | 2 | 是<p>升级到[!DNL AEM Assets]许可证</p> |
| 产品可视化协作者用户 | 通过AEM Commerce集成访问和使用资源，使用[!DNL Adobe Express]和[!DNL Firefly]创建和编辑内容，以及（如果启用）通过Content Hub门户利用批准的资源。 | 2 | 是<p>升级到[!DNL AEM Assets]许可证</p> |
| 产品可视化存储 | 为资产分配的存储空间 | 1 TB存储 | 否 |
| 动态媒体使用情况 | 拨备动态媒体处理业务，包括：<ul><li>图像投放</li><li>智能成像</li><li>视频交付</li></ul><p>有关详细信息，请参阅下面的&#x200B;*计算Dynamic Media使用情况*。 | 基于商品总值<p>最小分配：每月500万次操作</p> | 是<ul><li>购买许可证以进行其他操作</li><li>升级到[!DNL AEM Assets]许可证</li></ul> |
| 视频交付 | 视频投放或下载的备抵 | 300个视频，每个视频1分钟 | 是<p>升级到[!DNL AEM Assets]许可证</p> |
| 资源生成 | 访问用于创建图像的[!DNL Adobe Express]和[!DNL Adobe Firefly]创作AI | 无 | 单独购买Generative AI积分 |

{style="table-layout:auto"}

>[!NOTE]
>
>**超级用户**&#x200B;可以直接访问[!DNL Adobe Express]，也可以在[!DNL Adobe Commerce as a Cloud Service]内访问。
>
>**Collaborator用户**&#x200B;可以直接访问[!DNL Adobe Express]应用程序。 使用受[Adobe Express和Firefly产品特定的许可条款](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf)管辖。

>[!BEGINSHADEBOX “计算Dynamic Media使用情况”]

Dynamic Media的使用情况跟踪进入[!DNL Adobe Commerce as a Cloud Service]内的“产品可视化图表”组件的API请求，以促进以下操作之一：

- **对于以下情况的每次发生，图像投放都会占用一个Dynamic Media操作**：
  - 数字资源的&#x200B;**基本图像转换**，例如调整大小、缩放、格式转换、压缩或裁切操作。
  - **静态图像投放或下载**&#x200B;所述数字资源或数字资源演绎版（视频除外）。
- **智能图像投放每次针对单个数字资产进行优化投放都将使用20个Dynamic Media操作**，具体方法是自动为最终用户设备和浏览器生成最合适的图像演绎版。
- **视频交付占用20个Dynamic Media操作**，用于单个交付或下载视频或视频的转换变体。

>[!ENDSHADEBOX]

>[!NOTE]
>
>上述限制涵盖容量和使用分配。 有关产品可视化功能概述和功能约束，请参阅[AEM Assets的产品可视化图表](../optimizer/setup/product-visuals.md)。

<!--
### Catalog views and policies

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Catalog views | Number of configurable subsets of your master catalog | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
| Policies per catalog view | Number of data filters allowed | 10 | No |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100 | No |
| [Restricted access key assignment](setup/private-catalog-view.md) | Number of restricted access keys that can be assigned to a single catalog view | 3 | No |
| RSA key size (restricted access keys) | Minimum and maximum key strength accepted for a restricted access key | 2048-bit minimum, 8192-bit maximum | No |
| Restricted access keys | Key revocation propagation delay | Up to 5 minutes, due to caching. Tokens signed by a removed key are denied once the delay elapses. | Not applicable |

{style="table-layout:auto"}
-->

### 目录店面

目录店面功能的基本分配基于GMV（毛商品价值）层确定。 该表指示每个功能的最小分配。

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 目录检索率 | 系统（店面、交易系统、ERP或其他）每月调用目录API以从目录中检索数据的次数 | 基于GMV层<p>最小分配：1000万/月</p> | 是<p>每月添加100万个许可证包请求</p> |
| 内容请求 | 请求店面进行HTML页面查看或JSON API调用。 计为1次页面查看或5次API调用。 | 基于GMV层<p>最小分配：每月200万</p> | 是<p>每月添加100万份许可证包</p> |
| 店面GenAI变体 | 允许基于文本的内容生成 | 基于GMV层<p>最小分配：1K变量/月</p> | 是<p>单独购买Generative AI积分</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>图像生成需要将[!DNL Adobe Firefly]许可证配置为与[!DNL Adobe Commerce as a Cloud Service]相同的IMS组织。

### 产品发现

以下限制适用于storefront产品搜索、列表和促销配置。

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- |---------------------------------------------------|
| 产品检索 | 获取具有`products`、`productSearch`、`refineProduct`和`variants`的产品数据时，每个[!DNL Catalog Service] GraphQL请求的最大SKU数。 将较大的请求拆分为多个调用。 | 100 | 否 |
| 可过滤属性 | 可为分层导航和Facet启用的产品特征（如颜色、大小、品牌或材料）的数量 | 200 | 否 |
| 可搜索属性 | 可以为目录搜索编制索引的产品特征数 | 200 | 否 |
| 可排序的属性 | 在搜索和类别页面上可用作排序选项的产品特征数。 | 50 | 否 |
| 搜索分页深度 | 通过搜索分页可访问的最大产品数（例如，第100页×100个产品/页面） | 1万 | 否 |
| Facet | 可过滤的产品属性（如品牌、颜色、大小和价格）的数量，可配置这些属性以帮助购物者优化搜索结果和浏览类别 | 100<p>必须是可筛选的属性</p> | 是<p>可以通过支持请求增加到500</p> |
| 每个方面的选项 | 购物者可在Facet中选择的可过滤产品属性值的数量（例如，“红色”、“蓝色”表示颜色，“小”、“Medium”表示大小） | 100 | 是<p>可以通过支持请求增加</p> |

{style="table-layout:auto"}

### Recommendations

以下功能适用于产品推荐。 [!DNL Adobe Commerce as a Cloud Service]不支持其他Adobe Commerce产品中提供的某些功能。

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 有效的推荐单位 | 店面上实时推荐组件的数量（如“客户也查看了”或“您可能也喜欢”） | 产品推荐的每个页面类型有50个活动单位，必要时可明确设定目录模型范围 | 否 |

{style="table-layout:auto"}
<!-- Talos complained about this even thought it was copied directly from the ACO version of this page. Commenting out for now, | Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | Not supported | — | -->

### 可扩展性

| **功能** | **描述** | **基础分配** | **可扩展？** | **备注** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | 构建云原生扩展和集成的能力 | 基于GMV层<p>最小分配：1包/年</p> | 是<p>添加其他包</p> | 有关每个包定义的限制，请参阅：<ul><li>[App Builder产品说明](https://helpx.adobe.com/cn/legal/product-descriptions/adobe-developer-app-builder.html)。</li><li>*App Builder运行时指南*&#x200B;中的[系统设置和限制](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings)。</li><li>[App Builder存储要求](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--
## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your [!DNL Adobe Commerce as a Cloud Service] solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each)
-->
