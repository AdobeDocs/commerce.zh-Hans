---
title: 为Commerce Optimizer配置AEM Assets
description: 了解如何为 [!DNL Adobe Commerce Optimizer]配置AEM Assets集成。
feature: CMS, Media, Configuration, Integration
source-git-commit: 84cd0deaecda0790f9f123fc663d4db7b048746b
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---


# 为[!DNL Adobe Commerce Optimizer]配置AEM Assets

仅[!BADGE SaaS]{type=Positive tooltip="仅适用于Adobe Commerce Optimizer项目。"}

适用于[!DNL Adobe Commerce Optimizer]的AEM Assets集成使商家能够将AEM Assets用作产品图像的集中数字资产管理解决方案。 本指南介绍特定于[!DNL Commerce Optimizer]的配置。

下图是[!DNL Adobe Commerce Optimizer]与AEM Assets集成之间的产品同步概述。

![AEM Assets到[!DNL Commerce Optimizer]的流](../assets/aco-asset-sync-architecture.png){width="700"}

此集成具有两个独立的事件流。 两者都使用[Adobe I/O Events](https://developer.adobe.com/events/docs/)将事件传输到Assets集成服务，但每个方向都使用自己的事件提供程序：

* **从AEM Assets到Assets Integration Service**：批准、拒绝或删除资源时，该事件将交付到Assets Integration Service。 该服务使用`match-by-SKU` （元数据驱动）或[自定义匹配器(App Builder)](../synchronize/custom-match.md){target=_blank}将资源与产品匹配，然后将`product-asset`映射发送到[!DNL Commerce Optimizer]，在产品中存储这些映射作为产品层。

  >[!NOTE]
  >
  >集成使用的`AEM-Assets`目录层是在载入期间自动创建的。 您无需预先创建它。 有关目录层的工作方式以及AEM-Assets层行为方式的背景，请参阅[AEM-Assets层](../../optimizer/setup/catalog-layer.md#aem-assets-layer)。

* **从[!DNL Adobe Commerce Optimizer]到Assets集成服务**：在[!DNL Commerce Optimizer]中更新产品时，该事件将交付到Assets集成服务。 该服务将任何匹配的资产映射同步回[!DNL Commerce Optimizer]。

## 限制

[!DNL Commerce Optimizer]集成具有以下限制：

### 与图层相关的约束

* 为AEM Assets内容使用专用层。

  从AEM Assets发送的有效负载会填充Commerce Optimizer目录层。 该层中的值会覆盖提供字段的基本目录属性。 当集成忽略有效负载中的字段时，该层中的相应值可能会被空值覆盖。 与不相关的Commerce工作流共享层，或者重用已存储非AEM-Assets产品数据的层，可能会导致&#x200B;**意外数据丢失**&#x200B;或混淆覆盖。 主要为AEM驱动的产品图像同步保留图层名称（例如默认&#x200B;**`AEM-Assets`**）。

* 该集成支持每个租户一个目录源：单个区域设置和一个命名层。 目前不支持为同一租户配置多个AEM-Assets层或多个区域设置。

* 重用现有层或与不相关的工作流共享层经常导致出现可预防的支持案例。

### 其他限制

* **仅限图像**：集成当前不支持视频或其他媒体类型。
* **没有类别映像**：类别映像同步不可用。 不支持AEM Assets中用于Assets选择器（UI插入）的类别图像。
* **无多站点区别**：集成不处理多站点；与产品关联的图像在所有渠道和策略上显示相同。
* **图像位置/排序**：不支持图像位置和排序。
* **产品必须存在**：如果[!DNL Commerce Optimizer]中不存在该产品，则不会为该产品 — 资产映射创建层。

## 先决条件

在配置集成之前，请确保您具有：

* 具有&#x200B;**产品可视化图表**&#x200B;权利文件的活动[!DNL Adobe Commerce Optimizer]实例（捆绑Dynamic Media与OpenAPI功能+ [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime)），或客户提供的AEM Assets许可证（例如，**AEM Assets Ultimate**）已启用Dynamic Media。
* 访问AEM Assets as a Cloud Service环境。
* 同一Adobe IMS组织中的[!DNL Commerce Optimizer]和AEM Assets。
* 在您的AEM Assets环境中启用了OpenAPI的Dynamic Media （请参阅[配置AEM Assets项目](configure-aem.md#prerequisites)以了解启用步骤）。

### 首先配置AEM Assets

要支持集成，请在开始将AEM Assets集成与[!DNL Commerce Optimizer]载入的过程之前配置AEM Assets项目和环境。 这包括启用具有OpenAPI功能的Dynamic Media，以及使Commerce元数据架构、事件和UI在您的AEM项目中可用。

* [!BADGE 建议]{type=Positive}在AEM版本`2026.5.26309`及更高版本上，启用来自Cloud Manager的集成，而不部署代码。 请遵循[启用Commerce集成（自助服务）](configure-aem.md#enable-aem-commerce-self-service)。

* 在早期的AEM版本上，手动部署`assets-commerce`包。
请遵循[手动安装assets-commerce包](configure-aem.md#install-the-assets-commerce-package-manually)。

>[!TIP]
>
> 您可以从右上角菜单查看当前AEM版本： **[!UICONTROL Help]** > **[!UICONTROL About AEM]**。

## 入门

>[!IMPORTANT]
>
>在提交支持票证以启用与[!DNL Commerce Optimizer]的集成之前，请完成[配置AEM Assets](#configure-aem-assets-first)的过程。 支持需要将AEM Assets环境和项目配置为支持AEM Commerce集成，包括部署`assets-commerce`包（或等效的自助服务）以用于元数据和事件。 在配置AEM之前打开票证可能会延迟上线。

要加入AEM Assets与[!DNL Commerce Optimizer]的集成，Adobe支持部门必须向Assets集成服务注册您的Adobe Commerce Optimizer实例，然后将其订阅至：

* AEM Assets事件（已批准、更新和删除资产）
* [!DNL Commerce Optimizer]目录事件（产品已创建、已更新）

要启动此流程，请[创建支持票证](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case)，该票证包含以下信息：

* 在您的[!DNL Commerce Optimizer] URL或Commerce Cloud Manager UI中找到&#x200B;**[!DNL Adobe Commerce Optimizer]租户ID** （实例ID）。
* 当您[为集成配置了AEM](#configure-aem-assets-first)时，所设置的&#x200B;**AEM Assets项目ID和环境ID**。
* **匹配规则**：按SKU或[外部匹配器(App Builder)](../synchronize/custom-match.md){target=_blank}匹配。
* **层**：要向注册租户的目录层名称（请参阅&#x200B;**与层相关的约束**）。 仅在有意为之时才指定自定义名称；否则使用默认&#x200B;**`AEM-Assets`**。
* **区域设置**：向注册租户的目录源区域设置（例如，`en-US`）。 此区域设置必须与您在目录视图和产品目录数据中使用的区域设置相匹配。

### 配置目录视图

注册[!DNL Commerce Optimizer]租户后，配置目录视图，使店面和API显示AEM驱动的图像数据：

* **选择目录源（区域设置）** — 选择您在支持票证中指定的相同区域设置（例如&#x200B;**`en-US`**）。 集成为每个租户注册一个区域设置；不匹配，同步的图像无法在预期的目录视图中显示。
* **分配目录层** — 将&#x200B;**`AEM-Assets`**&#x200B;层（或票证中的自定义层名称）分配给该目录视图。

如果未正确分配区域设置或图层，则图像数据&#x200B;**不会显示**&#x200B;或行为异常 — 即使在上游同步成功也是如此。

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

1. 验证图像是否可见。 等待几分钟以完成同步，然后在[!DNL Commerce Optimizer] UI中检查产品或查询店面API以确认图像已返回。

## 图像角色处理

当一个产品有多个资源使用相同的图像角色时（例如，两个资源具有`thumbnail`角色），集成确保只有一个资源保留该角色，以避免[!DNL Commerce Optimizer]层出现重复角色和意外的店面行为。

**行为：**&#x200B;从AEM Assets发送更新时，最近更新的资源将收到图像角色（例如，`thumbnail`），并且该角色将从具有它的上一个资源中删除。 这样可防止店面中出现重复的图像角色。

## 更多此类内容

* [产品视觉效果](../../optimizer/setup/product-visuals.md)
* [配置AEM Assets项目](configure-aem.md)
* [自定义自动匹配](../synchronize/custom-match.md)
* [AEM Assets集成概述](../overview.md)
