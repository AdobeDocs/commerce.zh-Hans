---
title: 将媒体文件迁移到AEM
description: 将媒体文件从Adobe Commerce或外部源迁移到AEM Assets DAM。
feature: CMS, Media, Integration
exl-id: ccb13e90-8b18-4f1e-94ce-f0dacea2f617
source-git-commit: ac880333814d9d9a45e658e2a637cd9634dbfb1f
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 将媒体文件迁移到AEM Assets DAM

Adobe Commerce和Adobe Experience Manager (AEM)均提供内置功能，以简化从Commerce到AEM Assets **数字资产管理系统(DAM)**&#x200B;的媒体文件迁移。 您还可以从其他源迁移介质文件。

## 先决条件

| 类别 | 要求 |
|----------|-------------|
| **系统要求** | <ul><li>使用AEM Assets配置的AEM as a Cloud Service环境</li><li>足够的存储容量</li><li>用于大型文件传输的网络带宽</li></ul> |
| **所需的访问和权限** | <ul><li>AEM Assets as a Cloud Service的管理员访问权限</li><li>访问存储介质文件的源系统(Adobe Commerce或外部系统)</li><li>访问云存储服务的适当权限</li></ul> |
| **云存储帐户** | <ul><li>AWS S3或Azure Blob Storage帐户</li><li>专用容器/存储段配置</li><li>身份验证凭据</li></ul> |
| **Source内容** | <ul><li>准备好迁移的有组织的媒体文件</li><li>AEM Assets<a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/file-format-support#image-formats">支持的</a>格式的图像和视频文件。</li><li>干净的重复资源</li></li> |
| **元数据准备** | <ul><li>为AEM Assets资源配置的<a href="https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/content-design/aem-asset-management/getting-started/aem-assets-configure-aem">Commerce元数据配置文件</a></li><li>每个资源的映射元数据值</li><li>CSV文件编辑器(例如Microsoft Excel)</li></ul> |

## 迁移最佳实践

1. 在迁移之前，通过删除未使用和重复的内容来策划资源。

1. 按大小、格式或用例以逻辑方式组织资源。

1. 考虑将大型迁移分解为较小的批次。

1. 在非高峰时间安排资源密集型导入。

1. 在完全导入之前验证元数据映射。

## 迁移工作流

按照迁移工作流从Adobe Commerce或其他外部系统导出媒体文件，并将它们导入AEM Assets DAM。

### 步骤1：从现有数据源导出内容

仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"}

对于Adobe Commerce商家，**远程存储模块**&#x200B;可以促进媒体文件的导入和导出。 本模块允许企业使用AWS S3等远程存储服务存储和管理媒体文件。 要为Commerce实例设置远程存储，请参阅[Commerce配置指南](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/configuration-guide/storage/remote-storage/remote-storage-aws-s3)中的&#x200B;**配置远程存储**。

