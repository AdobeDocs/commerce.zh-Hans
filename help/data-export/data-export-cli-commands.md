---
title: 使用Commerce CLI同步馈送
description: 了解如何使用命令行界面命令来管理Adobe Commerce SaaS服务的 [!DNL data export extension] 的馈送和进程。
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 0f1d55f81cb030d218f0aa8dfa2af4dfd8f640c1
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# 使用Commerce CLI同步馈送

`saas:resync`程序包中的`magento/saas-export`命令允许您管理Adobe Commerce SaaS服务的数据同步。

Adobe不建议定期使用`saas:resync`命令。 使用该命令的典型情况包括：

- 初始同步
- 更改[SaaS数据空间ID](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/config/services/saas)后，将数据同步到新数据空间
- 故障排除

监视`var/log/saas-export.log`文件中的同步操作。

## 初始同步

>[!NOTE]
>
>启用实时搜索或产品推荐后，初始同步会自动运行。 不需要手动命令。

当从命令行触发`saas:resync`时，根据目录大小，数据更新可能需要几分钟到几小时的时间。

对于初始同步，Adobe建议按以下顺序运行命令：

```shell
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

## 使用CLI命令同步

`saas:resync`命令支持各种同步操作：

- 按SKU进行部分同步
- 恢复中断的同步
- 在不同步的情况下验证数据

查看所有可用选项：

```shell
bin/magento saas:resync --help
```

有关选项说明和示例，请参阅以下部分。


>[!NOTE]
>
>有关管理导出处理的高级选项，请参阅[自定义导出处理](customize-export-processing.md)。

## `--by-ids`

按其ID部分重新同步特定实体。 支持`products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`和`categoryPermissions`信息源。

默认情况下，在使用`--by-ids`选项时，您会使用产品SKU值指定值。 要使用产品ID，请添加`--id-type=ProductID`选项。

**示例：**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

在重新索引并将数据发送到SaaS之前，请清理馈送索引器表。 仅支持`products`、`productAttributes`、`productOverrides`、`inventoryStockStatus`、`prices`、`variants`和`categoryPermissions`。

如果与`--dry-run`选项一起使用，则该操作将对所有项目执行试运行重新同步操作。

>[!IMPORTANT]
>
>仅在环境清理后或通过`--dry-run`选项使用。 如果用于其他情况，清理操作可能会导致数据丢失和数据同步问题。

**示例：**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

恢复中断的重新同步操作。 仅支持`products`、`productAttributes`和`productOverrides`馈送。

**示例：**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

在不将馈送提交到SaaS且不保存到馈送表的情况下，运行馈送重新索引过程。 此选项对于识别数据集的任何问题很有用。

添加`EXPORTER_EXTENDED_LOG=1`环境变量以将有效负载保存到`var/log/saas-export.log`。

**示例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### 测试特定信息源项目

通过将`--by-ids`选项与扩展日志集合一起添加来测试特定馈送项目，以查看`var/log/saas-export.log`文件中生成的有效负载。

**示例：**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### 测试所有馈送项目

默认情况下，在`resync --dry-run`操作期间提交的信息源仅包含新项目，或以前无法导出的项目。 要在要处理的信息源中包含所有项，请使用`--cleanup-feed`选项。

**示例**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--feed`

必需。 指定要重新同步的馈送实体。

可用信息源：

- `categories`
- `categoryPermissions`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

>[!NOTE]
>
>根据您的Adobe Commerce环境中安装的模块，您环境中可用的信息源可能会有所不同。

**示例：**

```shell
bin/magento saas:resync --feed products
```

## `--no-reindex`

将现有目录数据重新提交到[!DNL Commerce Services]而不重新编制索引。 与产品相关的信息源不支持。

行为因[导出模式](data-synchronization.md#synchronization-modes)而异：

- 旧版模式：重新提交所有数据而不截断。
- 立即模式：忽略选项，仅同步更新/失败。

**示例：**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

## `--id-type=ProductId`

默认情况下，在将`saas:resync feed`命令与`--by-ids`选项一起使用时指定的实体由产品SKU指定。 使用`--id-type=ProductId`选项，按产品ID指定实体。

```shell
bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

**示例：**

## 故障排除

如果在连接的Commerce服务中未看到预期的数据，请通过检查数据导出错误日志并使用带有环境变量的`saas:resync`命令查看有效负载和探查器数据来解决问题。 查看[查看日志和疑难解答](troubleshooting-logging.md)。
