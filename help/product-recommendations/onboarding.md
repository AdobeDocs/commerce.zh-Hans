---
title: 入门
description: 了解 [!DNL Product Recommendations]中的要求和支持平台。
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
TQID: https://experienceleague.adobe.com/FLrOFe-Lwe7i3dOwCISflVGEv2MIkXmmE-NqTvpaY-0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 0802d0e53a1ed6701318647b7bf78435082ad5f3
workflow-type: tm+mt
source-wordcount: 477
ht-degree: 0%

---

# 入门

>[!IMPORTANT]
>
>**产品推荐不是HIPAA就绪的服务。** 请勿在使用HIPAA就绪产品或以其他方式处理受保护的健康信息(PHI)的任何Adobe Commerce实施中启用或使用产品推荐。 “产品推荐”是当前分类为不符合HIPAA要求的Commerce SaaS服务的一部分。
>
>有关哪些Adobe Commerce功能支持HIPAA以及哪些服务不能与PHI一起使用的详细信息，请参阅Adobe Commerce上的[HIPAA准备工作](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/start/compliance/hipaa-ready-service/overview)和[操作](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)。

[!DNL Product Recommendations]的载入流程需要访问服务器的命令行，该流程包含以下步骤。 如果您不熟悉如何使用命令行，请向开发人员或系统集成商寻求帮助。

- [实施工作流](implementation-workflow.md)
- [安装和配置](install-configure.md)
- [设置](settings.md)
- [验证](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify)
- [暂存环境](staging-environment.md)

## 要求

[Adobe Commerce](https://business.adobe.com/cn/products/magento/magento-commerce.html) 2.4.4+。 有关详细信息，请参阅[系统要求](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/system-requirements){target="_blank"}。

### 支持的平台

- Adobe Commerce内部部署(EE)：2.4.4+
- Adobe Commerce on Cloud (ECE) ：2.4.4+

有关详细要求，请参阅[系统要求](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/system-requirements)。

## 端点

[!DNL Product Recommendations]通过`https://catalog-service.adobe.io/graphql`处的端点进行通信。

### Page Builder支持

[!DNL Product Recommendations]可以作为页面生成器内容类型添加到页面中。 要向产品推荐添加页面生成器支持，请参阅[安装和配置](install-configure.md)。

有关如何将[!DNL Product Recommendations]添加到[!DNL Page Builder]内容的说明，请参阅[[!DNL Page Builder] 集成](page-builder.md)。

### Fastly图像优化

[!DNL Product Recommendations]支持可选的[Fastly图像优化](install-configure.md#fastlysupport)模块，该模块将Fastly图像优化参数应用于[!DNL Product Recommendations]图像URL。 要添加此支持，请参阅[安装和配置](install-configure.md#fastlysupport)。

### SaaS价格索引

产品推荐客户可以使用[SaaS价格索引](../price-index/price-indexing.md)，这提供了更快的价格更改更新和同步时间。

### B2B支持 {#b2bsupport}

B2B店面通常需要复杂的逻辑，这些逻辑指示每个购物者或客户组的产品可见性和定价。 [!DNL Product Recommendations]现在[支持](release-notes.md)此功能通过遵守[类别权限](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/categories/category-permissions)、[共享目录](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/b2b/shared-catalogs/catalog-shared)和[特定于客户组的定价](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/products/pricing/pricing-advanced)来实现。 例如，如果您在零售客户区段中隐藏了某些类别，则该区段中的购物者不会显示这些类别中的产品推荐。 此外，在为特定客户组和公司定义共享目录时，这些购物者只会看到他们能够访问的产品推荐。 所有推荐产品均反映了根据每位购物者的客户群确定的正确客户群特定价格。

>[!NOTE]
>
>商家可以使用[目录服务](../catalog-service/overview.md)店面API自定义和扩展构件或店面元素，但任何自定义都不在Adobe支持团队的覆盖范围内。
