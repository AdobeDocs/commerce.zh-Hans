---
title: '[!DNL Manage the Data Export extension]'
description: 了解如何升级 [!DNL Data Export] 扩展以及删除或禁用不需要的数据导出服务。
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
source-git-commit: ea722d5e427e5bf536b9f2d2322f0dabb2981c77
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 管理SaaS数据导出扩展

SaaS服务的[[!DNL data export] 扩展](https://github.com/magento/commerce-data-export)是启用Adobe Commerce与连接的Commerce服务之间的数据收集和同步的模块的集合。

Adobe Commerce Services扩展的中继中包含特定模块，例如
作为[实时搜索](/help/live-search/overview.md)、[产品推荐](/help/product-recommendations/overview.md)和[目录服务](/help/catalog-service/overview.md)。 如果您使用这些服务，则无需单独安装即可启用Data Export扩展。

## 删除或禁用Commerce数据导出功能

如果您不需要某个已安装的商务数据导出模块，请使用`magento:module:disable` CLI命令将其禁用。

例如，有一个[类别API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/)在内部使用类别权限馈送数据。 如果您未使用此API，则可以禁用类别权限馈送的数据导出。

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### 将模块更新至特定版本

您可以使用编辑器更新任何已安装的商务数据导出模块。 例如，您可以将模块更新为指定版本，也可以更新任何所需的依赖项。

1. 登录到Commerce应用程序服务器。

1. 从命令行中，使用编辑器更新模块：

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

如果将Commerce实例部署在云基础架构上，请从云项目目录更新扩展。 请参阅[云基础架构上的Adobe Commerce指南](https://experienceleague.adobe.com/zh-hans/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)中的&#x200B;_升级扩展_。
