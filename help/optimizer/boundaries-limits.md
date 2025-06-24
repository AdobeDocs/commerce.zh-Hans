---
title: 边界和限制
description: 了解 [!DNL Adobe Commerce Optimizer]的边界和限制。
role: Admin, Developer
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目(Adobe管理的SaaS基础架构)。"
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 边界和限制

下面提供了[!DNL Adobe Commerce Optimizer]的边界和限制。

## 目录

- 目录摄取的保证速率为：1000个产品/分钟，5000个价格/分钟。
- 每天的基本产品更新数为1,000,000。
- 单个实例中允许的SKU总数为250,000。 
- 目录源的最大数量为50。
- 每个产品的变体数量为10,000。
- 产品大小不能超过200kb。

## 价格

- 最大价格手册数量为1,000。

## 产品发现和店面

- 单个搜索请求可以返回的产品数为100。
- 可过滤属性的最大数量为200。
- 可搜索属性的最大数量为200。
- 可排序属性的最大数量为50。
- Facet的最大数量为100。 所有Facet都必须是可过滤属性。
- 单个Facet类别返回的最大选项数为100，可以按照支持请求增加该值。

## 目录视图和策略

- 每个租户的目录查看最大数量为1000。
- 分配给一个目录视图的策略的最大数量为10。
- 策略中使用的属性值的最大数量为100。 

## Recommendations

- 不支持类别或属性包含项或排除项。
- 您无法在[!DNL Adobe Commerce Optimizer]中预览推荐。
