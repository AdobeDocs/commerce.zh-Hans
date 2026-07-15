---
title: AEM Assets中的Commerce元数据
description: 了解Commerce集成添加到您的AEM Assets创作环境中的AEM Assets命名空间、元数据架构和替换文本。
feature: CMS, Media, Integration
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 749
ht-degree: 0%

---

# AEM Assets中的Commerce元数据

Commerce元数据是AEM Assets和Commerce之间的合同。 它可告知Commerce哪些资源适用于Commerce、属于哪些产品以及应如何使用或显示这些资源。 此元数据允许AEM Assets集成正确映射和同步资源文件。

Commerce元数据支持以下功能：

* **通过`commerce:isCommerce`字段将资产标记为Commerce合格**。
* **通过`commerce:skus`字段将资产与一个或多个产品SKU关联**。
* **通过`commerce:roles`和`commerce:positions`字段定义资源在Commerce**&#x200B;中的显示方式。
* **添加通过`commerce:altTextStoreViews`和`commerce:altTextValues`字段由商店视图**&#x200B;键入的特定于Commerce的alt文本。
* **通过&#x200B;**[!UICONTROL Commerce]**选项卡和架构表单在AEM Assets属性UI**&#x200B;中公开这些字段。

>[!IMPORTANT]
>
>**特定于Commerce的替代文本**&#x200B;功能尚无法通过[自助上线](get-started/configure-aem.md#enable-aem-commerce-self-service)使用。 当前仅当您部署`assets-commerce`自定义代码包时提供（请参阅[手动安装assets-commerce包](get-started/configure-aem.md#install-the-assets-commerce-package-manually)）。 计划对即将发布的AEM版本提供本机支持。

要在AEM项目中配置这些资源，请参阅[配置AEM Assets项目](get-started/configure-aem.md)。 本主题的其余部分介绍如何提供元数据。

## AEM Commerce assets-commerce包内容

Adobe提供了`assets-commerce` AEM Commerce代码包，用于将Commerce命名空间和元数据架构资源添加到Experience Manager Assets as a Cloud Service配置。

此包代码可将以下资源添加到AEM Assets创作环境：

* [自定义命名空间](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json)，`Commerce`用于标识与Commerce相关的属性。

   * 带有标签`Eligible for Commerce`的自定义元数据类型`commerce:isCommerce`用于标记与Adobe Commerce项目关联的Commerce资源。

   * 用于添加&#x200B;**[!UICONTROL Product Data]**&#x200B;属性的自定义元数据类型`commerce:skus`和相应的UI组件。 产品数据包含用于将Commerce资源与产品SKU关联的元数据属性。

     ![自定义产品数据UI控件](assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * 自定义元数据类型`commerce:roles`和`commerce:positions`属性，用于显示如何在Commerce中可视化该资源。

   * 替换文本多字段(_[!UICONTROL Alt texts]_)元数据，以便编辑人员可以为每个Commerce商店视图代码输入替换文本。 多字段在两个索引对齐的`String[]`属性中持续存在：

      * `commerce:altTextStoreViews` — 存储每行的视图代码。
      * `commerce:altTextValues` — 在与`commerce:altTextStoreViews`中的每个条目相同的索引处匹配替换文本。

     使用[外部匹配器](synchronize/custom-match.md){target=_blank}的App Builder实施可以在转换资源负载时拦截这些属性。 这不会更改在目录中为产品图像分配或设定范围的方式。 查看AEM Assets元数据中的[本地化的替换文本](#localized-alt-text-in-aem-assets-metadata)。

* 具有Commerce选项卡的元数据架构表单，包括用于标记Commerce资源的`Eligible for Commerce`和`Product Data`字段。 该表单还提供了在AEM Assets UI中显示或隐藏`roles`和`position`字段的选项。

  AEM Assets元数据架构表单的![Commerce选项卡](assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* [示例已标记并批准Commerce资源](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg`以支持初始资源同步。 只有已获批准的Commerce资源才能从AEM Assets同步到Adobe Commerce。

>[!NOTE]
>
> 有关&#x200B;**AEM Commerce包代码**&#x200B;的更多信息，请参阅GitHub上的[自述文件](https://github.com/ankumalh/assets-commerce)页面。

## AEM Assets元数据中的本地化替换文本

编辑符合条件的图像时，_[!UICONTROL Alt texts]_多字段在AEM Assets资源元数据编辑器的&#x200B;**[!UICONTROL Commerce]**选项卡上可用。

>[!IMPORTANT]
>
> 每次存储查看行为仅适用于替换文本。 AEM Assets集成不会同步每个Adobe Commerce商店视图中的其他产品图像。 AEM中的产品图像将继续同步到Commerce中，其库分配行为与此版本之前相同。

多字段在每个Commerce商店视图中包含一行。 每一行有两个输入：

* **[!UICONTROL Store View Code]** — 存储视图标识符（例如`default`或`en_US`）。

* **[!UICONTROL Alt Text]** — 该商店视图的替换文本，限制为255个字符。

选择&#x200B;**[!UICONTROL Add]**&#x200B;为其他存储视图添加更多行。 要删除某行，请选择该行上的&#x200B;**[!UICONTROL Delete]**&#x200B;图标以将其删除。

![Alt文本包含存储视图代码和Alt文本输入的多字段](assets/commerce-metadata-alt-texts-multifield.png){width="600" zoomable="yes"}

保存时，如果任何行具有空的&#x200B;_[!UICONTROL Store View Code]_或如果两行使用相同的存储视图代码（不区分大小写），则客户端验证会阻止提交。

替代文本条目作为两个索引对齐的`String[]`属性保留在JCR资产元数据中：

* `commerce:altTextStoreViews`：存储每行的视图代码。
* `commerce:altTextValues`：在与`commerce:altTextStoreViews`中的每个条目相同的索引处匹配替换文本。

当这些资源同步到Adobe Commerce时，每个商店视图替换文本将写入产品媒体集，以获得匹配的商店视图代码。 底层图像映射保持不变。
