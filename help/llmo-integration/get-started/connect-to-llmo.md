---
title: 连接 [!DNL Adobe Commerce] 到 [!DNL Adobe LLM Optimizer]
description: 在查看机会或部署更新之前，启用所需的Commerce服务、配置LLM Optimizer连接、验证目录访问权限并确认租户准备工作。
role: Admin, User
recommendations: noCatalog
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# 将[!DNL Adobe Commerce]连接到[!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>对此集成的访问受限。 请联系您的技术客户经理以了解详细信息。

本文介绍如何连接可用于LLM Optimizer的[!DNL Adobe Commerce]目录。

>[!NOTE]
>
>本文侧重于集成的Commerce方面。 有关LLM Optimizer的一般信息，请参阅[LLM Optimizer产品文档](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/home)。

## 启用所需的Commerce服务 {#enable-commerce-services}

请与Commerce管理员或实施合作伙伴合作，确保满足以下要求：

- 根据您的架构（包括部署中的任何SaaS数据导出器或连接器），LLM Optimizer必须读取的目录数据是&#x200B;**导出或同步的**。
- API访问、凭据和环境URL（沙盒与生产）与您要在LLM Optimizer中使用的&#x200B;**租户**&#x200B;匹配。

## 在LLM Optimizer中配置Commerce连接 {#configure-commerce-connection}

**配置Commerce连接：**

1. 在[!DNL Adobe LLM Optimizer] UI中，打开&#x200B;**客户配置**，然后选择&#x200B;**[!UICONTROL Commerce]**&#x200B;选项卡。

   “客户配置”选项卡上的![Commerce配置](../assets/llmo-commerce-config.png)

1. 单击&#x200B;**[!UICONTROL Add Store View]**&#x200B;以创建新行，或展开现有的存储视图条目以对其进行编辑。
1. 输入&#x200B;**[!UICONTROL Store View URL]**（必需）。

   使用该商店视图的店面URL，包括任何区域设置或路径前缀（例如，`https://brand.example.com/`或`https://brand.example.com/fr/`）。

1. 输入&#x200B;**[!UICONTROL Environment ID]**（必需） — LLM Optimizer应连接到的Adobe Commerce环境的标识符。
1. 输入&#x200B;**[!UICONTROL Website Code]**、**[!UICONTROL Store Code]**&#x200B;和&#x200B;**[!UICONTROL Store View Code]**（必需）。

   这些值必须与您在Commerce管理员中针对您连接的网站、商店和商店视图的代码匹配。

1. 可选：输入Commerce实例的主机名的&#x200B;**[!UICONTROL Host Name]**（例如`www.example.com`）（如果该值不属于URL）。
1. 输入&#x200B;**[!UICONTROL Adobe Commerce Endpoint]** — 用于API访问的Adobe Commerce实例的基本URL。
1. 输入或粘贴用于向Commerce API验证请求的&#x200B;**[!UICONTROL API Key]**。

   如果需要将密钥安全地复制到其他位置，请单击字段旁边的&#x200B;**[!UICONTROL Copy]**。

1. 单击&#x200B;**[!UICONTROL Save]**&#x200B;以存储配置。

保存后，请等待任何&#x200B;**初始同步**&#x200B;或验证作业完成，然后再依赖该存储视图的目录或审核结果。

要删除商店视图配置，请打开该项并单击&#x200B;**[!UICONTROL Delete]**。

### 字段描述 {#commerce-connection-fields}

| 字段 | 描述 |
| --- | --- |
| 商店视图URL | LLM Optimizer应将存储视图的公共URL视为目录和审核工作流的作用域。 |
| 环境ID | Commerce环境标识符(来自您的云或部署文档，或者来自管理员（如果适用）)。 |
| 网站代码 | 拥有该目录的网站的Commerce **[!UICONTROL Website Code]**。 |
| 商店代码 | 在该网站下的商店的Commerce **[!UICONTROL Store Code]**。 |
| 商店视图代码 | 商店视图的Commerce **[!UICONTROL Store View Code]**（例如，`default`）。 |
| 主机名 | 表单除了其他URL外还要求提供的Commerce店面或实例的主机名。 |
| Adobe Commerce端点 | LLM Optimizer用于访问Commerce API的实例URL。 |
| API密钥 | API身份验证的密钥；将其视为任何生产凭据。 |

## 确认租户和环境就绪 {#confirm-tenant-readiness}

- 验证连接的&#x200B;**沙盒**&#x200B;项目是否未与&#x200B;**生产** Commerce数据混合，除非是有意为之。
- 在Experience Cloud和Commerce中调整&#x200B;**用户角色**，以使批准部署操作的用户在双方都具有正确的权限。

## 后续步骤 {#next-steps}

[将LLM Optimizer与Adobe Commerce结合使用](use-llmo-with-commerce.md)以查看机会、部署目录更新并了解覆盖行为。
