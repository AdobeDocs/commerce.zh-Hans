---
title: 将 [!DNL Adobe LLM Optimizer] 与 [!DNL Adobe Commerce]一起使用
description: 在LLM Optimizer中导航Commerce机会，查看PDP和目录扩充，将更新部署到 [!DNL Adobe Commerce]，在管理员和店面中进行验证，并了解如何覆盖和摄取标记机会已过时。
role: Admin, User
recommendations: noCatalog
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# 将[!DNL Adobe LLM Optimizer]与[!DNL Adobe Commerce]一起使用

>[!IMPORTANT]
>
>对此集成的访问受限。 请联系您的技术客户经理以了解详细信息。

将Commerce[连接到LLM Optimizer](connect-to-llmo.md)后，您主要在&#x200B;**[!DNL Adobe LLM Optimizer]** UI中工作，以便在您准备就绪时查看机会并将批准的更改推送到目录中。 本文介绍了两种以Commerce为中心的优化类型，如何使用&#x200B;**[!UICONTROL Opportunities]**，部署操作在[!DNL Adobe Commerce]中的行为方式，以及外部更新如何与LLM Optimizer建议交互。 有关集成的更全面的信息，请参阅[集成概述](../overview.md)。

## 了解LLM Optimizer中的Commerce优化 {#understand-optimizations}

对于Commerce支持的目录，LLM Optimizer提供&#x200B;**[!UICONTROL Product Detail Page Enrichment]**&#x200B;和&#x200B;**[!UICONTROL Product Catalog Enrichment]**。

| 焦点 | 它的用途 |
| --- | --- |
| **[!UICONTROL Product Detail Page Enrichment]** （PDP扩充） | 建议改进产品页面的读取方式，以便进行AI驱动型发现，而无需更换店面布局。 |
| **[!UICONTROL Product Catalog Enrichment]** | 针对特定产品建议&#x200B;**产品名称**&#x200B;和&#x200B;**产品描述**&#x200B;更新，您可以根据需要查看和编辑这些更新并将其应用于您的Commerce目录。 |

使用&#x200B;**[!UICONTROL Opportunities]**&#x200B;打开产品或URL列表，并处理所选类型的建议。

## 导航Commerce机会 {#navigate-commerce-opportunities}

**打开与Commerce相关的机会：**

1. 在左边栏中，单击&#x200B;**[!UICONTROL Opportunities]**。
1. 单击&#x200B;**[!UICONTROL Commerce Opportunity]**&#x200B;以显示以您的[!DNL Adobe Commerce]目录为目标的优化类型。
1. 选择&#x200B;**[!UICONTROL Product Catalog Enrichment]**&#x200B;或&#x200B;**[!UICONTROL Product Detail Page Enrichment]**，具体取决于您要处理的内容。

![Commerce机会筛选器和优化类型](../assets/llmo-opportunities.png)

### 了解机会量度 {#opportunity-metrics}

每个机会视图都总结了影响，以便您能够确定工作的优先级：

- **产品页面**&#x200B;或&#x200B;**URL**：针对该优化类型评估的页面或产品。
- **代理流量**：由AI代理发起的访问和交互，可以帮助您首先优先处理高影响力的机会。

### 了解建议状态 {#suggestion-states}

这两种扩充类型使用相同的工作流视图：

- **[!UICONTROL Current Suggestions]**：要审阅的新项目或活动项目。
- **[!UICONTROL Fixed Suggestions]**：您已部署或解析的项。
- **[!UICONTROL Ignored Suggestions]**：您特意从操作中排除的项目。

### 审查和部署PDP扩充 {#review-deploy-pdp}

PDP扩充适用于以下团队：希望在AI驱动型发现中更清晰的产品页面消息传递，同时保留您的促销人员设计的店面体验。

**要查看和部署PDP扩充：**

1. 从&#x200B;**[!UICONTROL Opportunities]**&#x200B;中打开&#x200B;**[!UICONTROL Product Detail Page Enrichment]**。
1. 在&#x200B;**[!UICONTROL URLs with Suggestions]**&#x200B;表中，选择&#x200B;**[!UICONTROL Current Suggestions]**。
1. 对于URL或SKU，单击&#x200B;**[!UICONTROL Preview]**&#x200B;以查看AI分析和建议的扩充。
1. 可选：单击&#x200B;**[!UICONTROL Copy]**&#x200B;将内容粘贴到外部编辑器中，或单击&#x200B;**[!UICONTROL Edit suggestion]**&#x200B;就地编辑。
1. 可选：如果建议与您的策略不匹配，请将其移至&#x200B;**[!UICONTROL Ignored Suggestions]**。
1. 审核并批准后，选择要更新的URL或SKU的行，然后单击&#x200B;**[!UICONTROL Deploy optimizations]**&#x200B;并确认。

部署后，建议将移动到LLM Optimizer中具有优化状态的&#x200B;**[!UICONTROL Fixed Suggestions]**。

>[!NOTE]
>
>PDP扩充部署需要在LLM Optimizer中完成&#x200B;**在Edge中优化**。 如果载入不完整，UI会提示您先完成设置，然后再部署。

### 查看和部署产品目录扩充 {#review-deploy-catalog}

目录扩充适用于希望直接在Commerce中收紧产品名称和长说明的团队，您可以在保存任何内容之前查看建议。

**要审阅和部署产品目录扩充：**

