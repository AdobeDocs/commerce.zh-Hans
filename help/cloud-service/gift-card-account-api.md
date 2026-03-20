---
title: 礼品卡帐户REST端点
description: 了解如何使用礼品卡帐户REST API在 [!DNL Adobe Commerce as a Cloud Service]中以编程方式创建、更新、删除和查询礼品卡帐户。
role: Admin, Developer
level: Experienced
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# 礼品卡帐户API

{{accs-sandbox-experimental}}

礼品卡帐户REST端点在帐户级别（而非购物车或报价级别）提供礼品卡帐户的程序化管理。 使用此API可创建、检索、更新和删除礼品卡帐户，或通过JSON导入端点批量设置礼品卡帐户。

这些端点专为：

* 管理员管理礼品卡计划
* 第三方集成，可从外部系统（如ERP、CRM和营销平台）提供礼品卡
* 批量礼品卡创建的自动化工作流

## 身份验证

所有端点都需要管理员或集成持有者令牌。 令牌必须与包含`Magento_GiftCardAccount::giftcardaccount`访问控制列表(ACL)资源的角色关联。

对于批量导入操作，角色还必须包含`Magento_ImportExport::import_api` ACL资源。

## 网站和商店上下文

网站和商店视图值是从HTTP请求标头解析的，而不是从请求正文解析的。 在每个请求中传递以下标头之一：

* `Store: <store_view_code>`
* `Magento-Website-Code: <website_code>`

API自动从这些标头中解析网站。 请勿在REST请求有效负载中包含`website_id`。

>[!NOTE]
>
>批量导入终结点是一个异常。 由于导入操作是批量进行的，并且可能会以特定网站为目标，因此导入有效负载中的每一行都需要一个明确的`website_id`值。

## REST API引用

API在`/V1/giftcardaccounts`下公开以下操作，所有这些操作均受`Magento_GiftCardAccount::giftcardaccount` ACL资源保护：

| 方法 | URL | 描述 |
|--------|-----|-------------|
| POST | `/rest/V1/giftcardaccounts` | 创建礼品卡帐户 |
| GET | `/rest/V1/giftcardaccounts` | 列出帐户（支持searchCriteria） |
| GET | `/rest/V1/giftcardaccounts/:id` | 按ID获取帐户 |
| GET | `/rest/V1/giftcardaccounts/code/:code` | 按代码获取帐户 |
| PUT | `/rest/V1/giftcardaccounts/:id` | 更新帐户（合并语义） |
| DELETE | `/rest/V1/giftcardaccounts/:id` | 删除帐户 |

### 字段引用

| 字段 | 类型 | 有效值 | REST创建 | 导入 |
|---|---|---|---|---|
| `code` | 字符串 | 最多255个字符 | 必填 | 必填 |
| `balance` | 浮点数 | >= 0 | 必填 | 必填 |
| `status` | int | `0` （已禁用），`1` （已启用） | 可选，默认为`1` | 可选，默认为`1` |
| `state` | int | `0` （可用）、`1` （已使用）、`2` （已兑换）、`3` （已过期） | 可选，默认为`0` | 可选，默认为`0` |
| `is_redeemable` | int | `0`或`1` | 可选，默认为`1` | 可选，默认为`1` |
| `date_expires` | 字符串 | `YYYY-MM-DD`或null | 可选 | 可选 |
| `date_created` | 字符串 | `YYYY-MM-DD` | 自动设置 | 可选，如果省略，则自动设置 |
| `website_id` | int | 有效的网站ID | 不接受（从标题自动解析） | 必填 |

### 创建礼品卡帐户

创建具有重复代码检测的新礼品卡帐户。

| 项目 | 值 |
|---|---|
| **方法** | `POST` |
| **URL** | `/V1/giftcardaccounts` |

**请求正文：**

```json
{
  "giftcardAccount": {
    "code": "GIFT-1234-ABCD",
    "balance": 100.00,
    "status": 1,
    "state": 0,
    "is_redeemable": 1,
    "date_expires": "2027-12-31"
  }
}
```

**响应(200)：**

```json
{
  "account_id": 42,
  "code": "GIFT-1234-ABCD",
  "balance": 100,
  "status": 1,
  "state": 0,
  "is_redeemable": 1,
  "date_expires": "2027-12-31",
  "date_created": "2026-03-12"
}
```

### 按ID检索礼品卡帐户

| 项目 | 值 |
|---|---|
| **方法** | `GET` |
| **URL** | `/V1/giftcardaccounts/:id` |

**响应(200)：**

返回单个礼品卡帐户对象。

### 按代码检索礼品卡帐户

