---
title: 提高SaaS数据导出性能
description: 了解如何使用多线程数据导出模式提高Commerce服务的SaaS数据导出性能。
role: Admin, Developer
exl-id: 7151118c-5e30-44d0-b515-5801a73e44ec
source-git-commit: 9b28da0bf861a266e9d679ba59470f46d9a89c1c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 提高SaaS数据导出性能

**多线程数据导出模式**&#x200B;通过将馈送数据分成批处理并并发处理这些批处理来加速导出过程。

开发人员或系统集成商可以通过使用多线程数据导出模式而不是默认的单线程模式来提高性能。 在单线程模式下，馈送提交过程不会并行化。 此外，由于设置了默认限制，所有客户端只能使用一个线程。 在大多数情况下，不需要自定义配置。

## 使用多线程模式的注意事项

使用数据导出服务时，您希望优化性能，同时确保精确的同步。
Adobe建议使用默认配置进行数据摄取，这通常满足Commerce商家的同步要求。 但是，在某些情况下，自定义可能会加快处理时间。

在决定是否自定义数据导出配置时，请考虑以下关键因素：

- **初始同步** — 评估产品数量，[根据默认配置估计数据量和传输时间](estimate-data-volume-sync-time.md)。 问问自己：您能否在载入Commerce服务后等待此初始数据同步？

- **添加新的商店视图或网站** — 如果您计划在上线后添加具有相同产品数的商店视图或网站，请估计数据量和传输时间。 确定使用默认配置时同步时间是否可接受，或者是否需要多线程处理。

- **常规导入** — 预测常规导入，如价格更新或库存状态更改。 评估这些更新是否可以在一个可接受的时间范围内应用，或者是否需要更快的处理。

- **产品重量** — 考虑您的产品是轻量还是重量。 如果产品说明或属性夸大了产品大小，则相应地调整批次大小。

请记住，周到的规划（包括估计数据量以及同步时间）通常可以消除自定义的需要。 根据这些估计安排信息源摄取操作以实现最佳结果。

>[!NOTE]
>
>Adobe建议在使用多线程处理时务必谨慎。 如果配置多线程以提高性能，则可以触发包含的Adobe Commerce Services护栏，以防止在数据摄取期间误用系统。 这些护栏还限制用户触发可能使系统过载的同步更改。 当触发护栏时，请求被阻止，系统返回429错误。 如果您遇到这些错误，请调整您的配置，并提交支持票证以获得帮助。

## 配置多线程

所有[同步方法](data-synchronization.md#synchronization-process)都支持多线程模式 — 完全同步、部分同步和失败项目同步。 要配置多线程，请指定同步过程中要使用的线程数和批处理大小。

- `thread-count`是激活到进程实体的线程数。 默认`thread-count`为`1`。
- `batch-size`是一个迭代中处理的实体数。 除价格馈送之外，所有馈送的默认`batch-size`是`100`条记录。 对于价格馈送，默认值为`500`条记录。

您可以在运行resync命令时将多线程配置为临时选项，或者通过将多线程配置添加到Adobe Commerce应用程序配置中来配置多线程。

>[!NOTE]
>
>确保将SaaS数据导出的性能与为使用者端客户端定义的速率限制保持一致。

### 在运行时配置多线程

从命令行运行完整同步命令时，通过将`thread-count`和`batch-size`选项添加到CLI命令来指定多线程处理。

```
bin/magento saas:resync --feed=products --thread-count=2 --batch-size=200
```

在命令行中指定的选项会覆盖Adobe Commerce应用程序`config.php`文件中指定的数据导出配置。

### 将多线程添加到Commerce配置

要使用多线程处理所有数据导出操作，系统集成商或开发人员可以在Commerce应用程序配置中修改每个馈送的线程数和批量大小。

可以通过将自定义值添加到配置文件[的](https://experienceleague.adobe.com/zh-hans/docs/commerce-operations/configuration-guide/files/config-reference-configphp#system)系统节`app/etc/config.php`来应用这些更改。

**示例：为产品和价格配置多线程**

```php
<?php
return [
    'system' => [
        'default' => [
            'commerce_data_export' => [
                'feeds' => [
                    'products' => [
                        'batch_size' => 100,
                        'thread_count' => 2,
                    ],
                    'prices' => [
                        'batch_size' => 400,
                        'thread_count' => 4,
                    ]
                ]
            ],
//   ...
```
