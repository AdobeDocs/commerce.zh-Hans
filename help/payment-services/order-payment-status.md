---
title: 订单付款状态报表
description: 使用“订单付款状态”报表可以查看订单的付款状态，并确定任何潜在问题。
role: User
level: Intermediate
exl-id: 192e47b9-d52b-4dcf-a720-38459156fda4
feature: Payments, Checkout, Orders, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 0%

---

# 订单付款状态报表

[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]为您提供综合报告，以便您能够清楚地查看存储的[交易](reporting.md)、订单和付款。

有两个可用的“订单付款状态”报告视图，使您可以快速查看订单的付款状态：

* **[订单付款状态可视化视图](#order-payment-status-data-visualization-view)** — 付款服务主页上的可用图表，该图表以可视化形式显示订单付款状态报表视图中的每日汇总付款状态
* **[订单付款状态报表视图](#order-payment-status-report-view)** — 以订单付款状态显示所有交易记录的详细付款、已开票、已发运、退款和争议状态的可用报表

订单付款状态视图帮助您轻松了解特定订单在订单到现金流程中的位置。 这些报告允许您根据订单的付款状态和付款日期快速查看订单，并识别任何潜在问题。

您可以以.csv文件格式[下载订单付款状态](#download-order-payment-statuses)，以便在现有的会计或订单管理软件中使用。

>[!NOTE]
>
>如果您尚未为[!DNL Payment Services]载入并激活实时模式[，则无法查看财务报表。](production.md#enable-live-payments)

## 订单支付状态数据可视化视图

可在Payment Services主页中找到订单付款状态数据可视化视图。 它是详细表格[订单付款状态报告视图](#order-payment-status-report-view)中每日汇总付款状态的可视表示形式。

在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**销售** > **付款服务** > _订单_&#x200B;以查看数据可视化[付款状态图表](#statuses-information)。

管理员中的![支付数据可视化图表](assets/orderpayment-dataviz.png){width="800" zoomable="yes"}

单击&#x200B;**[!UICONTROL View Report]**&#x200B;以导航到详细的表格[订单付款状态报告视图](#order-payment-status-report-view)。

### 自定义状态时间范围

默认情况下，将显示30天的付款状态。

从“订单付款状态”可视化图表视图中，您可以通过选择日期范围来自定义要查看的付款状态的时间范围：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。 订单付款状态数据可视化图表视图在&#x200B;_订单_&#x200B;部分中可见。
1. 单击&#x200B;**[!UICONTROL Range]**&#x200B;选择器筛选器。
1. 选择适用的日期范围 — 30天、15天或7天。
1. 查看指定日期的状态信息。

### 状态信息

选定日期范围的付款状态显示在“订单付款状态”数据可视化视图的左侧。 所选日期范围的日期显示在视图底部。 如果特定日期没有订单，则该日期不会显示。

订单支付状态数据可视化视图包含以下信息。

| 数据 | 描述 |
| ------------ | -------------------- |
| [!UICONTROL Orders] | 指定时间范围内的订单金额范围；Y轴上的数据（左） |
| 日期范围 | 指定时间范围的日期范围；X轴（底部）上的数据 |
| 已授权 | 订单已授权 |
| 已请求捕获 | 订单捕获请求 |
| 捕获已确认 | 订单捕获已完成 |
| 部分捕获 | 部分捕获的订单 |
| 捕获失败 | 订单捕获失败 |
| 已失效 | 订单已失效 |

## 订单付款状态报表视图

在Payment Services的“主页”视图中可以使用“订单付款状态”报表视图。 它包括所有交易的详细状态 — 付款、已开票、已发运、退款、争议等。

在&#x200B;_管理员_&#x200B;侧边栏中，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**&#x200B;以查看详细的表格形式订单付款状态报告视图。

![管理员中的订单付款状态交易记录](assets/orders-report-data.png){width="800" zoomable="yes"}

您可以根据本主题中的部分对此视图进行配置，以便最好地呈现您希望查看的数据。

您可以[以.csv文件格式下载付款交易记录](#download-order-payment-statuses)，以便在现有的会计或订单管理软件中使用。

>[!NOTE]
>
>此表中显示的数据默认使用`TRANS DATE`按降序排序(`DESC`)。 `TRANS DATE`是事务启动的日期和时间。

### 付款状态更新

某些支付方式需要一段时间才能获取付款。 [!DNL Payment Services]现在通过以下方式检测订单中付款交易的待处理状态：

* 同步检测`pending capture`事务
* 异步监视`pending capture`事务

>[!NOTE]
>
>如果尚未收到付款，则检测订单中付款交易记录的待定状态可以防止意外发运订单。 电子支票和PayPal交易可能会发生这种情况。

#### 同步检测挂起捕获事务

自动检测处于`Pending`状态的捕获事务，并在检测到此类事务时阻止订单输入`Processing`状态。

在客户结账期间或管理员为以前授权的付款创建发票时，[!DNL Payment Services]自动检测处于`Pending`状态的捕获交易记录，并将相应的订单转移到`Payment Review`状态。

#### 异步监视挂起的捕获事务

检测挂起捕获事务何时进入`Completed`状态，以便商家可以继续处理受影响的订单。

为确保此流程按预期运行，商家必须配置新的cron作业。 一旦作业配置为自动运行，就不需要商家进行其他干预。

请参阅[配置cron作业](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html)。 配置完毕后，新作业每30分钟运行一次，以获取处于`Payment Review`状态的订单的更新。

商家可以通过“订单付款状态”报表视图检查更新的付款状态。

### 报表中使用的数据

[!DNL Payment Services]使用订单数据，并将其与其他来源（包括PayPal）的汇总付款数据相结合，以提供有意义且非常有用的报告。

订单数据将导出并保留在支付服务中。 当您[更改或添加订单状态](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-status#custom-order-status)或[编辑商店视图](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-views#edit-a-store-view)、[商店](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/store-details#store-information)或网站名称时，该数据将与付款数据相结合，并且订单付款状态报表将填充该组合信息。

此过程包括两个步骤：

1. 索引更改了数据`ON SAVE` （每次更改订单信息或存储信息时）或`BY SCHEDULE` （在预配置的cron计划上），具体取决于它在管理员的[索引管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management)中的配置方式。

   默认情况下，数据索引发生`ON SAVE`，这意味着每当订单、订单状态、商店视图、商店或网站中的某些内容发生更改时，索引过程都会立即发生。

1. 系统会将索引数据发送到付款服务，然后付款服务将填充到订单付款状态报表中。

为报告目的而导出和整理的唯一数据是“订单付款状态”报表使用的数据。

>[!NOTE]
>
>此表中显示的数据默认使用`ORDER DATE`按降序排序(`DESC`)。 `ORDER DATE`是创建订单的日期时间戳。

#### 配置数据导出

即使默认情况下在`ON SAVE`模式下进行重新索引，仍建议您在`BY SCHEDULE`模式下进行索引。 `BY SCHEDULE`索引按一分钟的cron计划运行，任何更改的数据会在任何数据更改后的两分钟内显示在订单状态报表中。 此计划的重新索引可帮助您减少存储空间上的任何压力，尤其是在您有大量传入订单的情况下，因为它按计划进行（而不是在每次下订单时）。

您可以在管理员[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode)中更改索引模式 — `ON SAVE`或`BY SCHEDULE`—。

要了解如何配置数据导出，请参阅[命令行配置](configure-cli.md#configure-data-export)。

### 选择数据源

在“订单付款状态”报表视图中，您可以选择要查看其报表结果的数据源（**[!UICONTROL Live]** _或&#x200B;**[!UICONTROL Sandbox]**）。

![数据源选择](assets/datasource.png){width="300" zoomable="yes"}

如果&#x200B;_[!UICONTROL Live]_&#x200B;是选定的数据源，则可以查看在生产模式下使用[!DNL Payment Services]的商店的报告信息。 如果&#x200B;_[!UICONTROL Sandbox]_&#x200B;是选定的数据源，则可以查看沙盒模式的报表信息。

数据源选择的工作方式如下所示：

* 如果您没有任何商店在实时模式下使用[!DNL Payment Services]，则数据源选择默认为&#x200B;_[!UICONTROL Sandbox]_。
* 如果您的任何商店（一个或多个商店）在实时模式下使用[!DNL Payment Services]，则数据源选择默认为&#x200B;_[!UICONTROL Live]_。
* 报表导出始终遵循数据源选择。

要为[!UICONTROL Order Payment Status]报表选择数据源：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Orders]** > **[!UICONTROL View Report]**。
1. 单击&#x200B;_[!UICONTROL Data source]_&#x200B;选择器筛选器并选择&#x200B;**[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**。

   报表结果会根据所选数据源重新生成。

### 自定义订单日期时间范围

从“订单付款状态”报表视图中，您可以通过选择特定日期，自定义要查看的状态结果的时间范围。 默认情况下，网格中显示30天的订单付款状态。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;_[!UICONTROL Order dates]_&#x200B;日历选择器筛选器。
1. 选择适用的日期范围。
1. 在网格中查看指定日期的订单付款状态。

### 筛选报表信息

从“订单付款状态”报表视图中，您可以通过选择筛选条件来筛选要查看的状态结果。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;**[!UICONTROL Filter]**&#x200B;选择器。
1. 切换&#x200B;_支付状态_&#x200B;选项，以便仅查看选定订单支付状态的报表结果。
1. 通过输入&#x200B;_[!UICONTROL Min Order Amount]_&#x200B;或_[!UICONTROL Max Order Amount_]查看订单金额范围内的报表结果。
1. 单击&#x200B;**[!UICONTROL Hide filters]**&#x200B;以隐藏筛选器。

### 显示和隐藏列

默认情况下，“订单付款状态”报表会显示所有可用的信息列。 但是，您可以自定义您在报表中看到的列。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;_列设置_&#x200B;图标（![列设置图标](assets/column-settings.png){width="20" zoomable="yes"}）。
1. 要自定义您在报表中看到的列，请选中或取消选中列表中的列。

   “订单付款状态”报表会立即显示您在“列设置”菜单中所做的任何更改。 列首选项已保存，如果您离开报表视图，这些首选项将保持有效。

### 查看状态

“订单付款状态”报表视图显示每个订单的综合付款状态信息。

默认情况下，网格中显示30天的订单付款状态。

向左和向右滚动以查看[订单付款状态信息](#column-descriptions)，包括订单日期、授权日期、开票、已发货、付款状态等。

在搜索中返回的行数，或默认显示的30天订单付款状态的行数，显示在“订单付款”状态视图网格的上方，与“订单日期”日历选择器过滤器一起显示。

#### 付款状态

“支付状态”列显示任何付款的当前状态。 `Capture failed`付款显示红色警报状态，`Voided`付款显示灰色警报状态。

#### 退款状态

退款状态列显示任何退款的当前状态。 `Capture failed`付款显示红色警报状态，`Voided`付款显示灰色警报状态。

### 更新报表数据

订单付款状态报表视图显示&#x200B;_[!UICONTROL Last updated]_&#x200B;时间戳，该时间戳显示上次更新报表信息的时间。 默认情况下，订单付款状态报表数据每三小时自动刷新一次。

您也可以手动强制刷新订单付款状态报表数据，以查看最新的报表信息。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;_刷新_&#x200B;图标（![刷新图标](assets/refresh-button-med.png){width="20" zoomable="yes"}）。

   订单付款状态报表数据已刷新，将显示&#x200B;*[!UICONTROL Update complete]*&#x200B;确认，并且网格中存在最新信息。

### 查看争议

您可以在订单付款状态报表中查看商店订单上的任何争议，然后定位至PayPal解决中心对其执行操作。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 导航到&#x200B;**[!UICONTROL Disputes column]**。
1. 查看特定订单的任何争议并查看[争议状态](#order-payment-status-information)。
1. 通过单击以&#x200B;_PP-D-_&#x200B;开头的争议ID链接，从[PayPal解决中心](https://www.paypal.com/us/cshelp/article/what-is-the-resolution-center-help246)查看争议详细信息。
1. 根据需要，对争议采取适当行动。

   要按状态对订单争议进行排序，请单击[!UICONTROL Disputes]列标题。

### 下载订单付款状态

您可以下载.csv文件，该文件的所有状态均显示在“订单付款”状态视图网格中，无论您查看的是默认的30天状态还是自定义的时间范围。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**。
1. 如果要查看过去30天以外的时间范围的状态，请[自定义状态的日期范围时间范围](#customize-dates-timeframe)。
1. 单击&#x200B;_下载_ （![下载图标](assets/icon-download.png){width="20" zoomable="yes"}）图标。

您的订单付款状态将以.csv格式下载。

### 列描述

订单付款状态报表包括以下信息。

| 列 | 描述 |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | Commerce订单ID<br> <br>要查看相关的[订单信息](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"}，请单击ID。 |
| [!UICONTROL Order Date] | 订单日期时间戳 |
| [!UICONTROL Authorized Date] | 付款授权的日期时间戳 |
| [!UICONTROL Order Status] | 当前Commerce [订单状态](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-status){target="_blank"} |
| [!UICONTROL Invoiced] | 订单的发票状态 — *[!UICONTROL No]*、*[!UICONTROL Partial]*&#x200B;或&#x200B;*[!UICONTROL Yes]* |
| [!UICONTROL Shipped] | 订单的配送状态 — *[!UICONTROL No]*、*[!UICONTROL Partial]*&#x200B;或&#x200B;*[!UICONTROL Yes]* |
| [!UICONTROL Order Amt] | 订单的总金额 |
| [!UICONTROL Cur] | 订单的货币类型 |
| [!UICONTROL Pay Status] | 特定订单的付款状态 |
| [!UICONTROL Paid Amt] | 订单已付金额 |
| [!UICONTROL Cur] | 订单上已付金额的货币类型 |
| [!UICONTROL Refund Status] | 订单上的退款状态（如退货、RMA和贷项通知单中的信息） —    *[!UICONTROL Requires refund]*、*[!UICONTROL Refund requested]*、*[!UICONTROL Refunded]*、*[!UICONTROL Refund failed]*&#x200B;或&#x200B;*[!UICONTROL Voided]* |
| [!UICONTROL Refund Amount] | 订单的已退款总额 |
| [!UICONTROL Cur] | 订单退款金额的币种类型 |
| [!UICONTROL Disputes] | 订单上任何争议的状态（来自争议和拖缺款项的信息） — *[!UICONTROL Open]*、*[!UICONTROL Waiting for buyer response]*、*[!UICONTROL Waiting for seller response]*、*[!UICONTROL Under review]*、*[!UICONTROL Resolved]*&#x200B;或&#x200B;*[!UICONTROL Other]* |
| [!UICONTROL Payment Method] | 订单的Commerce交易中使用的付款方法 |
| [!UICONTROL Website] | 从中下达订单的网站 |
| [!UICONTROL Store] | 下订单的商店 |
| [!UICONTROL Store View] | 从中下达订单的存储区视图 |
