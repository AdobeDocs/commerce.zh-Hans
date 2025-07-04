---
title: 扩展和自定义SaaS数据导出馈送数据
description: 了解如何扩展和自定义 [!DNL SaaS Data Export] 馈送数据。
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 扩展和自定义SaaS数据导出馈送数据

[!DNL Commerce Data Export]扩展提供了一种将数据从[!DNL Commerce]应用程序导出到Commerce服务（如Live Search、目录服务和产品推荐）的方法。 如果需要，您可以扩展和自定义馈送数据，以包含其他属性数据或修改收集的数据。

添加属性数据后，可从店面服务的GraphQL架构中的[属性字段](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)访问它。

>[!NOTE]
>
>添加或修改馈送数据可能会影响Commerce后端的性能和处理逻辑。 在合并到生产环境之前测试自定义的代码。 请使用API网格扩展目录服务GraphQL架构，而不是将数据添加到后端。 有关配置详细信息，请参阅[目录服务和API网格](../catalog-service/mesh.md)。

## 扩展产品信息源中的系统属性数据

产品信息源包括产品处理所需的或消费者常用的默认系统属性。 通过将其他系统属性添加到产品信息源，您可以在产品信息源中包含这些属性。

要完成此任务，请更新`magento/catalog-data-exporter`模块以将其他系统属性添加到[依赖项注入配置文件](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`)。

将属性添加到产品属性查询(`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`)。

**示例**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## 将产品属性添加到Adobe Commerce

开发人员可以使用以下方法之一添加可从[产品属性字段](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields)访问的产品属性：

- 将属性添加到Adobe Commerce，以包含在导出到Commerce店面服务的`products`信息源数据中。
- 在使用插件的馈送同步过程中动态添加属性。

### 将属性添加到Adobe Commerce

您可以通过Commerce管理员添加产品属性，或者使用自定义PHP模块以编程方式定义属性并更新Adobe Commerce。 从Commerce管理员中添加属性是最简单的方法，因为您可以同时添加属性和所有必需的元数据。 在下次计划同步期间，新属性及其元数据属性会自动导出到SaaS服务。

#### 从管理员创建产品属性

1. 在Commerce管理员中，从产品属性配置页面([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product])创建属性。

1. 根据需要将属性添加到属性集。

请参阅&#x200B;*Adobe Commerce管理指南*&#x200B;中的[创建产品属性](https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create)。

#### 以编程方式创建产品属性

通过创建实现`DataPatchInterface`的数据修补程序以编程方式添加产品属性，并在构造函数中实例化`EavSetup Factory`类的副本以配置属性选项。

定义属性选项时，除`type`、`label`和`input`之外的所有属性参数都是可选的。 定义以下附加参数以及与默认设置不同的任何其他参数。

- **`user_defined`=`1`** — 在数据同步期间将属性导出到storefront services
- **`used_in_product_listing`=`1`** — 使属性可在产品列表数据库查询中访问

有关创建数据修补程序的信息，请参阅&#x200B;*PHP Developer Guide*&#x200B;中的[开发数据和架构修补程序](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/)。

### 动态添加产品属性

有关在不引入新EAV属性的情况下动态创建产品属性的详细信息，请参阅[动态添加属性](add-attribute-dynamically.md)。
