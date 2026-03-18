---
title: 为AEM Assets集成配置IMS用户权限
description: 了解IMS身份和Admin Console配置文件如何启用AEM Assets交付访问权限、资产选择器和自动填充的Commerce配置字段。
feature: CMS, Media, Configuration
source-git-commit: 0fd98bf86555c914f7a5b1e177c31c37764dbf84
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 用户权限和IMS

**IMS** (Adobe Identity Management System)是身份验证层。 对于Adobe Commerce as a Cloud Service，默认情况下在管理员中启用IMS身份验证。 对于云上或内部部署的Adobe Commerce，IMS是可选的；[为Commerce启用IMS](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank}提供了增强的配置UI（资产选择器，自动填充的下拉列表），但您可以通过手动输入&#x200B;**项目ID**&#x200B;和&#x200B;**环境ID**&#x200B;来配置不使用IMS的集成。

使用IMS时，AEM Assets集成还需要特定&#x200B;**Adobe Admin Console产品配置文件**。 在Commerce管理员中配置集成的用户需要&#x200B;**AEM Assets DM OpenAPI Users - delivery**&#x200B;产品配置文件，或作为回退的&#x200B;**author**&#x200B;产品配置文件。 这可通过用户IMS组织中的Admin Console产品配置文件进行控制，并启用：

* **Asset Selector**&#x200B;允许在管理类别图像或页面生成器内容时从AEM Assets中选择图像。
* **自动填充的配置字段**，如&#x200B;**项目ID**、**环境ID**&#x200B;和&#x200B;**域映射**&#x200B;下拉列表，这些字段根据用户的Admin Console产品配置文件（投放或作者）从用户的IMS会话中提取值。

如果没有正确的权限，资产选择器将不可用，并且这些字段显示空白或需要手动输入。
>[!BEGINSHADEBOX]

**IMS和权限如何协同工作**

Adobe IMS提供用户标识和组织上下文，而Adobe Admin Console定义它拥有哪些&#x200B;**产品配置文件**（权限）。 AEM Assets集成使用IMS详细信息和分配的配置文件来确定它能否自动填充配置字段并启用资产选择器。

>[!ENDSHADEBOX]

## 为什么需要产品配置文件

该集成只能加载映射到配置文件的域。 因此，用户可以拥有以下产品配置文件：

* **AEM投放产品配置文件**。 当用户同时具有创作和投放配置文件时，资产选择器和配置UI需要此项。 该集成在可用时使用AEM交付产品配置文件。

* **作者产品配置文件**。 需要才能访问AEM Assets UI。 当用户的Admin Console中没有AEM交付产品配置文件时，还可以用作资产选择器和配置UI的回退。

域（包括项目ID、环境ID和域映射）已分配给AEM交付产品配置文件。 该集成会从&#x200B;**AEM交付产品配置文件**&#x200B;中加载域（如果可用），或回退到&#x200B;**作者产品配置文件**（如果AEM交付产品配置文件不在用户的Admin Console中）。 用户需要以下配置文件之一：

* 在Commerce管理配置中填充&#x200B;**项目ID**、**环境ID**&#x200B;和&#x200B;**域映射**&#x200B;下拉列表。
* 使用资源选择器从AEM Assets中浏览并选择资源。

如果两个配置文件均未配置，则用户可以手动输入&#x200B;**项目ID**&#x200B;和&#x200B;**环境ID**，但资产选择器将不可用。

## 按部署类型授予权限

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

仅[!BADGE SaaS]{type=Positive tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"}

默认情况下启用IMS身份验证。 将用户添加到&#x200B;**Adobe Admin Console**&#x200B;中的[AEM Assets DM OpenAPI Users - delivery](https://adminconsole.adobe.com/)产品配置文件，或添加到&#x200B;**author**&#x200B;产品配置文件（例如，`<environment-name> - author - <program-id> - <environment-id>`），以作为用户在其Admin Console中没有AEM交付产品配置文件时的后备。

>[!NOTE]
>
> 还必须将用户添加到Commerce和AEM Assets。 有关完整设置，请参阅[用户和AEM Assets](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank}指南中的&#x200B;_将用户添加到Identity Management或产品可视化图表_。

用于Admin Console投放的![AEM Assets产品配置文件](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>云或本地[!TAB Adobe Commerce]

仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce（Adobe管理的PaaS基础架构）。"}

Paa需要&#x200B;**IMS客户端ID**&#x200B;才能启用资产选择器。 请参阅[配置AEM Assets项目](configure-aem.md#prerequisites)以了解先决条件，包括使用OpenAPI启用Dynamic Media时如何获取IMS客户端ID。

要使用资产选择器和自动填充的配置字段（项目ID、环境ID、域映射），请执行以下操作：

1. [为Commerce启用Adobe IMS](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank}，以便Commerce管理员使用IMS身份验证并可以读取用户的Admin Console产品配置文件。

1. [打开支持票证](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases)以请求资产选择器的自定义IMS客户端ID。

1. 从[Adobe Admin Console](https://adminconsole.adobe.com/)，将用户添加到&#x200B;**AEM Assets DM OpenAPI Users - delivery**&#x200B;产品配置文件，或&#x200B;**author**&#x200B;产品配置文件（例如，`<environment-name> - author - <program-id> - <environment-id>`），以备用户在其Admin Console中没有AEM交付产品配置文件时作为回退。

如果没有IMS，您仍然可以通过在Commerce管理员中手动输入项目ID和环境ID来配置集成。

>[!ENDTABS]

## 相关文档

* [为AEM Assets集成配置IMS用户权限](setup-synchronization.md) — 将Commerce连接到AEM Assets并配置匹配规则。
* [手动资源选择](../synchronize/asset-selector-integration.md) — 将资源选择器用于类别图像和页面生成器。
* [将用户添加到AEM Assets或产品可视化图表](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} — 对于ACCS，请先将用户添加到Commerce和AEM Cloud Manager（业务负责人、部署管理员）。 **AEM Assets DM OpenAPI Users - delivery**&#x200B;配置文件（或作为回退的&#x200B;**author**&#x200B;配置文件）是Asset Selector和自动填充功能的额外要求。
* [将团队成员分配给AEM交付层](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}。 有关投放访问权限的AEM文档。
