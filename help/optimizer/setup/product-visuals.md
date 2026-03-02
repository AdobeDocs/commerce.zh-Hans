---
title: AEM Assets的产品可视化图表
description: 了解如何将AEM Assets用于 [!DNL Adobe Commerce Optimizer]中的产品图像。
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: bf1d88ef7daec25872678bb27bce0bb7c97fd296
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# AEM Assets的产品可视化图表

产品可视化图表使[!DNL Adobe Commerce Optimizer]商家能够通过Adobe Experience Manager (AEM) Assets管理产品图像。 此集成提供了一个无缝工作流程，用于使用目录层将高质量产品图像从AEM Assets同步到[!DNL Commerce Optimizer]目录。

## 主要优势

* **集中式资源管理**：管理企业级数字资产管理解决方案AEM Assets中的所有产品映像。
* **自动同步**：在AEM Assets中批准或更新资产时，产品图像会自动同步。
* **Dynamic Media投放**：利用Dynamic Media的OpenAPI功能优化图像投放。
* **目录图层**：产品图像应用为目录图层，允许您在基本目录上叠加AEM Assets图像。

## 工作原理

该集成有两个主要流程：

* **从AEM Assets**：批准、拒绝或删除资源时，事件将通过Adobe管道传输到Assets集成服务。 该服务使用`match-by-SKU`或自定义匹配器策略将资产与产品匹配，然后将`product-asset`映射发送到[!DNL Commerce Optimizer]，在产品中，这些映射存储为产品层。

* **从ACO**：在[!DNL Commerce Optimizer]中更新产品时，事件将通过Adobe管道传输到Assets集成服务。 该服务会将任何匹配的资产映射同步回ACO。

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

在启用产品可视化图表之前，请确保您满足Commerce Optimizer[的](../../aem-assets-integration/get-started/configure-aco.md#prerequisites)先决条件。

## 设置

要启用集成，请[创建支持票证](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)，其中包含您的[!DNL Commerce Optimizer]和AEM Assets详细信息。 Adobe支持配置集成并在Assets集成服务中注册您的租户。

有关入门信息，请参阅[为Commerce Optimizer配置AEM Assets](../../aem-assets-integration/get-started/configure-aco.md)。

### 配置AEM Assets元数据

要启用自动产品匹配，请使用Commerce元数据在AEM Assets中配置资源。

有关必需的元数据字段和步骤，请参阅[配置AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets)。

## 使用产品可视化图表

配置集成后，通过AEM Assets管理您的产品图像。

### 将图像添加到产品

1. 将图像上传到AEM Assets存储库。

1. 将Commerce元数据添加到资源。 请参阅[将元数据应用到资源](../../aem-assets-integration/get-started/configure-aco.md#step-3-apply-metadata-to-assets)。

1. 审批要交付的资产。 资源必须处于&#x200B;**已批准**&#x200B;状态才能触发同步。

1. 图像会自动同步到[!DNL Commerce Optimizer]。

### 应用AEM-Assets层

要在店面显示AEM Assets图像，请[将`AEM-Assets`图层分配给目录视图](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view)。

## 更多此类内容

* [目录层](catalog-layer.md)
* [目录视图](catalog-view.md)
* [AEM Assets集成指南](../../aem-assets-integration/overview.md)