1. 从&#x200B;**[!UICONTROL Opportunities]**&#x200B;中打开&#x200B;**[!UICONTROL Product Catalog Enrichment]**。
1. 在&#x200B;**[!UICONTROL URLs with Suggestions]**&#x200B;表中，选择&#x200B;**[!UICONTROL Current Suggestions]**。
1. 单击URL或SKU行的展开控件以显示建议的&#x200B;**产品名称**&#x200B;和&#x200B;**产品描述**&#x200B;更新。
1. 可选：在部署之前，单击编辑图标可调整建议的名称或描述。
1. 可选：如果建议与您的策略不匹配，请将其移至&#x200B;**[!UICONTROL Ignored Suggestions]**。
1. 审核并批准后，选择要更新的URL或SKU的行，然后单击&#x200B;**[!UICONTROL Deploy optimizations]**&#x200B;并确认。

批准的名称和描述更改会像其他产品更新一样保存到您的[!DNL Adobe Commerce]目录。

>[!IMPORTANT]
>
>将部署视为生产目录更改。 使用常规的更改控制、暂存和QA实践。 只有在推销和SEO利益相关者就最终副本达成一致后才能部署。

部署后，建议将移动到&#x200B;**[!UICONTROL Fixed Suggestions]**，状态为&#x200B;**已应用**。

## 在Commerce管理员中验证更新 {#verify-in-admin}

**要验证已部署的目录扩充：**

1. 登录到[!DNL Adobe Commerce] **管理员**。
1. 转到&#x200B;**[!UICONTROL Catalog]** > **[!UICONTROL Products]**。
1. 根据需要使用筛选器和&#x200B;**存储视图**&#x200B;选择器（例如，**[!UICONTROL Default Store View]**），然后搜索&#x200B;**SKU**。
1. 在编辑模式下打开产品。

   产品表单显示扩充的&#x200B;**产品名称**。

   LLM Optimizer扩充后的![产品名称字段](../assets/llmo-admin-name.png)

1. 可选：如果要保留手动输入的名称，请选择&#x200B;**[!UICONTROL Override LLM Optimizer provided Product Name]**。

手动覆盖会影响机会与目录保持同步的方式；请参阅[管理员中的手动覆盖](#manual-override-in-the-admin)。

1. 展开&#x200B;**[!UICONTROL Content]**&#x200B;部分并找到&#x200B;**描述**&#x200B;字段。

   当您部署说明更改时，即会显示扩充说明。

   LLM Optimizer扩充后的![描述字段](../assets/llmo-admin-description.png)

1. 可选：如果要保留手动输入的描述，请选择&#x200B;**[!UICONTROL Override LLM Optimizer provided Description]**。

## 验证店面更新 {#verify-storefront}

在您的店面中搜索SKU并打开PDP。 确认&#x200B;**name**&#x200B;和任何显示长&#x200B;**description**&#x200B;的区域反映了您批准的内容。 此外，还要确认任何使用相同目录属性的下游渠道（与转出相关）。

<!--
## PDP enrichment rollback {#pdp-rollback}

If your project includes PDP enrichment opportunities, **rollback** behavior may support **bulk** or **per-URL** actions, depending on your LLM Optimizer release. Follow the in-product options for rollback. For **[!UICONTROL Product Catalog Enrichment]**, undoing a name or description in Commerce is effectively a new catalog edit or a follow-up opportunity, not a separate undo control in the Admin unless your team implements one.
-->

## 覆盖、引入和陈旧机会 {#overrides-ingestion}

在LLM Optimizer更新产品的名称或描述后，其他摄取系统（如REST API调用、CSV导入、PIM馈送或类似流程）可能会更改相同的字段。 以下各节描述了这种情况下发生的情况。

### 摄取操作将再次发送原始目录值

如果外部进程写入原始名称或描述（在LLM Optimizer部署之前存在的值），则Commerce会根据集成规则继续执行该字段的LLM Optimizer部署值。 机会可能不会仅根据该摄取自动恢复。

### 摄取会发送一个新值

如果外部流程发送的新值不仅仅是LLM Optimizer之前文本的重复（例如，将“Red Shoes”重命名为“Iconic Red Shoes”），则将应用该新目录值，并且相关的LLM Optimizer机会通常在LLM Optimizer中标记为&#x200B;*过时*，因为实时目录不再与建议上下文匹配。

### 管理员中的手动覆盖 {#manual-override-in-the-admin}

如果您在[!DNL Adobe Commerce] *管理员*&#x200B;中手动编辑产品名称或描述：

- *Admin*&#x200B;值作为该手动更改的记录系统入选。
- LLM Optimizer机会标记为&#x200B;*过时*。
- 在LLM Optimizer中，UI会恢复到该机会的原始状态，以便您可以重新基线或在分析再次运行时接受新建议。

这些规则可帮助您了解在多个渠道接触同一SKU时，LLM Optimizer、摄取馈送或&#x200B;*管理员*&#x200B;编辑是否具有权威性。

## 最佳实践

- **记录产品名称和描述的系统所有权**，以便PIM或馈送作业不会无意中与LLM Optimizer预期冲突。
- **在批量部署标题或描述之前，请与SEO和品牌团队协调**。
- 主要目录导入后&#x200B;**重新同步**&#x200B;或&#x200B;**重新分析**，以便机会反映当前目录状态。

## 在演示中尝试

使用Frescopa演示环境查看正在运行的Commerce机会类型：

- [查看产品目录扩充演示](https://play.llmo.now/org/demo-org/opportunities/commerce-product-catalog-enrichment/e5f2a854-7477-421c-820f-74d5dd595647?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)
- [查看产品详细信息页面扩充演示](https://play.llmo.now/org/demo-org/opportunities/commerce-product-page-enrichment/4e8b0428-0893-4864-a00e-fc1d77fb3372?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## 相关主题

- [将Adobe Commerce连接到LLM Optimizer](connect-to-llmo.md)
- [集成概述](../overview.md)
- [集成限制和边界](../boundaries-limits.md)
