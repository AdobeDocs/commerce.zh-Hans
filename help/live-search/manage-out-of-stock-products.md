---
title: 在 [!DNL Live Search]中管理缺货的产品
description: 了解如何在 [!DNL Live Search] 中为Adobe Commerce管理缺货的产品。 配置库存显示、inStock过滤器和GraphQL API筛选。
feature: Services, Search
role: Admin, Developer
level: Intermediate
source-git-commit: 84cd0deaecda0790f9f123fc663d4db7b048746b
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 管理缺货产品

您可以使用库存配置、查询时间过滤器和可选的后端功能标记来控制缺货产品在[!DNL Live Search]搜索和类别结果中的显示方式。 这些选项有重要的限制，本主题将对此进行说明。

## 库存状态过滤器

不支持将Adobe Commerce stock属性`quantity_and_stock_status`作为Facet使用，该属性不会出现在&#x200B;**[!UICONTROL Add Facet]**&#x200B;对话框中。 但是，[!DNL Live Search]公开可在查询时用作过滤器的`inStock`字段。

## 隐藏缺货产品

使用以下方法之一来隐藏缺货产品。

### Commerce配置

1.从&#x200B;*管理员*，转到&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Catalog]**>**[!UICONTROL Inventory]**。

1.将&#x200B;**[!UICONTROL Display Out of Stock Products]**&#x200B;设置为&#x200B;**[!UICONTROL No]**。

1. 单击&#x200B;**[!UICONTROL Save Config]**。

当&#x200B;**[!UICONTROL Display Out of Stock Products]**&#x200B;设置为`No`时，[!DNL Live Search]通过PLP小组件将`inStock = 'no`添加到店面查询，因此不返回缺货产品。

### API过滤器

直接调用[!DNL Live Search] API（GraphQL或REST）时，请显式筛选缺货产品，例如：

```graphql
query productSearchInStockOnly {
  productSearch(
    phrase: ""
    filter: [
      { attribute: "inStock", eq: "true" }
    ]
  ) {
    total_count
    items {
      productView {
        sku
        name
        inStock
      }
    }
  }
}
```

当您不通过[Live Search PLP小组件](plp-styling.md)路由请求时，请使用此方法。

### 显示库存后缺货的结果

为了在结果集中保留缺货产品，但在按相关性排序时始终在缺货产品之后保留，Adobe可以为您的环境启用内部功能标记。

- 此功能标志未在[!DNL Live Search]管理员UI中公开。
- 若要请求该功能，请[联系Adobe支持](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide){target="_blank"}，并引用该功能以将缺货产品移动到搜索结果的结尾。

>[!NOTE]
>
>启用该标记后，在按&#x200B;*相关性*&#x200B;排序时，结果集中所有剩余缺货的产品都将移至底部。 其他排序顺序（例如，*价格*&#x200B;或&#x200B;*产品名称*）不受影响。

### 搜索促销规则和库存

搜索促销规则是基于查询的，以单个产品为目标，而不是以库存状态或Facet值为目标的整个组：

- 规则条件仅取决于购物者的搜索短语(`Query is`、`Query contains`、`Query starts with`、`Query ends with`)。
- 规则事件(Boost、Bury、Pin、Hide)适用于每个事件一个SKU。

由于这些限制：

- 您无法创建仅根据库存状态来埋藏或隐藏所有缺货产品的规则。
- 您可以手动隐藏或隐藏作为规则中的事件添加的特定SKU（受限于规则50个和每个规则25个事件）。

要隐藏或取消目录中的缺货产品的优先级，请使用本主题中所述的库存配置和`inStock`筛选器（和可选功能标记），而不是搜索促销规则。

>[!MORELIKETHIS]
>
> - [搜索促销规则](rules.md)
> - [配置Inventory management全局选项](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/configuration)
