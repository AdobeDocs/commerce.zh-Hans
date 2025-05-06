---
title: 载入和安装
description: 了解如何安装 [!DNL Catalog Service]
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# 载入和安装

安装目录服务，以使用[目录服务GraphQL API](https://developer.adobe.com/commerce/services/graphql/catalog-service/)从Commerce实例请求和接收产品数据。 目录服务是作为repo.magento.com存储库中的编辑器中继包提供的。

>[!NOTE]
>
>If your Commerce instance uses Live Search or Product Recommendations, the Catalog Service is installed or updated automatically when you onboard or upgrade those services. For details, see the installation instructions for [Live Search](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/install) and [Product Recommendations](https://experienceleague.adobe.com/zh-hans/docs/commerce/product-recommendations/getting-started/install-configure).



## 系统要求

**软件要求**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3, 8.4
- Composer： 2.x

**支持的平台**

- 云基础架构上的Adobe Commerce：2.4.4+
- Adobe Commerce内部部署：2.4.4+

## 端点

[!DNL Catalog Service]有两个端点可供载入：

- 沙盒(`https://catalog-service-sandbox.adobe.io/graphql`) — 用于上线前的测试和验证
- 生产(`https://catalog-service.adobe.io/graphql`) — 用于Commerce商家和网站的实时流量

所有Commerce测试实例都使用沙盒端点。

对沙盒端点执行所有加载测试。 在开始加载测试之前，请提交[支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=zh-Hans#submit-ticket)，以便服务团队可以预见额外的服务器流量。

## 安装和配置

To get started with [!DNL Catalog Service] for Adobe Commerce, the following steps are required:

- 安装目录服务扩展(`magento/catalog-service`)
- 配置服务和数据导出
- 访问服务

### 安装目录服务扩展

>[!BEGINSHADEBOX]

**预修课程**

- 访问[repo.magento.com](https://repo.magento.com)以安装扩展。 有关密钥生成和获取必要的权限，请参阅[获取您的身份验证密钥](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)。 有关云安装，请参阅[云基础架构上的Commerce指南](https://experienceleague.adobe.com/zh-hans/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- 访问Adobe Commerce应用程序服务器的命令行。

>[!ENDSHADEBOX]

在运行Adobe Commerce 2.4.4或更高版本的Adobe Commerce实例上安装最新版本的目录服务扩展(`magento/catalog-service`)。 目录服务是作为[repo.magento.com](https://repo.magento.com)存储库中的编辑器中继包提供的。

>[!BEGINTABS]

>[!TAB 云基础架构]

使用此方法为Commerce Cloud实例安装[!DNL Catalog Service]。

1. 在本地工作站上，转到云基础架构项目上Adobe Commerce的项目目录。

   >[!NOTE]
   >
   >有关在本地管理Commerce项目环境的信息，请参阅《云基础架构用户指南》_上的_ Adobe Commerce中的[使用CLI管理分支](https://experienceleague.adobe.com/zh-hans/docs/commerce-cloud-service/user-guide/develop/cli-branches)。

1. 查看要使用Adobe Commerce Cloud CLI更新的环境分支。

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. 添加目录服务模块。

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. 更新包依赖关系。

   ```bash
   composer update "magento/catalog-service"
   ```

1. 提交和推送`composer.json`和`composer.lock`文件的代码更改。

1. 添加、提交并将`composer.json`和`composer.lock`文件的代码更改推送到云环境。

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   将更新推送到云环境会启动[Commerce云部署流程](https://experienceleague.adobe.com/zh-hans/docs/commerce-cloud-service/user-guide/develop/deploy/process)以应用更改。 从[部署日志](https://experienceleague.adobe.com/zh-hans/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log)中检查部署状态。

>[!TAB 内部部署]

Use this method to install the [!DNL Catalog Service] for an on-premises instance.

1. Use Composer to add the Catalog Service module to your project:

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. 更新依赖项并安装扩展：

   ```bash
   composer update  "magento/catalog-service"
   ```

1. 升级Adobe Commerce：

   ```bash
   bin/magento setup:upgrade
   ```

1. 清除缓存：

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >在某些情况下，特别是在部署到生产环境时，您可能希望避免清除编译的代码，因为这样可能需要一些时间。 在进行任何更改之前，请确保备份系统。

>[!ENDTABS]

### 配置服务和数据导出

安装[!DNL Catalog Service]后，请完成以下任务以将目录服务与Adobe Commerce实例集成。 此集成支持在Commerce实例、目录服务和其他支持服务之间进行数据同步和通信。 数据同步由[SaaS Data Export扩展](../data-export/overview.md)处理。

1. 通过指定API密钥并选择SaaS数据空间来设置[Commerce Services Connector](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/integration-services/saas)。

   Commerce服务连接器设置是使用Adobe Commerce服务（如目录服务、实时搜索和产品推荐）所需的一次性过程。 如果已为其他服务配置了连接器，请跳过此步骤。

1. 从[数据管理功能板](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-dashboard)执行初始数据同步。

   初始同步可能需要几分钟到几小时时间，具体取决于目录大小。 您可以从“数据管理”仪表板监视同步状态。 初始同步后，目录会持续导出产品数据以使服务保持最新。

   >[!NOTE]
   >
   >您还可以使用Commerce CLI从命令行启动初始同步。 请参阅&#x200B;_SaaS数据导出指南_&#x200B;中的[初始同步](../data-export/data-export-cli-commands.md#initial-sync)。

To ensure that the catalog export is running correctly:

- [Confirm that cron jobs are running](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- 验证索引器是从[Admin](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/tools/index-management)运行，还是使用Commerce CLI命令`bin/magento indexer:info`运行。
- 验证`Catalog Attributes Feed, Product Feed, Product Overrides Feed`和`Product Variant Feed`索引器是否设置为`Update by Schedule`。

### 监测数据同步并排除其故障

通过Commerce Admin，您可以使用[数据管理功能板](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-dashboard)监视同步过程。 Use the [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) and logs to manage and troubleshoot the process.

### 访问服务

The [!DNL Catalog Service] GraphQL API is accessible from the ` https://catalog-service.adobe.io/graphql` endpoint using POST commands over HTTPS.

In your GraphQL queries, you must specify multiple HTTP headers including the public API key you added to the Adobe Commerce Services Connector configuration in the Admin. For details, see the [Storefront Services GraphQL](https://developer.adobe.com/commerce/services/graphql/) documentation.

### Firewall configuration

要允许[!DNL Catalog Service]通过防火墙，请将`commerce.adobe.io`添加到允许列表。

## 目录服务和API网格

适用于Adobe Developer App Builder[&#128279;](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/)的API Mesh使开发人员能够使用Adobe IO将专用或第三方API以及其他接口与Adobe产品集成。

有关安装和配置详细信息，请参阅[[!DNL Catalog Service] 和API Mesh](mesh.md)主题。

## 数据管理功能板

有关[!DNL Catalog Service]数据同步的详细信息，请参阅[数据管理功能板](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-dashboard)。
