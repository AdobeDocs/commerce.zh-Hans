---
title: 将自定义属性添加到订单
description: 了解如何将自定义订单属性添加到您的后台数据并将这些属性发送到Experience Platform。
role: Admin, Developer
feature: Personalization, Integration
exl-id: dcd0b9e7-8d36-4bde-b226-ac19e83f00e4
source-git-commit: 5b1387e18e059c938aca600cc31951a3f5289e7e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 2%

---

# 将自定义属性添加到订单

在本文中，您将了解如何向后台事件添加自定义属性。 通过自定义属性，您可以捕获丰富的数据见解以增强分析并进而为购物者创建个性化体验。

>[!NOTE]
>
>了解如何[将自定义身份](custom-identities.md)添加到配置文件。

自定义属性可在两个级别受支持：

- 订单级别
- 订单物料级别

>[!NOTE]
>
>Adobe [!DNL Commerce]支持数据类型为字符串、布尔值或日期的自定义属性。

将自定义属性添加到Back Office事件要求您：

1. 在[!DNL Commerce]安装中创建项目。
1. 更新您的架构，以便将新的自定义属性正确引入Experience Platform。
1. 在管理员中，确认正在捕获自定义属性并将其发送到Experience Platform。

>[!IMPORTANT]
>
>下面的目录结构和代码示例说明了如何实施自定义属性。 所需的实际目录结构和代码取决于存储配置和环境。

## 步骤1：创建目录结构

1. 导航到`app/code`安装中的[!DNL Commerce]目录并创建模块目录。 例如： `Magento/AepCustomAttributes`。 此目录包含自定义属性所需的文件。
1. 在模块目录中，创建一个名为`etc`的子目录。 `etc`目录包含`module.xml`、`query.xml`、`di.xml`和`et_schema.xml`文件。

## 步骤2：定义依赖项和设置版本

创建定义依赖项和安装版本的`module.xml`文件。 例如：

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Magento_AepCustomAttributes">
        <sequence>
            <module name="Magento_SalesOrderDataExporter"/>
        </sequence>
    </module>
</config>
```

## 步骤3：检索销售订单数据

创建检索销售订单数据的`query.xml`文件。 例如：

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:Module:Magento_QueryXml:etc/query.xsd">
  <query name="salesOrdersV2">
    <source name="sales_order">
      <link-source name="sales_order_inventory_source" link-type="inner">
        <attribute name="inventory_source_code" alias="inventory_source" />
        <using glue="and">
          <condition attribute="order_id" operator="eq" type="identifier">entity_id</condition>
         </using> 
        </link-source>
    </source>
  </query>
  </config>
```

## 步骤4：设置依赖项注入

创建用于设置依赖项注入的`di.xml`文件。 例如：

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
      <type name="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">commerceOrderId</argument>
          </arguments>
      </type>
      <type name="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">entityId</argument>
          </arguments>
      </type>
      <type name="Magento\DataServices\Model\ProductContext">
          <plugin name="product-context-plugin" type="Magento\AepCustomAttributes\Plugin\Model\ProductContext"/>
      </type>
  </config>
```

## 步骤5：定义用于依赖项注入的服务

创建一个`et_schema.xml`文件，该文件定义用于依赖项注入的服务。 例如：

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_DataExporter:etc/et_schema.xsd">
      <record name="OrderV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
              <using field="commerceOrderId"/>
          </field>
      </record>
      <record name="OrderItemV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
              <using field="entityId"/>
          </field>
      </record>
  </config>
```

## 步骤6：为PHP文件创建目录

在与`etc`目录相同的级别，创建一个名为`Module/Provider`的目录。 此目录包含`OrderCustomAttributes`和`OrderItemCustomAttributes` PHP文件。

## 步骤7：定义OrderCustomAttributes

