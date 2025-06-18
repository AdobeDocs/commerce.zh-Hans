---
title: 查看和管理日志
description: 了解在何处查找和管理产品可视化图表的日志。
feature: CMS, Media, Integration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目(Adobe管理的PaaS基础架构)和内部部署项目上的Adobe Commerce 。"
source-git-commit: b6e190e883087a942630f0a27781654cd2c68781
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# 查看和管理日志

产品可视化在您的Commerce实例中提供以下日志文件：

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

请要求系统管理员检查这些日志的日志文件轮换计划，以防止它们变得太大。 在某些环境中，日志会自动轮换；在另一些环境中，您必须手动配置日志轮换。  有关详细信息，请参阅以下主题：

- 对于Adobe Commerce内部部署，请要求系统管理员设置[日志轮换](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings)。
- 有关云基础架构项目上的Adobe Commerce，请参阅[查看和管理日志](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html)。
