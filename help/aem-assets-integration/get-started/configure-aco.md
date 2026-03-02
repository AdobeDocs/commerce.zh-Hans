---
title: 为Commerce Optimizer配置AEM Assets
description: 了解如何为 [!DNL Adobe Commerce Optimizer]配置AEM Assets集成。
feature: CMS, Media, Configuration, Integration
source-git-commit: bf1d88ef7daec25872678bb27bce0bb7c97fd296
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---


# 为[!DNL Adobe Commerce Optimizer]配置AEM Assets

仅[!BADGE SaaS]{type=Positive tooltip="仅适用于Adobe Commerce Optimizer项目。"}

适用于[!DNL Adobe Commerce Optimizer]的AEM Assets集成使商家能够将AEM Assets用作产品图像的集中数字资产管理解决方案。 本指南介绍特定于[!DNL Commerce Optimizer]的配置。

与Adobe Commerce (PaaS)或Adobe Commerce as a Cloud Service (ACCS)不同，[!DNL Commerce Optimizer]没有管理员配置UI。 要启用集成，请使用您的[!DNL Adobe Commerce Optimizer]和AEM Assets详细信息创建支持工单。 Adobe支持配置集成并在Assets集成服务中注册您的租户。

下图是[!DNL Adobe Commerce Optimizer]与AEM Assets集成之间的产品同步概述。

![AEM Assets到[!DNL Commerce Optimizer]的流](../assets/aco-asset-sync-architecture.png){width="700"}

此集成有两个主要流程：

* **从AEM Assets**：批准、拒绝或删除资源时，事件将通过Adobe管道传输到Assets集成服务。 该服务使用`match-by-SKU` （元数据驱动）或[自定义匹配器(App Builder)](../synchronize/custom-match.md){target=_blank}将资源与产品匹配，然后将`product-asset`映射发送到Commerce Optimizer，在产品中存储这些映射作为产品层。

* **从[!DNL Adobe Commerce Optimizer]**：在[!DNL Commerce Optimizer]中更新产品时，事件将通过Adobe管道传输到Assets集成服务。 该服务将任何匹配的资产映射同步回[!DNL Adobe Commerce Optimizer]。

## 先决条件

在配置集成之前，请确保您具有：

* 具有产品可视化权利或具有Dynamic Media的任何AEM Assets许可证的有效[!DNL Adobe Commerce Optimizer]实例。
* 访问AEM Assets as a Cloud Service环境。
* 同一Adobe IMS组织中的[!DNL Commerce Optimizer]和AEM Assets。
* AEM Assets环境中启用了OpenAPI的Dynamic Media。

## 入门

要载入与[!DNL Commerce Optimizer]的AEM Assets集成，您必须[创建支持票证](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)。

Adobe支持使用您票证中的信息来向Assets集成服务注册您的租户，并配置集成。

在您的支持工单中包含以下信息：

* 在您的&#x200B;**[!DNL Adobe Commerce Optimizer]URL或Commerce Cloud Manager UI中找到**&#x200B;租户ID[!DNL Commerce Optimizer] （实例ID）。
* **AEM项目ID**。
* **AEM环境ID**。
* **匹配规则**：按SKU或[外部匹配器(App Builder)](../synchronize/custom-match.md){target=_blank}匹配。
* **层**：要在其中注册租户的目录层名称。 根据需要指定自定义名称。 否则，将使用默认`AEM-Assets`。
* **区域设置**：向注册租户的目录源区域设置（例如，`en-US`）。

>[!IMPORTANT]
>
> 该集成支持每个租户一个源，即一个区域设置和一个层的组合。

Adobe支持处理您的票证后，配置集成，并且您的租户向Assets集成服务注册。

载入完成后：

1. **向Assets集成服务注册**：您的[!DNL Commerce Optimizer]租户已使用[!DNL Adobe Commerce Optimizer]租户ID、Assets项目ID、AEM环境ID和租户向AEM集成服务注册。

1. **身份验证设置**： IMS服务令牌身份验证在[!DNL Commerce Optimizer]和Assets集成服务之间配置，用于安全通信。

1. **事件订阅**： Assets集成服务订阅了：

   * AEM Assets事件（已批准、更新和删除资产）
   * [!DNL Commerce Optimizer]目录事件（产品已创建、已更新）

### 限制

[!DNL Commerce Optimizer]集成具有以下限制：

