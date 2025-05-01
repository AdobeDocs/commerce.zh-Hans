---
title: 渠道
description: 了解如何使用渠道将您的零售结构定义成有意义的业务组。
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 渠道

>[!NOTE]
>
>本文档描述了早期访问开发中的产品，并未反映用于正式发布的所有功能。

渠道帮助您将零售结构定义成有意义的业务组。 渠道通过应用特定策略和过滤器来影响产品可见性，这些策略和过滤器可确定哪些产品显示在店面上。 这些策略可以包括品牌、模型或部件类别等属性，从而确保根据渠道配置，购物者只能看到相关产品。 此外，渠道可以使用价格手册来显示特定于客户的价格，从而进一步定制购物体验。

## 添加渠道

在此部分中，您将创建一个渠道。 在继续创建渠道之前，请确保您已[创建策略](./policies.md)。

1. 在左侧菜单上，打开&#x200B;**[!UICONTROL Catalog]**&#x200B;部分并单击&#x200B;**[!UICONTROL Channels]**。

![渠道](../assets/channels.png)

1. 单击&#x200B;**[!UICONTROL Add Channel]**&#x200B;。

1. 在将渠道添加到列表表单中，填写渠道详细信息：

   * **名称** — 输入渠道的名称。 例如，“Celport”。&#x200B;AEM
   * **范围** — 添加范围（区域设置）。 例如，“en-US”。 按&#x200B;**enter**&#x200B;键。
   * **策略** — 使用下拉菜单选择相关策略。 例如，“品牌”、“型号”。&#x200B;AEM确保您已[创建策略](./policies.md)。

1. 单击&#x200B;**[!UICONTROL Add]**&#x200B;以创建渠道。&#x200B;AEM

   如果&#x200B;**[!UICONTROL Add]**&#x200B;按钮未处于活动状态，请通过将光标置于“范围”字段中并按&#x200B;**enter**&#x200B;来确保正确添加范围&#x200B;。

“渠道”页面将更新以显示新渠道&#x200B;。

![已更新渠道页面](../assets/updated-channels-list.png)

完成这些步骤后，新渠道将配置为根据您选择的范围和策略显示产品和定价。
