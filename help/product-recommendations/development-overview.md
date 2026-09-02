---
title: 产品Recommendations管理员开发
description: “产品推荐”体系结构和开发功能的概述。
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
TQID: https://experienceleague.adobe.com/DtPYY7DaB-A7-VyTeXkjL9Y2My-WOQx-9CD-TgrcTmk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: 127067a1ef47c7d9e51c5792e03b568dd818fe8e
workflow-type: tm+mt
source-wordcount: 300
ht-degree: 0%

---

# 产品Recommendations管理员开发

产品推荐是一个强大的营销工具，可用于提高转化率、增加收入和刺激购物者参与。 产品推荐以单元的形式出现在店面上，例如“查看了这个产品的客户也查看了”、“购买了这个产品的客户也购买了”、“为您推荐”等。 [Adobe AI](https://business.adobe.com/cn/ai.html)支持Adobe Commerce产品推荐，该推荐使用人工智能和机器学习算法对汇总的购物者数据进行深入分析。 此数据与Commerce目录结合使用后，可为购物者提供引人入胜、相关且个性化的体验。

>[!NOTE]
>
>如果店面是使用PWA Studio实现的，请参阅[PWA文档](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)。 了解如果您使用自定义前端技术（如React或Vue JS），如何在[headless](headless.md)环境中集成产品推荐。 Headless实例必须实施事件才能为产品推荐工作区提供支持。

## 架构概述

从较高层面来看，Commerce产品推荐部署为SaaS。 Commerce端包括店面（其中包含事件收集器和推荐布局模板）和后端（其中包含数据服务、SaaS导出模块和管理UI）。 Adobe AI情报服务在SaaS方面得到利用。

![产品推荐体系结构图](assets/arch-diag-sensei.svg)

安装和配置推荐模块后，您的店面即可收集行为数据。 Adobe AI会将此数据与目录数据相结合，以计算Recommendations服务使用的产品关联。 然后，您可以直接从管理UI创建、管理和部署产品推荐单元。

## 后续步骤

请阅读以下主题以开始使用产品推荐：

- [如何实施产品推荐](implementation-workflow.md)

- [安装和配置产品推荐](install-configure.md)

- [创建产品推荐](create.md)
