---
title: ' [!DNL Commerce] 服务的HIPAA准备就绪'
description: 了解如何使用 [!DNL Data Connection] 扩展与Experience Platform共享 [!DNL Commerce] 数据并保持HIPAA合规性。
role: Admin, Leader
feature: Security, Compliance
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# [!DNL Commerce]服务的HIPAA准备就绪

[!DNL Data Connection]扩展允许您与Experience Platform共享[!DNL Commerce]后台事件数据并维护HIPAA合规性。

>[!IMPORTANT]
>
>由于店面事件是在客户端生成的，因此商家应负责[不将店面事件数据](connect-data.md#data-collection)发送到Experience Platform。

在本文中，您将了解：

- 安装内容
- 如何确保发送到Experience Platform的数据已为HIPAA就绪
- [!DNL Commerce]中的数据加密

## 安装

如果您购买了Adobe [!DNL Commerce]的医疗保健加载项，则很可能已安装[HIPAA就绪扩展](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation)。 要确保您的[!DNL Commerce]后台事件数据为HIPAA就绪，您还需要安装[!DNL Data Connection]扩展和附加的&#x200B;**数据服务HIPAA**&#x200B;扩展。 **数据服务HIPAA**&#x200B;扩展可确保您发送到Experience Platform的任何后台数据都支持HIPAA。 了解[如何安装扩展](install.md#install-the-data-services-hipaa-extension)。

>[!IMPORTANT]
>
>安装&#x200B;**数据服务HIPAA**&#x200B;扩展时，将不再捕获实时搜索和产品推荐使用的店面事件数据。 这是因为店面事件数据是在客户端生成的。 要继续捕获和发送店面事件数据，请为这些服务重新启用事件收集。 有关详细信息，请参阅[常规配置](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services)。

## 如何确保发送到Experience Platform的数据已为HIPAA就绪

[!DNL Data Connection]扩展发送到Experience Platform的所有后台事件数据在[!DNL Commerce]中均被视为敏感。 但是，商家有责任将数据使用标签应用于他们在Experience Platform中的[!DNL Commerce]架构，以明确将特定数据标识为敏感数据。 将数据使用标签直接应用于架构时，这些标签会传播到基于该架构的所有现有和未来数据集。

有关数据使用标签及其在数据管理框架中的角色的概述，请参阅Experience Platform文档中的[数据使用标签概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/data-governance/labels/overview)。

### 将数据使用标签应用于[!DNL Commerce]字段

按照[管理架构的数据使用标签](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/tutorials/labels)教程中的步骤操作，了解如何将标签应用于[!DNL Commerce]架构。

查看[敏感标签词汇表](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/data-governance/labels/reference#sensitive)，了解可用于[!DNL Commerce]架构中字段的可用标签。 例如，标签`RHD`标识Protected Health Information (PHI)或Adobe按照合同规定允许您上传的病人的相关信息。

当您的[!DNL Commerce]数据标记为敏感时，您可以强制实施策略以防止构成策略违规的数据操作。 了解有关Experience Platform中[策略实施](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/data-governance/enforcement/overview)的更多信息。

## Commerce中的数据加密

Adobe [!DNL Commerce]使用块级加密。 对于存储，[!DNL Commerce]使用Amazon弹性块存储(EBS)。 所有EBS卷都使用AES-256算法进行加密，这意味着数据在静止时加密。 正在传输的[!DNL Commerce]数据是通过HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246)的安全加密连接传输的。

>[!IMPORTANT]
>
>当数据不处于静止状态或不在服务器之间传输时，Commerce不支持列或行级别的加密或加密。

### Experience Platform中的数据加密

当商家将其数据发送到Experience Platform时，将使用HTTPS TLS v1.2发送该数据。详细了解[Experience Platform](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/landing/governance-privacy-security/encryption)如何加密数据。

## [!DNL Commerce]如何处理隐私请求

了解[!DNL Commerce] [如何处理隐私请求](handle-privacy-request.md)。