* **每个商户一个层** - AEM Assets集成支持每个商户一个AEM-Assets层（每个租户一个源）。 目前不支持为每个商家配置多个图层。
* **仅图像** — 集成不支持视频或其他媒体类型。
* **无类别映像** — 类别映像同步不可用。 不支持AEM Assets中用于Assets选择器（UI插入）的类别图像。
* **无多站点区别** — 集成不处理多站点；与产品关联的图像在所有渠道和策略上显示相同。
* **图像位置/排序** — 不支持图像位置和排序。
* **产品必须存在** — 如果[!DNL Commerce Optimizer]中不存在该产品，则不会为该产品 — 资产映射创建层。
* **图层字段覆盖** — 图层中的值覆盖基本目录。 如果在层有效负载中未发送字段，则该字段可能会被空值覆盖。 将专用层用于AEM Assets内容；将现有层重复用于其他目的可能会导致意外的数据丢失。

### 配置AEM Assets

[!DNL Commerce Optimizer]的AEM Assets安装和配置过程与Adobe Commerce as a Cloud Service相同。 有关完整步骤，请参阅[配置AEM Assets项目以支持Commerce元数据](configure-aem.md)。

确保您的AEM Assets环境已准备就绪：

1. **AEM Assets配置**：配置Commerce元数据配置文件。 请参阅[配置元数据配置文件](configure-aem.md#configure-a-metadata-profile)。

1. **Dynamic Media启用**：验证是否在AEM Assets环境中启用了具有OpenAPI功能的Dynamic Media。

## 配置AEM Assets

要启用product-asset同步，请配置AEM Assets环境。

### 步骤1：使用OpenAPI启用Dynamic Media

必须在您的AEM Assets环境中启用具有OpenAPI的Dynamic Media。 产品可视化图表和新的AEM Assets许可证允许您通过Cloud Manager以自助方式启用它。 旧版AEM Assets许可证需要Adobe支持才能启用。 有关启用步骤，请参阅[配置AEM Assets项目](configure-aem.md#prerequisites)。

### 步骤2：可选。 配置Commerce元数据配置文件

在AEM Assets中设置元数据配置文件以存储Commerce特定的元数据。

有关详细说明，请参阅[配置元数据配置文件](configure-aem.md#step-2-optional-configure-a-metadata-profile)。

### 步骤3：将元数据应用于资源

将Commerce元数据添加到AEM Assets中的产品图像。

有关字段定义，请参阅[AEM Commerce包内容](configure-aem.md#aem-commerce-assets-commerce-package-contents)；有关设置步骤，请参阅[配置元数据配置文件](configure-aem.md#step-2-optional-configure-a-metadata-profile)。

资产必须处于&#x200B;**已批准**&#x200B;状态，数据同步才会触发。 仅保存元数据不会触发事件。

>[!CAUTION]
>
> 将`AEM-Assets`图层分配给您的[目录视图](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/setup/catalog-view)。 如果未指定图层，产品图像数据可能会意外被覆盖。

## 同步

配置完毕后，集成将自动同步`product-asset`映射。

有关详细信息，请参阅[自定义自动匹配](../synchronize/custom-match.md)。

### 按SKU匹配工作流示例

将现有资产添加到新产品时的典型流程：

1. 在[!DNL Commerce Optimizer]中创建产品（通过API或数据摄取）。 产品最初可能没有图像。

1. 在AEM Assets中，打开要映射到产品的资源。

1. 将产品SKU添加到&#x200B;**commerce:skus**&#x200B;元数据并分配图像角色（例如，`thumbnail`、`image`）。

1. 审批要交付的资产。 这会触发Assets集成服务处理的事件。

1. Assets集成服务将产品映像映射发送到[!DNL Commerce Optimizer]。 [!DNL Commerce Optimizer]中的产品已使用资产中的图像更新。

1. 验证图像是否可见。 留出时间让同步完成（通常在几分钟内），然后检查[!DNL Commerce Optimizer] UI中的产品（例如，数据同步或目录视图），或查询店面API(目录服务、实时搜索、店面GraphQL API)以确认图像已返回。

## 图像角色处理

当一个产品有多个资源使用相同的图像角色时（例如，两个资源具有`thumbnail`角色），集成确保只有一个资源保留该角色，以避免[!DNL Commerce Optimizer]层出现重复角色和意外的店面行为。

**行为：**&#x200B;从AEM Assets发送更新时，最近更新的资源将收到图像角色（例如，`thumbnail`），并且该角色将从具有它的上一个资源中删除。 这样可防止店面中出现重复的图像角色。

## 更多此类内容

* [产品视觉效果](../../optimizer/setup/product-visuals.md)
* [配置AEM Assets项目](configure-aem.md)
* [自定义自动匹配](../synchronize/custom-match.md)
* [AEM Assets集成概述](../overview.md)
