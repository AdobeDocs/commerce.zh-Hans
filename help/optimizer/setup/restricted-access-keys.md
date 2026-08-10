---
title: 访问密钥受限
description: 了解如何创建、分配和旋转受限访问密钥，以使用签名令牌身份验证保护 [!DNL Adobe Commerce Optimizer] 中的目录视图。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="仅限SaaS" type="Positive" url="https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/product-solutions" tooltip="仅适用于Adobe Commerce as a Cloud Service和 [!DNL Adobe Commerce Optimizer] 项目（Adobe管理的SaaS基础架构）。"
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 688bc6e28a4c5a94b1fe55c84f7c05401dd651bc
workflow-type: tm+mt
source-wordcount: 791
ht-degree: 0%

---

# 受限访问密钥

受限访问密钥允许授权客户端应用程序访问[专用目录视图](catalog-view.md) — 只有携带分配密钥中的有效签名令牌的请求才能检索目录数据。 所有其他请求都将被拒绝，包括来自匿名购物者的请求、未明确获得此目录视图访问权限的购物者请求，以及探究API的脚本。

## 受限访问关键用例

在[!DNL Adobe Commerce Optimizer]中，**[!UICONTROL Price Book ID]**&#x200B;确定请求能够查看的价格 — 它涉及定价，而不是谁能发出请求。 任何知道目录视图ID和价格手册ID的客户端都可以通过促销API检索该数据。 受限访问密钥添加了一个单独的、互补的控制：它们限定了谁有权访问目录视图，这与适用的价格手册无关。

受限访问密钥通常用于：

- **基于合同的B2B定价** — 限制链接到协议价格手册的目录视图，以便只有适用它的买方可以查询它。 其他收购机构和公众则不能。
- **合作伙伴和经销商门户** — 将目录的子集限制为直接与促销API集成的已批准合作伙伴。
- **预发布预览** — 让受信任的内部或合作伙伴系统先预览即将发布的产品，然后再公开显示它们。

>[!IMPORTANT]
>
>目前，密钥生成、令牌签名和轮换完全由用于验证购物者的后端客户端应用程序管理。 [!DNL Adobe Commerce Optimizer]不代表您生成或旋转这些密钥。

## 受限访问密钥的工作方式

受限访问密钥是RSA密钥对的公共组件。 您的客户端应用程序生成并使用此密钥来证明它有权读取专用目录视图。 在此上下文中，“客户端应用程序”是指对购物者进行身份验证的后端系统（例如，[!DNL Adobe Commerce]上的自定义逻辑或第三方后端），而不是店面前端本身。

以下步骤描述了密钥对和签名令牌如何从创建移动到验证：

1. 您的客户端应用程序生成一个RSA密钥对并保留私钥。
1. 您在[!DNL Commerce Optimizer]中将&#x200B;**公共**&#x200B;密钥注册为受限访问密钥。
1. 您的客户端应用程序使用私钥对JSON Web令牌(JWT)进行签名，并将其包含在每个对私有目录视图的请求中。
1. [!DNL Commerce Optimizer]根据已注册公钥验证令牌的签名，如果有效，则返回所请求的目录数据。

## 创建受限访问密钥

对于私有目录视图的初始测试，请使用诸如[!DNL OpenSSL]之类的工具生成密钥对。 保持私钥机密 — 仅将公钥上传到[!DNL Commerce Optimizer]。

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

密钥大小必须介于2048和8192位之间。 `public-key.pem`包含您粘贴到以下&#x200B;**[!UICONTROL Public key]**&#x200B;字段中的值。

## 将受限访问密钥添加到[!DNL Commerce Optimizer]

1. 从[!DNL Adobe Commerce Optimizer Studio]的左侧菜单中，转到&#x200B;**[!UICONTROL Store setup]**，然后单击&#x200B;**[!UICONTROL Restricted access keys]**。

   ![受限访问密钥列表，使用“添加受限访问密钥”按钮](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. 单击&#x200B;**[!UICONTROL Add Restricted Access Key]**。

1. 输入键详细信息：

   ![添加受限访问密钥表单，其中包含“标题”、“过期日期”和“公钥”字段](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** — 用于标识键的标签，显示在键列表和目录视图键选取器中，例如`ACME Corp wholesale portal — Tier 1 pricing`。
   - **[!UICONTROL Expiration date]** — 停止接受密钥的日期和时间(UTC)，即使对于尚未过期的令牌也是如此。
   - **[!UICONTROL Public key]** — 主体公钥信息(SPKI)格式的PEM编码的RSA公钥，包括`-----BEGIN PUBLIC KEY-----`和`-----END PUBLIC KEY-----`标记。 在整个环境中必须是唯一的。

1. 单击&#x200B;**[!UICONTROL Save]**。

键在创建后不可更改。 要更改任何值，请删除键并创建新键。 请参阅[旋转密钥](#rotate-a-key)以在没有访问中断的情况下执行此操作。

## 将键分配给目录视图

限制访问密钥仅在将其分配给启用了&#x200B;**[!UICONTROL Catalog Protection]**&#x200B;的目录视图后才会限制访问。 有关设置步骤，请参阅[保护目录视图](private-catalog-view.md#protect-a-catalog-view)。

## 删除键

1. 在&#x200B;**[!UICONTROL Restricted access keys]**&#x200B;页面上，找到要删除的密钥，然后单击&#x200B;**[!UICONTROL Delete]**。

   如果该键被分配给一个或多个目录视图，则会出现警告，说明依赖该键的客户端应用程序将失去访问权限。 目录视图本身仍受到保护 — 它们不能公开访问。

1. 确认删除。

## 旋转键

要在没有访问中断的情况下旋转键，请注意，目录视图最多可以同时分配三个键：

1. 生成新的密钥对并将新的公钥添加为新的受限访问密钥。
1. 将新键与现有键一起分配给目录视图。
1. 开始使用新私钥签名新令牌以完成密钥滚存。
1. 在新密钥上确认所有客户端应用程序后，删除旧密钥。

## 限制

查看[目录视图和策略限制](../boundaries-limits.md#catalog-views-and-policies)。

## 更多此类内容

- [私有目录视图](private-catalog-view.md) — 了解如何使用受限制的访问密钥保护目录视图。

