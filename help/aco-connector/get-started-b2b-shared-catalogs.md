---
title: 为B2B Commerce设置连接器
description: 了解如何安装B2B连接器、选择Commerce范围、同步共享目录数据、验证目录视图以及监控投影运行状况。
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
last-update: 2026-10-01
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
source-wordcount: '843'
ht-degree: 0%
---

# 为B2B Commerce设置连接器

使用[!DNL Adobe Commerce] B2B共享目录的商家可以使用[!DNL Adobe Commerce Optimizer Connector for B2B]将自定义共享目录数据和配置同步到[!DNL Adobe Commerce Optimizer]。

{{aco-integration-environment-alignment}}

## 使用该集成的要求 {#requirements-to-use-the-integration}

* 已安装并启用[Adobe Commerce B2B版本1.5.3+](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/install)的Commerce 2.4.8+。

* 具有已设置的沙盒实例的[!DNL Commerce Optimizer]许可证。

* [身份验证密钥](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)以使用编辑器下载连接器元包。

* 管理员访问[[!DNL Commerce Optimizer] 沙盒实例](../optimizer/get-started.md)。

配置集成的[!DNL Adobe Commerce]用户必须具有：

* Commerce管理员的管理员访问权限。

* [对 [!DNL Adobe Commerce] 应用程序服务器](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access)的命令行访问权限。

* 开发人员对配置了[!DNL Commerce Optimizer]项目的[IMS组织](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations？)的访问权限。

### 应用程序要求

* Commerce cron和索引器运行正常。
* 为导出标识的所需网站和存储视图。
* 在Adobe Commerce中配置或准备配置的共享目录、公司分配、分类和B2B定价。

>[!BEGINSHADEBOX]

## 删除冲突的扩展 {#remove-conflicting-extensions}

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## 配置步骤 {#configuration-steps}

要启用[!DNL Adobe Commerce Optimizer Connector for B2B]并开始将自定义共享目录配置从[!DNL Adobe Commerce]同步到[!DNL Commerce Optimizer]实例，请执行以下步骤。

1. **[使用编辑器安装 [!DNL Adobe Commerce Optimizer Connector for B2B] 包](#install-the-adobe-commerce-optimizer-connector-for-B2B-package)**&#x200B;以将您的[!DNL Adobe Commerce]实例连接到[!DNL Commerce Optimizer]。

1. 从管理员&#x200B;**[自定义Commerce范围导出配置](#data-export-and-scope-mapping)**。

1. **[启用 [!DNL Commerce Optimizer] 集成](#enable-the-adobe-commerce-optimizer-integration)**。

1. **[验证数据同步是否正常工作](#verify-that-the-data-sync-is-working)**。

## 安装[!DNL Adobe Commerce Optimizer Connector for B2B]包 {#install-the-adobe-commerce-optimizer-connector-for-B2B-package}

[!DNL Adobe Commerce Optimizer Connector for B2B]作为可用于所有Commerce商家（具有[!DNL Commerce Optimizer]的有效许可证）的Composer元包进行交付。

### 安装步骤

1. 使用编辑器添加`adobe-commerce/commerce-data-export-aco-adapter-b2b`模块：

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter-b2b
   ```

1. 将更改部署到[!DNL Adobe Commerce]暂存环境。

   部署完成后，[!DNL Commerce Optimizer]选项可从Commerce的“管理员”菜单使用。 选择&#x200B;**[!UICONTROL Commerce Optimizer]**&#x200B;以直接从Commerce管理员中打开您的[!DNL Commerce Optimizer]实例。

{{install-extension-links}}

### 数据导出和范围映射

选择要同步的网站和存储视图，然后验证初始馈送。 对于B2B，连接器在将共享目录数据项目到[!DNL Commerce Optimizer]时使用启用的范围。

* **→目录源存储视图**&#x200B;和本地化的产品内容
* **网站和客户组**→网站和客户组定价的价格手册
* **共享目录**→受保护的专用目录视图和强制的策略

共享目录定义产品分类，每个启用的商店视图都提供本地化的目录源。 网站和客户组确定适用的价格手册。 连接器会为每个启用的存储视图投影每个自定义共享目录，因此您不需要B2B投影的单独范围设置。

自定义共享目录可以生成多个受保护的专用目录视图，每个视图对应一个启用的存储视图。 默认的公共共享目录未投影为B2B专用目录视图。 有关详细的对象映射和运行时授权流程，请参阅[B2B共享目录投影](b2b-shared-catalog-projection.md)。

>[!IMPORTANT]
>
>更改导出设置会触发完全重新索引，此过程可能需要花费大量时间，具体取决于您的目录大小。 在启用集成并启动初始数据同步之前配置Commerce范围。

### 要更改作用域导出设置

1. 在Commerce管理员中，转到&#x200B;**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**。

1. 选择要配置的网站或商店视图。

1. 在&#x200B;**[!DNL Commerce Optimizer]导出程序设置**&#x200B;中，根据需要使用该复选框启用或禁用数据同步。

   ![更新数据同步配置](./assets/aco-connector-b2b-storeview-list.png){width="500" zoomable="yes"}

1. 保存更改。

### 启用和禁用行为

| 操作 | 结果 |
| -------- | -------- |
| 禁用商店视图 | **禁用同步将从B2B店面中删除目录数据。** 目录源仍保留在[!DNL Adobe Commerce Optimizer]中，但在下次cron运行时所有同步的数据都将被删除。 |
| 禁用并重新启用商店视图 | 使用完全数据重新同步重新填充同一目录源。 |

### 监视B2B共享目录更改

连接器会监视对共享目录和公司分配的更改。 当您在Commerce管理员中删除共享目录时，连接器会在可配置的宽限期之后删除对其专用目录视图的访问权限。

>[!NOTE]
>
>删除宽限期默认为七天。 您可以通过更新目录视图同步设置配置来更改它。 请参阅[目录视图同步状态配置](catalog-view-sync-status.md#configure-aco-catalog-view-sync-settings)。

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

1. **监视B2B目录视图投影**

在初始信息源同步之后，使用[目录视图同步状态](catalog-view-sync-status.md)验证预计的专用目录视图、策略、价格手册引用和受限访问密钥配置。 有关投影模型和运行时授权流，请参阅[B2B共享目录投影](b2b-shared-catalog-projection.md)。

1. **在[!DNL Edge Delivery Services]**&#x200B;上设置Commerce店面

   要将店面连接到[!DNL Commerce Optimizer]实例并开始提供个性化的商务体验，请按照[店面设置文档](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}操作。
