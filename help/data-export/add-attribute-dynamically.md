---
title: 动态添加产品属性
description: 了解如何在数据同步过程中动态地将自定义产品属性添加到数据导出馈送。
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
source-git-commit: bf45670a0bc5fb02dd229a9e3d7af7f2676c5a1f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# 在数据同步期间动态添加产品属性

您可以通过创建插件在数据同步过程中添加属性，来扩展产品属性，而无需在Adobe Commerce中注册这些属性。

>[!NOTE]
>
>扩展产品属性的最佳方法是[将这些属性添加到Adobe Commerce](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce)，您可以在其中通过Commerce管理员配置和管理这些属性。 仅当您仅用于Commerce店面服务并且不想在Adobe Commerce中注册时，才需要动态添加这些插件。 您还可以选择将[API Mesh与目录服务](../catalog-service/mesh.md)结合使用来管理自定义属性，以扩展目录服务GraphQL架构。

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

   ```
   bin/magento saas:resync --feed=products
   ```

## 声明自定义产品属性元数据

如果您动态创建自定义产品属性并希望将其用于店面服务中的显示、搜索或筛选，请添加产品属性元数据以配置店面行为。

1. 更新[依赖项插入配置文件](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`)以定义产品属性元数据的插件。

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. 创建指向以下提供程序`\Magento\CatalogDataExporter\Model\Provider\ProductMetadata`的插件。

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

   ```
   bin/magento saas:resync --feed=productattributes
   ```
