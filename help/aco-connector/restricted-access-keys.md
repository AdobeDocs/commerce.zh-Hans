---
title: 管理B2B共享目录的受限访问密钥
description: 了解如何管理Adobe Commerce Optimizer Connector用于保护B2B共享目录投影的受限制访问密钥。
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%
---

# 管理B2B共享目录的受限访问密钥

[!BADGE Private Beta]{type=Caution tooltip="需要Adobe Commerce Optimizer Connector B2B扩展，该扩展当前为私有Beta版。"}

如果您将[!DNL Adobe Commerce] B2B共享目录与[!DNL Adobe Commerce Optimizer Connector B2B extension]一起使用，则扩展会在创建目录视图时自动生成并分配第一个受限访问密钥。 使用Commerce管理员中的[!UICONTROL Restricted Access Keys]页面查看该密钥，并创建、分配或删除其他密钥。

![B2B共享目录视图的限制访问密钥](assets/restricted-access-keys.png){width="800" zoomable="yes"}

>[!NOTE]
>
>要管理您为非B2B用例（如合作伙伴门户）手动创建的密钥，请参阅[受限访问密钥](/help/optimizer/setup/restricted-access-keys.md#create-a-restricted-access-key)。

## 访问页面 {#access-the-page}

从Commerce管理员转到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Restricted Access Keys]**。