如果您的媒体文件存储在Adobe Commerce外部，请将其直接上传到AEM as a Cloud Service支持的[数据源](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/assets-view/bulk-import-assets-view#prerequisites)之一。

### 步骤2：构建用于元数据映射的CSV文件

创建一个CSV文件，将每个媒体文件映射到其Commerce产品数据。 选择以下方法之一：

* **Adobe Commerce (PaaS)**：使用CLI命令从目录自动生成CSV
* 手动创建CSV文件

#### 使用CLI导出元数据

仅[!BADGE PaaS]{type=Informative tooltip="仅适用于云项目上的Adobe Commerce(Adobe管理的PaaS基础架构)。"}

使用AEM Assets集成CLI命令可从存储在Commerce项目中的产品媒体文件中自动生成包含图像URL、职位和角色的元数据CSV文件。

1. 列出用于验证是否已安装AEM Assets集成模块的可用命令：

   ```bash
   bin/magento list aem
   ```

   自定义扩展命令显示在命令列表开头的`aem`下。

1. 运行带有AEM路径前缀的元数据导出命令：

   ```bash
   bin/magento aem:assets:export:csv <AEM-path-prefix>
   ```

   `<AEM-path-prefix>`是将资源存储在AEM Assets DAM中的基本文件夹路径（例如，`/content/dam/commerce/`）。

   ```bash
   bin/magento aem:assets:export:csv /content/dam/commerce/
   ```

   这会在`metadata.csv`目录中创建一个`var/export`文件，其中包含您的Commerce目录中每个产品资源的图像URL、职位和角色。

#### 手动创建CSV

对于存储在Adobe Commerce外部的媒体文件，请手动创建CSV文件。 列标题&#x200B;**必须与**&#x200B;在[AEM Assets元数据配置文件](configure-aem.md)中配置的字段名称匹配。 创建文件后，使用每个媒体文件的元数据值填充行。

| 元数据 | 描述 | 值 |
|-------|-------------|--------|
| 资产路径 | 资产存储在AEM Assets存储库中的完整路径。<br><br>使用路径创建子文件夹以整理Commerce资源，例如`content/dam/commerce/<brand>/<type>`。 | `/content/dam/commerce/<sub-folder>/..<filename>` |
| commerce:positions | 资产在产品库中的位置/顺序 | 多个用竖线分隔的数值（“数字：多个”） |
| commerce:isCommerce | 指示资产是否用于商业的标记 | `Yes` |
| commerce:skus | 与此资产关联的产品SKU | 用竖线分隔的多个字符串值（字符串：多个） |
| commerce:roles | 资产的角色或图像类型（例如，`thumbnail`、`main image`、`swatch`） | 多个值以分号分隔（例如，“thumbnail； image； swatch_image； small_image”） |

+++CSV代码

使用此示例CSV代码在代码编辑器或电子表格应用程序(如Microsoft Excel)中创建文件。

```csv
assetPath,commerce:positions{{Number: multi}},commerce:isCommerce{{String}},commerce:skus{{String: multi}},commerce:roles{{String: multi}}
/content/dam/commerce/sample1.jpg,1,Yes,sku1,thumbnail; image; swatch_image; small_image
/content/dam/commerce/sample2.jpg,1|1|1,Yes,sku1|sku2|sku3,thumbnail; image; swatch_image; small_image|image|image; small_change
```

+++

### 步骤3：将Assets批量导入AEM Assets

创建元数据映射文件后，请使用AEM Assets批量导入工具来导入您的资源。

以下是使用该工具的高级概述。

1. [登录到您的AEM Assets as a Cloud Service创作环境](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/onboarding/journey/aem-users#login-aem)。

1. 从“Experience Manager工具”视图中，选择&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**。

   ![AEM Assets创作](../assets/aem-assets-bulk-import-selection.png){width="600" zoomable="yes"}

1. 在批量导入配置中，选择&#x200B;**[!UICONTROL Create]**&#x200B;以打开配置表单。

   ![AEM Assets创作](../assets/aem-assets-bulk-import-configuration.png){width="600" zoomable="yes"}

1. 设置并保存配置。

   您将需要：

   * 数据源的身份验证凭据
   * AEM Assets中将存储导入文件的目标文件夹
   * 可选。 有关MIME类型、文件大小和其他参数的信息，以自定义导入配置
   * 您上传到云存储实例的元数据映射CSV文件的路径。

   有关详细步骤，请参阅[AEM Assets as a Cloud Service用户指南](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/manage/add-assets#configure-bulk-ingestor-tool)中的&#x200B;*配置批量导入工具*。

1. 保存配置后，使用批量导入工具测试和运行导入操作。

>[!MORELIKETHIS]
>
> [批量导入工具视频演示](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/manage/add-assets#asset-bulk-ingestor)
> [提示、最佳实践和限制](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/manage/add-assets#tips-limitations)
> [使用API上载或引入资源](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis#asset-upload)
