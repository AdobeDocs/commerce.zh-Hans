---
title: Inventory management Source传输
description: 使用Adobe Commerce Inventory management为 [!DNL Store Fulfillment solution] 配置库存。 设置新库存并从默认库存中转移库存，以便将其分配给为启用“商店履行”解决方案所需的商店提货功能而配置的来源。
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Inventory management Source传输

[!DNL Store Fulfillment]解决方案使用本机Adobe Commerce Inventory management。 默认情况下，[!DNL Commerce]配置将所有Web库存分配给默认库存，该库存不能分配额外的源。 由于网站只能分配单个库存，因此商家必须配置新库存，并可以选择将其默认来源库存转移到分配给相应范围的来源。 然后，可以将源分配给新库存。

>[!IMPORTANT]
>
>商家必须维护组和捆绑产品类型中包含的所有产品的默认来源。 这些产品需要库存数量满足库存物料的最小数量阈值并包含[!UICONTROL In Stock]的库存状态。

这些配置更改可帮助您完成三件事：

1. [将库存转移到来源](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/quantities/inventory-transfer)以将库存从默认库存/来源转移到新库存/来源。

1. [批量分配源](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/quantities/bulk-assignment)以添加所有产品的新源。

1. [完成产品属性的批量更新](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)以将`Allow Store Pickup`和`Allow Home Delivery`属性添加到现有产品。 安装解决方案后，属性具有最佳的&#x200B;*默认值*&#x200B;值。 但是，在完成批量更新内容过程之前，这些属性不会应用于现有产品。

库存从所选源（零售商店库位或电子商务仓库）中扣除。 用作电子商务仓库的来源必须分配给与商店取货地点相同的库存，并在零售地点之前排定优先次序。 有关其他信息，请参阅[优先处理股票的来源](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)。

有关管理库存、库存和来源的详细信息，请参阅Adobe Commerce用户文档：

- [管理库存](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/introduction)

- [管理库存数量](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/quantities/quantities-manage)

- [管理库存](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/stocks/stocks-manage)

- [管理源](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/sources/sources-manage)

- [优先处理库存的来源](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)

- [产品属性的批量更新](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)


>[!IMPORTANT]
>
>更改库存和库存源的配置也会对集成系统产生下游影响。 确保您了解对清单配置的更改如何影响这些系统。
