---
title: 开始使用[!DNL Adobe Commerce Optimizer Connector]
description: 了解如何安装[!DNL Adobe Commerce Optimizer Connector]、配置作用域导出设置、启用IMS身份验证以及验证目录同步。
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
autotag-review: '2026-06-09T16:55:50.934Z'
last-update: 2026-10-01
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: c76e776250d9f996daf61d3cf62e2070803e998c
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%
---

# 快速入门

安装并配置[!DNL Adobe Commerce Optimizer Connector]以将您的[!DNL Adobe Commerce]目录数据与[!DNL Adobe Commerce Optimizer]同步，然后监视数据同步状态以确保您的店面是最新的。

{{aco-integration-environment-alignment}}

>[!NOTE]
>
>本主题涵盖[!DNL Adobe Commerce Optimizer Connector]。 如果您使用[!DNL Adobe Commerce] B2B共享目录，请按照[开始使用 [!DNL Adobe Commerce Optimizer Connector for B2B]](get-started-b2b-shared-catalogs.md)说明。 B2B连接器扩展了基本目录数据同步，以支持自定义共享目录的同步。

## 使用该集成的要求 {#requirements-to-use-the-integration}

* [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.7+。 有关详细要求，请参阅[系统要求](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements)。

* 具有已设置的沙盒实例的[!DNL Commerce Optimizer]许可证。

* [身份验证密钥](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)以使用编辑器下载连接器中继包。

* 管理员访问[[!DNL Commerce Optimizer] 沙盒实例](../optimizer/get-started.md)。

配置集成的[!DNL Adobe Commerce]用户必须具有：

* Commerce管理员的管理员访问权限。

* [对 [!DNL Adobe Commerce] 应用程序服务器](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access)的命令行访问权限。

* 开发人员对配置了[!DNL Commerce Optimizer]项目的[IMS组织](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations？)的访问权限。

>[!BEGINSHADEBOX]

## 删除冲突的扩展

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## 配置步骤 {#configuration-steps}

要启用[!DNL Adobe Commerce Optimizer Connector]并开始将数据从[!DNL Adobe Commerce]同步到[!DNL Commerce Optimizer]实例，请执行以下步骤。

1. **[使用编辑器安装 [!DNL Adobe Commerce Optimizer Connector] 包](#install-the-adobe-commerce-optimizer-connector-package)**&#x200B;以将您的[!DNL Adobe Commerce]实例连接到[!DNL Commerce Optimizer]。

1. 从管理员&#x200B;**[自定义Commerce范围导出配置](#customize-the-commerce-scopes-export-configuration)**。

1. **[启用 [!DNL Commerce Optimizer] 集成](#enable-the-adobe-commerce-optimizer-integration)**。

1. **[验证数据同步是否正常工作](#verify-that-the-data-sync-is-working)**。

## 安装[!DNL Adobe Commerce Optimizer Connector]包 {#install-the-adobe-commerce-optimizer-connector-package}

[!DNL Adobe Commerce Optimizer Connector]作为编辑器中继资料传递，适用于具有[!DNL Commerce Optimizer]的有效许可证的所有Commerce商家。

### 安装步骤

1. 使用编辑器添加`adobe-commerce/commerce-data-export-aco-adapter`模块：

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. 将更改部署到[!DNL Adobe Commerce]暂存环境。

   部署完成后，[!DNL Commerce Optimizer]选项可从Commerce的“管理员”菜单使用。 选择&#x200B;**[!UICONTROL Commerce Optimizer]**&#x200B;以直接从Commerce管理员中打开您的[!DNL Commerce Optimizer]实例。

{{install-extension-links}}

## 自定义Commerce范围导出配置 {#customize-the-commerce-scopes-export-configuration}

默认情况下，所有Commerce作用域（网站、客户组和商店视图）均启用目录数据同步。 您可以自定义导出设置，以便根据业务需求仅同步特定范围的数据。 例如，如果多个存储视图共享相同的语言，则可以导出一个存储视图的数据，并将其用作[!DNL Commerce Optimizer]中多个目录视图的[目录源](../optimizer/setup/catalog-sources.md)。

>[!IMPORTANT]
>
>更改导出设置会触发完全重新建立索引，此过程可能需要大量时间，具体取决于您的目录大小。 Adobe建议先将Commerce范围配置为同步到[!DNL Commerce Optimizer]，然后再启用集成并启动初始数据同步。

下表描述了在每个作用域级别导出的数据：

| 范围 | 数据已导出 | 注释 |
| ----- | ------------- | ----- |
| 网站和客户组 | 价格和价格手册 | 使用命名约定`&lt;website&gt;::&lt;SHA1 of customer group ID&gt;`将每组价格导出为[价格手册](../optimizer/setup/pricebooks.md)。 包括该网站的所有客户组。 |
| 商店视图 | 产品和产品属性 | 每个存储视图在[!DNL Commerce Optimizer]中创建单独的[目录源](../optimizer/setup/catalog-sources.md)。 |

![具有Commerce Optimizer同步设置的商店网格](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

### 要更改作用域导出设置

1. 在Commerce管理员中，转到&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**。

1. 选择要配置的网站或商店视图。

1. 在&#x200B;**[!DNL Commerce Optimizer]导出程序设置**&#x200B;中，根据需要使用该复选框启用或禁用数据同步。

   ![更新数据同步配置](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. 保存更改。

### 启用和禁用行为

| 操作 | 结果 |
| -------- | -------- |
| 禁用商店视图 | **禁用同步将从店面中删除目录数据。** 目录源仍保留在[!DNL Commerce Optimizer]中，但在下次cron运行时所有同步的数据都将被删除。 |
| 禁用并重新启用商店视图 | 使用完全数据重新同步重新填充同一目录源。 |

## 启用[!DNL Commerce Optimizer]集成 {#enable-the-adobe-commerce-optimizer-integration}

通过运行`aco:config:init` CLI命令启用集成并启动数据同步。 此命令完成以下步骤：

1. 使用作为命令行参数提供的凭据获取IMS访问令牌。
1. 在`https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}`处调用Commerce Cloud Manager (CCM)服务以验证租户并提取引入URL和[!DNL Commerce Optimizer] Studio URL。
1. 将所有配置（已加密的客户端密钥）保存到`core_config_data`。
1. 通过使所有[!DNL Commerce Optimizer]馈送索引器失效来计划初始完全同步。


{{aco-data-sync-processing-note}}

## 获取所需的连接详细信息

{{$include /help/_includes/aco-connector/connection-details.md}}

### 获取[!DNL Commerce Optimizer]实例详细信息

{{$include /help/_includes/aco-connector/configure-connection.md}}

## 验证数据同步是否正常工作 {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## 后续步骤

1. **配置[!DNL Commerce Optimizer]目录视图和策略**

   在[!DNL Commerce Optimizer]用户界面中创建目录视图和策略。 请注意，价格手册是从[!DNL Adobe Commerce]客户组自动创建的。 有关说明，请参阅&#x200B;*[!DNL Commerce Optimizer]用户指南*&#x200B;中的[目录视图](../optimizer/setup/catalog-view.md)和[策略](../optimizer/setup/policies.md)文档。 要限制对目录视图的访问，请参阅[私有目录视图](../optimizer/setup/private-catalog-view.md)。

1. **在[!DNL Edge Delivery Services]**&#x200B;上设置Commerce店面

   要将店面连接到[!DNL Commerce Optimizer]实例并开始提供个性化的商务体验，请按照[店面设置文档](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}操作。
