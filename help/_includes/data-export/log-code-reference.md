---
source-git-commit: 1b8a6de3a35a626f211089955029207f8a88414c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---
# MDEE日志代码参考

日志代码格式： `CDE<group_id>-<log_id>` （如`CDE01-02`）

源： `commerce-data-export`，`commerce-data-export-ee`，`saas-export`

代码仅分配给`error`、`warning`和`critical`级别的日志消息。 排除了`info`、`notice`和`debug`级消息。

## 组01 — 数据收集阶段

与从源实体（通常在数据提供程序中）收集数据时发生的错误或警告相关的日志代码。
- 受影响的实体可能会使用部分数据进行处理，或者在发生错误时完全跳过。 有关详细信息，请参阅日志消息。
- 警告可能表示第三方模块与Data Export扩展不正确集成；但是，同步操作通常会继续。

| 日志代码 | 级别 | 消息 |
|----------|---------|------------------------------------------------------------------------------------------------------------------------------------|
| CDE01-01 | 错误 | `CDE01-01 Failed to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-02 | 警告 | `CDE01-02 Field "{field}" is missing in row {row_data}` |
| CDE01-03 | 警告 | `CDE01-03 Invalid field "{field}" requested from inventory config {config_data}` |
| CDE01-04 | 错误 | `CDE01-04 Was not able to add data to "ac_attribute_set" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-05 | 错误 | `CDE01-05 Unable to sync feed "{feed}" for ids "{ids}". Affected data provider: "{provider}". Error: {exception_message}` |
| CDE01-06 | 错误 | `CDE01-06 Unable to sync feed "{feed}" for ids "{ids}". Error: {exception_message}` |
| CDE01-07 | 错误 | `CDE01-07 Source entity id is null. Item sync was skip for feed "{feed}". field: "{field}", item: {item}` |
| CDE01-08 | 错误 | `CDE01-08 Cannot collect "inStock" for products "{product_ids}": no sales channel data for stores "{store_view_codes}"` |
| CDE01-09 | 错误 | `CDE01-09 Cannot get status attribute. Product variants ignore stock status. Error: {exception_message}` |
| CDE01-10 | 错误 | `CDE01-10 Unable to retrieve gift card product options for products "{values}". Error: {exception_message}` |
| CDE01-11 | 错误 | `CDE01-11 Unable to retrieve gift card shopper input options for products "{values}". Error: {exception_message}` |
| CDE01-12 | 警告 | `CDE01-12 Catalog Permissions: Global Configuration path was not found for path {path}. {config_dump}` |
| CDE01-13 | 错误 | `CDE01-13 Catalog Permissions: wrong state in global config. item: {item}, config: {config}` |
| CDE01-14 | 错误 | `CDE01-14 Failed to assign UUIDs for type: {type}, ids: {ids}` |
| CDE01-15 | 错误 | `CDE01-15 Failed to assign UUIDs for type: {type}, ids: {ids}. duplicates: {duplicates}` |
| CDE01-16 | 错误 | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` |
| CDE01-17 | 警告 | `CDE01-17 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` |
| CDE01-18 | 警告 | `CDE01-18 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` |
| CDE01-19 | 警告 | `CDE01-19 GiftCard {sku} does not have shopper input options` |
| CDE01-20 | 警告 | `CDE01-20 GiftCard {sku} doesn't have valid options: {options}` |
| CDE01-21 | 错误 | `CDE01-21 Unable to resolve url_path for category {id} with path "{path}", url_key "{urk_key}", store "{store}"` |
| CDE01-22 | 错误 | `CDE01-22 Unable to resolve url_path for category{id} with path "{path}" for store view "{store}"` |

## 组02 — 将数据发送到SaaS阶段

与将馈送数据提交到SaaS端点时发生的错误或警告相关的日志代码。
- 错误通常指示HTTP请求、响应处理或数据验证期间发生故障，导致数据无法被接受。
- 警告通常指示自动重试请求的临时情况（例如速率限制或服务器错误）。

