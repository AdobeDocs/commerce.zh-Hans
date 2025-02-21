---
title: 安装
description: 使用适用于PHP的编辑器为Adobe Commerce店面安装 [!DNL Store Fulfillment solution] 。
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# 安装

在非生产环境中完成[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]扩展的初始安装，队列管理器正在运行，缓存配置为允许异常处理。 确保您的开发环境包含开发工具，以确保操作和维护您的Adobe Commerce实例的最佳实践。

>[!TIP]
>
>按照&#x200B;_Adobe Commerce Upgrade Guide_&#x200B;中的[升级说明](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/modules/upgrade.html)升级Adobe Commerce内部部署的Store Fulfillment扩展。 有关云基础架构上的Adobe Commerce，请参阅《云基础架构上的Commerce指南》*中的[升级扩展](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/extensions.html#upgrade-an-extension)*。

## 先决条件

查看Store Fulfillment解决方案的[要求](solution-requirements.md)，并收集所需信息，然后再安装或升级Adobe Commerce的[!DNL Store Fulfillment]扩展。

如果您已安装预发行版或测试版的Store Fulfillment for Adobe Commerce扩展，请使用以下命令将其删除，然后再安装当前版本。

```bash
rm -rf composer.lock vendor/walmart &&
composer require walmart/magento-bopis-metapackage:1.0.0
```

## 安装要求

- **访问Walmart Commerce Technologies软件存档（.zip文件）的“商店履行”** — 在新用户引导和启用过程中，请与您的客户经理合作，以访问“商店履行”扩展的安装文件。

- **Adobe Commerce帐户信息** — 安装[!DNL Store Fulfillment]解决方案需要[[!DNL Commerce] 帐户](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-create){target="_blank"}。 您需要具有对[!DNL Adobe Commerce]项目的所有者或管理员访问权限的帐户ID和凭据。

- 对于云基础架构项目上的[!DNL Adobe Commerce]，软件安装程序必须具有对云项目的管理员访问权限。 请参阅[管理用户访问权限](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access)。

- **使用编辑器和[!DNL Commerce CLI]**&#x200B;的体验 — 有关使用这些工具在[!DNL Adobe Commerce]平台上安装和管理扩展的信息，请参阅[常规CLI安装](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions){target="_blank"}。

