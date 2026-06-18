---
source-git-commit: 3d05a7307e58ea2758ac4b6f2b70d24b8ea7a5ac
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---
# 验证优化程序数据同步

确认数据已从Commerce管理员成功导出，并且数据已成功提交到[!DNL Commerce Optimizer]。 从Commerce管理员中的导出开始，然后在[!DNL Commerce Optimizer]中确认交付。

1. **在Commerce管理员中检查同步状态：**

   转到&#x200B;**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**。

   ![带有馈送项状态报告的数据馈送同步状态页面](/help/aco-connector/assets/data-feed-sync-status.png){width="700" zoomable="yes"}

   同步运行时，馈送数据显示已成功发送的记录。 选择信息源以查看详细信息或解决同步问题。

1. **确认数据已传送到[!DNL Commerce Optimizer]：**

   从[!DNL Commerce Optimizer]菜单中选择&#x200B;**[!UICONTROL Data Sync]**。

   Adobe Commerce Optimizer中的![数据同步页面显示同步的目录数据](/help/aco-connector/assets/data-sync.png){width="700" zoomable="yes"}

   验证是否显示预期的产品、价格和属性。

当同步按预期工作时：

- **[!UICONTROL Data Feed Sync Status]**&#x200B;显示连接器馈送的成功发送的记录，没有未解析的项目级错误。
- [!DNL Commerce Optimizer]中的&#x200B;**[!UICONTROL Data Sync]**&#x200B;列出了预期的目录源、产品、价格和属性。

>[!TIP]
>
>如果数据同步有任何问题，请参阅[疑难解答](/help/aco-connector/troubleshooting.md)指南。
