---
title: 扩展和自定义SaaS数据导出馈送数据
description: 了解如何扩展和自定义 [!DNL SaaS Data Export] 馈送数据。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 815
ht-degree: 0%

---

# 扩展和自定义SaaS数据导出馈送数据

[!DNL Commerce Data Export]扩展提供了一种将数据从[!DNL Commerce]应用程序导出到Commerce服务（如Live Search、目录服务和产品推荐）的方法。 如果需要，您可以扩展和自定义馈送数据，以包含其他属性数据或修改收集的数据。

添加属性数据后，可从GraphQL架构中的[属性字段](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)访问店面服务。

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

请参阅&#x200B;*Adobe Commerce管理指南*&#x200B;中的[创建产品属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create)。

#### 以编程方式创建产品属性

通过创建实现`DataPatchInterface`的数据修补程序以编程方式添加产品属性，并在构造函数中实例化`EavSetup Factory`类的副本以配置属性选项。

定义属性选项时，除`type`、`label`和`input`之外的所有属性参数都是可选的。 定义以下附加参数以及与默认设置不同的任何其他参数。

- **`user_defined`=`1`** — 在数据同步期间将属性导出到storefront services
- **`used_in_product_listing`=`1`** — 使属性可在产品列表数据库查询中访问

有关创建数据修补程序的信息，请参阅&#x200B;*PHP Developer Guide*&#x200B;中的[开发数据和架构修补程序](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/)。

### 动态添加产品属性

有关在不引入新EAV属性的情况下动态创建产品属性的详细信息，请参阅[动态添加产品属性](add-attribute-dynamically.md)。

## 信息源架构概述(`et_schema.xml`) {#feed-schema-overview}

每个馈送数据结构都使用简单的XML DSL在`etc/et_schema.xml`中声明。 框架读取此文件以确定要收集哪些字段以及要调用哪些PHP提供程序类。

```xml
<record name="Product">
  <field name="sku" type="ID" />
  <field name="name" type="String" />
  <field name="attributes" type="Attribute" repeated="true"
         provider="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
    <using field="productId" />
    <using field="storeViewCode" />
  </field>
</record>
```

关键元素：

- `<record>` — 定义馈送实体
- `<field>` — 声明一个数据字段；`provider`属性指向一个实现获取数据的`DataProcessorInterface`的PHP类
- `repeated="true"` — 字段是对象数组
- `<using>` — 输入参数从父记录上下文传递到提供程序

>[!IMPORTANT]
>
>向`et_schema.xml`添加新字段只会更改[!DNL Adobe Commerce]在本地收集的内容。 接收SaaS服务也必须更新为接受和处理新字段，然后才能对店面产生任何影响。

## 提交后观察数据 {#observe-data-after-submission}

在每次成功向SaaS服务提交批次后，[!DNL SaaS Data Export]都会调度`data_sent_outside`事件。 使用此事件进行审核日志记录、webhook触发器或量度收集。

**事件：** `data_sent_outside`

**可用数据：**

| 键 | 描述 |
|---|---|
| `timestamp` | 提交的Unix时间戳 |
| `type` | 信息源名称（例如，`products`，`prices`） |
| `data` | 已提交的信息源有效负载 |

**观察者示例：**

```php
<?php
namespace My\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class DataSentOutsideObserver implements ObserverInterface
{
    public function execute(Observer $observer): void
    {
        $feedName = $observer->getData('type');
        $timestamp = $observer->getData('timestamp');
        $data = $observer->getData('data');

        // Custom logic: audit logging, webhook, metrics
    }
}
```

在`etc/events.xml`中注册观察者：

```xml
<event name="data_sent_outside">
    <observer name="my_module_data_sent_outside"
              instance="My\Module\Observer\DataSentOutsideObserver" />
</event>
```

有关活动和观察者的一般信息，请参阅Adobe Commerce开发人员文档中的[活动和观察者](https://developer.adobe.com/commerce/php/development/components/events-and-observers){target="_blank"}。

## 提交前筛选数据

使用`Magento\SaaSCommon\Model\DataFilter`扩展点标记敏感字段或跳过特定实体，然后再将数据发送到SaaS服务。 这对于合规性要求（例如GDPR或PCI）非常有用，因为此类要求中某些字段不得离开Commerce实例。

在`etc/di.xml`中实施接口并通过DI首选项连接它：

```xml
<preference for="Magento\SaaSCommon\Model\DataFilter"
            type="My\Module\Model\MyDataFilter" />
```

>[!NOTE]
>
>筛选在数据收集后应用。 如果设置了`PERSIST_EXPORTED_FEED=1`，则馈送表会在进行筛选之前存储未筛选的有效负载。

>[!MORELIKETHIS]
>
> - [动态添加产品属性](add-attribute-dynamically.md)
> - [添加税类、属性集和库存元数据](add-tax-attribute-set-inventory-attributes.md)
> - [同步的工作方式](sync-overview.md)