您可以从“共享目录”网格或“公司”网格为目录视图分配键。 请参阅[将密钥分配给B2B共享目录视图](#assign-keys-to-a-shared-catalog-view)。

>[!NOTE]
>
>有关此页上的字段的引用，请参阅&#x200B;*Commerce管理指南*&#x200B;中的[受限访问密钥管理](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"}。—>

## 当您需要自动键以外的其他键时 {#when-you-need-more-than-the-automatic-key}

[!DNL Adobe Commerce Optimizer Connector B2B extension]生成的自动密钥涵盖了大多数B2B共享目录，无需您执行任何操作。 在以下情况下自行管理密钥：

- **旋转键** — 创建新键，将其与现有键一起分配给目录视图，确认它正常工作，然后删除旧键。 自动旋转尚不可用。
- **密钥无法链接** — 如果[目录视图同步状态](catalog-view-sync-status.md)显示与密钥相关的漂移，请尝试再次保存目录视图分配以重试失败的链接。 如果密钥仍然失败，请先运行[!UICONTROL Reconcile & Repair]以恢复密钥或状态，然后再创建替换。 仅当密钥过期或故障永久不可恢复时才创建替换密钥。
- **查找公钥** — 在“受限访问密钥”页面上，选择&#x200B;**[!UICONTROL View Public Key]**&#x200B;以查看并复制密钥的公共密钥。

一个目录视图最多可以同时具有三个分配的键。 在密钥轮换期间，[!DNL Adobe Commerce Optimizer]接受由任何分配的未过期密钥签名的令牌，无需手动步骤来设置“活动”密钥。

## 创建密钥

在[!UICONTROL Restricted Access Keys]页面上，通过选择&#x200B;**[!UICONTROL Create Key]**&#x200B;创建一个键。

Commerce会生成一个新的密钥对并保留私钥。 “受限访问密钥”表将更新为显示唯一密钥ID的新密钥条目。 将密钥分配给目录视图时使用此[!UICONTROL Key ID]。

在将公钥分配给目录视图之前，该公钥未向[!DNL Adobe Commerce Optimizer]注册。 注册后，将更新受限访问密钥表条目，以显示目录分配和到期日期。

## 将键分配给从B2B共享目录投影的目录视图 {#assign-keys-to-a-shared-catalog-view}

从公司帐户或共享目录页的目录视图中分配或取消分配键，而不是从主[!UICONTROL Restricted Access Keys]网格中分配或取消分配键。

目录视图必须至少有一个键，并且最多可以有三个。

- 如果尝试分配第四个键，则在尝试保存值时会收到一条错误消息：`A Catalog View can have at most 3 access keys.`
- 如果目录视图只有一个键，则无法删除或取消分配该键。

要更新目录视图键配置，您可以从公司帐户页面或共享目录页面访问该配置。

>[!BEGINTABS]

>[!TAB 从公司帐户管理密钥]

1. 从Commerce管理员中，打开公司页面(**[!UICONTROL Customers]** > **[!UICONTROL Companies]**)。

1. 在公司的[!UICONTROL Action]列中，选择[!UICONTROL Edit]。

1. 要查看从分配给公司的共享目录投影的目录视图列表，请展开&#x200B;_[!UICONTROL Catalog Views]_&#x200B;部分。

选项卡列出了从共享目录投影的目录视图，包括其分配的键值。

1. 在要更新的目录视图的[!UICONTROL Actions]列中，选择&#x200B;**[!UICONTROL Edit Restricted Access Keys]**。

   ![编辑受限访问密钥下拉列表，显示分配给目录视图的密钥](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. 要分配密钥，请选择&#x200B;**[!UICONTROL Access Keys]**&#x200B;下拉列表。 然后，选择[!UICONTROL key ID]未分配的键，例如`#42`。 然后，单击[!UICONTROL Done]将其分配给目录视图。

   已分配给其他目录视图的键将相应地添加标签。

1. 要删除访问令牌，请选择密钥标签中的`x`控件，将其从[!UICONTROL Access Tokens]字段中删除。

1. 要保存并应用配置更新，请选择&#x200B;**[!UICONTROL Save]**。

>[!TAB 从共享目录管理密钥]

1. 从Commerce管理员中，打开共享目录页面(**[!UICONTROL Catalog]** > **[!UICONTROL Shared catalogs]**)。

1. 在共享的[!UICONTROL Action]列中，从[!UICONTROL Select]菜单中选择&#x200B;**[!UICONTROL General Settings]**。

1. 要查看从共享目录投影的目录视图列表，请从[!UICONTROL Shared Catalog Information]菜单中选择&#x200B;**[!UICONTROL Catalog Views]**。

[!UICONTROL Catalog Views]页列出了每个目录视图的目录视图ID、关联的商店视图和访问密钥。

1. 在要更新的目录视图的[!UICONTROL Actions]列中，选择&#x200B;**[!UICONTROL Edit Restricted Access Keys]**。

   ![编辑受限访问密钥下拉列表，显示分配给目录视图的密钥](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. 要分配密钥，请选择&#x200B;**[!UICONTROL Access Keys]**&#x200B;下拉列表。 然后，根据默认键标题选择未分配的键，例如`#42`。 然后，单击[!UICONTROL Done]将其分配给目录视图。

   已分配给其他目录视图的键将相应地添加标签。

1. 要删除访问令牌，请选择密钥标签中的`x`控件，将其从[!UICONTROL Access Tokens]字段中删除。

1. 要保存并应用配置更新，请选择&#x200B;**[!UICONTROL Save]**。

>[!ENDTABS]

## 管理密钥到期和续订

您可以为受限访问密钥配置默认密钥生命周期。 此值确定[!DNL Adobe Commerce Optimizer Connector B2B]扩展生成初始密钥或手动创建新密钥时设置的到期日期。

到期日期显示在[!UICONTROL Restricted Access Keys]页面的[!UICONTROL Expires At]列中。

要更改持续时间，请转到&#x200B;**[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Restricted Access Keys]**。 在[!UICONTROL Provisioning]页面上，更新&#x200B;**[!UICONTROL Default Key Expiry (days)]**&#x200B;字段。 默认系统密钥生命周期最初设置为较长的期限（约100年）。 请确保将其更新为与您的安全策略匹配的值。

### 密钥续订

当密钥到期后10天内，[!UICONTROL Restricted Access Keys]页面在其条目旁边显示警告图标。 如果您在密钥过期之前未续订密钥，则在您分配新密钥之前，将无法访问目录视图。

您可以随时创建和分配新密钥，并在确认新密钥有效后删除旧密钥。

## 已知限制

自动密钥轮换尚不可用。

>[!MORELIKETHIS]
>
> - [管理受限访问密钥](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} — 在&#x200B;*Commerce管理指南*&#x200B;中，此页面的完整字段引用 — >
> - [监视目录视图同步](catalog-view-sync-status.md) — 监视这些密钥保护的目录视图
> - [私有目录视图](/help/optimizer/setup/private-catalog-view.md) — 了解什么是连接器管理的私有目录视图
> - [受限访问密钥](/help/optimizer/setup/restricted-access-keys.md) — 了解基于ACO Studio的手动密钥流如何用于非B2B用例
