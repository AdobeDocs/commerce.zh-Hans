---
title: 集成限制和边界
description: 了解使用Commerce的LLM Optimizer的第三方目录的范围限制、自动修复覆盖范围、抓取先决条件、企业规模注意事项以及受限制的测试版访问限制。
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 集成限制和边界

>[!IMPORTANT]
>
>对此集成的访问受限。 请联系您的技术客户经理以了解详细信息。

使用此主题可以设置对[!DNL Adobe Commerce]和[!DNL Adobe LLM Optimizer]集成可以自动执行的操作、您仍然负责的位置以及哪些约束仍在演变的期望。

## 第三方目录限制 {#third-party-catalog}

当目录&#x200B;**不**&#x200B;在[!DNL Adobe Commerce]中处于活动状态时：

- 根据您的设置，LLM Optimizer仍然可以使用镜像或导入的目录数据来识别问题并提出改进建议。
- **直接将自动修复**&#x200B;写入商户的商务平台与写入商户的源目录不同。 可能需要镜像目录、导出/导入或合作伙伴自动化来应用更改。

对于Commerce托管的目录，将批准的名称和描述更新转至Commerce记录系统。 请参阅[将LLM Optimizer与Adobe Commerce结合使用](get-started/use-llmo-with-commerce.md)。

## 规模和技术限制 {#scale-limits}

大型目录和高的URL计数可能会增加抓取、分析和边缘部署模式的压力。

## 抓取和机器人可读性 {#crawling}

有意义的目录和PDP分析假设与LLM相关的&#x200B;**机器人可以访问**&#x200B;您关心的URL，并且页面结构合理，自动化分析是可靠的。 机器人规则、身份验证、地理阻挡和高度个性化可能会减少覆盖范围。

## 相关主题

- [集成概述](overview.md)
- [将Adobe Commerce连接到LLM Optimizer](get-started/connect-to-llmo.md)
- [将LLM Optimizer与Adobe Commerce一起使用](get-started/use-llmo-with-commerce.md)
