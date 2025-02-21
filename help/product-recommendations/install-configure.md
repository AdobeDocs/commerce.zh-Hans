---
title: 安装和配置
description: 了解如何安装、更新和卸载 [!DNL Product Recommendations]。
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '565'
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

通过&#x200B;_视觉相似度_&#x200B;推荐类型，您可以将推荐单元部署到产品详细信息页面，该页面显示与正在查看的产品[视觉上相似](type.md#visualsim)的产品。 当产品的图像和视觉方面是购物体验的重要部分时，此推荐类型最有用。 通过运行以下命令安装&#x200B;_视觉相似度_&#x200B;推荐类型：

```bash
composer require magento/module-visual-product-recommendations
```

## 配置[!DNL Product Recommendations] {#configure}

1. 安装`magento/product-recommendations`模块后，通过指定API密钥并选择SaaS数据空间来配置[Commerce Services Connector](../landing/saas.md)。

   通过配置此连接，可以实现Commerce实例、目录服务和其他支持服务之间的数据同步和通信。 数据同步由[SaaS Data Export扩展](../data-export/overview.md)处理。

1. 为确保目录导出可以正确运行，请确认[cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)作业和[索引器](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers)正在运行，并且`Product Feed`索引器设置为`Update by Schedule`。

成功将Commerce应用程序链接到Commerce Services并指定[SaaS数据空间](../landing/saas.md#saas-configuration)后，将开始目录同步。 然后，您可以[验证](verify.md)行为数据是否已发送到店面。

## 监测数据同步并排除其故障

通过Commerce Admin，您可以使用[数据管理功能板](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard)监视同步过程。 使用[Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting)和日志管理该进程并对其进行故障排除。

然后，您可以[验证](verify.md)行为数据是否已发送到店面。

## 更新[!DNL Product Recommendations]安装 {#update}

与所有Adobe Commerce一样，[!DNL Product Recommendations]使用Composer进行安装和更新。 要更新`magento/product-recommendations`模块，请运行以下命令：

```bash
composer update magento/product-recommendations --with-dependencies
```

要更新到主要版本，例如从3.0到4.0，您必须编辑项目的根`composer.json`文件。 （有关最新版本的信息，请参阅[发行说明](release-notes.md)。） 例如，让我们打开主`composer.json`文件并搜索`magento/product-recommendations`模块：

```json
"require": {
    ...
    "magento/product-recommendations": "^3.0",
    ...
}
```

让我们将主要版本从`3.0`增大到`4.0`：

```json
"require": {
    ...
    "magento/product-recommendations": "^4.0",
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
