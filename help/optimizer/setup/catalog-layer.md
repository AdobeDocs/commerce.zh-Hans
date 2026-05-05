---
title: 目录层
description: 了解目录层如何允许您修改产品数据而不更改原始源数据，以便您可以安全地自定义并随时恢复更改。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 00f5aaa4d08e686195096b3fee0dcca2d2ac56d8
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 0%

---

# 目录层

目录层允许您在不更改原始源数据的情况下修改产品数据。 图层通过在基本目录之上创建一个图层，将更改应用于特定的产品属性，如名称、描述、图像、链接和元数据。 原始产品数据将保持不变，允许您安全地自定义产品并随时恢复更改。

![目录层](../assets/catalog-layers.png)

## 目录层的工作方式

当客户查看您的店面时，系统会将您的基本目录数据与活动目录层相结合，以显示最终产品信息。 以下是此过程的工作方式：

1. **层应用程序** — 使用通道ID和环境ID发出请求时，存储服务将检索相关的目录视图。

1. **数据合并** — 系统根据层优先级顺序将目录层应用于产品数据。

1. **字段处理** — 不同的字段类型处理方式不同：

   * **覆盖字段** — 名称、说明和元标题等文本字段将替换为图层中定义的值，优先级较高的图层优先。
   * **合并字段** — 图像、链接和属性等数组字段由多个图层组合而成，可提供统一的响应。

1. **优先级分辨率** — 顺序字段确定优先的层。 当多个层修改同一个字段时，顺序数较高的层具有更高的优先级（例如，顺序为10的层最高）。

## 目录层用例

目录层通常用于：

* **SEO优化** — 根据[Sites Optimizer](../manage-results/opportunities.md)中的AI建议覆盖产品元标题和描述。
* **季节性促销活动** — 在不更改源数据的情况下临时更新促销活动的产品名称、描述或图像。
* **区域自定义** — 根据地理位置或语言显示不同的产品信息。
* **A/B测试** — 测试不同的产品演示以优化转化率。
* **多品牌管理** — 自定义不同品牌目录视图的产品属性。
* **产品视觉效果** — 将AEM Assets中的产品图像作为图层应用于基础目录之上。

## AEM-Assets layer

