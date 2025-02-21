---
title: 支付报表
description: 使用“付款”报表，可以完全透明地显示付款金额、已处理数量以及财务对帐的交易记录级别的详细报表。
role: User
level: Intermediate
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# 支付报表

[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]为您提供全面的报告，以便您能够清楚地查看存储交易、订单和付款。

有两个可用的付款报告视图，使您能够查看有关所有付款的深入信息：

* **[支付数据可视化视图](#payouts-data-visualization-view)** — 支付服务主页上可用的图表，它以可视化形式显示支付报告视图中的每日汇总金额
* **[付款报表视图](#payouts-report-view)** — 付款中可用的报表，其中显示所有交易记录的详细付款信息

“付款”视图一目了然地显示全面的付款信息，使您可以对付款金额、处理数量以及财务对帐事务处理级别的详细报告实现完全透明。

您可以[以.csv文件格式下载付款交易记录](#download-transactions)，以便在现有的会计或订单管理软件中使用。

>[!NOTE]
>
>付款报表仅显示捕获的订单（付款操作设置为[`Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/production.html#set-payment-services-as-payment-method)），或[标记为`Invoiced`](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice)。

## 支付数据可视化视图

支付数据可视化图表视图在Payment Services主页中可用。 它是详细表格[支付报告视图](#payouts-report-view)中每日汇总金额的可视表示形式。

在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**&#x200B;以查看贷方与借方的数据可视化图表以及随时间变化的移动平均值。

管理员中的![支付数据可视化图表](assets/payouts-report.png){width="800" zoomable="yes"}

单击&#x200B;**[!UICONTROL View Report]**&#x200B;以导航到详细的表格[支付报告视图](#payouts-report-view)。

### 自定义事务时间范围

默认情况下，将显示30天的交易记录。

从“支付数据”可视化视图中，您可以通过选择日期范围来自定义要查看的支付事务处理的时间范围：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**。 支付数据可视化图表视图在“支付”部分中可见。
1. 单击&#x200B;**[!UICONTROL Range]**&#x200B;选择器筛选器。
1. 选择适用的日期范围 — 30天、15天或7天。
1. 查看指定日期的事务信息。

### 交易信息

选定日期范围的交易金额显示在支付数据可视化视图的左侧。 所选日期范围的日期显示在视图底部。 如果特定日期没有付款，则该日期将不会显示。

支付数据可视化视图包含以下信息。

| 数据 | 描述 |
| ------------ | -------------------- |
| [!UICONTROL Transaction amount] | 指定时间范围内交易记录的金额范围；Y轴上的数据（左） |
| 日期范围 | 指定时间范围的日期范围；X轴（底部）上的数据 |
| 来源 | 指定时间范围的付款 |
| 借方 | 指定时间范围内的借项（退款） |
| 均线 | 表示指定时间范围内每个日期的平均派息 |
| 范围净值 | 指定时间范围（范围）的净支付金额 |

## 支付报表视图

付款报表视图在Payment Services的“付款”视图中可用。 它包括有关您商店的付款的所有可用信息。

在&#x200B;_管理员_&#x200B;侧边栏中，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**以查看详细的表格式支付报告视图。

管理员中的![付款交易记录](assets/payouts-report-new.png){width="800" zoomable="yes"}

您可以根据本主题中的部分对此视图进行配置，以便最好地呈现您希望查看的数据。

请参阅链接的Commerce订单和交易ID、交易金额、每笔交易的支付方式等，所有这些都包含在此报表中。

您可以[以.csv文件格式下载付款交易记录](#download-transactions)，以便在现有的会计或订单管理软件中使用。

>[!NOTE]
>
>此表中显示的数据默认使用`TRANS DATE`按降序排序(`DESC`)。 `TRANS DATE`是事务启动的日期和时间。

### 选择数据源

在支付报表视图中，您可以选择要查看其报表结果的数据源 — **[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**。

![数据源选择](assets/datasource.png){width="300" zoomable="yes"}

如果&#x200B;_[!UICONTROL Live]_是选定的数据源，则可以查看生产模式下存储的报表信息。 如果_[!UICONTROL Sandbox]_&#x200B;是选定的数据源，则可以看到在沙盒模式下存储的报表信息。

数据源选择的工作方式如下所示：

* 如果您没有任何处于实时模式的存储，则数据源选择默认为&#x200B;_[!UICONTROL Sandbox]_。
* 如果您在实时模式下具有任何存储（一个或多个存储），则数据源选择将默认为&#x200B;_[!UICONTROL Live]_。
* 报表导出始终遵循数据源选择。

要为订单付款状态报表选择数据源，请执行以下操作：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;**[!UICONTROL Data source]**&#x200B;并选择&#x200B;**[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**。

   报表结果会根据所选数据源重新生成。

### 查看交易记录

默认情况下，将显示30天的交易记录。

搜索中返回的行数，或显示在默认的30天事务处理的行数，显示在付款视图网格的上方，与事务日期日历选择器过滤器一起显示。

向左和向右滚动查看每日报表中每个付款交易](#column-descriptions)的[信息，包括交易日期、参考ID、发票编号和付款方式详细信息。

#### 自定义事务时间范围

在“支付报表”视图中，您可以通过输入特定日期或从日期选择器中选择日期范围，自定义要查看的支付事务处理的时间范围：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;_[!UICONTROL Transaction dates]_日历选择器筛选器。
1. 选择适用的日期范围。
1. 查看网格中指定日期的付款状态。

### 显示和隐藏列

默认情况下，“付款”报表视图会显示大多数可用的信息列。 但是，您可以自定义您在报表中看到的列。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;_列设置_&#x200B;图标（![列设置图标](assets/column-settings.png){width="20" zoomable="yes"}）。
1. 要自定义您在报表中看到的列，请选中或取消选中列表中的列。

   支付报表视图将立即显示您在“列设置”菜单中所做的任何更改。 列首选项将进行保存，如果您离开报表视图，这些首选项将保持有效。

### 下载交易记录

您可以下载一个.csv文件，其中包含在“付款”视图网格中显示的所有事务。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**。
1. [自定义交易的日期范围时间范围](#customize-transactions-timeframe)。
1. 单击&#x200B;_下载_ （![下载图标](assets/icon-download.png){width="20" zoomable="yes"}）图标。

您的付款交易记录将以.csv格式下载。

### 列描述

支付报表包括以下信息。

| 列 | 描述 |
| ------------ | -------------------- |
| [!UICONTROL Provider] | 付款提供商 |
| [!UICONTROL Provider trans] | 交易ID |
| [!UICONTROL Trans date] | 启动交易的日期和时间 |
| [!UICONTROL Type] | 事务类型 — *[!UICONTROL PAYMENT]*，*[!UICONTROL BONUS]*，*[!UICONTROL CHARGEBACK]*，*[!UICONTROL CORRECTION]*，*[!UICONTROL CURRENCY_CONVERSATION]*，*[!UICONTROL DEPOSIT]*，*[!UICONTROL DISBURSEMENT]*，*[!UICONTROL DISPUTE]*，*[!UICONTROL FEES]*，*[!UICONTROL HOLD]*，*[!UICONTROL HOLD_RELEASE]*，*[!UICONTROL INCENTIVES]*，*[!UICONTROL OTHERS]*，*[!UICONTROL RECOUP]*，*[!UICONTROL REFUND]*，*[!UICONTROL REVERSAL]*，*[!UICONTROL WITHDRAWAL]* <br> <br>有关详细信息，请参阅[事务类型](#transaction-types)。 |
| [!UICONTROL Status] | 交易的当前状态 — *[!UICONTROL SUCCESS]*，*[!UICONTROL DENIED]*，*[!UICONTROL PENDING]* |
| [!UICONTROL Code] | 表示贷方(*CR*)或借方(*DR*)的交易代码 |
| [!UICONTROL Reference ID] | 与此事件相关的原始交易ID |
| [!UICONTROL Invoice] | 交易的发票ID（每张订单一个） |
| [!UICONTROL Commerce order] | Commerce订单ID <br> <br>要查看相关的[订单信息](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders)，请单击ID。 |
| [!UICONTROL Commerce trans] | Commerce交易ID |
| [!UICONTROL Pay method] | 信用卡类型 — *[!UICONTROL BANK]*、*[!UICONTROL PAYPAL]*、*[!UICONTROL CREDIT_CARD]* — 和相关联的卡提供商（如&#x200B;*Visa*&#x200B;或&#x200B;*MasterCard*） |
| [!UICONTROL TRANS AMT] | 交易金额 |
| [!UICONTROL CUR] | 交易记录金额的货币单位 |
| [!UICONTROL PENDING] | 尚未支付的金额 |
| [!UICONTROL CUR] | 待定金额的货币单位 |
| [!UICONTROL SELLER AMT] | 向客户转移或从客户转移的资金金额<br> <br>从卖方帐户移出的基金显示一个短划线(-)前缀。 |
| [!UICONTROL CUR] | 卖方金额的货币单位 |
| [!UICONTROL PARTNER FEE] | 与交易<br>关联的合作伙伴费用 <br>从合作伙伴费用帐户移出的基金显示短划线(-)前缀。 |
| [!UICONTROL CUR] | 合作伙伴费用的货币单位 |
| [!UICONTROL PROV FEES] | 与交易记录<br>关联的费用 <br>从提供商费用帐户移出的基金显示短划线(-)前缀。 |
| [!UICONTROL CUR] | 提供商费用的货币单位 |
| [!UICONTROL FEE %] | 收取费用的交易金额的百分比 |
| [!UICONTROL FIXED FEE] | 固定提供商费用金额 |
| [!UICONTROL CHBK FEE] | 与交易记录<br>关联的按存储容量使用计费费用 <br>短划线(-)前缀表示已冲销按存储容量使用计费费用。 |
| [!UICONTROL CUR] | 拖缺费用的货币单位 |
| [!UICONTROL HOLD AMT] | 暂停或解除暂停的金额<br> <br>短划线(-)前缀表示正在释放保留资金。 |
| [!UICONTROL CUR] | 暂挂金额的货币单位 |
| [!UICONTROL RECOUP AMT] | 从补偿帐户<br>中扣除的金额 <br>从回收帐户移出的基金显示短划线(-)前缀。 |
| [!UICONTROL CUR] | 回收金额的货币单位 |

### 交易类型

这些交易类型可以在支付交易中进行记录。

| 报表 | 描述 |
| ------------ | -------------------- |
| [!UICONTROL PAYMENT] | 为订单在买方和卖方之间转移的资金 |
| [!UICONTROL AUTH] | 授权和授权撤消交易记录 |
| [!UICONTROL BONUS] | — |
| [!UICONTROL CHARGEBACK] | 拖缺款项费用和拖缺款项费用冲销交易记录 |
| [!UICONTROL CORRECTION] | — |
| [!UICONTROL CURRENCY_CONVERSION] | — |
| [!UICONTROL DEPOSIT] | — |
| [!UICONTROL DISBURSEMENT] | — |
| [!UICONTROL DISPUTE] | — |
| [!UICONTROL FEES] | 合作伙伴费用、支付费用和费用冲销交易记录 |
| [!UICONTROL HOLD] | — |
| [!UICONTROL HOLD_RELEASE] | — |
| [!UICONTROL INCENTIVES] | — |
| [!UICONTROL OTHERS] | — |
| [!UICONTROL RECOUP] | 从银行或亏损帐户中收回 |
| [!UICONTROL REFUND] | — |
| [!UICONTROL REVERSAL] | — |
| [!UICONTROL WITHDRAWAL] | — |
