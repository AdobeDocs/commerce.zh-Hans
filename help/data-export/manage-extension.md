---
title: '[!DNL Manage the Data Export extension]'
description: 了解如何升级 [!DNL Data Export] 扩展以及删除或禁用不需要的数据导出服务。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
TQID: https://experienceleague.adobe.com/ghrA-YFR7hurQgEnjS8PdxR7Zcx-ayLTuyBfhbCC-KI
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: d3cdead0-685a-4489-9250-4bb709942f66
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# 管理SaaS数据导出扩展

SaaS服务的[[!DNL data export] 扩展](https://github.com/magento/commerce-data-export)是启用Adobe Commerce与连接的Commerce服务之间的数据收集和同步的模块的集合。

Adobe Commerce Services扩展的中继中包含特定模块，例如
作为[实时搜索](/help/live-search/overview.md)、[产品推荐](/help/product-recommendations/overview.md)、[目录服务](/help/catalog-service/overview.md)和[[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md)。 如果您使用这些服务，则无需单独安装即可启用Data Export扩展。

## 删除或禁用Commerce数据导出功能

如果您不需要某个已安装的商务数据导出模块，请使用`magento:module:disable` CLI命令将其禁用。

例如，有一个[类别API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/)在内部使用类别权限馈送数据。 如果您未使用此API，则可以禁用类别权限馈送的数据导出。

```shell
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### 将模块更新至特定版本

您可以使用编辑器更新任何已安装的商务数据导出模块。 查看[发行说明](release-notes.md)以确定是否有所需的修复可用，然后升级到特定版本和任何所需的依赖项。

>[!NOTE]
>
>如果您更新到[Live Search](/help/live-search/overview.md)、[目录服务](/help/catalog-service/overview.md)、[产品推荐](/help/product-recommendations/overview.md)或[[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md)的最新版本，您还将获得最新版本的数据导出扩展。 数据导出中继包是这些服务的Composer包的依赖项。

1. 登录到Commerce应用程序服务器。

1. 从命令行中，使用编辑器更新模块：

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

如果将Commerce实例部署在云基础架构上，请从云项目目录更新扩展。 请参阅&#x200B;_云基础架构上的Adobe Commerce指南_&#x200B;中的[升级扩展](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension)。

>[!MORELIKETHIS]
>
> - [发行说明](release-notes.md)
> - [SaaS数据导出模块](reference/data-export-modules.md)
> - [指南概述](overview.md)