当您启用[产品可视化图表](product-visuals.md)时，AEM Assets集成会自动创建和管理专门用于AEM Assets内容的目录层。 默认图层名称为`AEM-Assets`，但是您可以在AEM Assets集成[&#128279;](../../aem-assets-integration/get-started/configure-aco.md)的新用户引导期间指定自定义名称。

此层包含与AEM Assets同步的产品图像。 与其他目录层一样，它是通过[产品层API](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank}填充的。 Assets集成服务将AEM资源元数据和交付URL转换为API格式，并在AEM Assets中批准资源时自动发送数据。

集成支持每个租户一个源（一个区域设置+一个层）。

>[!CAUTION]
>
> 将AEM-Assets层分配给目录视图。 如果未指定图层，产品图像数据可能会意外被覆盖。

### AEM-Assets层的工作原理

1. **自动创建**：在为[!DNL Commerce Optimizer]实例配置AEM Assets集成时创建层。

1. **图像同步**：在AEM Assets中批准资源后，Assets Integration Service将转换资源数据并通过产品层API更新`AEM-Assets`层。

1. **图层分配**：将`AEM-Assets`图层分配给要显示AEM Assets图像的目录视图。

### 将AEM-Assets层分配给目录视图

要在店面中显示AEM Assets图像，请执行以下操作：

1. 导航到&#x200B;_商店设置_，然后单击&#x200B;**[!UICONTROL Catalog views]**。

1. 选择要应用图层的目录视图。

1. 在目录层部分中，找到&#x200B;**AEM-Assets**&#x200B;层。

1. 激活图层以为此目录视图启用它。

1. 单击&#x200B;**[!UICONTROL Save]**&#x200B;以应用更改。

分配后，店面API（目录服务、实时搜索、产品推荐和店面GraphQL API）会返回产品的基本目录图像和AEM Assets图像。

有关配置产品视觉效果的更多信息，请参阅[使用AEM Assets的产品视觉效果](product-visuals.md)。

## 通过数据摄取添加目录层

您可以在数据摄取过程中向产品添加目录层。 此方法非常适用于批量操作或自动化工作流。

>[!NOTE]
>
>您使用摄取API导入目录层，但[使用UI完成图层顺序](#manage-layer-priorities)的设置。

**先决条件：**

* 具有访问数据摄取服务权限的API凭据
* 基础目录中已存在的产品SKU

**步骤：**

1. 使用要修改的产品属性以所需格式准备层数据。

1. 使用产品层API端点摄取层数据。

1. 通过检查目录视图配置，验证是否已成功摄取层。

有关详细的API规范和有效负载示例，请参阅开发人员文档中的[产品层](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank}。

## 在UI中手动添加目录层

>[!NOTE]
>
>此功能尚不可用。

目录视图UI允许您手动创建和管理层，这对于生成AI支持的推荐的Sites Optimizer等集成特别有用。

>[!NOTE]
>
>如果目录视图中不存在Sites Optimizer图层，则Sites Optimizer中的自动修复功能会自动创建一个图层，并为其分配最高优先级（最高编号）。 如果删除此图层，则下次运行Sites Optimizer中的自动修复功能时将重新创建此图层，并将现有图层转换为较低顺序编号。 如果Sites Optimizer层的订单号不同，则自动修复功能不会更改其优先级。

>[!TIP]
>
>对于批量层操作，请使用上面描述的数据摄取API方法[&#128279;](#add-a-catalog-layer-via-data-ingestion)。

**创建手动图层：**

1. 导航到&#x200B;**商店设置** > **目录视图**。

1. 选择要应用图层的目录视图。

1. 在目录层部分中，单击&#x200B;**添加目录层**。

1. 配置层属性：

   * **图层名称** — 输入一个描述性名称以标识该图层的用途。
   * **产品** — 选择应用此层的产品。
   * **属性** — 选择要修改的产品属性（名称、描述、图像、元标记等）。
   * **值** — 为每个选定的属性输入新值。

1. 单击&#x200B;**保存**&#x200B;以创建图层。

新层将添加到目录视图，并自动分配下一个可用订单编号。

## 预览图层效果

>[!NOTE]
>
>此功能尚不可用。

在激活层或更改优先级之前，您可以预览它们对产品数据的影响。

**要预览图层更改：**

1. 导航到&#x200B;**商店设置** > **目录视图**。

1. 选取包含要预览的图层的目录视图。

1. 在目录图层部分中，选择特定产品或使用预览功能。

1. 查看组合的产品数据，该数据显示了层如何修改基本目录值。

1. 根据需要调整图层内容或优先级顺序。

## 激活、取消激活或删除层

您可以在不删除目录层的情况下启用或禁用目录层，从而控制应用特定自定义项的时间。

**要激活或取消激活图层：**

1. 导航到&#x200B;**商店设置** > **目录视图**。

1. 选择包含图层的目录视图。

1. 在目录图层部分中，找到要切换的图层。

1. 单击激活切换可启用或禁用图层。

   * **活动** — 层应用于产品数据。
   * **非活动** — 层已保留，但未应用于产品数据。

1. 更改会立即在您的店面生效。

**要删除图层：**

使用数据摄取API [删除目录层](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers){target=_blank}。

## 管理层优先级

应用图层的顺序决定了当多个图层修改同一产品属性时，哪些值出现在店面上。 管理优先级可确保显示正确的数据。

**了解优先级顺序：**

* 每个层都分配有一个序号（1、2、3等）
* 数字越大，表示优先级越高，并覆盖所有其他层
* 当多个层修改同一个字段时，顺序号较高的层优先
* 优先级仅适用于覆盖字段（名称、描述、元标记）
* 合并字段（图像、链接、属性）组合来自所有图层的数据

**要重新排序层优先级：**

1. 导航到&#x200B;**商店设置** > **目录视图**。

1. 选择包含要重新排序的图层的目录视图。

1. 在目录图层部分中，找到要移动的图层。

1. 拖放图层以更改其位置，或者使用重新排序控件。

1. 系统将根据新顺序自动更新订单编号。

1. 单击&#x200B;**保存**&#x200B;以应用新的优先级顺序。

>[!IMPORTANT]
>
>对层优先级的更改将立即生效，并可能影响客户在您店面看到的内容。 在保存之前查看预览，以确保应用正确的值（**预览尚不可用**）。

## 最佳实践

使用目录层时，请遵循以下建议：

* **使用描述性名称** — 为图层命名以清楚地指示其用途（例如，“Holiday 2025 Campaign”或“SEO优化 — 产品页面”）。

* **限制层** — 虽然系统支持多个层，但使用太多可能会影响性能。 如果可能，合并层。

<!--- **Test before activating**—Always preview layer effects before activating them on your live storefront. !!!REMOVE IF PREVIEW NOT AVAILABLE FOR GA!!!-->

* **文档优先级逻辑** — 跟踪应该优先的层，以避免意外覆盖。

* **查看Sites Optimizer图层** — 使用Sites Optimizer中的自动修复时，系统会创建具有最高优先级的图层。 在添加可能覆盖AI推荐的手动层时请务必小心。 了解有关使用[Sites Optimizer](../manage-results/opportunities.md)的更多信息。

* **监控性能** — 如果您发现产品页面加载速度慢，请检查您的层配置并考虑合并层。

## 更多此类内容

* [目录视图](catalog-view.md) — 为不同的店面配置目录视图
* [产品视觉效果](product-visuals.md) — 将AEM Assets用于产品图像
* [机会](../manage-results/opportunities.md) — 了解使用目录层的AI支持优化
