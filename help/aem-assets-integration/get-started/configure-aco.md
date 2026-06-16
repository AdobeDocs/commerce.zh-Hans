---
title: 为Commerce Optimizer配置AEM Assets
description: 了解如何为 [!DNL Adobe Commerce Optimizer]配置AEM Assets集成。
feature: CMS, Media, Configuration, Integration
source-git-commit: 2cc7b70a6923687c74fe3f4b88448eaada6d16af
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 0%

---


# 为[!DNL Adobe Commerce Optimizer]配置AEM Assets

仅[!BADGE SaaS]{type=Positive tooltip="仅适用于Adobe Commerce Optimizer项目。"}

适用于[!DNL Adobe Commerce Optimizer]的AEM Assets集成使商家能够将AEM Assets用作产品图像的集中数字资产管理解决方案。 本指南介绍特定于[!DNL Commerce Optimizer]的配置。

与Adobe Commerce (PaaS)或[!DNL Adobe Commerce as a Cloud Service]不同，[!DNL Commerce Optimizer]没有管理员配置UI。 要启用集成，请使用您的[!DNL Adobe Commerce Optimizer]和AEM Assets详细信息创建支持工单。 Adobe支持配置集成并在Assets集成服务中注册您的租户。

**在提交票证之前准备AEM Assets。** 租户注册假定AEM端可用于Commerce。 例如，部署AEM Commerce `assets-commerce`包后，元数据和事件将按说明工作。 **在配置AEM之前打开票证可能会延迟上线。**

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
* 在您的AEM Assets环境中启用了OpenAPI的Dynamic Media （请参阅[配置AEM Assets项目](configure-aem.md#prerequisites)以了解启用步骤）。

## 首先配置AEM Assets

在&#x200B;**之前**&#x200B;完成AEM Assets步骤[打开支持票证](#onboarding)以进行租户注册。 安装模式与Adobe Commerce as a Cloud Service匹配 — 请参阅[配置AEM Assets项目以支持Commerce元数据](configure-aem.md)。

### 步骤1：部署AEM Commerce包

在AEM项目中安装和部署`assets-commerce`包，以便Commerce元数据架构、事件和UI可用。

完成[安装`assets-commerce`包](configure-aem.md#step-1-install-the-assets-commerce-package)中的完整过程。 在打开支持工单之前，请执行以下步骤：

1. 克隆Cloud Manager Git存储库，并将[AEM Assets Commerce存储库](https://github.com/ankumalh/assets-commerce)代码复制到项目中。

1. 在您的项目的所有`filter.xml`和`pom.xml`文件中，将所有出现的&lt;my-app>替换为应用程序名称。

1. 提交、推送、运行部署管道，并验证&#x200B;**[!UICONTROL Commerce]**&#x200B;选项卡是否显示在资产属性上。

如果缺少&#x200B;**[!UICONTROL Commerce]**&#x200B;选项卡，请参阅[安装`assets-commerce`包](configure-aem.md#step-1-install-the-assets-commerce-package)，以了解Cloud Manager屏幕截图、管道步骤和疑难解答。

### 步骤2：使用OpenAPI启用Dynamic Media

必须在您的AEM Assets环境中启用具有OpenAPI功能的Dynamic Media。 自助式路径（例如，用于产品可视化的Cloud Manager）和Adobe支持路径在[配置AEM Assets项目](configure-aem.md#prerequisites)下进行了说明。

### 步骤3：应用Commerce元数据并批准资源

将Commerce元数据添加到AEM Assets中的产品图像 — 有关字段定义，请参阅[AEM Commerce包内容](configure-aem.md#aem-commerce-assets-commerce-package-contents)。

资产必须处于&#x200B;**已批准**&#x200B;状态，数据同步才会触发。 仅保存元数据不会触发事件。

### 步骤4：可选 — 配置Commerce元数据配置文件

如果您选择使用AEM元数据配置文件来简化创作过程，请在&#x200B;**之后**&#x200B;配置这些配置文件，部署包并且您的团队了解必需的Commerce字段 — 与&#x200B;**配置AEM Assets项目**&#x200B;相同的可选模式。

请参阅[配置元数据配置文件](configure-aem.md#step-2-optional-configure-a-metadata-profile)。

## 限制

[!DNL Commerce Optimizer]集成具有以下限制：

### 与图层相关的约束

在&#x200B;**之前**&#x200B;阅读本节，您可以在支持票证中选择目录层名称。 选择或共享没有此上下文的层是造成可预防的支持案例的常见原因。

**为AEM Assets内容使用专用层。** 从AEM Assets发送的有效负载会填充Commerce Optimizer目录&#x200B;**层**。 提供字段的层&#x200B;**覆盖**&#x200B;基本目录属性中的值。 当集成忽略有效负载中的字段时，该层中的相应值可能会被空值覆盖。 与不相关的Commerce工作流共享层，或者重用已存储非AEM-Assets产品数据的层，可能会导致&#x200B;**意外数据丢失**&#x200B;或混淆覆盖。 在&#x200B;**之前规划图层选择**&#x200B;打开支持票证，并保留该图层名称（例如默认&#x200B;**`AEM-Assets`**）主要用于AEM驱动的产品图像同步。

>[!IMPORTANT]
>
>集成支持每个租户&#x200B;**一个目录源**：单个区域设置和&#x200B;**一个命名层**。 目前不支持为同一租户配置多个AEM-Assets层或多个区域设置。

### 其他限制

* **仅限图像**：集成当前不支持视频或其他媒体类型。
* **没有类别映像**：类别映像同步不可用。 不支持AEM Assets中用于Assets选择器（UI插入）的类别图像。
* **无多站点区别**：集成不处理多站点；与产品关联的图像在所有渠道和策略上显示相同。
* **图像位置/排序**：不支持图像位置和排序。
* **产品必须存在**：如果[!DNL Commerce Optimizer]中不存在该产品，则不会为该产品 — 资产映射创建层。

## 入门

要载入与[!DNL Commerce Optimizer]的AEM Assets集成，您必须[创建支持票证](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)。

Adobe支持使用您票证中的信息来向Assets集成服务注册您的租户，并配置集成。

确保在提交票证之前先完成[配置AEM Assets](#configure-aem-assets-first)。

在您的支持工单中包含以下信息：

* 在您的[!DNL Commerce Optimizer] URL或Commerce Cloud Manager UI中找到&#x200B;**[!DNL Adobe Commerce Optimizer]租户ID** （实例ID）。
* **AEM项目ID**。
* **AEM环境ID**。
* **匹配规则**：按SKU或[外部匹配器(App Builder)](../synchronize/custom-match.md){target=_blank}匹配。
* **层**：要向注册租户的目录层名称（请参阅&#x200B;**与层相关的约束**）。 仅在有意为之时才指定自定义名称；否则使用默认&#x200B;**`AEM-Assets`**。
* **区域设置**：向注册租户的目录源区域设置（例如，`en-US`）。 这必须符合您在目录视图和产品目录数据中使用的区域设置。

Adobe支持处理您的票证后，配置集成，并且您的租户向Assets集成服务注册。

载入完成后：

1. **向Assets集成服务注册**：您的[!DNL Commerce Optimizer]租户已使用票证中提供的[!DNL Adobe Commerce Optimizer]租户ID、AEM项目ID、AEM环境ID、匹配规则、区域设置和层名称向Assets集成服务注册。

1. **事件订阅**： Assets集成服务订阅了：

   * AEM Assets事件（已批准、更新和删除资产）
   * [!DNL Commerce Optimizer]目录事件（产品已创建、已更新）

配置[目录视图](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view)，以便店面和API显示AEM驱动的图像数据：

* **目录源（区域设置）** — 选择您在支持票证中指定的相同区域设置（例如&#x200B;**`en-US`**）。 集成为每个租户注册一个区域设置；不匹配，同步的图像无法在预期的目录视图中显示。
* **目录层** — 将&#x200B;**`AEM-Assets`**&#x200B;层（或票证中的自定义层名称）分配给该目录视图。

如果未正确分配区域设置或图层，则图像数据可能&#x200B;**未出现**&#x200B;或出现意外行为 — 即使在上游同步成功也是如此。

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

1. 验证图像是否可见。 留出时间让同步完成（通常在几分钟内），然后检查[!DNL Commerce Optimizer] UI中的产品（例如，数据同步或目录视图），或查询店面API（目录服务、实时搜索、店面GraphQL API）以确认图像已返回。

## 图像角色处理

当一个产品有多个资源使用相同的图像角色时（例如，两个资源具有`thumbnail`角色），集成确保只有一个资源保留该角色，以避免[!DNL Commerce Optimizer]层出现重复角色和意外的店面行为。

**行为：**&#x200B;从AEM Assets发送更新时，最近更新的资源将收到图像角色（例如，`thumbnail`），并且该角色将从具有它的上一个资源中删除。 这样可防止店面中出现重复的图像角色。

## 更多此类内容

* [产品视觉效果](../../optimizer/setup/product-visuals.md)
* [配置AEM Assets项目](configure-aem.md)
* [自定义自动匹配](../synchronize/custom-match.md)
* [AEM Assets集成概述](../overview.md)
