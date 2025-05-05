---
title: 安装 [!DNL Payment Services]
description: 安装Payments Services扩展。
role: Admin
feature: Payments, Checkout, Install, Upgrade
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# 安装[!DNL Payment Services]

要开始使用[!DNL Adobe Commerce]和[!DNL Magento Open Source]的支付服务，您必须完成一些入门步骤。

>[!INFO]
>
> 有关更多信息，请参阅我们的[为Adobe Commerce](https://experienceleague.adobe.com/zh-hans/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services)配置 [!DNL Payment Services] 视频。

下载并安装[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]扩展是使用[!DNL Payment Services]的必备步骤。

## 下载扩展

必须先从[Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html?lang=zh-Hans)下载该扩展，然后才能安装它。

1. 导航到Commerce Marketplace[&#128279;](https://commercemarketplace.adobe.com/magento-payment-services.html)中的Payment Services扩展。
1. 要选择版本和版本，请将&#x200B;**[!UICONTROL Edition]**&#x200B;和&#x200B;**[!UICONTROL Your store version]**&#x200B;切换到您的首选选项。
1. 单击&#x200B;**[!UICONTROL Add to Cart]**。
1. 完成签出，然后单击&#x200B;**[!UICONTROL Place Order]**。
1. 检查与您的Marketplace下载关联的电子邮件，以查看订单确认和详细信息。

>[!NOTE]
>
> 对于Adobe Commerce版本2.4.7或更高版本，[!DNL Payment Services]现成可用。

## 安装扩展

您可以在云基础架构和本地实例上为[!DNL Adobe Commerce]安装[!DNL Payment Services]扩展，这些实例已链接到注册过程中提供的Commerce帐户[mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys)。
[!DNL Magento Open Source]客户使用本地说明。

Composer在初始安装[!DNL Adobe Commerce]期间使用这些密钥，或者在以前未将Composer密钥保存到`auth.json`文件的情况下使用这些密钥。

有关获取编辑器密钥的详细信息，请参阅[获取您的身份验证密钥](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)。

请参阅[安装扩展](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/tutorials/extensions)，以了解有关下载和安装扩展之前应考虑哪些内容的更多信息。

### 云基础架构上的[!DNL Adobe Commerce]

此方法用于为Commerce Cloud实例安装[!DNL Payment Services]扩展。

1. 更新您的`composer.json`文件：

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 更新依赖项并安装扩展：

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   使用`composer update`命令更新所有根依赖项。

1. 提交并推送更改。

### 内部部署和其他配置

此方法用于为内部部署实例和[!DNL Magento Open Source]客户安装[!DNL Payment Services]扩展。

1. 要获取该扩展，请运行以下命令：

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 更新依赖项并安装扩展：

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   使用`composer update`命令更新所有根依赖项。

1. 升级实例：

   ```bash
   bin/magento setup:upgrade
   ```

1. 清除缓存：

   ```bash
   bin/magento cache:clean
   ```

1. 提交更改。
1. 要确保已提交的代码已部署，请更新您的实例。

>[!NOTE]
>
> [!DNL Payment Services] 1.6.1与PHP版本7.x兼容。但是，强烈建议更新到最新的[!DNL Payment Services]版本。

## 升级扩展

发布[!DNL Payment Services]的新版本后，您可以轻松升级扩展。

1. 要获取包的最新版本，请执行以下操作：

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   使用`composer update`命令更新所有根依赖项。

1. 更新编辑器后，运行：

   ```bash
   bin/magento setup:upgrade
   ```

1. 提交并推送更改。

## 故障排除

在尝试安装[!DNL Payment Services]扩展时，您可能会看到错误。 使用以下故障排除方法解决错误。

### 存储库列表

验证存储库列表中是否存在`repo.magento.com`。

### 不正确的编辑器键

如果您看到以下错误，表明您的编辑器键不正确：

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

验证您的编辑器密钥是否有效，以及您是否有权访问其他Magento包。

要查看已配置的编辑器键：

1. 查找`auth.json`文件的位置：

   ```bash
   composer config --global home
   ```

1. 查看`auth.json`文件：

   ```bash
   cat /path/to/auth.json
   ```

1. 查看[哪些密钥与您的Commerce帐户`MageID`](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)关联。

### 内存不足，无法用于PHP

如果看到以下错误，表示您没有足够的内存来安装PHP：

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

在`php.ini`中增加环境上PHP的内存限制[&#128279;](https://experienceleague.adobe.com/zh-hans/docs/commerce-cloud-service/user-guide/configure/app/php-settings#increase-php-memory-limit)。

或者，也可以使用此命令指定内存限制： `php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`。

例如：

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
