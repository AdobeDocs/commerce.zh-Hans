---
title: 查看日志并排除故障
description: 了解如何使用data-export和saas-export日志排除 [!DNL data export] 错误。
feature: Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# 查看日志并排除故障

[!DNL data export]扩展提供日志以跟踪数据收集和同步过程。

## 日志

日志位于Commerce应用程序服务器上的`var/log`目录中。

| 日志名称 | 文件名 | 描述 |
|-----------------| ----------| -------------|
| SaaS数据导出日志 | `commerce-data-export.log` | 提供有关数据导出活动（如实体事件和完全重新同步触发器）的信息。  每个日志记录都具有特定的结构，并提供有关馈送、操作、状态、占用时间、进程ID和调用者的信息。 |
| SaaS数据导出错误日志 | `data-export-errors.log` | 提供在数据同步过程中发生的错误消息和栈栈跟踪。 |
| SaaS导出日志 | `saas-export.log` | 提供有关发送到Commerce SaaS服务的数据的信息。 |
| SaaS导出错误日志 | `saas-export-errors.log` | 提供有关将数据发送到Commerce SaaS服务时发生的错误的信息。 |

如果您没有看到Adobe Commerce服务的预期数据，请使用数据导出扩展的错误日志来确定出现问题的位置。 此外，您还可以使用其他数据扩展日志，以进行跟踪和故障排除。 请参阅[扩展日志记录](#extended-logging)。

### 日志格式

每个日志记录具有以下结构。

```
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elaspsed from script run>",
   "pid": "<proccess id who executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>基于JSON的字符串经过美化以提高可读性。

下表描述了可在日志中记录的操作类型。

| 操作 | 描述 | 调用方示例 |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 完全同步 | 完全同步会收集给定馈送的所有数据并将这些数据发送到SaaS。 | `bin/magento saas:resync --feed=products` |
| 部分重索引 | 部分同步仅会收集给定馈送中更新的实体的数据并将这些数据发送到SaaS。 仅当存在更新的实体时，此日志才存在。 | `bin/magento cron:run --group=index` |
| 重试失败的项目 | 如果上一个同步操作因Commerce应用程序或服务器错误而失败，则将给定馈送的项目重新发送到SaaS。 仅当存在失败项目时，此日志才存在。 | `bin/magento cron:run --group=saas_data_exporter` (任何“*_data_exporter”cron组) |
| 完全同步（旧版） | 在旧版导出模式下，给定馈送的完全同步。 | `bin/magento saas:resync --feed=categories` |
| 部分重新索引（旧版） | 在旧版导出模式下，为给定的馈送将更新的实体发送到SaaS。 仅当存在更新的实体时，此日志才存在。 | `bin/magento cron:run --group=index` |
| 部分同步（旧版） | 在旧版导出模式下，为给定的馈送将更新的实体发送到SaaS。 仅当存在更新的实体时，此日志才存在。 | `bin/magento cron:run --group=saas_data_exporter` (任何“*_data_exporter”cron组) |


### 日志记录示例

在完全重新同步期间，默认情况下每30秒跟踪并记录一次进度。 以下是示例日志条目。

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

在此示例中，`status`值提供了有关同步操作的信息：

- **`"Progress 2/5"`**&#x200B;表示已完成5次迭代中的2次。 迭代次数取决于导出的图元数。
- **`"processed: 200"`**&#x200B;表示已处理200个项目。
- **`"synced: 100"`**&#x200B;表示已向SaaS发送100个项目。 `"synced"`应不等于`"processed"`。 示例如下：
   - **`"synced" < "processed"`**&#x200B;表示与先前同步的版本相比，信息源表未检测到项中的任何更改。 在同步操作过程中将忽略此类项目。
   - **`"synced" > "processed"`**&#x200B;同一实体ID（例如，`Product ID`）可以在不同的范围中具有多个值。 例如，一个产品可以分配给五个网站。 在这种情况下，您可能具有“1个已处理”项目和“5个已同步”项目。

+++ **示例：价格馈送的完整重新同步日志**

```
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## 使用New Relic查看日志并进行故障排除

如果您将Adobe Commerce日志存储在New Relic中，则可以添加解析规则以提高可读性和查询体验。

1. 登录到New Relic。

1. 转到`Logs => Parsing`。

1. 单击`Create parsing rule`。

1. 通过添加以下值来配置解析规则。

   - **根据NRQL筛选日志**

     `filePath LIKE '%commerce-data-export%.log'`

   - **正在分析规则**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel} %{GREEDYDATA:feed:json}`

此示例添加了一个规则，允许您按特定馈送类型、操作等查询New Relic日志。

**示例查询字符串**—`feed.feed:"products" and feed.status:"Complete"`

## 故障排除

如果Commerce Services中的数据缺失或不正确，请检查日志，以查看在从Adobe Commerce实例同步到Commerce服务平台期间是否出现问题。 如果需要，可使用扩展日志记录将其他信息添加到日志以进行故障排除。

- commerce-data-export-errors.log — 如果在收集阶段发生错误
- saas-export-errors.log — 如果在传输阶段发生错误

如果看到与配置或第三方扩展无关的错误，请提交包含尽可能多信息的[支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket)。

### 解决目录同步问题 {#resolvesync}

触发数据重新同步时，最多可能需要一小时才能更新数据并反映在UI组件中，例如实时搜索和推荐单元。 如果您仍然看到目录与Commerce店面中的数据之间存在差异，或者如果目录同步失败，请参阅以下内容：

#### 数据差异

1. 在搜索结果中显示相关产品的详细视图。
1. 复制JSON输出，并验证内容是否与您在[!DNL Commerce]目录中的内容匹配。
1. 如果内容不匹配，请对目录中的产品进行细微更改，例如添加空格或句点。
1. 等待重新同步或[触发手动重新同步](#resync)。

#### 同步未运行

如果同步未按计划运行或未同步任何内容，请参阅此[知识库](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html)文章。

#### 同步失败

如果目录同步的状态为&#x200B;**失败**，请提交[支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket)。

## 扩展日志记录

有关其他日志信息，您可以使用环境变量通过用于跟踪和疑难解答的其他数据来扩展日志。

`var/log/`目录中有两个日志文件：

- commerce-data-export-errors.log — 如果在收集阶段发生错误
- saas-export-errors.log — 如果在传输阶段发生错误

您可以使用环境变量通过其他数据扩展日志，以进行跟踪和故障排除。

### 检查馈送有效负荷

重新同步馈送时，通过添加`EXPORTER_EXTENDED_LOG=1`环境变量将馈送有效负载包含在SaaS导出日志中。

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

操作完成后，馈送有效负载可在SaaS导出日志(`var/.log/saas-export.log`)中查看。

### 在馈送索引表中保留有效负载

对于Commerce SaaS数据导出扩展(`magento/module-data-exporter`) 103.3.0及更高版本，立即导出馈送在索引表中仅保留最低要求数据。 信息源包括所有目录和库存状态信息源。

不建议在生产环境中保留索引表中的有效负荷数据，但在开发人员环境中可能很有用。 在重新同步馈送时，通过添加`PERSIST_EXPORTED_FEED=1`环境变量在索引中包含馈送有效负载。

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### 运行Profiler以解决性能缓慢的问题

如果特定信息源的重新索引过程耗时过长，请运行Profiler以收集可能对支持团队有用的其他数据。

运行reindex命令时，通过添加`EXPORTER_PROFILER=1`环境变量来运行探查器。

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

Profiler数据按以下格式存储在数据导出日志(`var/log/commerce-data-export.log`)中：

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
