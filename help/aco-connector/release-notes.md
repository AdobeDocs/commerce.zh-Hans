---
title: '[!DNL Adobe Commerce Optimizer Connector]发行说明'
description: 了解 [!DNL Adobe Commerce Optimizer Connector] 发行说明，包括目录同步和导出的新功能、错误修复和已知问题。
autotag-review: '2026-06-17T15:08:59.000Z'
feature: Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: f08fa0de-a550-4acd-b570-f81cf1d03aafid: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2: id: dad884f1-e840-49a1-970e-2f965bdbc410id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 1d14f7827de3274564941765fd2943ecefac5fad
workflow-type: tm+mt
source-wordcount: 460
ht-degree: 0%

---

# Adobe Commerce Optimizer Connector发行说明

这些发行说明介绍了[!DNL Adobe Commerce Optimizer Connector]的所有版本，包括：

![新](../assets/new.svg)新功能
![已修复问题](../assets/fix.svg)修复和改进
![已知问题](../assets/bug.svg)已知问题

## 2026版

### 1.0.16发行版

_2026年8月7日_

![修复](../assets/fix.svg) **目录同步在无效配置上不再停止** — 修复了如果[!DNL Adobe Commerce Optimizer Connector]配置缺失或无效，目录同步可能会无限期运行的问题。 同步现在完成并记录警告，而不是继续运行。 <!--MDEE-1413-->
![修复](../assets/fix.svg) **更可靠的[!DNL Adobe Commerce Optimizer]管理员请求** — 修复了[!DNL Adobe Commerce Optimizer Connector]可能为[!DNL Adobe Commerce Optimizer]管理员请求使用不正确URL的问题，此问题可能导致这些请求失败。 <!--COMOPT-2288-->
![修复](../assets/fix.svg) **更可靠的刷新和修补操作** — 修复了刷新和修补操作可能针对错误环境的问题，该问题可能导致请求失败。<!--COMOPT-2288-->

### 1.0.15发行版

_2026年7月10日_

![Fix](../assets/fix.svg)为类别信息源添加了排序支持。<!--MDEE-1409-->

### 1.0.14版本

_2026年6月11日_

![修复](../assets/fix.svg) **PHP 8.5兼容性** - [!DNL Adobe Commerce Optimizer Connector]现在支持PHP 8.5，因此您可以升级您的[!DNL Adobe Commerce]环境，而不会中断连接器功能或目录同步。<!--MDEE-1388-->

![修复](../assets/fix.svg) **货币更改后价格手册更新** — 货币更改后，更新的价格会自动反映在Adobe Commerce Optimizer中。<!--MDEE-1384-->

![修复](../assets/fix.svg) **导航尊重已禁用或隐藏的父类别** — 来自已禁用或隐藏类别层次结构的产品不再意外出现在导航体验中。<!--MDEE-1385-->

![修复](../assets/fix.svg) **暂存更新后一致的类别URL** — 应用暂存更新后，类别链接和导航保持准确。<!--MDEE-1395-->

### 1.0.13发行版

_2026年5月6日_

![修复](../assets/fix.svg) **改进了[!DNL Adobe Commerce Optimizer Connector]配置说明** — 更新了Commerce管理员中的[!DNL Adobe Commerce Optimizer]配置页面，以链接到&#x200B;_[!DNL Adobe Commerce Optimizer Connector]集成指南_。
<!--COMOPT-1922-->

![修复](../assets/fix.svg) **[!DNL Adobe Commerce Optimizer Connector]元数据增强** - [!DNL Adobe Commerce Optimizer Connector]现在在元数据标头中包含其已安装的版本。 此改进使团队能够快速识别在疑难解答或支持服务期间使用的连接器版本。<!--MDEE-1323-->

### 1.0.12发行版

_2026年4月2日_

![新](../assets/new.svg) **在`saas:resync`命令中添加了对类别馈送的支持** — 您现在可以使用`saas:resync` CLI命令轻松刷新和查看最新的类别数据：

```shell
bin/magento saas:resync --feed=categories
```

### 1.0.11发行版

_2026年3月10日_

![修复了问题](../assets/fix.svg)修复了当在[!DNL Adobe Commerce]实例上安装[!DNL Adobe Commerce Optimizer Connector]时，会阻止从Commerce管理员&#x200B;**[!UICONTROL System]**&#x200B;和&#x200B;**[!UICONTROL Configuration]**&#x200B;菜单访问[!DNL Commerce Services Connector]配置页面的兼容性问题。  现在，安装两个扩展后，您可以访问[!DNL Commerce Services Connector]配置页面。<!--MDEE-1322-->


### 1.0.10发行版

_2026年3月9日_

![修复](../assets/fix.svg)如果您在完成连接器配置之前访问&#x200B;**[!UICONTROL Data Feed Sync Status]**&#x200B;页面，现在会自动重定向到连接器配置页面。 此引导式流程可确保连接器设置完成，并有助于防止因缺少配置设置而导致状态项失败或不完整的错误。<!--MDEE-1296-->

### v1.0.9发布

_2026年3月01日_

[!DNL Adobe Commerce Optimizer Connector]的正式发布版本。

>[!NOTE]
>
>如果您参与了[!DNL Adobe Commerce Optimizer Connector]的Beta计划并且安装了早期版本的扩展，请升级到正式发布版本以接收最新更新。
