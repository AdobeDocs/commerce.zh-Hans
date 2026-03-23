---
title: 以客户身份登录并具有一次性代码
description: 了解如何使用“作为客户OTC登录”功能为 [!DNL Adobe Commerce as a Cloud Service]中的客户身份验证生成一次性代码。
role: Admin
level: Intermediate
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和Adobe Commerce Optimizer项目（Adobe管理的SaaS基础架构）。"
source-git-commit: 2de1006ad3cee936d114bcf1b9a98b43a54d8c76
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# 客户登录

{{accs-sandbox-experimental}}

“以客户身份登录OTC（一次性代码）”功能允许管理员用户为客户生成短期的一次性代码。 此代码可以通过GraphQL交换客户访问令牌，从而支持无密码的&#x200B;**登录作为销售商辅助购物方案的客户**&#x200B;工作流。

作为客户登录包含以下组件：

* **管理员UI** — 在客户编辑页面上，管理员可以请求一次性代码(OTC)，而不是以客户身份直接登录。
* **REST API** - OTC生成的程序化端点，用于管理脚本和第三方集成。
* **GraphQL API** — 将OTC交换为店面或headless商务流的客户访问令牌的突变。

## 从管理员生成一次性代码

“以客户身份登录”OTC将客户编辑页面上的“以客户身份登录”标准按钮替换为&#x200B;[!UICONTROL **获取客户登录OTC**]&#x200B;按钮。 然后，生成的一次性代码可用于店面或GraphQL以进行卖方辅助购物。

>[!NOTE]
>
>“**以客户身份登录**”按钮在“订单”、“发票”、“装运”和“贷项通知单”页面上不可用。

### 先决条件

在将登录作为客户功能使用之前，您必须满足以下要求：

* **管理员权限** — 管理员用户必须在其管理员角色中启用`Magento_LoginAsCustomer::login`访问控制列表(ACL)权限，才能作为客户登录。

* **客户同意** — 客户必须将`login_as_customer_assistance_allowed`扩展属性设置为&#x200B;**2**。 可以在管理员的&#x200B;**编辑客户**&#x200B;页面上或通过GraphQL在创建或编辑客户时配置此项。

  在“编辑客户”页面上![客户同意扩展属性配置](./assets/customer-consent-attribute.png){width="600" zoomable="yes"}

* **启用“以客户扩展身份登录”** — 禁用“以客户扩展身份登录”功能时，该功能不可用。 要验证扩展是否已启用，请导航到&#x200B;[!UICONTROL **商店**] > [!UICONTROL **配置**] > [!UICONTROL **客户**] > [!UICONTROL **以客户身份登录**] > [!UICONTROL **启用扩展**]。

### 请求一次性代码(OTC)

1. 导航到&#x200B;[!UICONTROL **客户**]&#x200B;并选择客户以打开编辑页面。

1. 在“编辑客户”页面上，单击&#x200B;[!UICONTROL **获取客户登录OTC**]。

   在“编辑客户”页面上![获取客户登录OTC按钮](./assets/get-customer-login-otc-button.png){width="600" zoomable="yes"}

