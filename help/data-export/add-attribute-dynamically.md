---
title: 动态添加产品属性
description: 了解如何在数据同步过程中动态地将自定义产品属性添加到数据导出馈送。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
TQID: https://experienceleague.adobe.com/SZWtLSvxb-w-968f4wqWrPTBn1c9IEuthvhIv86Pvss
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# 动态添加产品属性

您可以通过创建插件在数据同步过程中添加产品属性，来扩展产品属性，而无需在[!DNL Adobe Commerce]中注册这些属性。

>[!NOTE]
>
>扩展产品属性的最佳方法是使用 [!DNL Catalog Service]](../catalog-service/mesh.md)将这些属性[添加到 [!DNL Adobe Commerce]](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) where you can configure and manage them from the Commerce Admin. Only add them dynamically if you need them solely for Commerce storefront services and do not want to register them in [!DNL Adobe Commerce]. You also have the option to manage custom attributes using [[!DNL API Mesh] 以扩展[!DNL Catalog Service] [!DNL GraphQL]架构。

## 添加产品属性

创建将`customer_attribute`添加到`Magento\CatalogDataExporter\Model\Provider\Product\Attributes`类的插件。

1. 更新[依赖项注入配置文件](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`)以定义插件。

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. 创建插件。

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\Product\Attributes;
   
    class AddAttribute {
   
         /**
          * @param Attributes $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
          public function afterGet(Attributes $subject, array $result, $arguments): array
          {
              $additionalAttributes = [];
              $attributeCode = 'customer_attribute';
              foreach ($result as $product) {
                  if (!isset($product['productId']) || !isset($product['storeViewCode'])) {
                      continue;
                  }
                  // HINT: if needed, do filtration by "storeViewCode" and or "productId"
   
                  $productId = $product['productId'];
                  $storeViewCode = $product['storeViewCode'];
   
                  $newKey = \implode('-', [$product['storeViewCode'], $product['productId'], $attributeCode]);
                  if (isset($additionalAttributes[$newKey])) {
                      continue;
                  }
                  $additionalAttributes[$newKey] = [
                      'productId' => $productId,
                      'storeViewCode' => $storeViewCode,
                      'attributes' => [
                          'attributeCode' => $attributeCode,
                          // provide single or multiple values for the attribute
                          'value' => [
                              rand(1, 42)
                          ]
                      ]
                  ];
   
              }
   
              return array_merge($result, $additionalAttributes);
          }
    }
   ```

   添加插件后，在下次计划同步期间，更改将同步到连接的店面服务。 要立即发送更新，请使用以下CLI命令手动启动同步过程。

   ```shell
   bin/magento saas:resync --feed=products
   ```

## 声明自定义产品属性元数据

如果您动态创建自定义产品属性并希望将其用于店面服务中的显示、搜索或筛选，请添加产品属性元数据以配置店面行为。

1. 更新[依赖项插入配置文件](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`)以定义产品属性元数据的插件。

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. 为以下提供程序`Magento\CatalogDataExporter\Model\Provider\ProductMetadata`创建插件。

   检查`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`中的`ProductAttributeMetadata`以了解必填字段。

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\ProductMetadata;
   
    class AddAttributeMetadata {
   
         /**
          * @param ProductMetadata $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(ProductMetadata $subject, array $result, $arguments): array
         {
              $result[] = [
                'id' => '123',
                // provide storeCode, websiteCode and storeViewCode applicable for your AC instance
                'storeCode' => 'default',
                'websiteCode' => 'base',
                'storeViewCode' => 'default',
                // specify the customer attribute code - should be the same as used in the products attributes plugin
                'attributeCode' => 'customer_attribute',
                // only product attributes are supported
                'attributeType' => 'catalog_product',
                // specify the data type
                'dataType' => 'int',
                'multi' => false,
                'label' => 'Customer Attribute',
                'frontendInput' => 'select',
                'required' => false,
                'unique' => false,
                'global' => true,
                'visible' => true,
                'searchable' => true,
                'filterable' => true,
                // This value must be set to true to export it to the storefront services
                'visibleInCompareList' => true,
                'visibleInListing' => true,
                'sortable' => true,
                'visibleInSearch' => true,
                'filterableInSearch' => true,
                'searchWeight' => 1.0,
                'usedForRules' => true,
                'boolean' => false,
                'systemAttribute' => false,
                'numeric' => false,
                // specify the list of attribute options
                'attributeOptions' => [
                    'option1',
                    'option2',
                    'option3'
                ]
             ];
   
              return $result;
         }
      }
   ```

   添加插件后，在下次计划同步期间，更改将同步到连接的店面服务。 要立即发送更新，请使用以下CLI命令手动启动同步过程。

   ```shell
   bin/magento saas:resync --feed=productAttributes
   ```

>[!MORELIKETHIS]
>
> * [扩展和自定义SaaS数据导出馈送](extensibility-and-customizations.md)
> * [使用Commerce CLI同步源](data-export-cli-commands.md)
> * [同步的工作方式](sync-overview.md) — 了解同步模式以及计划与手动重新同步。
> * [查看日志和疑难解答](troubleshooting/logging.md)
