---
title: 目录适配器扩展
description: 使用目录适配器呈现来自Commerce服务的价格
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# 目录适配器

`[!DNL Catalog Adapter]`扩展禁用Commerce应用程序中包含的默认产品价格索引器，并改用[目录服务](../catalog-service/overview.md)提供的价格。

该适配器设计用于[SaaS数据导出](../data-export/overview.md)和Adobe Commerce服务。 SaaS数据导出负责提交价格，[!DNL Catalog Adapter]将从Adobe Commerce服务中检索所有价格。

启用[!DNL Catalog Adapter]后，价格索引和操作将在以下方面受到影响：

- Adobe Commerce应用程序中包含的价格索引器已禁用。
- 使用SaaS数据导出和[SaaS价格索引器](price-indexing.md)来管理价格。
- 当客户打开产品、类别或其他页面显示产品价格时，将从Adobe Commerce服务中检索价格。
- 通过同步[SaaS数据导出](../data-export/overview.md)中的数据，将价格发送到Adobe Commerce服务。
- 结账会动态重新计算价格。

您可以通过删除或禁用Catalog Adapter扩展在Commerce应用程序中重新启用价格索引。

## 要求

- Adobe Commerce 2.4.4+
- 安装了以下Commerce服务之一：

   - [实时搜索](../live-search/install.md)
   - [产品推荐](../product-recommendations/install-configure.md)
   - [目录服务](../catalog-service/installation.md)

## 安装

Catalog Adapter扩展是一个Composer中继，用于安装以下模块：

- **价格索引器禁用** — 此模块禁用Commerce应用程序中的价格索引，以便通过SaaS价格索引来提供价格。 安装SaaS价格索引扩展后，Commerce应用程序中的产品价格索引器无法打开。
- **价格提供程序** — 此模块提供Adobe Commerce服务产品的价格。 它形成搜索查询并获取前端产品的价格。
- **目录服务搜索适配器** — 此模块将价格从Adobe Commerce应用程序传输到Adobe Commerce服务，以响应产品搜索请求。

## 安装步骤

>[!BEGINTABS]

>[!TAB 云基础架构]

使用此方法为Commerce Cloud实例安装[!DNL Catalog Adapter]。

1. 在本地工作站上，转到云基础架构项目上Adobe Commerce的项目目录。

   >[!NOTE]
   >
   >有关在本地管理Commerce项目环境的信息，请参阅《云基础架构用户指南》_上的_ Adobe Commerce中的[使用CLI管理分支](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches)。

1. 查看要使用Adobe Commerce Cloud CLI更新的环境分支。

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. 添加目录适配器模块。

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. 更新包依赖关系。

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. 提交和推送`composer.json`和`composer.lock`文件的代码更改。

1. 添加、提交并将`composer.json`和`composer.lock`文件的代码更改推送到云环境。

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   将更新推送到云环境会启动[Commerce云部署流程](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process)以应用更改。 从[部署日志](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log)中检查部署状态。

>[!TAB 内部部署]

使用此方法为内部部署实例安装[!DNL Catalog Adapter]。

1. 使用编辑器将目录适配器添加到您的项目中：

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. 更新依赖项并安装扩展：

   ```bash
   composer update  "magento/catalog-adapter"
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


## 重新启用Adobe Commerce产品价格索引器

如果您的第三方应用程序依赖于默认的Adobe Commerce产品价格索引器，则可以使用以下命令重新启用它：

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## 禁用Headless店面的产品价格索引器方案

如果您有Headless Commerce实例，则可能需要禁用Adobe Commerce产品价格索引器以减少Adobe Commerce实例的负载。 您可以通过安装`magento/module-price-indexer-disabler`模块来完成此任务：

```bash
composer require magento/module-price-indexer-disabler
```

## 使用方案

以下是一些常见的`[!DNL Catalog Adapter]`方案。

### 不依赖于Adobe Commerce产品价格索引器

- 您是已安装所需服务（实时搜索、产品推荐、目录服务）的Luma或Adobe Commerce Core GraphQL商家
- 没有与依赖于Adobe Commerce产品价格索引器的第三方扩展集成

1. 安装[!DNL Catalog Adapter]。

### 依赖于Adobe Commerce产品价格索引器

- 您是已安装支持服务（Live Search、产品推荐、目录服务）的Luma或Adobe Commerce Core GraphQL商家
- 您使用依赖于Adobe Commerce产品价格索引器的第三方扩展

1. 安装[!DNL Catalog Adapter]。
1. 重新启用默认的Adobe Commerce产品价格索引器。

### Headless Commerce实例

- 具有安装了所需服务（实时搜索、产品推荐、目录服务）的Headless Commerce实例的商家
- 不依赖默认的Adobe Commerce产品价格索引器

1. 从[!DNL Catalog Adapter]包安装`magento/module-price-indexer-disabler`模块。

