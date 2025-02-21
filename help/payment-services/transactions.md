---
title: 事务报表
description: 使用事务报表可以查看事务授权率和事务趋势。
role: User
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# 事务报表

[!DNL Adobe Commerce]和[!DNL Magento Open Source]的[!DNL Payment Services]为您提供全面的报告，以便您能够清楚地查看存储交易、订单和付款。

![事务报表](assets/transactions-report.png){width="700" zoomable="yes"}

“交易”报表提供了交易授权率和负交易趋势的可见性，因此您可以有效地监控存储设备的运行状况，并提前发现和处理任何交易问题。

有关在店面下单的订单及其付款方式、结果、付款回应代码等，请参阅单个交易记录。

交易报告中提供的信息仅供商家使用。 请勿与客户或其他潜在欺诈者共享此信息。 交易信息可用于绕过安全检查或下单导致拖缺款项。

您可以下载.csv文件格式的“交易”报表，以便在现有的会计或订单管理软件中使用。

>[!NOTE]
>
>如果您尚未为[!DNL Payment Services]载入并激活实时模式[，则无法查看财务报表。](production.md#enable-live-payments)

## 交易报表视图

“事务处理”报表视图在“付款服务”的“事务处理”视图中可用。 它包括有关您商店交易的所有可用信息。

在&#x200B;_管理员_&#x200B;侧边栏中，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**以查看详细的表格化交易报告视图。

![事务报表视图](assets/transactions-report-view.png){width="800" zoomable="yes"}

您可以根据本主题中的部分对此视图进行配置，以便最好地呈现您希望查看的数据。

请参阅链接的Commerce订单和PayPal交易ID、交易金额、每笔交易的支付方式等，所有这些都包含在此报表中。

并非所有支付方式都提供相同的信息粒度。 例如，信用卡交易提供回复、AVS和CCV代码，以及“交易”报表中卡的最后四位；PayPal支付按钮不提供。

您可以[以.csv文件格式下载事务](#download-transactions)，以便在现有的会计或订单管理软件中使用。

>[!WARNING]
>
> 事务报表不包含在[!DNL Payment Services]之外执行的任何捕获。

### 选择数据源

在“事务”报表视图中，您可以选择要查看其报表结果的数据源（**[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**）。

![数据源选择](assets/datasource.png){width="300" zoomable="yes"}

如果&#x200B;_[!UICONTROL Live]_是选定的数据源，则可以查看在生产模式下使用[!DNL Payment Services]的商店的报告信息。 如果_[!UICONTROL Sandbox]_&#x200B;是选定的数据源，则可以查看沙盒模式的报表信息。

数据源选择的工作方式如下所示：

* 如果您没有任何商店在生产模式下使用[!DNL Payment Services]，则数据源选择默认为&#x200B;_[!UICONTROL Sandbox]_。
* 如果您的任何商店（一个或多个商店）在生产模式下使用[!DNL Payment Services]，则数据源选择默认为&#x200B;_[!UICONTROL Live]_。
* 报表导出始终遵循数据源选择。

要为[!UICONTROL Transactions]报表选择数据源：

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;**[!UICONTROL Data source]**&#x200B;并选择&#x200B;**[!UICONTROL Live]**&#x200B;或&#x200B;**[!UICONTROL Sandbox]**。

   报表结果会根据所选数据源重新生成。

### 自定义日期时间范围

从“事务处理”报表视图中，通过选择特定日期可以自定义要查看的事务处理的时间范围。 默认情况下，网格中显示30天的事务处理。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;**[!UICONTROL Transaction dates]**&#x200B;日历选择器筛选器。
1. 选择适用的日期范围。
1. 在网格中查看指定日期的事务。

### 筛选报表信息

从“事务”报表视图中，您可以通过选择筛选条件来筛选要查看的状态结果。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;**[!UICONTROL Filter]**&#x200B;选择器。
1. 切换&#x200B;_[!UICONTROL Transaction Result]_选项以仅查看选定订单交易记录的报表结果。
1. 切换&#x200B;_[!UICONTROL Payment Method]_选项以查看用于交易的付款类型的报告结果。
1. 切换&#x200B;_[!UICONTROL Payment Detail]_选项以查看使用的付款类型的附加信息（如果可用）。
1. 输入&#x200B;_最小订单金额_&#x200B;或&#x200B;_最大订单金额_&#x200B;以查看该订单金额范围内的报表结果。
1. 输入&#x200B;_[!UICONTROL Order ID]_以搜索特定事务。
1. 介绍&#x200B;_[!UICONTROL Card Last Four]_以搜索特定的信用卡或借记卡。
1. 输入&#x200B;_[!UICONTROL Customer ID]_以显示特定客户的所有交易记录。
1. 输入&#x200B;_[!UICONTROL Customer Email]_以筛选该电子邮件的事务。
1. 单击&#x200B;**[!UICONTROL Hide filters]**&#x200B;以隐藏筛选器。

### 显示和隐藏列

默认情况下，“事务处理”报表会显示所有可用的信息列。 但是，您可以自定义您在报表中看到的列。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;**[!UICONTROL Column settings]**&#x200B;图标![列设置图标](assets/column-settings.png){width="20" zoomable="yes"}。
1. 要自定义您在报表中看到的列，请选中或取消选中列表中的列。

   事务报表会立即显示您在“列设置”菜单中所做的任何更改。 列首选项已保存，如果您离开报表视图，这些首选项将保持有效。

### 更新报表数据

事务报表视图显示一个&#x200B;_[!UICONTROL Last updated]_时间戳，该时间戳显示上次更新报表信息的时间。 默认情况下，事务报表数据每三小时自动刷新一次。

您还可以手动强制刷新报表数据以查看最新的报表信息。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**。
1. 单击&#x200B;_刷新_&#x200B;图标（![刷新图标](assets/refresh-button-med.png){width="20" zoomable="yes"}）。

   刷新了事务报表数据，显示了&#x200B;*[!UICONTROL Update complete]*&#x200B;确认，网格中提供了最新信息。

### 下载交易记录

您可以下载一个.csv文件，其中包含事务视图网格中显示的所有事务，无论您查看的是默认的30天事务还是自定义的时间范围。

1. 在&#x200B;_管理员_&#x200B;侧边栏上，转到&#x200B;**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Transactions]**。
1. 如果要查看过去30天以外的时间范围内的事务，请[自定义状态的日期范围时间范围](#customize-dates-timeframe)。
1. 单击&#x200B;_下载_ ![下载图标](assets/icon-download.png){width="20" zoomable="yes"}图标。

您的交易将以.csv格式下载。

### 列描述

事务报表包含以下信息。

| 列 | 描述 |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | Commerce订单ID（仅包含成功交易的值，对于拒绝的交易为空）<br> <br>要查看相关的[订单信息](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"}，请单击ID。 |
| [!UICONTROL PayPal Transaction ID] | 由付款提供商提供的交易ID；仅包含成功交易的值，并包含拒绝交易的短划线。 您可以单击此ID以访问PayPal交易详细信息页面。 |
| [!UICONTROL Customer ID] | 订单的Commerce客户ID<br> <br>有关详细信息，请参阅[客户信息](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/account-create){target="_blank"}主题。 |
| [!UICONTROL Transaction Date] | 交易日期时间戳 |
| [!UICONTROL Payment Method] | 用于交易的付款类型，其中包含有关品牌和卡类型的信息。 有关详细信息，请参阅[卡类型](https://developer.paypal.com/docs/api/orders/v2/#definition-card_type)；适用于Payment Services 1.6.0及更高版本 |
| [!UICONTROL Payment Detail] | 提供有关用于交易的付款类型的附加信息（如果可用）。 |
| [!UICONTROL Card Last Four] | 用于交易记录的信用卡或借记卡的最后四位数字 |
| [!UICONTROL Result] | 交易的结果 — *[!UICONTROL OK]* （成功交易），*[!UICONTROL Rejected by Payment Provider]* （由PayPal拒绝），*[!UICONTROL Rejected by Bank]* （由签发卡的银行拒绝） |
| [!UICONTROL Response Code] | 提供来自付款提供商或银行的拒绝原因的错误代码；请参阅[`Rejected by Bank`状态](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response)和[`Rejected by Payment Provider`状态](https://developer.paypal.com/api/rest/reference/orders/v2/errors/)的可能响应代码列表和描述。 |
| [!UICONTROL AVS Code] | 地址验证服务代码；付款请求的处理器响应信息。 有关详细信息，请参阅[可能的代码和说明列表](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response)。 |
| [!UICONTROL CVV Code] | 信用卡和借记卡的卡验证值代码；有关详细信息，请参阅[可能的代码和说明列表](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response)。 |
| [!UICONTROL Amount] | 交易记录的订单金额 |
| [!UICONTROL Currency] | 交易记录中用于订单的货币 |
| [!UICONTROL Type] | [交易的`Authorize`或`Authorize and Capture`付款操作](../payment-services/production.md#set-payment-services-as-payment-method) |

### 错误响应代码

_响应代码_&#x200B;列显示与事务相关的特定错误或成功代码。 您可能会看到的一些常见错误代码包括：

* `PAYMENT_DENIED` — PayPal已拒绝交易，因为它涉嫌欺诈。
* `INTERNAL_SERVER_ERROR` — 交易被PayPal拒绝并发生PayPal服务器错误。 可以重试事务。
* `INSTRUMENT_DECLINED`—PayPal根据所选的付款方式拒绝了客户。 可以使用其他支付方式重试交易。
* `9500` — 关联银行拒绝了该交易，因为它涉嫌欺诈。
* `5120` — 关联银行拒绝了交易记录，因为客户没有足够的资金进行付款。
* `5650` — 关联银行拒绝了交易记录，因为该银行要求强大的客户身份验证([3DS](security.md#3ds))。

失败交易的详细错误响应代码可用于2023年6月1日以后的交易。 对于2023年6月1日之前发生的交易，将显示部分报表数据。
