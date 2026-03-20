---
title: 通过REST触发的电子邮件
description: 了解如何使用REST API按需触发事务性电子邮件，方法是为 [!DNL Adobe Commerce as a Cloud Service]指定模板ID、收件人电子邮件和模板变量。
role: Admin
level: Experienced
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 9661e368f7a0dc85edcd3e52a67ae2a98355d8b5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# 通过REST API触发的电子邮件

以前，您只能在触发事件时发送电子邮件，例如在客户注册或订单购买期间。 在[!DNL Adobe Commerce as a Cloud Service]中，您可以通过指定模板ID、收件人电子邮件和模板变量，根据需要通过REST API发送电子邮件。

>[!NOTE]
>
>目前，只能发送新创建的自定义模板。 不支持预定义的和系统模板。

`V1/custom-email/send`端点允许&#x200B;**第三方系统**（如集成和外部服务）通过指定以下内容按需发送电子邮件：

- **模板ID** — 电子邮件模板标识。
- **收件人电子邮件** — 此请求的目标电子邮件地址。
- **变量** — （可选）要插入模板的自定义键值对，如`customer_name`或`order_id`。

>[!NOTE]
>
>使用当前存储范围和默认的&#x200B;**发件人**&#x200B;电子邮件地址或为模板定义的电子邮件地址同步发送电子邮件。

## REST合同

以下部分将介绍如何使用REST API按需发送事务性电子邮件。

### 端点

- **URL** - `POST /rest/V1/custom-email/send`
- **授权** — 仅支持&#x200B;**服务到服务IMS授权**。 调用方必须有权访问&#x200B;**通过API** (`Magento_CustomEmailSend::send_custom_email`)发送自定义电子邮件。 有关详细信息，请参阅[REST身份验证](https://developer.adobe.com/commerce/webapi/rest/authentication/)。
- **异步使用**（推荐） — 尽管此端点是同步实施的，但我们建议使用&#x200B;**异步REST API**&#x200B;调用它，以便请求被排入队列并由使用者处理，从而避免长期HTTP连接。 在[!DNL Adobe Commerce as a Cloud Service]中，您可以在`/async`之后使用`V1`路由，例如： `POST https://<server>.api.commerce.adobe.com/<tenant-id>/V1/async/custom-email/send`。

  有关详细信息，请参阅[异步Web端点(SaaS)](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/)。

### 请求正文

- **templateId** （整数，必需） — 管理员在&#x200B;[!UICONTROL **营销**] > [!UICONTROL _通信_] > [!UICONTROL **电子邮件模板**]&#x200B;下定义的电子邮件模板ID。

- **recipientEmail**（字符串，必需） — 目标电子邮件地址。 必须为有效的电子邮件格式。 缺少值或值为空将触发验证错误。
- **变量** （对象，可选） — 键值映射作为`UnstructuredArray`插入到模板中。

  如果不使用变量，请传递一个空对象或忽略该对象。 在电子邮件模板正文和主题中，使用变量语法引用变量，例如`var order_id`。 主题还支持[支持的模板方案](#supported-template-scenarios)中描述的相同自定义变量和语法。

### 成功响应(HTTP 200)

成功发送时，API返回HTTP 200。

### 错误响应

- **HTTP 400 — 验证错误**

  集成必须为每个请求提供有效的`templateId`和`recipientEmail`。

   - `"message": "Invalid recipient email format"` — 收件人地址无效或格式不正确
   - `"message": "Recipient email is required."` — 缺失或为空`recipientEmail`
   - `"message": "Template ID must be a positive integer."` - `templateId`缺失、零或无效

- **HTTP 404 — 未找到模板**

  示例： `"message": "Email template with ID \"999\" does not exist."`

## 支持的模板方案

**电子邮件正文**&#x200B;和&#x200B;**模板主题**&#x200B;均支持以下模板功能：

>[!NOTE]
>
>模板主题还支持自定义变量。 按照以下部分所述，使用`var variableName`和其他语法。

- **Include指令** — 包含其他设计模板，如电子邮件标头。

  ```javascript
  {{template config_path="design/email/header_template"}}
  ```

- **简单变量** — 使用`var variableName`，例如`var order_id`或`var g`。

  ```javascript
  {{var order.test}}
  {{var g}}
  {{var order_id}}
  ```

- **嵌套/点表示法** — 对于在请求`variables`中传递的嵌套键，在翻译中使用带有美元前缀的名称，如`$order_data.customer_name`、`$order.increment_id`或`$order_data.frontend_status_label`。

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **翻译(trans)** — 参数化文本、带多个占位符的多行翻译和HTML标记。

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **原始输出** — 当翻译的内容或变量内容包含HTML（例如，`|raw`或`<strong>`）时，请使用`<a>`筛选器。

  ```javascript
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **URL帮助程序** — 用于存储翻译中的URL。

  ```javascript
  {{trans 'You can check the status of your order by [logging into your account](%account_url).' account_url=$this.getUrl($store,'customer/account/',[_nosid:1]) |raw}}
  ```
