---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%
---
# 获取[!DNL Commerce Optimizer]实例详细信息

从[!DNL Commerce Optimizer]实例[[!DNL Instance details] 页面](/help/optimizer/get-started.md#manage-instances)上的&#x200B;_[!DNL Instance Id]_&#x200B;字段或用于访问实例的URL获取_&#x200B;租户ID _。 例如，在`https://experience.adobe.com/#/@<your organization>/in:<tenant>/commerce-optimizer-studio/home`中。

1. 从Commerce Admin中，选择&#x200B;**[!UICONTROL Adobe Commerce Optimizer]**&#x200B;以显示包含说明的配置页面。

   ![[!DNL Commerce Optimizer]配置页面](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. 从命令行中，[使用SSH](https://experienceleague.adobe.com/zh-hans/docs/commerce-on-cloud/user-guide/develop/secure-connections)连接到[!DNL Adobe Commerce]暂存环境。

1. 要配置集成，请运行以下[!DNL Adobe Commerce] CLI命令，将占位符值替换为[!DNL Commerce Optimizer]项目的值：

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. 通过返回Commerce管理员并选择[!UICONTROL Adobe Commerce Optimizer]选项来验证连接。

   选择该选项后，它将在新选项卡中打开[!DNL Commerce Optimizer] UI。