1. 输入&#x200B;[!UICONTROL **原因**]（必需），然后单击&#x200B;[!UICONTROL **请求**]。

   ![包含原因字段的OTC请求模式](./assets/otc-reason-modal.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >**原因**&#x200B;字段为必填项。 此变量将传递到OTP生成流程，并保留用于即将推出的审核和事件日志记录功能。

1. 生成的OTC将显示在模态中。 将此代码与`generateCustomerToken`或`exchangeOtpForCustomerToken`GraphQL突变一起使用，以获得客户授权。

   ![生成的OTC显示在模式窗口中](./assets/otc-generated-code.png){width="300" zoomable="yes"}

>[!IMPORTANT]
>
>默认情况下，生成的一次性代码OTC的有效期为30秒，并且在一次使用后失效。 可以通过提交[支持票证](https://experienceleague.adobe.com/home?lang=zh-Hans&support-tab=home#support)来配置TTL。

生成一次性代码后，您可以通过导航到店面并使用以下凭据登录来使用该代码：

* **电子邮件**：客户的电子邮件地址
* **密码**：生成的一次性代码(OTC)

## 使用REST API生成一次性代码

POST `V1/customer/:customerId/otp`端点提供了一种以编程方式为客户生成OTC的方法。 这对于需要以一致方式触发OTC颁发的管理员UI、脚本或第三方集成非常有用。

### REST合同

| 项目 | 值 |
|---|---|
| **方法** | POST |
| **URL** | `/rest/V1/customer/:customerId/otp` |
| **身份验证** | 管理令牌（持有者）。 所需的ACL： `Magento_LoginAsCustomer::login`。 |
| **请求正文** | 包含可选`reason`字段的JSON。 用于审核和日志记录。 |
| **成功响应** | HTTP 200，带有`otp`的JSON（32个字符的十六进制字符串）。 |
| **错误响应** | 标准Web API错误（例如，401、403）。 如果客户禁用了以客户协助身份登录，则可能会显示为500或映射的异常。 |

### 请求示例

```text
POST /rest/V1/customer/:customerId/otp
Content-Type: application/json
```

```json
{"reason": "Support session"}
```

### 响应示例

```json
{"otp": "a1b2c3d4e5f6789012345678abcdef01"}
```

## 使用GraphQL交换客户令牌的一次性代码

生成OTC后（从管理员UI或REST API），请使用以下GraphQL突变之一将其交换为客户访问令牌。

### `generateCustomerToken`突变

`generateCustomerToken(email, password)`突变返回客户令牌。 `password`参数的计算顺序如下：

1. **客户密码（默认）** — 客户的帐户密码。
1. **客户重置密码令牌（一次性使用）** - **忘记密码**&#x200B;中的有效令牌（例如，`requestPasswordResetEmail`突变）。 在首次使用时消耗。
1. **管理员生成的OTC（一次性代码）** — 管理员通过REST API或管理员UI为客户生成的代码。 一次性使用，短期使用（默认为30秒）。

**架构：**

```graphql
type Mutation {
  generateCustomerToken(email: String!, password: String!): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**示例：使用管理员OTC登录**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

变量（使用OTC作为`password`）：

```json
{
  "email": "customer@example.com",
  "password": "<admin-generated-OTC>"
}
```

**示例：使用密码登录**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

变量：

```json
{
  "email": "customer@example.com",
  "password": "CustomerPassword123"
}
```

**示例：使用密码重置令牌登录**

在客户请求重置密码（例如，`requestPasswordResetEmail`）后，通过电子邮件链接收到的重置令牌可在`password`（一次性使用）中用作`generateCustomerToken`。

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

变量（使用重置令牌作为`password`）：

```json
{
  "email": "customer@example.com",
  "password": "<reset-password-token-from-email-link>"
}
```

**示例响应：**

```json
{
  "data": {
    "generateCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### `exchangeOtpForCustomerToken`突变

`exchangeOtpForCustomerToken`突变将管理员生成的密码重置令牌或OTP交换为客户访问令牌。 成功交换（一次性使用）后，OTP失效。 此端点遵循reCAPTCHA配置。

**架构：**

```graphql
type Mutation {
  exchangeOtpForCustomerToken(
    email: String!
    otp: String!
  ): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**示例请求：**

```graphql
mutation ExchangeOtpForCustomerToken($email: String!, $otp: String!) {
  exchangeOtpForCustomerToken(email: $email, otp: $otp) {
    token
  }
}
```

变量：

```json
{
  "email": "customer@example.com",
  "otp": "<one-time-password>"
}
```

**示例响应：**

```json
{
  "data": {
    "exchangeOtpForCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### 突变摘要

| 变异 | 用例 |
|---|---|
| `generateCustomerToken(email, password)` | 单一入口点：客户密码、密码重置令牌、管理员OTC或OTP（在密码/重置后尝试）。 |
| `exchangeOtpForCustomerToken(email, otp)` | OTP或重置密码令牌交换。 OTP（或重置密码令牌）在使用后使用。 |

密码重置令牌和管理员OTC都作为`password`参数传递给`generateCustomerToken`。 解析器检测令牌类型并相应地验证。
