---
title: 限制和边界
description: 了解 [!DNL Adobe Commerce Optimizer] 限制和边界以规划容量并防止性能问题。
role: Admin, Developer
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 4f238b002d1481126d4fec0a249b7f9ff437248e
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# 限制和边界

[!DNL Adobe Commerce Optimizer]有两种类型的限制：

- **许可证限制** — 基于您购买容量；可通过购买其他包来扩展。
- **系统边界** — 固定限制以保护系统资源并确保所有用户的可靠性能。

您的使用情况必须保持在这些限制之内。 超过这些超时可能会导致延迟增加并请求限制。

## 请求额外容量

通过购买[许可证限制和系统边界](#license-limits-and-system-boundaries)部分中描述的许可证包，或通过就独特用例协商自定义许可证，可以增加许可证限制。 请联系您的Adobe客户代表以讨论您的要求。

有关系统边界的问题，请联系[Adobe支持](https://experienceleague.adobe.com/home?lang=en#support)。

## 防止出现性能问题

遵循这些最佳实践以保持在限制范围内并避免操作问题：

- **查看您的限制** — 在启动新店面或营销活动之前了解您的[容量限制](#license-limits-and-system-boundaries)。
- **跟踪您的使用情况** — 使用内置量度仪表板或CDN日志。

## 许可证限制和系统边界

下表按功能区域汇总了许可证限制和系统边界，并包含有关添加其他许可证以扩展适用容量的信息。

### 环境限制

| **环境** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| **沙盒环境** | 包含的沙盒环境数 | 每个实例2个 | 是<p>为每个实例添加一个额外的环境许可证</p> |
| **生产环境** | 包含的生产环境数 | 每个实例1个 | 许可证<p>为每个实例添加一个额外的环境许可证</p> |

{style="table-layout:auto"}

### 目录

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 产品摄取率 | 创建或更新的产品数 | 每分钟1千次更新<p>每天最多可更新10万次</p> | 是<p>添加一个许可证包：</p><ul><li>每分钟5K更新<br>每天最多500K更新</li> <li>每分钟10K更新<br>每天最多更新1M</li></ul><p>每天的最大数据摄取容量为100万次更新。</p> |
| 产品有效负载大小 | 使用API创建、更新或摄取产品信息时允许的最大数据量 | 200 KB | 否 |
| 目录变体 | 店面用户可用的目录查看次数。<p>被计为(*目录查看次数×价格手册数量*)</p> | 100个变量 | 是<p>添加100个目录变体许可证包</p> |
| 单个目录源中的产品 | 目录中支持的SKU | 25万SKU | 是<p>添加100K SKU许可证包</p> |
| 每个产品的变体 | 每个产品允许的产品变体数量（大小、颜色组合） | 1万 | 否 |
| 目录源 | 目录数据上下文的数量（例如，区域设置或PIM和ERP等数据源） | 50 | 否 |

{style="table-layout:auto"}

### 价格手册

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 价格手册 | 每个实例允许的价格簿数量 | 基于[目录变体](#catalog)的数量 | 是<br>增加目录变体 |
| 每个价格记录的折扣 | 单个价格手册中可应用于产品价格的折扣数 | 10 | 否 |

{style="table-layout:auto"}

### 由AEM Assets提供支持的产品视觉效果

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 产品视觉效果高级用户 | 具有完整数字资产管理功能(包括AI工具、Adobe Express/Firefly集成和Content Hub共享)的许可用户，可处理核心DAM任务和高级云原生功能以实现最佳效率。 | 2 | 是<p>升级到AEM Assets许可证</p> |
| 产品可视化协作者用户 | 通过AEM Commerce集成访问和使用资源，使用Adobe Express和Firefly创建和编辑内容，以及（如果启用）通过Content Hub门户利用批准的资源。 | 2 | 是<p>升级到AEM Assets许可证</p> |
| 产品可视化存储 | 为资产分配的存储空间 | 1 TB存储 | 否 |
| 动态媒体使用情况 | 拨备动态媒体处理业务，包括：<ul><li>图像投放</li><li>智能成像</li><li>视频交付</li></ul><p>有关详细信息，请参阅下面的&#x200B;*计算Dynamic Media使用情况*。 | 基于GMV<p>最小分配：每月500万次操作</p> | 是<ul><li>购买许可证以进行其他操作</li><li>升级到AEM Assets许可证</li></ul> |
| 视频交付 | 视频投放或下载的备抵 | 300个视频，每个视频1分钟 | 是<p>升级到AEM Assets许可证</p> |
| 资源生成 | 访问Adobe Express和Adobe Firefly创作AI以创建图像 | 无 | 单独购买Generative AI积分 |

{style="table-layout:auto"}


>[!NOTE]
>
>**超级用户**&#x200B;可以直接访问Adobe Express或在Adobe Commerce Optimizer中访问。 **Collaborator用户**&#x200B;可以直接访问Adobe Express应用程序。 使用受[Adobe Express和Firefly产品特定的许可条款](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf)管辖。


>[!BEGINSHADEBOX “计算Dynamic Media使用情况”]

Dynamic Media使用情况会跟踪进入Adobe Commerce Optimizer中产品可视化组件的API请求，以促进以下操作之一：

- **对于以下情况的每次发生，图像投放都会占用一个Dynamic Media操作**：
   - 数字资源的&#x200B;**基本图像转换**，例如调整大小、缩放、格式转换、压缩或裁切操作。
   - **静态图像投放或下载**&#x200B;所述数字资源或数字资源演绎版（视频除外）
- **智能图像投放每次针对单个数字资产进行优化投放都将使用20个Dynamic Media操作**，具体方法是自动为最终用户设备和浏览器生成最合适的图像演绎版。
- **视频交付占用20个Dynamic Media操作**，用于单个交付或下载视频或视频的转换变体。

>[!ENDSHADEBOX]


### 目录视图和策略

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 目录视图 | 主目录的可配置子集的数量 | 基于[目录变体](#catalog)的数量 | 是<br>增加目录变体 |
| 每个目录视图的策略 | 允许的数据过滤器数量 | 10 | 否 |
| 策略中的属性值 | 可配置为进行筛选的产品特征数 | 100 | 否 |

{style="table-layout:auto"}

### 目录店面

目录店面功能的基本分配是根据GMV层确定的。 该表指示每个功能的最小分配。

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 目录检索率 | 系统（店面、交易系统、ERP或其他）每月调用目录API以从目录中检索数据的次数 | 基于GMV层<p>最小分配：1000万/月</p> | 是<p>每月添加100万个许可证包请求</p> |
| 内容请求 | 请求Commerce Storefront以进行HTML页面查看或JSON API调用。 计为1次页面查看或5次API调用。 | 基于GMV层<p>最小分配：200万/月</p> | 是<p>每月添加100万份许可证包</p> |
| 店面GenAI变体 | 允许基于文本的内容生成 | 基于GMV层<p>最小分配：1K变量/月</p> | 是<p>单独购买Generative AI积分</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>图像生成需要将Adobe Firefly许可证配置为与Adobe Commerce Optimizer相同的IMS组织。


### 产品发现

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 每个搜索请求的产品 | 搜索结果中每页返回的最大产品数 | 100 | 否 |
| 可过滤属性 | 可为分层导航和Facet启用的产品特征（如颜色、大小、品牌或材料）的数量 | 200 | 否 |
| 可搜索属性 | 可以配置为与产品目录搜索服务一起使用的产品特征数 | 200 | 否 |
| 可排序的属性 | 可配置为确定搜索结果值顺序的产品特征数 | 50 | 否 |
| 搜索分页深度 | 通过分页可访问的最大产品数量(例如，第100页×100个产品/页面) | 1万 | 否 |
| Facet | 可过滤的产品属性（如品牌、颜色、大小和价格）的数量，可配置这些属性以帮助购物者优化搜索结果和浏览类别 | 100<p>必须是可筛选的属性</p> | 否 |
| 每个方面的选项 | 购物者可以从列表中选择的可过滤产品属性值(例如“红色”、“蓝色”代表颜色；“小”、“Medium”代表大小)的数量 | 100 | 是<p>可以通过支持请求增加</p> |

{style="table-layout:auto"}

### Recommendations

以下功能适用于产品推荐。 [!DNL Adobe Commerce Optimizer]不支持其他Adobe Commerce产品中提供的某些功能。

| **功能** | **描述** | **基础分配** | **可扩展？** |
| --- | --- | --- | --- |
| 有效的推荐单位 | 店面上实时推荐组件的数量（如“客户也查看了”或“您可能也喜欢”） | 50 | 否 |
| 类别或属性包含/排除项 | 将产品筛选到符合推荐条件的特定集 | 不支持 | |

{style="table-layout:auto"}

### 可扩展性

| **功能** | **描述** | **基础分配** | **可扩展？** | **备注** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | 构建云原生扩展和集成的能力 | 基于GMV层<p>最小分配：1包/年</p> | 是<p>添加其他包</p> | 有关每个包定义的限制，请参阅：<ul><li>针对每个包定义的限制，[App Builder产品描述](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html)。</li><li>[App Builder运行时指南](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings)中的&#x200B;*系统设置和限制*。</li><li>[App Builder存储要求](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

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
   * Add-On: 10 × dynamic media packs (1M each) -->
