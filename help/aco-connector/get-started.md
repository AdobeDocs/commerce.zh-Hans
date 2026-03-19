---
title: Adobe Commerce Optimizer Connector入门
description: 了解如何安装和配置连接器、自定义导出配置、连接到Adobe Commerce Optimizer以及监控数据同步状态。
feature: Personalization, Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
source-git-commit: f302efcb6c08d5a3c695a47ae16fdac790a8bc24
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---


# 快速入门

安装并配置Commerce Optimizer Connector以将您的Adobe Commerce目录数据与[!DNL Adobe Commerce Optimizer]同步，然后监视数据同步状态以确保您的店面为最新状态。

## 使用该集成的要求

* Adobe Commerce 2.4.7+

   * PHP 8.2、8.3或8.4
   * Composer 2.x

* 具有已设置的沙盒实例的[!DNL Adobe Commerce Optimizer]许可证。

* 访问[repo.magento.com](https://repo.magento.com)以使用Composer下载Commerce连接器中继包。

* 管理员访问[Adobe Commerce Optimizer沙盒实例](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance)。

配置集成的Adobe Commerce用户必须具有：

* Adobe Commerce管理员的管理员访问权限。

* [对Adobe Commerce应用程序服务器的命令行访问权限](https://experienceleague.adobe.com/zh-hans/docs/commerce-on-cloud/user-guide/project/user-access)。

* 开发人员对配置了[项目的](https://experienceleague.adobe.com/zh-hans/docs/core-services/interface/administration/organizations?)IMS组织[!DNL Adobe Commerce Optimizer]的访问权限。

>[!BEGINSHADEBOX]

## 先决条件

如果已安装以下任何扩展，请在安装Commerce Optimizer Connector之前卸载它们：

* Adobe Commerce Live Search (`magento/live-search`)
* Adobe Commerce产品推荐(`magento/product-recommendations`)
* Adobe Commerce目录服务(`magento/catalog-service`， `magento/catalog-service-installer`)
* 数据管理仪表板(`magento-catalog-sync-admin`)

与这些扩展关联的数据仍会在Commerce数据库中可用。 但是，在启用连接器时，它不会导出到[!DNL Adobe Commerce Optimizer]。 要在启用连接器后实施这些扩展提供的搜索和促销功能，请从[[!DNL Adobe Commerce Optimizer] 管理员UI](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/overview#quick-tour)配置它们。

>[!ENDSHADEBOX]

## 配置步骤

按照以下步骤启用连接器并开始将数据从Commerce同步到Adobe Commerce Optimizer实例。

1. **[使用编辑器安装Commerce Optimizer连接器包](#install-the-commerce-connector-package)**&#x200B;以将您的Commerce实例连接到[!DNL Adobe Commerce Optimizer]。

1. **[从管理员查看和自定义数据导出配置](#customize-commerce-data-export-configuration)**。

1. **[获取在Commerce和Commerce Optimizer之间建立连接所需的API凭据](#get-required-values-for-configuring-the-commerce-optimizer-connection)**。

1. **[启用 [!DNL Adobe Commerce Optimizer] 集成](#enable-the-adobe-commerce-optimizer-integration)**。

1. **[验证数据同步是否正常工作](#verify-that-the-data-sync-is-working)**。


## 安装Commerce Optimizer连接器软件包

Adobe Commerce Optimizer Connector是作为编辑器中继提供的，适用于具有[!DNL Adobe Commerce Optimizer]的有效许可证的所有Commerce商家。

### 安装步骤

1. 使用编辑器添加`adobe-commerce/commerce-data-export-aco-adapter`模块：

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. 将更改部署到Adobe Commerce暂存环境。

部署完成后，Commerce Optimizer选项可从Commerce的“管理员”菜单使用。 单击&#x200B;**[!UICONTROL Commerce Optimizer]**&#x200B;以直接从Commerce管理员中打开您的Commerce Optimizer实例。

>[!NOTE]
>
>有关详细的扩展安装说明，请参阅以下指南：
>
>在云基础架构上的Adobe Commerce上[安装扩展](https://experienceleague.adobe.com/zh-hans/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[在Adobe Commerce内部部署上安装扩展](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/tutorials/extensions)

### 获取所需的连接详细信息

从Adobe Developer Console中，创建一个为[!DNL Adobe Commerce Optimizer]摄取服务启用的开发人员项目，并生成OAuth服务器到服务器凭据。 有关详细说明，请参阅[促销开发人员指南](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)中的&#x200B;*获取IMS凭据*。

>[!TIP]
>
>如果您在与您的Commerce Optimizer实例相同的IMS组织中已经使用数据摄取API配置了开发人员项目，则可以重用现有的OAuth服务器到服务器凭据。

从“身份证明”页中保存以下值：

* **组织ID** (`org_id`)
* **客户端ID** (`client_id`)
* **客户端密码** (`client_secret`)

### 获取[!DNL Adobe Commerce Optimizer]实例详细信息

从您的[!DNL Adobe Commerce Optimizer]实例中保存实例ID（也称为租户ID）。 您可以在用于访问实例的URL中找到它。 例如，在`https://experience.adobe.com/#/@<project-id>/in:TToyu73daQRn66KAYaq8YZ/commerce-optimizer-studio/home`中，实例ID为`TToyu73daQRn66KAYaq8YZ`。

## 自定义Commerce数据导出配置

默认情况下，所有Commerce作用域（网站和商店视图）的目录数据同步处于启用状态。 您可以自定义导出设置，以便根据业务需求仅同步特定范围的数据。 例如，如果您有多个存储视图，但只想导出其中一个存储视图的数据，则可以为其他存储视图禁用导出程序。

>[!IMPORTANT]
>
>更改导出设置会触发完全重新建立索引，此过程可能需要大量时间，具体取决于您的目录大小。 在低流量期间计划这些更改，以最大程度地降低对性能的影响。

### 按范围导出数据

下表描述了在每个作用域级别导出的数据：

| 范围 | 数据已导出 | 注释 |
| ------- | --------------- | ------- |
| 网站 | 价格和价格手册 | 使用命名约定[将每组价格导出为](../optimizer/setup/pricebooks.md)价格手册`website::customergroupcode`。 包括该网站的所有客户组。 |
| 商店视图 | 产品和产品属性 | 每个存储视图在[!DNL Adobe Commerce Optimizer]中创建一个单独的目录源。 |

### 启用和禁用行为

| 操作 | 结果 |
| -------- | -------- |
| 禁用商店视图 | 目录源仍保留在[!DNL Adobe Commerce Optimizer]中，但已删除所有数据。 |
| 禁用并重新启用商店视图 | 使用完全数据重新同步重新填充同一目录源。 |

### 更新导出配置

安装连接器软件包后，管理员中的商店网格现在会显示Commerce Optimizer的导出配置设置。

![具有Commerce Optimizer同步设置的商店网格](./assets/aco-connector-sync-config.png){width="600" zoomable="yes"}

**要更改网站或商店视图的设置：**

1. 在Commerce管理员中，导航到&#x200B;**[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**。

1. 选择要配置的网站或商店视图。

1. 在&#x200B;**[!DNL Adobe Commerce Optimizer]导出程序设置**&#x200B;中，根据需要使用该复选框启用或禁用数据同步。

   ![更新数据同步配置](./assets/aco-connector-store-website-export-settings.png){width="500" zoomable="yes"}

1. 保存更改。

## 启用[!DNL Adobe Commerce Optimizer]集成

>[!IMPORTANT]
>
>运行配置命令后，数据同步处理便会立即启动。 默认情况下，所有Commerce作用域（网站和商店视图）的目录数据同步处于启用状态。 根据目录的大小，数据同步过程可能需要几分钟到几小时。

使用您在上一步中收集的API凭据和实例详细信息，您现在可以配置Commerce与[!DNL Adobe Commerce Optimizer]实例之间的集成。

1. 从Commerce Admin中，选择&#x200B;**[!UICONTROL Adobe Commerce Optimizer]**&#x200B;以显示包含说明的配置页面。

   ![[!DNL Adobe Commerce Optimizer]配置页面](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. 从命令行中，[使用SSH](https://experienceleague.adobe.com/zh-hans/docs/commerce-on-cloud/user-guide/develop/secure-connections)连接到Commerce暂存环境。

1. 运行以下Commerce CLI命令配置集成，将占位符值替换为Commerce Optimizer项目的值：

```terminal
bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
```

1. 通过返回Commerce管理员并选择[!UICONTROL Adobe Commerce Optimizer]选项来验证连接。

   单击该选项后，它将在新选项卡中打开[!DNL Adobe Commerce Optimizer] UI。

## 验证数据同步是否正常工作

启用集成后，数据同步将自动开始。 根据目录大小，初始同步可能需要几分钟到几小时。

1. **在Commerce管理员中检查同步状态：**

   转到&#x200B;**[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**。

   ![带有馈送项状态报告的数据馈送同步状态页面](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   同步运行时，馈送数据显示已成功发送的记录。 选择信息源以查看详细信息或解决同步问题。

1. **确认数据已送达Commerce Optimizer：**

   从[!DNL Adobe Commerce Optimizer]菜单中选择&#x200B;**[!UICONTROL Data Sync]**。

   ![数据同步](./assets/data-sync.png){width="500" zoomable="yes"}

   验证是否显示预期的产品、价格和属性。

>[!TIP]
>
>如果您遇到数据同步问题，请参阅[SaaS数据导出](/help/data-export/troubleshooting-logging.md)文档中的&#x200B;*疑难解答*&#x200B;部分。

## 后续步骤

1. **[配置 [!DNL Adobe Commerce Optimizer] 目录视图和策略](#configure-adobe-commerce-optimizer-stores)**

   在[!DNL Adobe Commerce Optimizer]指南中创建目录视图和策略。 请注意，价格手册是自动从Adobe Commerce客户组创建的。

1. **[在Edge Delivery Services上设置Commerce店面](#set-up-a-commerce-storefront-on-edge-delivery-services)**

   按照[Storefront设置文档](https://experienceleague.adobe.com/developer/commerce/storefront/setup/?lang=zh-Hans)将您的店面连接到[!DNL Adobe Commerce Optimizer]实例，并开始提供个性化的商务体验。


