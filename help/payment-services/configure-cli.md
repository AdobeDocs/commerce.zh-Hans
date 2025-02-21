---
title: 命令行配置
description: 安装后，可以使用命令行界面(CLI)配置 [!DNL Payment Services] 。
role: Admin, Developer
level: Intermediate
feature: Payments, Checkout, Configuration, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 命令行配置

安装[!DNL Payment Services]后，可以从[在主页](payments-home.md)中或通过命令行界面(CLI)轻松对其进行配置。

## 配置数据导出

[!DNL Payment Services]将从[!DNL Magento Open Source]和[!DNL Adobe Commerce]导出的订单数据与来自付款提供商的汇总付款数据组合在一起，以创建有用的报告。 [!DNL Payment Services]扩展使用索引器高效地收集报告的所有必要数据。

若要了解[!DNL Payment Services]报表中使用的数据，请参阅[订单付款状态报表](order-payment-status.md#data-used-in-the-report)。

### 在[!DNL Magento Open Source]上配置cron

如果要在[!DNL Magento Open Source]上使用`BY SCHEDULE`索引模式，则必须配置cron。 请参阅[配置和运行cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)。

### 设置索引器

使用两种索引模式之一 — `ON SAVE`（默认值）或`BY SCHEDULE`（推荐），在支付服务中导出并保留订单数据。

以下索引用于[!DNL Payment Services]：

| 代码 | 名称 | 描述 |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | 销售订单信息源 | 生成订单数据的索引 |
| `sales_order_status_data_exporter` | 销售订单状态信息源 | 生成销售订单状态数据的索引 |
| `store_data_exporter` | 商店信息源 | 生成存储数据的索引 |

要更改所有三个索引器的索引模式，请运行：

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>如果未在命令中指定任何索引器，则所有索引器都会更新为相同的值。 如果要更改特定索引器，必须在命令中列出该索引器。

要了解有关手动更改索引器模式的更多信息，请参阅开发人员文档中的[配置索引器](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"}。 若要了解如何在管理员中更改它，请参阅核心用户指南中的[索引管理](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"}。

### 手动重新索引数据

您可以手动重新索引数据，而不是等待数据自动生成。 有关详细信息，请参阅[管理索引器](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"}中的[重新索引](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex){target="_blank"}。

当设置`BY SCHEDULE`模式时，系统跟踪更改的实体，并且cron作业会根据设置的计划更新这些实体的索引。 请参阅[配置和运行cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)中的命令行[运行cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run)，了解如何使用cron作业手动触发索引。

### 将重新索引的数据发送到付款服务

数据编制索引后，将自动发送给[!DNL Payment Services]。 您还可以使用此命令手动触发发送索引数据的过程：

```bash
bin/magento saas:resync --feed [feedName]
```

使用以下命令选项：

| 命令 | 描述 |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | 执行指定馈送的重新索引并将其发送到相应的服务 |
| `bin/magento saas:resync --no-reindex` | 跳过索引并发送来自索引的未同步数据 |

`--feed`参数允许您指定要发送的信息源：

| 信息源 | 描述 |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | 生产模式下的订单馈送 |
| `paymentServicesOrdersSandbox` | 沙盒模式下的订单馈送 |
| `paymentServicesOrderStatusesProduction` | 生产模式下的订单状态 |
| `paymentServicesOrderStatusesSandbox` | 沙盒模式中的订单状态 |
| `paymentServicesStoresProduction` | 在生产模式下存储 |
| `paymentServicesStoresSandbox` | 以沙盒模式存储 |

如果配置并安装了cron，则报告所需的所有数据都会自动发送到[!DNL Payment Services]。 您还可以手动触发将cron数据发送到[!DNL Payment Services]的过程。

```bash
bin/magento cron:run --group payment_services_data_export
```

要了解有关重新索引和索引器的更多信息，请参阅开发人员文档中的[管理索引器](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers)主题。

## 配置L2/L3处理

[!DNL Payment Services]可以处理来自卡付款交易的第2级和第3级数据，以便为商家提供其他信息。

>[!WARNING]
>
> 通过PayPal与2级和3级处理集成仅适用于美国商家。 有关详细信息，请参阅PayPal开发人员文档中的[付款处理](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank}。

如果要使用L2/L3处理[!DNL Payment Services]的数据，或者如果您有任何问题，请联系您的[!DNL Payment Services]帐户经理。

要了解[!DNL Payment Services]中使用的L2和L3处理，请参阅[第2级和第3级处理](levels-card-payment-transactions.md)。
