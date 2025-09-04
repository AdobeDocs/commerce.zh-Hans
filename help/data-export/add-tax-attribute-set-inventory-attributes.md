---
title: 添加税分类、属性集和库存属性
description: 了解如何扩展产品信息源数据，以包含税分类、属性集和高级库存设置的属性
role: Admin, Developer
badgePaas: label="仅限PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
source-git-commit: 6abfeca68ab67fb11493f78440e09408479e1535
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 添加税分类、属性集和库存属性

Adobe Commerce额外产品属性模块可扩展产品数据馈送。 它包括Adobe Commerce产品配置中的其他产品属性：

* [税分类](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [属性集](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [库存](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

安装后，模块将自动运行。 它会在产品同步期间捕获并导出其他属性。 无需其他配置。

## 主要优势

* **自动增强**：使用税类、属性集和库存属性丰富产品馈送
* **无缝集成**：为外部系统和服务提供基本上下文
* **零配置**：安装后立即工作
* **实时更新**：与产品更改自动同步

## 特征和导出的属性

模块会向现有产品数据馈送添加三个其他属性：

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### 1.税种信息(`ac_tax_class`)

**用途**：提供每个产品的税务分类信息

**数据格式**：包含税类名称的字符串值

**示例输出**：

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**用例**：

将税分类数据导出到Commerce目录服务时，此数据可用于支持以下功能的应用程序：

* 税务合规性报告
* 与外部税务计算服务集成
* 会计系统的产品分类

### 2.属性集信息(`ac_attribute_set`)

**用途**：标识分配给每个产品的属性集

**数据格式**：包含属性集名称的字符串值

**示例输出**：

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**用例**：

将属性集数据导出到Commerce目录服务时，它会在外部系统中启用高级产品管理功能。 这些功能包括：

* 产品模板识别
* 目录管理和组织
* 需要属性集上下文的第三方系统集成

### 3.高级清单数据(`ac_inventory`)

**用途**：为每个产品提供库存管理设置

**数据格式**：包含库存配置的JSON编码字符串

**包含的字段**：

* `manageStock` （布尔值）：是否启用库存管理
* `cartMinQty` （浮动）：购物车中允许的最小数量
* `cartMaxQty` （浮动）：购物车中允许的最大数量
* `backorders` （字符串）：延交策略。 该值为以下值之一：
   * `"no"`：不允许延期交货
   * `"allow"`：允许数量低于0
   * `"allow_notify"`：允许数量低于0并通知客户
* `enableQtyIncrements` （布尔值）：是否启用数量增量
* `qtyIncrements` （浮动）：所需的数量增量值

**示例输出**：

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**用例**：

将清单数据导出到Commerce目录服务时，它会在外部系统中启用高级清单管理功能。 这些功能包括：

* Inventory management系统集成
* 购物车验证规则
* 订单履行流程优化
* 客户体验自定义

## 数据导出信息源增强功能

“额外产品属性”模块增强了现有的产品信息源。 它自动集成新的属性数据。

* **产品信息源** (`products`)：已通过三个附加属性进行增强

   * 向每个产品记录添加`ac_tax_class`、`ac_attribute_set`和`ac_inventory`属性
   * 保持原始产品数据不变
   * 保持与现有信息源使用者的向后兼容性

* **产品属性信息源** (`productAttributes`)：为新属性增强了属性元数据

   * 自动为`productAttributes`信息源中的三个新属性注册元数据
   * 提供属性配置详细信息（数据类型、可见性设置等）
   * 帮助外部系统了解新的属性架构

## 安装扩展

**要求**

* PHP 8.1、8.2、8.3或8.4
* Adobe Commerce 2.4.4+
* [Adobe Commerce数据导出扩展](manage-extension.md#update-a-module-to-a-specific-version)，版本103.4.11或更高版本
* 访问[repo.magento.com](https://repo.magento.com)

  若要生成密钥并获取必要的权限，请参阅[获取您的身份验证密钥](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)。 有关云安装，请参阅[Commerce on Cloud Infrastructure指南](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/authentication-keys)。
* 访问Adobe Commerce应用程序服务器的命令行。

### 安装步骤

使用编辑器添加`adobe-commerce/module-extra-product-attributes`模块：

```shell
composer require adobe-commerce/module-extra-product-attributes
```

有关详细的安装步骤，请参阅以下指南：

* 在云基础架构上的Adobe Commerce上[安装扩展](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [在本地安装Adobe Commerce扩展](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extension)

## 同步产品数据

重新部署后，Adobe Commerce实例会在产品同步期间自动导出附加数据。 您还可以使用`resync` CLI命令立即同步。

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## 故障排除

**产品缺少其他属性：**

* 验证模块是否已正确安装和启用
* 运行resync命令以刷新产品数据
* 检查产品是否具有有效的税分类和属性集分配

**清单数据显示不正确：**

* 验证是否在“管理员”中正确配置了清单设置
* 检查网站特定的清单覆盖
* 验证[Inventory management模块](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview)是否正常工作

有关详细信息，请参阅[Inventory management商家文档](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/guide-overview)中的&#x200B;*Adobe Commerce指南*。

**性能问题：**

* 监视安装后的导出过程性能
* 考虑在低流量期间计划重新同步

### 日志记录和调试

模块会将导出错误和警告的日志记录到标准的Commerce日志记录系统。 如果在产品同步过程中遇到问题，请检查数据导出日志。

有关详细信息，请参阅[查看日志和疑难解答](troubleshooting-logging.md)。

