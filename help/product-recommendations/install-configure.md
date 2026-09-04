---
title: 安装和配置
description: 了解如何安装、更新和卸载 [!DNL Product Recommendations]。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
TQID: https://experienceleague.adobe.com/z-ue-sojw9Iewuz-ZToCzkumP3qN-TCWWF3UWdpdIL0
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
last-update: 2026-09-03
source-git-commit: c9f36200e5c4a6f7770ce5897f4b800bf9e60fe1
workflow-type: tm+mt
source-wordcount: 600
ht-degree: 0%

---

# 安装和配置

将[!DNL Product Recommendations]部署到店面和管理员需要安装模块并配置[Commerce服务连接器](../landing/saas.md)。 发布更新后，您可以轻松地将安装更新为最新版本。

- [安装](#install)
- [配置](#configure)
- [更新](#update)
- [卸载](#uninstall)

## 安装[!DNL Product Recommendations] {#install}

由于[!DNL Product Recommendations]模块是独立的中继包，因此比Adobe Commerce更频繁地发布更新。 为确保您及时了解最新的错误修复和功能，请参阅[发行说明](release-notes.md)。

>[!IMPORTANT]
>
>确保您拥有正确的[权利](../landing/saas.md#credentials)以使用产品推荐。

使用编辑器安装`magento/product-recommendations`模块：

```bash
composer require magento/product-recommendations
```

### 添加页面生成器支持 {#pbsupport}

页面生成器的[!DNL Product Recommendations]是一个可选模块，需要单独安装。 要将[!DNL Product Recommendations]与页面生成器一起使用，请通过运行以下命令来安装模块：

```bash
composer require magento/module-page-builder-product-recommendations
```

通过在页面生成器中启用[!DNL Product Recommendations]，您可以将现有的活动[推荐单元](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations)添加到在页面生成器中创建的任何内容，例如页面、块和动态块。

有关详细说明，请参阅[将 [!DNL Product Recommendations] 与页面生成器内容一起使用](page-builder.md)。

### 添加视觉相似性推荐类型 {#vissimsupport}

_视觉相似度_&#x200B;推荐类型显示的产品与在产品详细信息页面上查看的产品视觉上相似[](type.md#visualsim)。 当产品图像和外观对于购物体验很重要时，它最有用。 要安装此软件，请运行以下命令：

```bash
composer require magento/module-visual-product-recommendations
```

### 添加Fastly图像优化支持 {#fastlysupport}

对[!DNL Product Recommendations]的Fastly图像优化支持是一个可选模块，是单独安装的。 此模块将[Fastly图像优化](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/cdn/fastly)参数应用于[!DNL Product Recommendations]图像URL。 要安装此软件，请运行以下命令：

```bash
composer require magento/module-fastly-recommendations
```

## 配置[!DNL Product Recommendations] {#configure}

1. 安装`magento/product-recommendations`模块后，通过指定API密钥并选择SaaS数据空间来配置[Commerce Services Connector](../landing/saas.md)。

   通过配置此连接，可以实现Commerce实例、目录服务和其他支持服务之间的数据同步和通信。 [SaaS数据导出扩展](../data-export/overview.md)处理数据同步。

1. 为确保目录导出可以正确运行，请确认[cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)作业和[索引器](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers)正在运行，并且`Product Feed`索引器设置为`Update by Schedule`。

成功将Commerce应用程序链接到Commerce Services并指定[SaaS数据空间](../landing/saas.md#saas-configuration)后，将开始目录同步。 然后，您可以[验证](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify)行为数据是否已发送到店面。

## 监测数据同步并排除其故障

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

{{install-data-sync-feed-status}}

## 更新[!DNL Product Recommendations]安装 {#update}

与所有Adobe Commerce一样，[!DNL Product Recommendations]使用Composer进行安装和更新。 要更新`magento/product-recommendations`模块，请运行以下命令：

```bash
composer update magento/product-recommendations --with-dependencies
```

要更新到主要版本，例如从5.0到6.0，您必须编辑项目的根`composer.json`文件。 （有关最新版本的信息，请参阅[发行说明](release-notes.md)。） 例如，让我们打开主`composer.json`文件并搜索`magento/product-recommendations`模块：

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

将主版本从`5.0`更新为`6.0`：

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

保存`composer.json`文件并运行：

```bash
composer update magento/product-recommendations --with-dependencies
```

或者，如果您已安装`magento/module-visual-product-recommendations`和`magento/module-page-builder-product-recommendations`模块：

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> 在3.x.x版的产品推荐中，您只需要一个API密钥。 在版本4.x.x及更高版本中，您必须为沙盒和生产环境提供公共API密钥和私有API密钥。 如果您未提供这两对API密钥，则无法在管理员中访问产品推荐功能。 但是，数据收集会在您的店面中继续，并且现有推荐将继续向您的购物者显示。

## 防火墙

要允许产品推荐通过防火墙，请将`commerce.adobe.io`添加到允许列表。

## 卸载[!DNL Product Recommendations] {#uninstall}

如有必要，您可以[卸载](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules)产品推荐模块。
