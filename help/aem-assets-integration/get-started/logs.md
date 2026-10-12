---
title: 查看和管理日志
description: 了解在何处查找和管理Commerce的AEM Assets集成的日志。
feature: CMS, Media, Integration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%
---
# 查看和管理日志

AEM Assets集成在您的Commerce实例中提供以下日志文件：

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

有关管理员中已同步资产的以资产为中心的视图（包括搜索、筛选器和同步错误摘要），请参阅[查看AEM Assets同步状态](sync-status.md)。

请要求系统管理员检查这些日志的日志文件轮换计划，以防止它们变得太大。 在某些环境中，日志会自动轮换；在另一些环境中，您必须手动配置日志轮换。  有关详细信息，请参阅以下主题：

- 对于Adobe Commerce内部部署，请要求系统管理员设置[日志轮换](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/next-steps/configuration#server-settings)。
- 有关云基础架构项目上的Adobe Commerce，请参阅[查看和管理日志](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/test/log-locations)。