创建定义顺序自定义属性的`OrderCustomAttributes.php`文件。 例如：

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class CustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param string $usingField
   * @param Json $jsonSerializer
   */
  public function __construct(
      string $usingField,
      Json $jsonSerializer
  ) {
      $this->usingField = $usingField;
      $this->jsonSerializer = $jsonSerializer;
  }

  /**
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];

      /**
       * Entity IDs
       */
      $ids = array_column($values, $this->usingField);

      foreach ($this->flatten($values) as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];

          if (isset($row)) {
              $unserializedData['order_channel'] = 'order_channel';
              $unserializedData['order_status'] = 'order_status';

              $additionalInformation = [];
              foreach ($unserializedData as $name => $value) {
                  $additionalInformation[] = [
                      'name' => $name,
                      'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
                  ];
              }
              foreach ($additionalInformation as $information) {
                  $output[] = [
                      'additionalInformation' => $information,
                      $this->usingField => $row[$this->usingField],
                  ];
              }
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## 步骤8：定义OrderItemCustomAttributes

创建定义订单项自定义属性的`OrderItemCustomAttributes.php`文件。 例如：

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class OrderItemCustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param Json $jsonSerializer
   * @param string $usingField
   */
  public function __construct(
      Json $jsonSerializer,
      string $usingField
  ) {
      $this->jsonSerializer = $jsonSerializer;
      $this->usingField = $usingField;
  }

  /**
   * Getting additional attributes data.
   *
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];
      $values = $this->flatten($values);

      foreach ($values as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];
          $unserializedData['product_brand'] = implode(',', ['label 1', 'label 2']);

          $additionalInformation = [];
          foreach ($unserializedData as $name => $value) {
              $additionalInformation[] = [
                  'name' => $name,
                  'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
              ];
          }
          foreach ($additionalInformation as $information) {
              $output[] = [
                  'additionalInformation' => $information,
                  $this->usingField => $row[$this->usingField],
              ];
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## 步骤9：为productContext文件创建目录

在与`etc`目录相同的级别，创建一个名为`Plugin/Module`的目录。 此目录包含`ProductContext.php`文件。

## 步骤10：定义ProductContext类

创建名为`ProductContext.php`的文件，该文件定义`ProductContext`类。 例如：

```php
<?php>
namespace Magento\AepCustomAttributes\Plugin\Model;
use Magento\Catalog\Model\Product;
use Magento\DataServices\Model\ProductContext as Subject;
use Magento\Framework\App\ResourceConnection;

class ProductContext
{
    private ?array $brandCache = [];
    public function __construct(
        private ResourceConnection $resourceConnection ) {
    }  

    public function afterGetContextData(Subject $subject, array $result Product $product)
    {
        $brand = $product->getCustomAttribute('cust_attr1');
        if (!empty($brand) && $brand->getValue()) {
            $result['brands'] = ['brand_label_1', 'brand_label_2'];
            }
            return $result;
      }
  }
```

## 步骤11：注册模块

在与`etc`目录相同的级别，创建注册模块的`registration.php`文件。 例如：

```php
<?php>
declare(strict_types=1);

use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Magento_AepCustomAttributes',
    __DIR__
);
```

## 步骤12：扩展现有XDM架构

要确保Experience Platform中的[!DNL Commerce]架构能够摄取新的自定义订单属性，您需要扩展架构以包含这些自定义字段。

要了解如何扩展现有XDM架构以包含这些自定义字段，请参阅Experience Platform文档中的[在UI中创建和编辑架构](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/ui/resources/schemas#custom-fields-for-standard-groups)一文。 租户ID字段是动态生成的；但是，字段结构应类似于Experience Platform文档中提供的示例。

>[!IMPORTANT]
>
>XDM自定义属性必须与从[!DNL Commerce]发送的属性匹配。

到`commerce.order`，为订单级别添加字段：

![订单级别](assets/order-level.png)

到`productListItems`，为订单项级别添加字段：

![订单项级别](assets/order-item-level.png)

## 步骤12：确认正在捕获数据

查看管理员中的[数据自定义](connect-data.md#data-customization)选项卡，以确认正在捕获自定义属性数据并将其发送到Experience Platform。

### 故障排除

如果您在`No custom order attributes found.`选项卡上看到消息&#x200B;**[!UICONTROL Data Customization]**，请确认以下事项：

1. 您已完成启用[Data Connector扩展](overview.md#prerequisites)的先决条件。
1. 您已配置[自定义订单属性](#add-custom-order-attributes)。
1. 至少已生成一个订单事件。
