---
title: 安装
description: 了解如何安装 [!DNL Catalog Service]
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"
source-git-commit: 1cb6443e79e0e3d813550f9b619b3a0f641cd989
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# 载入和安装

安装目录服务，以使用[目录服务GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)从Commerce实例请求和接收产品数据。 目录服务是作为repo.magento.com存储库中的编辑器中继包提供的。

>[!NOTE]
>
>如果您的Commerce实例使用实时搜索或产品推荐，则当您载入或升级这些服务时，会自动安装或更新目录服务。 有关详细信息，请参阅[实时搜索](https://experienceleague.adobe.com/zh-hans/docs/commerce/live-search/install)和[产品推荐](https://experienceleague.adobe.com/zh-hans/docs/commerce/product-recommendations/getting-started/install-configure)的安装说明。


## 系统要求

**软件要求**

- Adobe Commerce 2.4.4+
- PHP 8.1、8.2、8.3和8.4
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

要开始使用Adobe Commerce的[!DNL Catalog Service]，需要执行以下步骤：

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
   >有关在本地管理Commerce项目环境的信息，请参阅《云基础架构用户指南》[上的](https://experienceleague.adobe.com/zh-hans/docs/commerce-cloud-service/user-guide/develop/cli-branches)Adobe Commerce中的&#x200B;_使用CLI管理分支_。

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

1. 添加、提交并将`composer.json`和`composer.lock`文件的代码更改推送到云环境。

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   将更新推送到云环境会启动[Commerce云部署流程](https://experienceleague.adobe.com/zh-hans/docs/commerce-cloud-service/user-guide/develop/deploy/process)以应用更改。 从[部署日志](https://experienceleague.adobe.com/zh-hans/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log)中检查部署状态。

>[!TAB 内部部署]

使用此方法为内部部署实例安装[!DNL Catalog Service]。

1. 使用Composer将Catalog Service模块添加到您的项目中：

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
   >您还可以使用Commerce CLI从命令行启动初始同步。 请参阅[SaaS数据导出指南](../data-export/data-export-cli-commands.md#initial-sync)中的&#x200B;_初始同步_。

要确保正确运行目录导出，请执行以下操作：

- [确认cron作业正在运行](https://experienceleague.adobe.com/zh-hans/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)。
- 验证索引器是从[Admin](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/tools/index-management)运行，还是使用Commerce CLI命令`bin/magento indexer:info`运行。
- 验证`Catalog Attributes Feed, Product Feed, Product Overrides Feed`和`Product Variant Feed`索引器是否设置为`Update by Schedule`。

### 监测数据同步并排除其故障

通过Commerce Admin，您可以使用[数据管理功能板](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-dashboard)监视同步过程。 使用[Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting)和日志管理该进程并对其进行故障排除。