| 日志代码 | 级别 | 消息 |
|-----------|---------|---------|
| CDE02-01 | 错误 | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-02 | 错误 | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-03 | 警告 | `CDE02-03 Cannot parse the API response because the request was not successful.` |
| CDE02-04 | 错误 | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` |
| CDE02-05 | 错误 | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` |
| CDE02-06 | 错误 | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` |
| CDE02-07 | 警告 | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` |
| CDE02-08 | 警告 | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-09 | 错误 | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` |
| CDE02-10 | 警告 | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-11 | 警告 | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` |
| CDE02-12 | 错误 | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` |
| CDE02-13 | 警告 | `CDE02-13 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` |

## 组03 — 计划实体更新时同步

与响应实体更改而调度或触发同步时发生的错误或警告相关的日志代码。
- 错误可能会阻止计划增量同步，并且通常需要完全或部分重新同步才能恢复。
- 警告指示由于不支持的输入、缺少标识符或配置问题而跳过或延迟了同步操作。

| 日志代码 | 级别 | 消息 |
|----------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| CDE03-01 | 错误 | `CDE03-01 Cannot schedule resync for feeds` |
| CDE03-02 | 警告 | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` |
| CDE03-03 | 错误 | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` |
| CDE03-04 | 错误 | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` |
| CDE03-05 | 错误 | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` |
| CDE03-06 | 错误 | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` |
| CDE03-07 | 警告 | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` |
| CDE03-08 | 错误 | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` |
| CDE03-09 | 警告 | `CDE03-09 The '{feed_name}' feed does not support partial resync by IDs, or an unsupported identifier type was specified.` |
| CDE03-10 | 警告 | `CDE03-10 There are no {id_field}s found to reindex for provided identifiers list: {identifiers}` |
| CDE03-11 | 错误 | `CDE03-11 Categories Permissions feed sync scheduling error on category "{category_id_and_name}" delete. Error: {error_message}` |
| CDE03-12 | 警告 | `CDE03-12 Product Overrides sync failed. Marked indexer as invalid. Error: {error_message}` |
| CDE03-13 | 错误 | `CDE03-13 Cannot invalidate indexers "{indexer_ids}" for event "{event_name}". Error: {error_message}` |
| CDE03-14 | 错误 | `CDE03-14 Failed to read config values. Indexer invalidation skipped. Error: {error_message}` |
| CDE03-15 | 错误 | `CDE03-15 Categories Permissions feed sync scheduling error on config save: {error_message}` |
| CDE03-16 | 错误 | `CDE03-16 Failed to reindex category permissions global configuration after full reindex: {error_message}` |
| CDE03-17 | 关键 | `CDE03-17 Failed to recreate product override view subscriptions on customer group save: {error_message}` |
| CDE03-18 | 关键 | `CDE03-18 Failed to recreate product override view subscriptions on customer group delete: {error_message}` |
| CDE03-19 | 错误 | `CDE03-19 Failed to remove product override view subscriptions during table maintenance: {error_message}` |
| CDE03-20 | 错误 | `CDE03-20 Failed to recreate product override view subscriptions after table maintenance: {error_message}` |
| CDE03-21 | 错误 | `CDE03-21 Product sync scheduling error on attribute {%s} option change. Run resync. Error: %s` |
| CDE03-22 | 警告 | `CDE03-22 StagedCategoryUrlKeyChangeDetector: no active row at version {version_id} for entity_id(s) [{entity_ids}]; skipping.` |
| CDE03-23 | 错误 | `CDE03-23 StagedCategoryUrlKeyChangeDetector: catalog_category url_key attribute not found; failing open.` |
| CDE03-24 | 错误 | `CDE03-24 InvalidateProductFeedOnCategoryUrlKeyChange: scheduler failed for path "{path}": {error_message}` |
| CDE03-25 | 错误 | `CDE03-25 InvalidateProductFeedOnCategoryUrlKeyChange: gate query failed: {error_message}` |
| CDE03-26 | 错误 | `CDE03-26 InvalidateProductFeedOnCategoryUrlKeyChange: unable to expand staged url_key category reindex scope: {error_message}` |
| CDE03-27 | 错误 | `CDE03-27 Failed to invalidate indexers after config "{config_section}" change. Error: {error_message}` |
| CDE03-28 | 警告 | `CDE03-28 StagedCategoryUrlKeyChangeDetector: catalog category staging schema is not present; skipping staged url_key change detection.` |

## 组04 — 与索引或配置相关的常规错误

与索引过程中或由于配置错误导致的错误相关的日志代码。

| 日志代码 | 级别 | 消息 |
|-----------|---------|---------|
| CDE04-02 | 错误 | `CDE04-02 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` |
| CDE04-03 | 警告 | `CDE04-03 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` |
| CDE04-04 | 错误 | `CDE04-04 Feed metadata does not contain indexer name. Check di.xml config` |
| CDE04-05 | 错误 | `CDE04-05 Cannot load feed indexer for feed` |
| CDE04-06 | 错误 | `CDE04-06 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` |
| CDE04-07 | 错误 | `CDE04-07 Error on partial resync for feed "{feed_name}". Error: {message}` |
| CDE04-08 | 错误 | `CDE04-08 Error retrying failed items sync for feed "{feed_name}". Error: {message}` |
| CDE04-09 | 错误 | `CDE04-09 Error on full resync for feed "{feed_name}". Error: {message}` |
| CDE04-10 | 错误 | `CDE04-10 Error during full sync. Message: "{message}". The following IDs were skipped: [{ids}]` |
| CDE04-11 | 警告 | `CDE04-11 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` |
| CDE04-12 | 警告 | `CDE04-12 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` |
| CDE04-13 | 错误 | `CDE04-13 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` |
| CDE04-14 | 错误 | `CDE04-14 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` |
| CDE04-15 | 警告 | `CDE04-15 Failed to serialize metadata after sync. Error: {message}` |
| CDE04-16 | 警告 | `CDE04-16 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` |
| CDE04-17 | 警告 | `CDE04-17 Failed to check indexer type when setting schedule mode: {message}` |
| CDE04-18 | 警告 | `CDE04-18 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` |
| CDE04-19 | 警告 | `CDE04-19 The identifier for a feed item is empty. Sync is skipped for the entity.` |
| CDE04-20 | 警告 | `CDE04-20 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` |
| CDE04-21 | 错误 | `CDE04-21 Failed to clean up deleted feed items for feed "{feed_name}". Error: {error_message}` |
