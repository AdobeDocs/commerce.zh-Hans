---
title: '[!DNL SaaS Data Export Extension]发行说明'
description: Adobe Commerce的 [!DNL Data Export Extension] 的最新发行信息。
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: e30210e6aac469929e4767e3747bd819bc10b9f4
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# [!DNL SaaS Data Export]扩展发行说明

以下发行说明介绍了[!DNL SaaS data export]扩展的最新版本。 为当前的主要发行版本提供支持。 提供了旧版本的发行说明以供参考。

更新包括：

![新](../assets/new.svg)新功能
![修复](../assets/fix.svg)修复和改进
![错误](../assets/bug.svg)已知问题


>[!NOTE]
>
>SaaS数据导出扩展是随“实时搜索”、“产品推荐”和“目录服务”一起自动安装的模块的集合。 您可以使用编辑器检查系统上安装的版本。 在某些情况下，您可能希望升级系统上的数据导出扩展以获取修复或新功能，而不更新Commerce服务版本。

## 当前主要版本

## 103.3.21发行版

![修复](../assets/new.svg)添加了基于指定的产品SKU列表部分同步`product`、`productOverrides`和`productAttributes`馈送的功能。 通过将`--by-ids`选项添加到`bin/magento saas:resync --feed=<FEED_NAME>` CLI命令来使用新功能。 <!--MDEE-606-->
![修复](../assets/fix.svg)通过解决已弃用的功能，减少了与PHP 8.4的潜在兼容性问题。<!--MDEE-1002-->

## 103.3.20发行版

![修复](../assets/fix.svg)通过改进与目录数据导出cron作业失败相关的错误消息传送功能，修复了`cron.log`中无法跟踪的`BulkException`错误。<!--MDEE-966-->
![修复](../assets/fix.svg)提高了产品重新同步过程在拥有大量存储视图的实例上的性能。<!--MDEE-974-->

## 103.3.19发行版

![修复](../assets/fix.svg)更新了数据导出扩展以提高馈送可扩展性。 <!--MDEE-936-->
![修复](../assets/fix.svg)数据导出处理器现在会在完全重新同步之前验证索引器状态，以避免馈送表中意外的数据丢失。

## 103.3.18发行版

![修复](../assets/fix.svg)产品和类别实体的暂存更新现在在数据导出数据更新中正确触发。<!--MDEE-963-->

## 103.3.17发行版

![修复](../assets/fix.svg)添加了与PHP 8.4的兼容性。<!--MDEE-941-->

## 103.3.16发行版

![Fix](../assets/fix.svg)对于多个商店视图的可配置产品，选项值可以为空。<!--MDEE-926-->

## 103.3.15发行版

![修复](../assets/fix.svg)已确保在旧配置上稳定运行集成测试。 <!--MDEE-869-->
![修复](../assets/fix.svg)停止传播不必要的属性选项。 <!--MDEE-882-->
![修复](../assets/fix.svg)修复了数据序列化失败时发送到数据导出日志的错误消息。 <!--MDEE-913-->
![修复](../assets/fix.svg)通过额外的测试覆盖率提高了简单产品更新的可靠性。<!--MDEE-886-->

## 103.3.14发行版

![修复](../assets/fix.svg)导出程序索引器现在为依赖的索引器维护正确的状态。 以前，这些索引错误地失效，需要进行额外的检查和验证，从而减慢索引性能。<!--MDEE-866-->

## 103.3.13发行版

![修复](../assets/fix.svg)通过为属性选项数据添加本地缓存，提高了数据同步过程的性能。<!--MDEE-864-->

## 103.3.12发行版

![修复](../assets/fix.svg)解决了增加简单和虚拟产品同步时间的问题。<!--MDEE-861-->

## 103.3.11发行版

![修复](../assets/fix.svg)数据导出服务现在以百分比形式发送捆绑产品的特殊价格数据，从而更正了以前发送捆绑产品的特殊价格数据作为最终价格的问题。 <!--MDEE-854-->
![Fix](../assets/fix.svg)已更新单色实现，以便与Monolog 3兼容。<!--MDEE-858-->

## 103.3.10发行版

![Fix](../assets/fix.svg)修复了产品自定义选项馈送的多重审核过滤。 <!--MDEE-842-->
![修复](../assets/fix.svg)在馈送的哈希值发生更改之前，不会重新提交无效的馈送。<!--MDEE-848-->

## 103.3.9发行版

![修复](../assets/fix.svg)当删除实体时，将为网站(`scopesWebsite`)和客户组(`scopesCustomerGroup`)的范围界定服务源传播`deleted`标志。<!--MDEE-839-->

