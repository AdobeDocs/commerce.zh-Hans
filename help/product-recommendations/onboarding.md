---
title: 入门
description: 了解 [!DNL Product Recommendations]中的要求和支持平台。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# 入门

[!DNL Product Recommendations]的载入流程需要访问服务器的命令行，该流程包含以下步骤。 如果您不熟悉如何使用命令行，请向开发人员或系统集成商寻求帮助。

- [实施工作流](implementation-workflow.md)
- [安装和配置](install-configure.md)
- [设置](settings.md)
- [验证](verify.md)
- [暂存环境](staging-environment.md)

## 要求

- Adobe Commerce 2.4.4+
- PHP 8.1、8.2
- 作曲者2

### 支持的平台

- Adobe Commerce内部部署(EE)：2.4.4+
- Adobe Commerce on Cloud (ECE) ：2.4.4+

## 端点

[!DNL Product Recommendations]通过`https://catalog-service.adobe.io/graphql`处的端点进行通信。

### Page Builder支持

[!DNL Product Recommendations]可以作为页面生成器内容类型添加到页面中。 要向产品推荐添加页面生成器支持，请参阅[安装和配置](install-configure.md)。

有关如何将[!DNL Product Recommendations]添加到[!DNL Page Builder]内容的说明，请参阅[[!DNL Page Builder] 集成](page-builder.md)。

### SaaS价格索引

产品推荐客户可以使用[SaaS价格索引](../price-index/price-indexing.md)，这提供了更快的价格更改更新和同步时间。

### B2B支持 {#b2bsupport}

B2B店面通常需要复杂的逻辑，这些逻辑指示每个购物者或客户组的产品可见性和定价。 [!DNL Product Recommendations]现在[支持](release-notes.md)此功能通过遵守[类别权限](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html)、[共享目录](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html)和[特定于客户组的定价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)来实现。 例如，如果您在零售客户区段中隐藏了某些类别，则该区段中的购物者不会显示这些类别中的产品推荐。 此外，在为特定客户组和公司定义共享目录时，这些购物者只会看到他们能够访问的产品推荐。 所有推荐产品均反映根据每位购物者的客户组确定的正确客户组特定价格。

>[!NOTE]
>
>商家可以使用[目录服务](../catalog-service/overview.md)店面API自定义和扩展构件或店面元素，但任何自定义都不在Adobe支持团队的覆盖范围内。