| 项目 | 值 |
|---|---|
| **方法** | `GET` |
| **URL** | `/V1/giftcardaccounts/code/:code` |

>[!IMPORTANT]
>
>如果礼品卡代码是纯数字（例如，`12345`），则对`/V1/giftcardaccounts/12345`的请求与ID路由匹配，而不是与代码路由匹配。 当代码可以是数字时，始终使用`/V1/giftcardaccounts/code/12345`进行基于代码的查找。

**响应(200)：**

返回单个礼品卡帐户对象。

### 列出具有搜索条件的礼品卡帐户

| 项目 | 值 |
|---|---|
| **方法** | `GET` |
| **URL** | `/V1/giftcardaccounts` |

将搜索条件作为查询参数传递。 以下示例返回`status`等于`1`（已启用）的礼品卡帐户：

```text
GET /V1/giftcardaccounts?searchCriteria[filterGroups][0][filters][0][field]=status&searchCriteria[filterGroups][0][filters][0][value]=1&searchCriteria[pageSize]=10&searchCriteria[currentPage]=1
```

**响应(200)：**

```json
{
  "items": [
    {
      "account_id": 42,
      "code": "GIFT-1234-ABCD",
      "balance": 100,
      "status": 1,
      "state": 0,
      "is_redeemable": 1,
      "date_expires": "2027-12-31",
      "date_created": "2026-03-12"
    }
  ],
  "search_criteria": { ... },
  "total_count": 1
}
```

### 更新礼品卡帐户

使用合并语义更新现有礼品卡帐户。 仅应用请求中的非null字段。 `code`字段不可更改。 传递其他代码会返回验证错误。

| 项目 | 值 |
|---|---|
| **方法** | `PUT` |
| **URL** | `/V1/giftcardaccounts/:id` |

**请求正文：**

```json
{
  "giftcardAccount": {
    "balance": 75.00,
    "status": 1
  }
}
```

**响应(200)：**

返回更新的礼品卡帐户对象。

### 删除礼品卡帐户

| 项目 | 值 |
|---|---|
| **方法** | `DELETE` |
| **URL** | `/V1/giftcardaccounts/:id` |

**响应(200)：**

```json
true
```

## 通过JSON批量导入

可以使用实体类型为`POST /V1/import/json`的`giftcardaccount`批量配置礼品卡帐户。 除了礼品卡帐户ACL之外，此端点还需要`Magento_ImportJsonApi::import_api`访问控制列表(ACL)资源。

### 支持的行为

| 行为 | 描述 |
|---|---|
| `append` | 创建新的礼品卡帐户。 如果某个代码已存在，则该行将失败，并且导入将继续其余的行。 |
| `replace` | 按代码更新和插入礼品卡帐户。 如果代码不存在，则创建帐户；如果代码不存在，则替换帐户。 |
| `delete` | 按代码删除礼品卡帐户。 |

### 请求示例

```json
{
  "source": {
    "entity": "giftcardaccount",
    "behavior": "append",
    "validation_strategy": "validation-stop-on-errors",
    "allowed_error_count": "10",
    "items": [
      {
        "code": "BULK-001",
        "balance": 50.00,
        "website_id": 1,
        "status": 1,
        "state": 0,
        "is_redeemable": 1,
        "date_expires": "2027-06-30"
      },
      {
        "code": "BULK-002",
        "balance": 25.00,
        "website_id": 1
      }
    ]
  }
}
```

### 导入行为详细信息

* 导入有效负载中的每一行都需要一个显式的`website_id`，这与REST端点从请求标头推断网站不同。
* 每一行都经过独立验证。 无效行会生成每行错误，而不会影响同一批次中的有效行。
* 在同一批中检测到重复代码并将其报告为每行错误，而不是导致事务回滚。
* 将写操作直接导入数据库以提高性能，并绕过供应商模型的保存生命周期。 导入期间不会创建余额更改历史记录条目。
* REST创建操作会拒绝过去的到期日期。 导入功能在设计上接受过去的过期日期，以支持历史数据迁移。

## 错误处理

API返回标准HTTP状态代码：

| 状态代码 | 条件 |
|---|---|
| `400` | 验证错误。 REST创建时缺少必填字段、值无效或过期日期。 |
| `401` | 持有者令牌缺失或无效。 |
| `403` | 令牌缺少所需的ACL资源。 |
| `404` | 未找到礼品卡帐户。 |
| `409` | 礼品卡代码重复。 |

输入验证涵盖必填字段、值范围（状态必须为`0`或`1`，状态必须为`0`-`3`，余额必须为非负数）、日期格式和类型安全性。 数字字段的非数值将被拒绝。
