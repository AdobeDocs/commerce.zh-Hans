---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 27%
---

# 删除冲突的扩展

如果安装了以下任何扩展，请在安装[!DNL Adobe Commerce Optimizer Connector for B2B]之前卸载它们：

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

与这些扩展关联的数据仍会在Commerce数据库中可用。 但是，在启用连接器时，不会将其导出到[!DNL Commerce Optimizer]。 要在启用连接器后实施这些扩展提供的Adobe Commerce搜索和促销功能，请从[[!DNL Commerce Optimizer] 管理员UI](https://experienceleague.adobe.com/zh-hans/docs/commerce/optimizer/overview#quick-tour)配置它们。

>[!IMPORTANT]
>
>在启用连接器之前无法删除这些扩展会导致配置屏幕损坏、[!DNL Commerce Optimizer]中的数据重复，以及401或403身份验证错误。