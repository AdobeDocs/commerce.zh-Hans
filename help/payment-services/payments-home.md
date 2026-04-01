---
title: 主页
description: 使用管理员中的 [!DNL Payment Services] 主页来载入（包括ACCS）、打开交易报告、管理PaaS上的订单和付款入口点，以及访问“学习”、“帮助”和“设置”。
role: Admin, User
level: Intermediate
exl-id: d7a4c87f-33cb-446a-b442-3cdf05b518a2
feature: Payments, Checkout, Paas, Saas
source-git-commit: e4aede88f8470f79e5987afcb7311bf6ef44c16e
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# [!DNL Payment Services]主页

适用于Adobe Commerce和Magento Open Source的[!DNL Payment Services]提供了“主页”视图，其中包含设置和使用扩展所需的信息。 主页顶部的选项取决于您的部署：云上的Adobe Commerce或内部部署(PaaS)、[!DNL Adobe Commerce as a Cloud Service]或[!DNL Adobe Commerce Optimizer] (SaaS)。

在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**：

>[!BEGINTABS]

>[!TAB 云和内部部署上的 Adobe Commerce]

![主页视图](assets/home-view.png){width="700" zoomable="yes"}

>[!TAB Adobe Commerce as a Cloud Service和Commerce Optimizer]

在您完成入门之前，**[!UICONTROL Home]**&#x200B;将显示&#x200B;**[!UICONTROL ACCS Onboarding Required]**。 该通知链接到[设置沙盒服务](sandbox.md#enable-sandbox-testing)（使用测试PayPal处理帐户）或[启用实时付款](production.md#enable-live-payments)（如果您已在其他环境中测试）：

![Payment Services主页需要ACCS载入](assets/payment-services-home-accs-onboarding.png){width="700" zoomable="yes"}

载入完成后（或在已配置的实例上），**[!UICONTROL Home]**&#x200B;为表格报告显示&#x200B;**[!UICONTROL Transactions]**&#x200B;和&#x200B;**[!UICONTROL View Report]**，以及&#x200B;**[!UICONTROL Learn]**&#x200B;和&#x200B;**[!UICONTROL Help]**&#x200B;区域：

![SaaS上的付款服务主页](assets/payment-services-home-saas.png){width="700" zoomable="yes"}

>[!ENDTABS]

在此主页视图中，您可以访问&#x200B;_主页_、_了解_&#x200B;有关[!DNL Payment Services]的信息、配置扩展&#x200B;_设置_&#x200B;或获取&#x200B;_帮助_。 使用&#x200B;**[!UICONTROL View Report]** (SaaS)或&#x200B;**[!UICONTROL Orders]**&#x200B;和&#x200B;**[!UICONTROL Payouts]**&#x200B;入口点（云端和内部部署上的Adobe Commerce）打开报告；请参阅[报告](reporting.md)。

## 主页

仅[!BADGE PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于云项目（Adobe管理的PaaS基础架构）和内部部署项目上的Adobe Commerce 。"}

| 字段 | 描述 |
|---|---|
| [!UICONTROL Orders] | 这些报表允许您快速查看订单的付款状态并识别任何潜在问题。 |
| [!UICONTROL Payouts] | “付款”报表一目了然地显示全面的付款信息，使您可以对付款金额、处理数量以及财务对帐事务处理级别的详细报告实现完全透明。 |

仅[!BADGE SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"}

| 字段 | 描述 |
|---|---|
| [!UICONTROL Transactions] | 汇总了“事务处理”报表，这有助于您了解特定事务处理的结果。 单击&#x200B;**[!UICONTROL View Report]**&#x200B;以打开交易网格（例如，订单和PayPal交易ID、付款方式、结果和响应代码）。 查看[事务报表视图](reporting.md#transactions-report-view)。 |

## 学习

| 字段 | 描述 |
|---|---|
| [!UICONTROL Read documentation] | 查看[!DNL Payment Services]的最新用户和开发人员文档。 |
| [!UICONTROL How to onboard] | 找到设置所需的一切并开始使用[!DNL Payment Services]功能。 |
| [!UICONTROL Understand financial reports] | 对[!DNL Payment Services]中现金流管理报告的深入说明。 |

## 帮助

| 字段 | 描述 |
|---|---|
| [!UICONTROL Visit help center] | [!DNL Adobe Commerce]帮助中心有有关[!DNL Payment Services]的知识库文章。 |
| [!UICONTROL Get support] | 访问[!DNL Adobe Commerce]支持门户以获取[!DNL Payment Services]的帮助。 |

## 设置

在“主页”视图中，单击&#x200B;**[!UICONTROL Settings]**。 有关详细信息，请参阅[[!DNL Payment Services] 配置](configure-admin.md)。

付款服务区域的页脚将显示&#x200B;**付款服务**&#x200B;和&#x200B;**付款服务仪表板**&#x200B;版本标签 — 例如，当您收集支持详细信息时。
