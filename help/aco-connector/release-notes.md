---
title: '[!DNL Adobe Commerce Optimizer Connector]发行说明'
description: Adobe Commerce的 [!DNL Adobe Commerce Optimizer Connector] 的最新发行信息。
feature: Services, Catalog Service, Release Notes
source-git-commit: 205fca38b379f94027a965b58826ffd922577f61
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Adobe Commerce Optimizer Connector发行说明

这些发行说明介绍了[!DNL Adobe Commerce Optimizer Connector]的所有版本，包括：

![新](../assets/new.svg)新功能
![已修复问题](../assets/fix.svg)修复和改进
![已知问题](../assets/bug.svg)已知问题

## 2026版

### 1.0.12发行版

_2026年4月2日_

![新](../assets/new.svg) **在`saas:resync`命令中添加了对类别馈送的支持** — 您现在可以使用`saas:resync` CLI命令轻松刷新和查看最新的类别数据：

```terminal
bin/magento saas:resync --feed=categories
```

_2026年3月10日_

![修复了问题](../assets/fix.svg)修复了当在Commerce实例上安装Commerce连接器时，阻止从Commerce管理系统和配置菜单访问Adobe Commerce Optimizer服务连接器配置页面的兼容性问题。  现在，您可以在安装了两个扩展后访问“Commerce服务连接器配置”页面。<!--MDEE-1322-->


### v1.0.10发布

_2026年3月9日_

![修复](../assets/fix.svg)如果在完成连接器配置之前访问数据馈送同步状态页面，则现在会自动将您重定向到连接器配置页面。 此引导式流程可确保连接器设置完成，并有助于防止因缺少配置设置而导致状态项失败或不完整的错误。<!--MDEE-1296-->

### v1.0.9发布

_2026年3月01日_

Adobe Commerce Optimizer Connector的正式发布版。

>[!NOTE]
>
>如果您参加了针对Adobe Commerce Optimizer Connector的Beta计划并安装了早期版本的扩展，请升级到正式发布版本以接收最新更新。

