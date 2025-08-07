---
title: 将自定义属性添加到配置文件
description: 了解如何将自定义属性添加到客户配置文件。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 5489910382edc70eea5d7c0ca94da41c653b577d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 将自定义属性添加到配置文件

自定义配置文件属性允许您通过使用默认`customerId`和`emailId`以外的其他标识符来增强Experience Platform中的客户配置文件识别。 这些附加标识符支持更精确的客户匹配，并改善了Commerce平台和Experience Platform之间的数据集成。

>[!NOTE]
>
>了解如何[将自定义属性](custom-attributes.md)添加到订单。

## 优点

- 使用多个标识符以更好地匹配客户。
- 根据您的业务需求将自定义字段映射到身份属性。
- 减少重复用户档案并提高客户数据准确性。
- 实现更有针对性的客户体验。

## 先决条件

在实施自定义身份属性之前，请确保您：

- [安装数据连接扩展](install.md)
- [连接到Adobe Experience Platform](connect-data.md)
- [发送客户个人资料数据](connect-data.md#send-customer-profile-data)

## 步骤1：配置Experience Platform架构

1. 登录Adobe Experience Platform并选择您的Commerce架构。
1. [在根级别添加自定义标识字段](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/ui/resources/schemas?lang=en#custom-fields-for-standard-groups)：
   - `hashedPID` （字符串） — 主身份哈希
   - `hashedSID` （字符串） — 辅助标识哈希
   - `primaryID` （字符串） — 主标识字段名称
   - `secondaryID` （字符串） — 辅助标识字段名称

![Experience Platform架构配置](./assets/aep-schema-configuration.png)

>[!NOTE]
>
>您可以根据自己的要求自定义确切的字段名称。 该示例使用`hashedPID`和`hashedSID`作为标识字段。

## 步骤2：创建处理器类

在自定义模块中创建以下PHP处理器类：

### AddressCustomHashedId类

此处理器为客户地址对`parent_id`和`entity_id`进行哈希处理。

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['parent_id'] ?? '';
        $sid = $eventData['entity_id'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### AddressCustomId类

此处理器设置地址事件的主ID和次ID字段名称。

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

### CustomHashedId类

此处理器为客户配置文件对`entity_id`和`email`进行哈希处理。

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['entity_id'] ?? '';
        $sid = $eventData['email'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### CustomId类

此处理器设置配置文件事件的主ID和次ID字段名称。

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

>[!NOTE]
>确保在事件数据中发送`primaryID`和`secondaryID`。 如果缺少其中一项，Commerce将默认使用：
>
>- primaryID = customerId
>- secondaryID = emailId

>[!BEGINSHADEBOX]

完成这两个步骤后：

- Experience Platform中的Commerce架构可以为您的配置文件事件数据正确摄取自定义身份。
- Commerce PHP代码中的处理器类从配置文件事件中收集自定义标识信息。

现在，从Commerce发送的任何用户档案事件数据都包含您的自定义标识信息。

>[!ENDSHADEBOX]

## 数据格式示例

以下示例演示了配置文件属性和完整客户配置文件数据格式中自定义身份属性的预期JSON结构。

### 配置文件属性格式

```json
{
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "warehousecode": "1256",
    "method": "ina2354",
    "source": "commerce",
    "primaryID": "hashedPID",
    "secondaryID": "hashedSID"
  }
}
```

### 完整的客户配置文件结构

```json
{
  "id": 137,
  "entity_id": "137",
  "created_at": "2025-02-10 20:10:30",
  "updated_at": "2022-02-10 20:10:31",
  "email": "customer@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "dob": "2007-10-01 00:00:00",
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "primaryID": "137",
    "secondaryID": "customer@example.com"
  },
  "_metadata": {
    "commerceEdition": "Adobe Commerce",
    "commerceVersion": "2.4.6",
    "eventsClientVersion": "1.9.0",
    "storeId": "1",
    "websiteId": "1",
    "storeGroupId": "1",
    "websiteCode": "base",
    "storeCode": "default",
    "storeViewCode": "main_website_store"
  }
}
```

## 故障排除

### 缺少主ID或辅助ID

- **症状：**&#x200B;数据默认为customerId/emailId，而不是自定义值。
- **解决方案：**&#x200B;确保在`primaryID`对象中同时设置了`secondaryID`和`profileAttributes`。

### 哈希值无效

- **症状：**&#x200B;哈希值为空或格式不正确。
- **解决方案：**&#x200B;验证源字段(`parent_id`、`entity_id`、`email`)是否包含有效的数据，然后再进行哈希处理。

### 处理器无法执行

- **症状：**&#x200B;自定义属性未出现在事件数据中。
- **解决方案：**&#x200B;检查是否已在`events.xml`中正确注册处理器，并且模块已启用。

### Experience Platform架构不匹配

- **症状：**&#x200B;数据未出现在Experience Platform或架构验证错误中。
- **解决方案：**&#x200B;确保Experience Platform架构包含具有正确数据类型的自定义标识字段。
