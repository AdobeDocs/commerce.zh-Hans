---
title: '[!DNL Catalog Adapter]发行说明'
description: Adobe Commerce的 [!DNL Catalog Adapter] 的最新发行信息。
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
source-git-commit: 47419e7e19611dc4a045c195f259e2126ab77372
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# [!DNL Catalog Adapter]扩展发行说明

以下发行说明介绍了[!DNL Catalog Adapter]扩展的最新版本。 为当前的主要发行版本提供支持。 提供了旧版本的发行说明以供参考。

更新包括：

![新](../assets/new.svg)新功能
![修复](../assets/fix.svg)修复和改进
![错误](../assets/bug.svg)已知问题


>[!NOTE]
>
>[Catalog Adapter扩展](catalog-adapter.md)禁用Adobe Commerce价格索引。 如果已安装，则可以使用编辑器检查系统上安装的版本。 在某些情况下，您可能需要升级系统上的目录适配器扩展以获得修复或新功能，而不更新Commerce服务版本。

## 当前主要版本

## 1.0.10发行版

![修复](../assets/fix.svg)修复了导入或新建捆绑产品的价格查询可能会导致内部服务器错误的问题，因为系统尝试使用连接的SKU而不是正确的有效SKU进行查找。 捆绑产品的价格查询现在使用适当的SKU并正确解析。<!--MDEE-1040-->

## 1.0.9版本

![修复](../assets/fix.svg)添加了与PHP 8.4的兼容性。<!--MDEE-941-->

## 1.0.8版本

![修复](../assets/fix.svg)修复了在将具有数字SKU的可配置产品变体添加到愿望清单时，导致异常日志中出现错误的问题。<!--MDEE-876-->