- **在Adobe Commerce上安装第三方扩展的体验** — 有关参考，请参阅Adobe Commerce文档。

   - [在云基础架构实例上安装Adobe Commerce的扩展](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#install-an-extension)。

   - [为Adobe Commerce本地实例安装扩展](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)。

### 步骤1：下载扩展包

按照您的客户代表提供的说明，下载包含用于安装Store Fulfillment Services扩展的Composer包的存档文件。

### 第2步：将扩展工件提取到应用程序

提取包含集成捆绑包的存档文件以安装Store Fulfillment Services扩展。

1. 为提取的文件创建目标目录。

   - 从命令行转到Web服务器doc根目录。

   - 创建`artifacts`目录。

1. 将存档文件提取到新目录。

1. 通过查看文件列表验证是否成功提取了文件。

   ```
   ../var/www/html/artifacts]$ ls -a
   .
   ..
   bopis-sdk.zip
   module-magento-bopis-alternate-pickup-contact-admin-ui.zip
   module-magento-bopis-alternate-pickup-contact-api.zip
   ```

### 步骤3：使用编辑器配置应用程序

使用Composer为安装配置源目录并安装Store Fulfillment Services扩展。

1. 为Composer安装配置源存储库。

   ```bash
   composer config repositories.artifacts artifact artifacts/
   ```

1. 将Store Fulfillment Services扩展添加到`composer.json`。

   ```bash
   composer require walmart/magento-bopis-metapackage:1.0.0
   ```

>[!NOTE]
>
>为提高Adobe Commerce本地实例的性能，您可以[更新自动加载配置](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/deployment-flow.html#update-the-autoloader)： `composer dump-autoload --optimize`

### 步骤4：升级数据库架构和数据

使用`bin/magento setup:upgrade`更新数据库架构和数据，并使用更改支持商店履行解决方案，从而完成安装。

>[!NOTE]
>
>对于云基础架构项目上的Adobe Commerce，您无需注册扩展。 相反，请提交上一步中的代码更改，并将它们推送到您的环境分支。 更新数据库架构和数据的命令在云构建和部署过程中自动运行。

### 步骤5：完成安装

1. 使用`setup:upgrade` Magento CLI命令在Adobe Commerce中注册该扩展。

   ```bash
   bin/magento setup:upgrade
   ```

1. 如果出现提示，请重新编译您的[!DNL Commerce]项目。

   ```bash
   bin/magento setup:di:compile
   ```

1. 清理缓存。

   ```bash
   bin/magento cache:clean
   ```

1. 禁用维护模式。

   ```bash
   bin/magento maintenance:disable
   ```

### 步骤6：验证安装

在Adobe Commerce服务器上，验证是否已安装和启用Store Fulfillment Services扩展的模块。

1. 登录到服务器。

   对于云基础架构上的Adobe Commerce安装，[使用SSH登录到远程环境](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh)。

1. 验证是否已启用“商店履行服务”模块。

   ```bash
   bin/magento module:status  --enabled | grep Walmart
   ```

   输出应包括以下模块：

   ```
   Walmart_BopisBase
   Walmart_BopisAlternatePickupContact
   Walmart_BopisAlternatePickupContactFrontend
   Walmart_BopisApiConnector
   Walmart_BopisAlternatePickupContactAdminUi
   Walmart_BopisCheckoutPickInStoreApi
   Walmart_BopisInventorySourceAdminUi
   Walmart_BopisCheckoutPickInStore
   Walmart_BopisInventoryCatalogApi
   Walmart_BopisPreferredLocationApi
   Walmart_BopisHomeDeliveryApi
   Walmart_BopisHomeDelivery
   Walmart_BopisPreferredLocation
   Walmart_BopisInventoryCatalog
   Walmart_BopisPreferredLocationFrontend
   Walmart_BopisCheckoutPickInStoreAdminUi
   Walmart_BopisInventorySourceApi
   Walmart_BopisInventorySourceFaasSync
   Walmart_BopisInventorySourceReservation
   Walmart_BopisLocationCheckInApi
   Walmart_BopisLogging
   Walmart_BopisStoreAssociateApi
   Walmart_BopisLocationCheckInFrontend
   Walmart_BopisStoreAssociate
   Walmart_BopisOperationQueue
   Walmart_BopisOperationQueueAdminUi
   Walmart_BopisOperationQueueApi
   Walmart_BopisOrderFaasSync
   Walmart_BopisOrderUpdateApi
   Walmart_BopisLocationCheckIn
   Walmart_BopisInventoryCatalogAdminUi
   Walmart_BopisPreferredLocationAdminUi
   Walmart_BopisDeliverySelection
   Walmart_BopisCheckoutPickInStoreFrontend
   Walmart_BopisLocationCheckInAdminUi
   Walmart_BopisStoreAssociateAdminUi
   Walmart_BopisOrderUpdate
   Walmart_BopisStoreAssociateTfa
   Walmart_BopisStoreAssociateTfaApi
   ```

### 其他步骤

如果需要，请使用[setup:static-content:deploy](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/cli-reference/commerce-on-premises){target="_blank"} CLI命令将静态视图文件部署到生产环境。

```bash
php bin/magento setup:static-content:deploy -f
```

如果使用空白主题，则必须使用`-f`选项。

>[!NOTE]
>
>有关详细信息，请参阅Adobe Commerce帮助中心的[Adobe Commerce中的静态内容部署最佳实践](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/development/static-content-deployment.html)。


