---
title: 检查扩展更新
description: 了解Adobe Commerce如何检查新的AEM Assets集成扩展版本（包括手动CLI检查）并将其通知管理员。
feature: CMS, Media
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7950f5d171b35054be42ca60d19bafcf43c53cd6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%
---
# 检查扩展更新

使用AEM Assets集成扩展版本1.4.6及更高版本时，Adobe Commerce会自动检查扩展的较新版本是否可用，并在管理员中通知管理员。 此检查作为计划处理的一部分异步运行，不会阻止管理员页面渲染。

## 更新检查的工作方式

* 更新检查将您安装的`aem-assets-integration`包版本与[repo.magento.com](https://repo.magento.com/admin/dashboard)提供的最高兼容版本进行比较。
* 结果已缓存。 加载管理页面时，会读取最近缓存的结果，而不是触发实时网络请求。
* 如果`repo.magento.com`不可用，或返回的元数据无效，Commerce将保留上次成功缓存的结果，并且不会阻止管理员。

>[!NOTE]
>
>更新检查针对的是Adobe Commerce on Cloud和内部部署。

## 查看更新通知

管理员可以在以下任一位置看到可用的更新通知：

* **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**
* 管理员通知下拉列表

将显示每个通知：

* 安装的版本
* 可用版本
* 版本分类
* 指向发行说明的链接

选择&#x200B;**[!UICONTROL Remind me later]**&#x200B;以暂停此Commerce实例的通知，或完全选择退出更新通知。

## 运行手动更新检查

要立即检查是否有可用的更新，请从Commerce根目录运行以下命令：

```bash
bin/magento aem:assets:check-update
```

此命令仅检查和报告可用更新。 它不会修改编辑器文件或部署更新。 要安装更新，请按照[安装Adobe Commerce包](configure-commerce.md)中的编辑器说明操作。

## 发布扩展包的元数据

更新检查从已安装包`composer.json`文件的`extra`部分读取发行元数据：

```json
{
  "extra": {
    "release_notes_url": "https://experienceleague.adobe.com/zh-hans...",
    "release_type": "feature",
    "compatible_commerce_versions": ">=2.4.7 <2.5.0"
  }
}
```

## 下一步

* [安装Adobe Commerce包](configure-commerce.md)
