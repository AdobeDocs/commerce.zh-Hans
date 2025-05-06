---
title: 入门
description: 了解 [!DNL Product Recommendations]中的要求和支持平台。
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Onboarding

The onboarding process for [!DNL Product Recommendations] requires access to the command line of the server and consists of the following steps. If you are not familiar with working from the command line, ask a developer or system integrator to help.

- [Implementation Workflow](implementation-workflow.md)
- [Install and Configure](install-configure.md)
- [设置](settings.md)
- [验证](verify.md)
- [暂存环境](staging-environment.md)

## 要求

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
- Composer 2

### 支持的平台

- Adobe Commerce on premise (EE) : 2.4.4+
- Adobe Commerce on Cloud (ECE) ：2.4.4+

## 端点

[!DNL Product Recommendations]通过`https://catalog-service.adobe.io/graphql`处的端点进行通信。

### Page Builder支持

[!DNL Product Recommendations]可以作为页面生成器内容类型添加到页面中。 要向产品推荐添加页面生成器支持，请参阅[安装和配置](install-configure.md)。

See [[!DNL Page Builder] Integration](page-builder.md) for instructions on how to add [!DNL Product Recommendations] into [!DNL Page Builder] content.

### SaaS price indexing

Product Recommendation customers can use [SaaS price indexing](../price-index/price-indexing.md), which provides faster price changes updates and synchornization time.

### B2B支持 {#b2bsupport}

B2B storefronts often require complex logic that dictates product visibility and pricing for each shopper or customer group. [!DNL Product Recommendations] now [support](release-notes.md) this functionality by honoring [category permissions](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=zh-Hans), [shared catalogs](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html?lang=zh-Hans), and [customer group-specific pricing](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hans). For example, if you have hidden certain categories from your retail customer segment, then a shopper in that segment would not be shown recommendations for products in those categories. Also, when you define a shared catalog for specific customer groups and companies, those shoppers see recommendations only for products they can access. All recommended products reflect correct customer group-specific price based on each shopper&#39;s customer group.

>[!NOTE]
>
>商家可以使用[目录服务](../catalog-service/overview.md)店面API自定义和扩展构件或店面元素，但任何自定义都不在Adobe支持团队的覆盖范围内。
