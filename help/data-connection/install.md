---
title: 安装 [!DNL Data Connection]
description: 了解如何从Adobe Commerce安装、更新和卸载 [!DNL Data Connection] 扩展。
role: Admin, Developer
feature: Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 安装[!DNL Data Connection]

在安装扩展之前，[查看先决条件](overview.md#prereqs)。

## 安装扩展

[!DNL Data Connection]扩展可从[Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html)获得。 从服务器的命令行安装此扩展时，它将作为[服务](../landing/saas.md)连接到Adobe Commerce安装。 该过程完成后，**[!DNL Data Connection]**&#x200B;和&#x200B;**Commerce Services Connector**&#x200B;将出现在Commerce _管理员_&#x200B;的&#x200B;**服务**&#x200B;下的&#x200B;**系统**&#x200B;菜单中。

![[!DNL Data Connection]扩展管理员视图](assets/epc-adminui.png)

>[!IMPORTANT]
>
>虽然扩展名已从Experience Platform连接器更改为[!DNL Data Connection]，但包名仍为`experience-platform-connector`以支持向后兼容性。

1. 要下载`experience-platform-connector`包，请从命令行运行以下命令：

   ```bash
   composer require magento/experience-platform-connector
   ```

   此元包包含以下模块和扩展：

   - `magento/orders-connector`
   - `magento/data-services`
   - `magento/customers-connector`
   - `magento/module-experience-connector`
   - `magento/module-experience-connector-admin`
   - `magento/module-experience-connector-admin-graph-ql`
   - `magento/module-experience-connector-aep-integration`

1. （可选）要包含[!DNL Live Search]数据（包含[搜索事件](events.md#search-events)），请安装[[!DNL Live Search]](../live-search/install.md)扩展。

1. （可选）要包含B2B数据（包含[申请事件](events.md#b2b-events)），请安装[B2B扩展](#install-the-b2b-extension)。

1. （可选）如果您是医疗保健商人，请安装[数据服务HIPAA](#install-the-data-services-hipaa-extension)扩展，以便您的[!DNL Commerce]后台数据可以支持HIPAA。

### 安装Adobe I/O Events并配置客户连接器模块

安装`experience-platform-connector`扩展后，必须安装适用于Adobe Commerce的Adobe I/O Events并配置`customers-connector`模块。

以下步骤适用于云基础架构和内部部署安装的Adobe Commerce。

1. 如果您正在运行Commerce 2.4.4或2.4.5，请使用以下命令加载事件模块：

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   Commerce 2.4.6及更高版本会自动加载这些模块。

1. 更新项目依赖关系。

   ```bash
   composer update
   ```

1. 启用新模块：

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

根据部署类型最终完成安装：云基础架构或内部部署上的Adobe Commerce 。

#### 在云基础架构上

在云基础架构上的Adobe Commerce中，在`.magento.env.yaml`中启用`ENABLE_EVENTING`全局变量。 [了解更多](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html?lang=zh-Hans#enable_eventing)。

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

提交更新的文件并将其推送到云环境。 部署完成后，使用以下命令启用发送事件：

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### 内部部署

在内部部署环境中，您必须手动启用代码生成和Adobe Commerce事件：

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### 安装B2B扩展

对于B2B商家，请安装以下扩展以包含[申请列表](events.md#b2b-events)事件数据。

通过从命令行运行以下命令来下载`magento/experience-platform-connector-b2b`扩展：

```bash
composer require magento/experience-platform-connector-b2b
```

### 安装数据服务HIPAA扩展

对于医疗保健商家，请安装以下扩展以确保后台事件数据符合HIPAA要求。

通过从命令行运行以下命令来下载`magento/module-data-services-hipaa`扩展：

```bash
composer require magento/module-data-services-hipaa
```

## 更新[!DNL Data Connection]扩展 {#update}

要更新[!DNL Data Connection]扩展，请从命令行运行以下命令：

```bash
composer update magento/experience-platform-connector --with-dependencies
```

或者，对于B2B商家：

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

要更新到主要版本，例如从2.0.0到3.0.0，请按如下方式编辑项目的根[!DNL Composer] `.json`文件：

1. 打开根`composer.json`文件并搜索`magento/experience-platform-connector`。

1. 在`require`部分中，更新版本号，如下所示：

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **保存** `composer.json`。 然后，从命令行运行以下命令：

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   或者，对于B2B商家：

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## 卸载[!DNL Data Connection]扩展 {#uninstall}

要卸载[!DNL Data Connection]扩展，请参阅[卸载模块](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html?lang=zh-Hans)。
