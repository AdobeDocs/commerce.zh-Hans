---
title: SaaS数据导出命令行界面
description: 了解如何使用命令行界面命令来管理Adobe Commerce SaaS服务的 [!DNL data export extension] 的馈送和进程。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# SaaS数据导出命令行界面参考

开发人员和系统管理员可以使用[Adobe Commerce命令行工具](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI)管理SaaS数据导出的同步操作。 `saas:resync`命令包含在`magento/saas-export`程序包中。

Adobe不建议定期使用`saas:resync`命令。 使用该命令的典型情况包括：

- 初始同步
- [SaaS数据空间ID](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)已更改，您需要将数据同步到新数据空间。
- 故障排除

## 初始同步

>[!NOTE]
>如果您使用的是实时搜索或产品推荐，则无需运行初始同步。 将服务连接到Commerce实例后，将自动启动该流程。

当从命令行触发`saas:resync`时，根据目录大小，数据更新可能需要几分钟到几小时的时间。

对于初始同步，Adobe建议按以下顺序运行命令：

```bash
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

## 命令示例

在使用`saas:resync`命令之前，请查看[选项说明](#command-options)。

- 对实体馈送执行完全重新同步。

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  已成功导出的信息源不会重新同步。

- 完全重新同步指定的馈送和清理数据

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  仅在执行[!DNL Data Space ID Cleanup]操作后使用。

- 对于立即导出信息源，请在不截断信息源表中的索引数据的情况下，将所有数据重新发送到连接的Commerce服务

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- 列出可用命令和选项及其说明。

  ```
  bin/magento saas:resync --help
  ```

## 命令选项

以下选项可用于管理`saas:resync`操作。

>[!NOTE]
>
>`saas:resync`命令还支持高级选项，以便通过增加批处理大小和添加多线程处理来改进数据导出命令。 请参阅[自定义导出处理](customize-export-processing.md)。

### `feed`

此必需选项指定要重新同步的信息源实体，如`products`。

`feed`选项值可以包含任何可用的实体馈送：

- `products`：产品数据馈送
- `productAttributes`：产品属性数据馈送
- `categories`：类别数据馈送
- `variants`：可配置的产品变体数据馈送
- `prices`：产品价格数据馈送
- `categoryPermissions`：类别权限数据馈送
- `productOverrides`：产品权限数据馈送
- `inventoryStockStatus`：库存库存状态数据馈送
- `scopesWebsite`：具有商店和商店视图数据馈送的网站
- `scopesCustomerGroup`：客户组数据馈送
- `orders`：销售订单数据馈送

根据已安装的[Commerce Services](../landing/saas.md)，可能有其他一组源可用于`saas:resync`命令。

### `no-reindex`

此选项将现有目录数据重新提交到[!DNL Commerce Services]而不重新索引。 如果未指定此选项，则命令会在同步数据之前运行完全重新索引。

此选项的行为取决于信息源是以[旧版还是立即导出模式](data-synchronization.md#synchronization-modes)导出

- 对于旧版导出馈送，同步过程不会截断馈送表中的索引数据。 而是将所有数据重新发送到Adobe Commerce服务。
- 对于立即导出源，如果指定，将忽略此选项。 对于这些馈送，重新同步过程不会截断索引，而只重新同步之前失败的更新或项目。

### `cleanup`

此选项在同步之前清除馈送索引器表。 指定后，SaaS数据导出将对指定的馈送运行完全重新同步，并清除馈送表中的所有现有数据。

Adobe建议仅在执行[!DNL Data Space ID Cleanup]操作后使用此命令。

>[!WARNING]
>
>**请勿定期使用此选项**。 它可能会导致Adobe Commerce Services中出现数据同步问题。 例如，如果使用`cleanup`选项，`delete product event`可能不会传播到Adobe Commerce服务。

## 故障排除

如果在连接的Commerce服务中未看到预期的数据，请通过检查数据导出错误日志并使用带有环境变量的`saas:resync`命令查看有效负载和探查器数据来解决问题。 查看[查看日志和疑难解答](troubleshooting-logging.md)。