## 103.3.8发行版

![修复](../assets/fix.svg)已禁用的配置选项不再导出为活动选项。<!--MDEE-812-->
![Fix](../assets/fix.svg)在对子产品进行更改时，可配置产品的选项和值现在会更新。 <!--MDEE-835-->
![新](../assets/new.svg)添加了在产品属性馈送中包含其他系统属性数据的功能。

## 103.3.7发行版

![修复](../assets/fix.svg)从InventoryDataExporter模块中删除了不必要的依赖项。
![修复](../assets/fix.svg)更改了CatalogInventoryDataExporter模块中包含的清单模块的必需版本，以支持Adobe Commerce版本2.4.4。

## 103.3.6发行版

![修复](../assets/fix.svg)修复了在多线程模式下重新索引馈送期间发生的死锁。 现在，查询分为插入和更新操作。
![Fix](../assets/fix.svg)已针对包含许多网站的大型目录优化价格查询。
![New](../assets/new.svg)添加了重试逻辑，以便在发生死锁时重新运行失败的事务。

## 103.3.5发行版

![修复](../assets/fix.svg)设置SaaS公共模块的最新兼容数据导出版本的依赖关系。

![修复](../assets/fix.svg)已将`ScopeConfig`实例替换为`ServiceConfigInterface`以支持不同的服务配置。

## 103.3.4发行版

![修复](../assets/fix.svg)通过添加每次将数据从Commerce实例传输到Commerce服务<!--MDEE-785-->时发送`data_sent_outside`事件的机制，增加了对数据传输审核日志记录的支持

## 103.3.3发行版

![新](../assets/new.svg) SaaS数据导出现在为属性元数据查询缓存Entity-Attribute-Value (EAV)属性。

![修复](../assets/fix.svg)修复了在删除产品时，重试时未保存`InventoryStockStatus`馈送的问题。

## 103.3.2发行版

![修复](../assets/fix.svg)修复了已删除的实体源中缺少`modifiedAt`字段的问题。

## 103.3.1发行版

![修复](../assets/fix.svg)修复了在安装页面生成器时导致在产品馈送重新索引期间显示`Invalid Template File`消息的问题。

## 103.3.0发行版

![新](../assets/new.svg)已将立即导出信息源表迁移到统一结构：
`id`、`source_entity_id`、`feed_id`、`modified_at`、`is_deleted`、`status`、`feed_data`、`feed_hash`、`errors`

![新](../assets/new.svg)已将目录和清单源迁移到立即导出解决方案。

![新](../assets/new.svg)已将立即导出源cron-job重命名为`*_feed_resend_failed_items`。

![新](../assets/new.svg)重命名了立即导出信息源、索引器视图ID和更改日志表。
- 信息源表（和索引器视图ID）：
   - `catalog_data_exporter_products` -> `cde_products_feed`
   - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
   - `catalog_data_exporter_categories` -> `cde_categories_feed`
   - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
   - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
   - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`
- 更改日志表名称 — 遵循与信息源表相同的命名模式，但更改日志表名称会添加`_cl`后缀。  例如`catalog_data_exporter_products_cl`-> `cde-products_feed_cl`
如果您的自定义代码引用了其中的任何实体，请使用新名称更新引用，以确保代码继续正常运行。

![修复](../assets/fix.svg)仅为需要它的馈送设置馈送数据中的`modified_at`字段。

![修复](../assets/fix.svg)修改`productAttributes`查询以仅检索产品属性。

## 103.2.6发行版

![修复](../assets/fix.svg)修复了在表具有前缀时阻止重新索引馈送的问题。

## 103.2.5发行版

![修复](../assets/fix.svg)已优化价格查询。

## 103.2.4发行版

![修复](../assets/fix.svg)修复了在启用Commerce Inventory management时为产品显示的错误库存状态。

## 103.2.3发行版

![Fix](../assets/fix.svg)修复了网站级别的特别定价。
![Fix](../assets/fix.svg)为所有已处理的馈送添加了Mutex。


## 103.2.2发行版

![修复](../assets/fix.svg)已改进大型目录的馈送批量处理策略。 现在，批处理表中填入了有限数量的ID，以减少内存使用。

![修复](../assets/fix.svg)消除了CommerceInventoryDataExporter对MSI模块的硬依赖关系。

![修复](../assets/fix.svg)改进了`commerce-data-exporter`日志，以收集更多信息并按不同的导出阶段进行组织。

## 103.2.1发行版

- 已发布更新版本。

## 103.2.0发行版

- 为产品和价格添加了多线程数据同步。
