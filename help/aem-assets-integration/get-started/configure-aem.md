---
title: 配置AEM Assets项目
description: 通过添加集成所需的元数据，启用Adobe Commerce和AEM Assets之间的无缝资源同步。
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
source-git-commit: 6cd37fda03bb51a1375b0e9dc542f9e02d3c6e54
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# 配置AEM Assets项目以支持Commerce元数据

要在AEM Assets中管理Commerce资源文件，请完成以下步骤以使用所需的样板代码和元数据配置AEM Assets项目，从而从AEM创作环境管理Commerce资源。

* **步骤1：**&#x200B;使用样板代码安装AEM项目模板，以将Commerce命名空间和元数据架构资源添加到Experience Manager Assets as a Cloud Service环境配置。
* **步骤2：**&#x200B;设置要应用于Commerce资源文件的元数据配置文件

## 将样板代码添加到您的AEM项目

Adobe提供了AEM Commerce样板`assets-commerce`，用于将Commerce命名空间和元数据架构资源添加到Experience Manager Assets as a Cloud Service环境配置。 将此代码作为&#x200B;**Maven**&#x200B;包部署到您的环境。 然后，在AEM Assets创作环境中配置Commerce元数据以完成设置。

样板可向AEM Assets创作环境添加以下资源：

* [自定义命名空间](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json)，`Commerce`用于标识与Commerce相关的属性。

   * 带有标签`commerce:isCommerce`的自定义元数据类型`Eligible for Commerce`用于标记与Adobe Commerce项目关联的Commerce资源。

   * 用于添加`commerce:skus`属性的自定义元数据类型&#x200B;**[!UICONTROL Product Data]**&#x200B;和相应的UI组件。 产品数据包含用于将Commerce资源与产品SKU关联的元数据属性。

     ![自定义产品数据UI控件](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * 自定义元数据类型`commerce:roles`和`commerce:positions`属性，用于显示如何在Commerce中显示该资源。

* 具有Commerce选项卡的元数据架构表单，包括用于标记Commerce资源的`Eligible for Commerce`和`Product Data`字段。 该表单还提供了在AEM Assets UI中显示或隐藏`roles`和`position`字段的选项。

  AEM Assets元数据架构表单的![Commerce选项卡](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* [示例已标记并批准Commerce资源](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg`以支持初始资源同步。 只有已获批准的Commerce资源才能从AEM Assets同步到Adobe Commerce。

>[!NOTE]
>
> 有关[AEM Commerce样板](https://github.com/ankumalh/assets-commerce)的更多信息，请参阅&#x200B;**自述文件**&#x200B;页面。

### 先决条件

您需要以下资源和权限才能将`commerce-assets`包部署到AEM Assets as a Cloud Service AEM环境：

* [使用计划和部署管理员角色访问AEM Assets Cloud Manager计划和环境](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo)。

* [本地AEM开发环境](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview)，熟悉AEM本地开发过程。

* 了解[AEM项目结构](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure)以及如何使用Cloud Manager部署自定义内容包。

### 安装`commerce-assets`包

1. 如果需要，可在AEM Cloud Manager中为AEM Assets项目创建生产和暂存环境。

1. 根据需要配置部署管道。

1. 从GitHub中，从[AEM Commerce样板](https://github.com/ankumalh/assets-commerce)下载代码。

1. 从[本地AEM开发环境](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview)，将自定义代码作为Maven包安装到AEM Assets环境配置中，或者通过将代码手动复制到现有项目配置中。

1. 提交更改并将本地开发分支推送到Cloud Manager Git存储库。

1. 从AEM Cloud Manager [部署您的代码以更新AEM环境](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager)。

## 可选。 配置元数据配置文件

在AEM Assets创作环境中，通过创建元数据配置文件来设置Commerce资源元数据的默认值。 然后，将新配置文件应用到AEM Asset文件夹以自动使用这些默认值。 此配置通过减少手动步骤来简化资产处理。

配置元数据配置文件时，您只需配置以下组件：

* 添加Commerce选项卡。 此选项卡启用由模板添加的特定于Commerce的配置设置
* 将`Eligible for Commerce`字段添加到Commerce选项卡。

产品数据UI组件会根据模板自动添加。

### 定义元数据配置文件

1. 登录到Adobe Experience Manager创作环境。

1. 在Adobe Experience Manager工作区中，单击Adobe Experience Manager图标以转到为AEM Assets创作内容管理工作区。

   ![AEM Assets创作](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

1. 通过选择锤子图标打开管理员工具。

   ![AEM作者管理员管理元数据配置文件](../assets/aem-manage-metadata-profiles.png){width="600" zoomable="yes"}

1. 通过单击&#x200B;**[!UICONTROL Metadata Profiles]**&#x200B;打开配置文件配置页面。

1. **[!UICONTROL Create]** Commerce集成的元数据配置文件。

   ![AEM作者管理员添加元数据配置文件](../assets/aem-create-metadata-profile.png){width="600" zoomable="yes"}

1. 为Commerce元数据添加选项卡。

   1. 单击左侧的&#x200B;**[!UICONTROL Settings]**。

   1. 在选项卡部分中单击&#x200B;**[!UICONTROL +]**，然后指定&#x200B;**[!UICONTROL Tab Name]**、`Commerce`。

1. 将`Eligible for Commerce`字段添加到表单。

   ![AEM作者管理员将元数据字段添加到配置文件](../assets/aem-edit-metadata-profile-fields.png){width="600" zoomable="yes"}

   * 单击&#x200B;**[!UICONTROL Build form]**。

   * 将`Single Line text`字段拖到表单中。

   * 通过单击`Eligible for Commerce`为标签添加&#x200B;**[!UICONTROL Field Label]**&#x200B;文本。

   * 在“设置”选项卡上，将标签文本添加到&#x200B;**字段标签**。

   * 将占位符文本设置为`yes`。

   * 在&#x200B;**[!UICONTROL Map to Property]**&#x200B;字段中，复制并粘贴以下值

     ```terminal
     ./jcr:content/metadata/commerce:isCommerce
     ```

1. 可选。 要在已批准的Commerce资源上传到AEM Assets环境时自动对其进行同步，请将&#x200B;_[!UICONTROL Review Status]_&#x200B;选项卡上`Basic`字段的默认值设置为`approved`。

1. 保存更新。

#### 将元数据配置文件应用到Commerce资源源文件夹

1. 从[!UICONTROL &#x200B; Metadata Profiles]页面中，选择Commerce集成配置文件。

1. 从操作菜单中选择&#x200B;**[!UICONTROL Apply Metadata Profiles to Folders]**。

1. 选择包含Commerce资源的文件夹。

   创建不存在的Commerce文件夹。

1. 单击&#x200B;**[!UICONTROL Apply]**。

## 后续步骤

仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"} [安装Adobe Commerce包](configure-commerce.md)

**配置您的Commerce店面** — 要将AEM Assets与由Edge Delivery Services提供支持的Commerce店面一起使用，请完成[EDS AEM Assets配置](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=zh-Hans)主题中所述的店面配置。
