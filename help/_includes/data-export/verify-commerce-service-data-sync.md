---
source-git-commit: e7d9c056ef8d565b4a143b05ff4e06d607fbfa8e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---
# 验证Commerce服务数据同步

要验证数据同步是否正常工作，请确认已成功从[!DNL Adobe Commerce]导出数据，并且数据已成功传递到连接的Commerce服务。 使用部署中的功能板检查这两个步骤。

从导出开始，然后确认投放。

1. 在Commerce管理员中检查同步状态。

   转到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**。

   ![带有馈送项状态报告的数据馈送同步状态页面](/help/data-export/assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   同步运行时，馈送数据显示已成功发送的记录。 选择信息源以查看详细信息或解决同步问题。

1. 确认数据已传送到“连接的Commerce服务”。

   从Commerce管理员转到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**。

   ![数据管理功能板显示连接的Commerce服务中已同步的目录数据](/help/data-export/assets/data-management-dashboard.png){width="700" zoomable="yes"}

   验证是否显示预期的产品、价格和属性。

>[!TIP]
>
>如果数据同步还有其他问题，请参阅[查看日志和疑难解答](/help/data-export/troubleshooting/logging.md)。

