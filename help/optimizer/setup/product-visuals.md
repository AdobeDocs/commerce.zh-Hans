---
title: AEM Assets的产品可视化图表
description: 了解如何将AEM Assets用于 [!DNL Adobe Commerce Optimizer]中的产品图像。
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 264658bee09a22cfd55828c6960153cc1239d3fb
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# AEM Assets的产品可视化图表

产品可视化图表使[!DNL Adobe Commerce Optimizer]商家能够通过Adobe Experience Manager (AEM) Assets管理产品图像。 此集成提供了一个无缝工作流程，用于使用目录层将高质量产品图像从AEM Assets同步到[!DNL Commerce Optimizer]目录。

>[!NOTE]
>
>**产品可视化图表**&#x200B;是随[!DNL Adobe Commerce as a Cloud Service]和[!DNL Adobe Commerce Optimizer]一起提供的包的名称。 它结合了[Dynamic Media与OpenAPI功能](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview)和[AEM Assets Prime](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/assets-prime)。
>
>拥有其他AEM Assets许可证（例如，**AEM Assets Ultimate**）的客户可以使用相同的集成；只有AEM版本会影响载入步骤，而不会影响许可证类型。

## 主要优势

* **集中式资源管理**：管理企业级数字资产管理解决方案AEM Assets中的所有产品映像。
* **自动同步**：在AEM Assets中批准或更新资产时，产品图像会自动同步。
* **Dynamic Media投放**：利用Dynamic Media的OpenAPI功能优化图像投放。
* **目录图层**：产品图像应用为目录图层，允许您在基本目录上叠加AEM Assets图像。

## 工作原理

该集成具有两个独立的事件流。 两者都使用[Adobe I/O Events](https://developer.adobe.com/events/docs/)将事件传输到Assets集成服务，但每个方向都使用自己的事件提供程序：

* **从AEM Assets到Assets集成服务**：批准、拒绝或删除资产后，该事件将交付到Assets集成服务。 该服务使用`match-by-SKU`或自定义匹配器策略将资产与产品匹配，然后将`product-asset`映射发送到[!DNL Commerce Optimizer]，在产品中，这些映射存储为产品层。

* **从[!DNL Commerce Optimizer]到Assets集成服务**：在[!DNL Commerce Optimizer]中更新产品时，该事件将交付到Assets集成服务。 该服务将任何匹配的资产映射同步回[!DNL Commerce Optimizer]。

更新的图像可通过店面API（目录服务、实时搜索、产品推荐）获得。

### Source和层配置

AEM Assets中的图像将作为目录层摄取，并采用以下源配置：

> 源配置示例

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

此配置可确保将AEM Assets图像作为叠加应用于基本产品目录。

## 先决条件

在启用产品可视化图表之前，请确保您满足Commerce Optimizer[&#128279;](../../aem-assets-integration/get-started/configure-aco.md#prerequisites)的先决条件。

## 设置

要启用集成，请[创建支持票证](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/help-and-support/create-a-support-ticket)，其中包含您的[!DNL Commerce Optimizer]和AEM Assets详细信息。 Adobe支持配置集成并在Assets集成服务中注册您的租户。

有关入门信息，请参阅[为Commerce Optimizer配置AEM Assets](../../aem-assets-integration/get-started/configure-aco.md)。

### 配置AEM Assets元数据

要启用自动产品匹配，请使用Commerce元数据在AEM Assets中配置资源。

有关必需的元数据字段和步骤，请参阅[配置AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets-first)。

## 限制

在使用产品可视化图表之前，请查看[集成限制](../../aem-assets-integration/get-started/configure-aco.md#limitations) — 与层相关的限制，这些限制会影响AEM Assets数据与基础目录的合并方式。

有关容量和使用率分配（资产存储、Dynamic Media操作、用户许可证），请参阅&#x200B;_边界和限制指南_&#x200B;中的[产品可视化限制](../boundaries-limits.md#product-visuals-limits)。

## 使用产品可视化图表

配置集成后，通过AEM Assets管理您的产品图像。

### 将图像添加到产品

1. 将图像上传到AEM Assets存储库。

1. 将Commerce元数据添加到资源。

   请参阅[默认自动匹配](../../aem-assets-integration/synchronize/default-match.md)和[自定义自动匹配](../../aem-assets-integration/synchronize/custom-match.md)。

1. 审批要交付的资产。 资源必须处于&#x200B;**已批准**&#x200B;状态才能触发同步。

1. 图像会自动同步到[!DNL Commerce Optimizer]。

### 应用AEM-Assets层

要在店面显示AEM Assets图像，请[将`AEM-Assets`图层分配给目录视图](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view)。

## 更多此类内容

* [目录层](catalog-layer.md)
* [目录视图](catalog-view.md)
* [AEM Assets集成指南](../../aem-assets-integration/overview.md)
