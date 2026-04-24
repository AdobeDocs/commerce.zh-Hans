---
title: 投放评估扩展教程
description: 了解如何使用App Builder、Edge Delivery Services和人工智能辅助开发工具为Adobe Commerce as a Cloud Service构建投放日期估计扩展。
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '3398'
ht-degree: 0%

---

# 投放估计扩展教程

本教程将指导您使用[!DNL Adobe App Builder]、[!DNL Edge Delivery Services]和AI辅助开发工具为[!DNL Adobe Commerce as a Cloud Service]构建投放日期估计扩展。 该扩展从外部API获取配送时间和配送日期估计值，并在店面中显示它们。

您可以构建两个部分：

- **App Builder扩展** — 包含外部投放估算API的后端 — 前端(BFF)操作、在结账时提供投放日期以丰富配送方式的webhook，以及用于管理设置而不需重新部署的管理UI配置页面。
- **Storefront集成** — 使用[!DNL Edge Delivery Services]放置组件和共享客户端模块显示在产品详细信息页面(PDP)、购物车页面和结账页面上的预计交付日期。

>[!NOTE]
>
>AI代理是不确定的。 本教程中的提示、问题和输出是示例。 您的代理可能会提出不同的问题、要求或体系结构建议。 使用本教程中的示例引导代理获得相似的结果。

在开始之前，请完成[先决条件](./tutorial-prerequisites.md)。 本教程使用&#x200B;**签出入门工具包**。 验证是否已克隆该扩展，并完成先决条件页面上描述的设置步骤。

## 验证先决条件

验证是否安装了以下必备组件：

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

如果前面的任何命令未返回预期结果，请参阅[先决条件](./tutorial-prerequisites.md)获取指导。

此外，请验证以下各项：

- 您有一个包含产品数据的[!DNL Adobe Commerce as a Cloud Service]实例。 查看[Commerce Cloud服务实例](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}。
- 您有一个店面项目连接到您的[!DNL Commerce]实例。 如果没有店面，请按照[创建店面](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}中的步骤操作。
- 已安装`aem` CLI：

  ```bash
  npm install -g @adobe/aem-cli
  ```

- 您有&#x200B;**购物者帐户** — [!DNL Commerce]中的注册客户，已保存默认送货地址。 PDP和购物车页面上的投放估计值仅向已登录的购物者显示。 结账显示所有购物者的估计值，而不管身份验证状态如何。

>[!IMPORTANT]
>
>本教程使用&#x200B;**签出入门工具包**（不是集成入门工具包）。 Checkout Starter Kit为付款、运费、税费和活动提供了基于webhook的可扩展性。 确保从签出工具包中引导。

## 设置模拟投放估算API

该扩展会调用外部投放估算API来获取装运日期和时间估算。 在本教程中，您将使用模拟API，这样您就可以在没有实际运营商帐户的情况下运行完整流程。 提供了两个选项：

- **选项A：Pipedream工作流** — 免费套餐，快速设置，但有每月调用限制。
- **选项B： App Builder运行时操作** — 在后端开发步骤期间没有创建外部依赖项。

>[!TIP]
>
>在开发期间，如果您达到自由层调用配额，则可以从Pipedream（选项A）开始并切换到运行时操作（选项B）。 这两个选项均实施相同的API合同。

### API规范

模拟API接受POST请求并返回交货日期估计值（包括承运人、运输天数、截止时间和最佳估计值）。

**请求正文** （模拟的所有字段都是可选的）：

```json
{
  "origin": { "country_code": "US", "postal_code": "90210", "city": "Beverly Hills" },
  "destination": { "country_code": "US", "postal_code": "10001", "city": "New York" },
  "ship_date": "2026-03-10",
  "carriers": ["standard", "express"],
  "service_levels": ["standard", "express"]
}
```

**响应(200 OK)：**

```json
{
  "estimates": [
    {
      "carrier_code": "standard",
      "service_code": "ground",
      "delivery_date": "2026-03-14",
      "safe_delivery_date": "2026-03-15",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-10T17:00:00.000Z"
    },
    {
      "carrier_code": "express",
      "service_code": "2day",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-12",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-10T12:00:00.000Z"
    }
  ],
  "best_estimation": { "carrier_code": "express", "delivery_date": "2026-03-12", "transit_days": 2 }
}
```

**错误响应：** 401 （缺少/无效的API密钥）、400 （无效的`ship_date`格式）、503（模拟停机时间）。

### 设置模拟

>[!BEGINTABS]

>[!TAB Pipedream工作流]

Pipedream选项使用持有者令牌身份验证并接受对工作流触发器URL的POST请求。

| 项目 | 描述 |
|------|-------------|
| 基本URL | 完整的Pipedream工作流触发器URL（例如`https://<id>.m.pipedream.net`） |
| 身份验证 | `Authorization: Bearer <API_KEY>` |
| 方法 | POST |

{style="table-layout:auto"}

**创建工作流：**

1. 在[Pipedream](https://pipedream.com){target="_blank"} (**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**)中创建新工作流。

1. 添加为POST配置的&#x200B;**HTTP / Webhook**&#x200B;触发器。 Pipedream分配webhook URL。

1. 添加&#x200B;**运行Node.js代码**&#x200B;步骤并粘贴以下处理程序代码：

   ```javascript
   const DEFAULT_CARRIERS = [
     { carrier_code: "standard", service_code: "ground", transit_days: 4 },
     { carrier_code: "express", service_code: "2day", transit_days: 2 },
     { carrier_code: "priority", service_code: "overnight", transit_days: 1 },
   ];
   
   const ISO_DATE = /^\d{4}-\d{2}-\d{2}$/;
   
   function parseShipDate(shipDate) {
     if (shipDate == null || typeof shipDate !== "string") return null;
     if (!ISO_DATE.test(shipDate)) return null;
     const d = new Date(shipDate + "T12:00:00.000Z");
     if (Number.isNaN(d.getTime())) return null;
     return shipDate;
   }
   
   function addBusinessDays(isoDate, days) {
     const d = new Date(isoDate + "T12:00:00.000Z");
     let added = 0;
     while (added < days) {
       d.setUTCDate(d.getUTCDate() + 1);
       const dow = d.getUTCDay();
       if (dow !== 0 && dow !== 6) added += 1;
     }
     return d.toISOString().slice(0, 10);
   }
   
   function cutoffUtc(isoDate, hour = 17) {
     return `${isoDate}T${String(hour).padStart(2, "0")}:00:00.000Z`;
   }
   
   function getBearerToken(headers) {
     const auth = headers?.Authorization ?? headers?.authorization ?? "";
     if (typeof auth !== "string" || !auth.startsWith("Bearer ")) return null;
     return auth.slice(7).trim() || null;
   }
   
   function handleDeliveryEstimate(body) {
     const shipDate = parseShipDate(body?.ship_date);
     const baseDate = shipDate ?? new Date().toISOString().slice(0, 10);
     let carriers = DEFAULT_CARRIERS;
     if (Array.isArray(body?.carriers) && body.carriers.length > 0) {
       const set = new Set(body.carriers.map((c) => String(c).toLowerCase()));
       carriers = DEFAULT_CARRIERS.filter((c) => set.has(c.carrier_code.toLowerCase()));
     }
     if (Array.isArray(body?.service_levels) && body.service_levels.length > 0) {
       const set = new Set(body.service_levels.map((s) => String(s).toLowerCase()));
       carriers = carriers.filter(
         (c) => set.has(c.service_code.toLowerCase()) || set.has(c.carrier_code.toLowerCase())
       );
     }
     if (carriers.length === 0) {
       return { status: 200, body: { estimates: [], best_estimation: null } };
     }
     const estimates = carriers.map((c) => {
       const delivery_date = addBusinessDays(baseDate, c.transit_days);
       const safe_delivery_date = addBusinessDays(baseDate, c.transit_days + 1);
       const cutoff_datetime_utc = cutoffUtc(baseDate, 17 - c.transit_days);
       return {
         carrier_code: c.carrier_code,
         service_code: c.service_code,
         delivery_date,
         safe_delivery_date,
         transit_days: c.transit_days,
         cutoff_datetime_utc,
       };
     });
     return { status: 200, body: { estimates, best_estimation: estimates[0] } };
   }
   
   export default defineComponent({
     async run({ steps, $ }) {
       const event = steps.trigger?.event ?? steps.trigger ?? {};
       const body = event.body ?? {};
       const headers = event.headers ?? {};
       const auth = getBearerToken(headers);
       const expectedKey =
         (typeof process.env.MOCK_API_KEY === "string" && process.env.MOCK_API_KEY.trim()) || null;
       if (expectedKey && (!auth || auth !== expectedKey)) {
         await $.respond({
           immediate: true,
           status: 401,
           headers: { "Content-Type": "application/json" },
           body: { error: "unauthorized", message: "Missing or invalid API key." },
         });
         return;
       }
       if (body?.ship_date != null && !parseShipDate(body.ship_date)) {
         await $.respond({
           immediate: true,
           status: 400,
           headers: { "Content-Type": "application/json" },
           body: { error: "bad_request", message: "Invalid ship_date; use YYYY-MM-DD." },
         });
         return;
       }
       const { status, body: responseBody } = handleDeliveryEstimate(body);
       await $.respond({
         immediate: true,
         status,
         headers: { "Content-Type": "application/json" },
         body: responseBody,
       });
     },
   });
   ```

1. （可选）在工作流设置中添加`MOCK_API_KEY`环境变量以强制实施持有者令牌身份验证。 如果未设置，则接受任何请求。

1. 部署工作流。

   您的端点是webhook触发器URL。

**测试模拟：**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB App Builder运行时操作]

App Builder Runtime action选项将模拟部署为同一[!DNL App Builder]项目中的Runtime操作。 此方法没有外部依赖性和调用配额。

提示代理创建模拟操作：

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- Add it to a separate package
- Use the code in docs/pipedream as inspiration
```

代理使用与Pipedream选项相同的API协定创建`actions/mock-delivery-api/index.js`。 部署后，端点为：

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

已针对`.env`中的`MOCK_API_KEY`环境变量验证身份验证。

>[!ENDTABS]

## 扩展开发

此部分将指导您完成投放估算扩展的[!DNL App Builder]后端的开发。 后端提供三个操作：

| 操作 | 类型 | 用途 |
|--------|------|---------|
| `delivery-estimates` | 独立Web操作 | 店面的BFF — 在交付日期使用PDP和购物车呼叫此项 |
| `shipping-methods` | Webhook操作 | 在结账时按交货日期`additional_data`扩充运费 |
| `delivery-estimates-config` | 管理员后端操作 | `aio-lib-state`中存储的配置的CRUD |

{style="table-layout:auto"}

1. 从编码代理中的MCP设置中，验证`commerce-extensibility`工具集是否已启用，并且没有错误。

   例如，在光标中，转到&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**。

   如果看到错误，请关闭和打开工具集。

   >[!NOTE]
   >
   >使用人工智能辅助开发工具时，预期代码和代理生成的响应会发生自然变化。
   >如果您遇到任何代码问题，请要求代理帮助您对其进行调试。

1. 如果有任何文档添加到光标上下文中，请禁用它。

   导航到&#x200B;**[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]**&#x200B;并删除列出的任何文档。

### 步骤1：提供初始提示

为代理提供上下文的外部API规范并提示其开始。 告诉代理停止操作并提问可帮助您尽早指导实施。

在座席的聊天窗口中输入以下提示：

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date and time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
Implement this feature by using the skills in this workspace for backend code, and a separate workspace with storefront skills. For this extension, focus on the backend skills and create an API_SPEC to hand work over to the storefront skills.

STOP and ask me clarifying questions about the requirements before you do any work.
```

>[!TIP]
>
>在提示中引用外部API规范文件(`@docs/API_SPEC.md`)可为代理提供有关第三方API合同的具体上下文。 代理将使用此字段来设计BFF操作、共享HTTP客户端以及管理员UI配置字段。 让代理停止操作并提问会触发引导式工作流，并帮助您尽早指导实施。

### 第2步：回答座席的问题

代理返回时提供一系列澄清问题，涵盖目标环境（PaaS与SaaS）、范围（独立BFF操作、webhook扩充或两者）、源地址源、缓存策略和测试偏好设置等主题。 以下示例显示了典型的问题和答案。 您的代理可能会问不同的问题，但主题通常相同。

**代理问题示例：**

1. **Target环境** — 您是为PaaS（内部部署）还是SaaS(Adobe Commerce as a Cloud Service)构建？
2. **范围** — 这应该是一个独立的BFF操作（店面直接调用它）、webhook扩充（在结账时扩展配送方式）还是同时使用两者？
3. **管理员可配置性** — 是否应通过Commerce Admin配置API URL、API密钥和源地址等设置，或将其存储在`.env`中？
4. **来源地址** — 发货地址（仓库）来自何处？ 它应该是静态配置还是动态解析的？
5. **缓存** — 是否应在服务器端缓存投放估算，以减少对外部API的调用？ 如果是，什么TTL？

**示例答案：**

```shell-session
Clarifications:
1. Let's build for SaaS
2. Let's do this:
(A) Can the PDP/cart call the 3rd party API directly — or are there any benefits of wrapping this call with a runtime action?
(B) Let's use the shipping-methods webhook
3. Let's use a Single-page application (SPA) that uses the Admin UI SDK to integrate with the admin. Since we are adding this config screen, let's make anything else that makes sense configurable to avoid redeployments when changing settings
4. Static configuration — origin address should be configurable in the Admin UI (e.g. warehouse address)
5. Yes, cache on the server side; suggest a TTL (e.g. 30 minutes) and make it configurable in the Admin UI
```

>[!TIP]
>
>询问代理是应直接调用第三方API还是通过运行时操作会触发有用的架构讨论。 代理解释了BFF（前端后端）模式的好处：API密钥保留在服务器端，CORS得到处理，缓存得到集中化，并且您获得供应商抽象。 询问管理员UI可配置性会促使代理将所有设置存储在`aio-lib-state`中，而不是`.env`中，从而消除更改设置时的重新部署。

>[!NOTE]
>
>您的代理可能会问不同的问题。 使用这些答案作为指导，引导代理实现相同的功能结果：店面调用的BFF操作、用于扩充签出的配送方式webhook，以及在`aio-lib-state`中存储设置的管理UI配置页面。

### 第3步：审查要求和体系结构

代理程序会生成需求和体系结构文档供您审查。 验证要求与您提供的答案是否匹配，以及体系结构是否涵盖：

- **BFF操作** (`delivery-estimates`) — 店面从PDP和购物车页面调用的独立Web操作。 它从`aio-lib-state`中读取配置，调用外部投放估算API，并返回格式化的估算。
- **webhook操作** (`shipping-methods`) — 在结账期间通过交货日期`additional_data`提高运费。 使用`plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` webhook方法。
- **管理员配置操作** (`delivery-estimates-config`) — 存储在`aio-lib-state`中的配置（API URL、API密钥、源地址、运营商、缓存TTL）的CRUD。
- **共享库** — 外部API的HTTP客户端和用于读取和写入`aio-lib-state`的配置模块。

>[!NOTE]
>
>AI代理是不确定的，其行为因模型和IDE而异。 您可能会收到一组不同的问题，这些问题会产生一组不同的要求和体系结构。 如果是这样的话，在继续之前，请尝试将代理引导到某个方向，以便该实施与本教程中介绍的内容非常匹配。

### 步骤4：选择实施计划

该代理为您提供了创建详细实施计划或完成直接实施的选项。

- 如果希望可复查计划能够以更多控制分阶段执行，请选择第一个选项。
- 如果您希望代理以最小的干预完成整个实施，请选择第二个选项。

### 步骤5：清理和部署

代理完成实施后，将进行清理。 由于仅使用Shipping域，因此代理会删除未使用的基架：

- 付款操作和配置(`validate-payment/`， `filter-payment/`， `payment-methods.yaml`)
- 税务操作和配置(`collect-taxes/`、`collect-adjustment-taxes/`、`tax-integrations.yaml`)
- 事件操作和配置(`commerce-events/`， `3rd-party-events/`， `events.config.yaml`)
- 通用基架(`generic/`)
- 其他域中的管理员UI SPA组件（例如，与税相关的页面和挂钩）
- 未使用的脚本、测试文件和环境变量

>[!TIP]
>
>要求代理同时在Admin UI SPA中检查来自其他域的残留内容。 “税类”页面及其挂钩可能仍然存在于入门套件基架中，需要移除。

清理后，请按照以下顺序&#x200B;**使用这些步骤**&#x200B;进行部署：

```bash
# 1. Copy env template and fill in credentials.
cp env.dist .env

# 2. Select your App Builder workspace.
aio app use --merge

# 3. Sync OAuth credentials from workspace.
npm run sync-oauth-credentials

# 4. Deploy the extension.
aio app deploy

# 5. Register shipping carriers in Commerce.
npm run create-shipping-carriers
```

>[!IMPORTANT]
>
>请勿跳过或重新排序这些步骤。 步骤1至3是部署的先决条件。 如果未配置凭据，`aio app deploy`命令将失败。

### 步骤6：配置webhook和管理UI

部署后，配置送货webhook。 代理可以创建以编程方式订阅的脚本：

```bash
npm run subscribe-webhook
```

此命令使用以下设置订阅shipping webhook：

| 字段 | 值 |
|-------|-------|
| Webhook方法 | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Webhook类型 | `after` |
| 必填 | 可选（允许回退到默认装运） |
| 超时 | 5000毫秒 |

{style="table-layout:auto"}

>[!NOTE]
>
>对于SaaS，webhook方法名称从路径中删除`magento.`。 PaaS的webhook名称为`plugin.magento.out_of_process_shipping_methods...`，而SaaS的webhook名称为`plugin.out_of_process_shipping_methods...`。

接下来，配置管理员UI：

1. 启用&#x200B;**Admin UI SDK** (**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL Admin UI SDK]** > **[!UICONTROL Enable]** > **[!UICONTROL Yes]**)。

1. 通过选择您的[!DNL App Builder]工作区和扩展来配置扩展。

1. 单击&#x200B;**[!UICONTROL Refresh registrations]**。

1. 在[!DNL Admin]侧边栏中导航到&#x200B;**[!UICONTROL Apps]** > **[!UICONTROL Delivery Estimates]**。

1. 通过启用该功能并指定所需的设置（包括API URL和API密钥、源地址、默认运营商、缓存TTL以及运营商代码映射）来完成配置。

### 步骤7：测试扩展

直接测试投放估算BFF操作：

```bash
curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-runtime-url>/api/v1/web/commerce-checkout-starter-kit/delivery-estimates" | jq .
```

响应应类似于：

```json
{
  "estimates": [
    {
      "carrier": "standard",
      "service_level": "ground",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-13",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-06T18:00:00Z"
    },
    {
      "carrier": "express",
      "service_level": "2day",
      "delivery_date": "2026-03-10",
      "safe_delivery_date": "2026-03-10",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-06T20:00:00Z"
    }
  ],
  "best_estimation": {
    "carrier": "express",
    "delivery_date": "2026-03-10",
    "transit_days": 2
  }
}
```

### 创建服务合同

现在，后端已完成，请要求代理为店面工作创建服务合同：

```shell-session
Produce a spec called STOREFRONT_API_SPEC that I can use in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

代理生成`docs/STOREFRONT_API_SPEC.md`时具有完整的BFF终结点协定（请求和响应格式、示例负载、错误处理）以及店面工作区的现成提示。

在开始店面开发步骤之前，将此文件复制到您的店面项目中。

>[!TIP]
>
>让代理同时生成另一个工作区的服务协定&#x200B;**和**&#x200B;的提示可确保后端和店面团队（或代理）之间的干净切换。 店面代理可以立即开始工作，而无需询问有关API的问题。

## 连接到店面

此部分将指导您使用[!DNL Edge Delivery Services]和AI辅助开发工具实施投放估算扩展的店面部分。 将估计投放日期添加到PDP、购物车页面和结账页面。

>[!NOTE]
>
>提供的提示是起点。 虽然您可以不修改这些模板就加以使用，但可以考虑与代理进行自然对话。
>
>在使用人工智能辅助开发工具时，代理生成的代码和响应始终存在自然变化。
>
>如果您遇到任何代码问题，请要求代理帮助您对其进行调试。

### 店面先决条件

在开始店面集成之前，请验证您是否具备以下条件：

- 店面项目已连接到您的[!DNL Commerce]实例
- 使用CLI安装的Commerce storefront AI工具[&#128279;](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- 已将`STOREFRONT_API_SPEC.md`文件复制到店面项目的`docs/`文件夹中

### 步骤1：验证环境

打开`config.json`文件并验证`commerce-core-endpoint`和`commerce-endpoint`的值是否指向您的[!DNL Adobe Commerce as a Cloud Service] GraphQL终结点。

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### 第2步：提供初始提示

由于服务合同已存在于您的项目中，请提示代理实施店面集成。 使用&#x200B;**计划**&#x200B;模式（如果代理中可用），以防止代理在没有计划的情况下继续。

```shell-session
I need to implement delivery date estimates on the storefront for an Adobe Commerce (SaaS) store using Edge Delivery Services with storefront drop-ins. The backend is already built and deployed as an App Builder extension.

The full integration contract is in the `docs/STOREFRONT_API_SPEC.md` file— please read it first. It covers two integration points:

PDP and Cart pages — Call the delivery-estimates BFF action (HTTP POST) to fetch estimates for a destination and display the best delivery date.

Checkout shipping step — Delivery dates are already injected into each shipping method's `additional_data` by a webhook. No API call is needed. Just read `additional_data` from the shipping methods and display the delivery date next to each option.

Requirements:
- Show "Get it by [date]" on PDP using best_estimation.delivery_date
- Show a delivery date range on the cart page using delivery_date / safe_delivery_date
- Show delivery dates next to each shipping method at checkout, reading from additional_data
- Show "Order within X hours" countdown using cutoff_datetime_utc where appropriate
- Cache estimates client-side in sessionStorage to avoid redundant calls
- Never block the purchase flow — if estimates are unavailable, hide the UI silently

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>提示是详细的，因为后端代理已经提供了完整的API合同。 通过引用`@docs/STOREFRONT_API_SPEC.md`，代理可以知道确切的端点URL、请求和响应格式以及错误处理。 明确的要求列表会阻止代理创建范围。 具体而言，请求计划模式会触发分阶段工作流，帮助您尽早指导实施。

### 步骤3：回答澄清问题

代理返回有关身份验证范围、签出方法和样式的问题。 以下示例显示了典型的问题和答案。

**代理问题示例：**

1. **匿名与已登录的用户** — 应在PDP和购物车页面上为所有购物者显示估价，还是只显示所有经过身份验证的购物者？
2. **签出方法** — ShippingMethods放置容器未公开`additional_data`，因此代理建议两个选项：
   - **选项A：**&#x200B;在结账和DOM插入投放日期时调用BFF（更简单，与PDP/购物车一致）
   - **选项B：**&#x200B;通过`overrideGQLOperations`扩展签出GraphQL片段以包含`additional_data`
3. **样式** — 表情符号与现有设计令牌

**示例答案：**

```shell-session
1. Only for logged-in users — that way we can use the shopper's default shipping address and avoid a zip code input
2. Let's do Option A if feasible
3. Use anything that matches the current styling
```

>[!TIP]
>
>只显示登录购物者的估价是一个务实的选择。 代理可以自动（通过GraphQL）使用购物者的默认送货地址，因此无需输入邮政编码。 PDP和Cart上的匿名购物者需要输入邮政编码，这增加了摩擦。 在结账时，所有购物者都会看到交货日期，因为运输地址已输入。

>[!NOTE]
>
>您的代理可能会问不同的问题。 请将这些答案用作指导：
>
>- 仅显示已登录购物者的PDP和购物车估计值（无需输入邮政编码）。
>- 为了进行结账，请使用选项A（BFF调用+ DOM注入）来进行简化。
>- 使用现有设计令牌进行样式设置。

### 第4步：审查要求和体系结构

该代理设计共享模块体系结构。 验证它是否涵盖：

| 组件 | 用途 |
|-----------|---------|
| `scripts/delivery-estimates.js` | 共享模块 — BFF客户端、缓存（sessionStorage，30分钟TTL）、日期格式、倒计时逻辑、客户地址查找、运营商映射 |
| PDP集成 | 显示“在[日期]前获取”，在价格和描述之间可选择倒计时 |
| 购物车集成 | 在订单摘要上方的右栏中显示日期范围（“星期四，3月12日 — 星期五，3月13日”） |
| 签出集成 | 在配送步骤处于活动状态时呼叫BFF，DOM通过`MutationObserver`注入交货日期 |

{style="table-layout:auto"}

要验证的关键设计决策：

- 所有BFF调用均无阻塞 — 页面首先呈现，估计值异步显示。
- 所有失败都是静默的 — 仅`console.debug`，没有面向购物者的错误。
- `CARRIER_MAP`将Commerce运营商代码(DPS、Fedex)映射到BFF运营商代码（标准、快速）。
- 动态`import()`将投放模块保留在关键渲染路径之外。

>[!NOTE]
>
>AI代理是不确定的，其行为因模型和IDE而异。 您可能会收到一组不同的问题，这些问题会产生一组不同的要求和体系结构。 如果是这样的话，在继续之前，请尝试将代理引导到某个方向，以便该实施与本教程中介绍的内容非常匹配。

### 步骤5：选择实施计划

该代理为您提供了创建详细实施计划或完成直接实施的选项。

- 如果希望可复查计划能够以更多控制分阶段执行，请选择第一个选项。
- 如果您希望代理以最小的干预完成整个实施，请选择第二个选项。

在实施过程中，代理会创建和修改以下文件：

**新文件：**

- `scripts/delivery-estimates.js` — 已与`fetchDeliveryEstimates()`、`getCustomerShippingAddress()`、`formatDeliveryDate()`、`buildCountdownText()`、`findEstimateForCarrier()`共享模块

**修改的文件：**

- `blocks/product-details/product-details.js` + `.css` — 右列的投放估算div，主渲染后异步获取
- `blocks/commerce-cart/commerce-cart.js` + `.css` — 交货预估div高于订单摘要
- 装运方法标签基于`blocks/commerce-checkout/commerce-checkout.js`、`containers.js`、`.css` — `MutationObserver`的DOM注入

观察生成的代码并提问或根据需要重定向代理。

### 步骤6：启动服务器并测试

代理完成实施后，启动开发服务器并测试投放估计值。

1. 启动本地开发服务器：

   ```bash
   npm run start
   ```

1. 在浏览器中，登录到您的购物者帐户。

   PDP和Cart上的估计投放需要具有已保存默认送货地址的经过身份验证的会话。

1. 导航到产品页面，并验证以下结果：

   | 页面 | 预期结果 | 需要身份验证 |
   |------|-----------------|---------------|
   | PDP | “3月12日星期四前收到”，带有可选的倒数计时 | 是（仅登录） |
   | 购物车 | “预计交付时间：3月12日星期四至3月13日星期五” | 是（仅登录） |
   | 结帐 | 按配送方式“预计交货时间：3月12日星期四” | 否（结帐时输入的地址） |

   {style="table-layout:auto"}

>[!NOTE]
>
>没有匹配承运人的发运方法（例如，统一费率）不显示估计值。 这是特意设计的 — 只有`CARRIER_MAP`中映射的运营商才能获取交货日期。

您可以手动测试或要求代理使用其浏览器功能为您进行测试：

```shell-session
Run complete browser testing using the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### 步骤7：清理

跳过或完成测试后，代理会提示您继续清理。 确认后，代理将存档实施期间生成的任何文档工件。

## 故障排除

如果在教程中遇到问题，请使用以下提示。

### 后端(App Builder)

| 症状 | 原因 | 修复 |
|---------|-------|-----|
| 管理员UI配置操作返回了`400 Bad Request`和“请求定义了不允许的参数（保留的属性）” | 前端挂接正在请求正文中发送`__ow_method`。 以`__ow_`为前缀的属性由OpenWhisk保留，当操作具有`final: true`时拒绝。 | 发送自定义`method`属性而不是`__ow_method`。 后端操作首先读取`params.method`，然后回退到`params.__ow_method`（运行时自动提供）。 |
| `aio app deploy`失败，“productDependencies中需要maxVersion” | CLI验证需要`app.config.yaml`产品依赖项中的`minVersion`和`maxVersion`。 | 向`app.config.yaml`中的每个`productDependencies`条目添加一个`maxVersion`值。 |
| 部署命令失败 | 未在部署之前配置凭据。 必须先进行`.env`、工作区选择和OAuth同步。 | 请遵循正确的顺序： `cp env.dist .env` > `aio app use --merge` > `npm run sync-oauth-credentials` > `aio app deploy`。 |

{style="table-layout:auto"}

### 店面(Edge Delivery Services)

| 症状 | 原因 | 修复 |
|---------|-------|-----|
| 登录购物者未出现PDP投放估计 | PDP块未初始化`account`放置项，因此`getCustomerAddress()`静默失败，并且未获取任何估计值。 | 直接使用`CORE_FETCH_GRAPHQL.fetchGraphQl()`查询购物者地址，而不是依赖帐户放置区API。 这适用于任何页面。 |
| 修复GraphQL后PDP仍不显示 | 使用了方法名称`CORE_FETCH_GRAPHQL.fetch()`中的拼写错误而不是`CORE_FETCH_GRAPHQL.fetchGraphQl()`。 | 使用正确的方法名称： `fetchGraphQl` （大写Q，小写l）。 |
| 首次加载时未显示签出投放日期 | `checkout/updated`事件侦听器在`checkout/initialized`触发后注册，因此缺少初始数据。 | 添加具有`{ eager: true }`的`checkout/initialized`侦听器，以捕获注册之前发出的事件。 保留`checkout/updated`侦听器以进行后续更改。 |
| 未显示购物车投放评估 | `block.appendChild(fragment)`将所有子项移出片段，因此`fragment.querySelector('.cart__delivery-estimate')`返回null。 | 在附加操作后从`block`而不是`fragment`进行查询。 |
| 统一费率配送在结账时未显示交货日期 | 按设计 — `CARRIER_MAP`仅将DPS映射到标准，并将Fedex映射到表示。 统一速率在外部API中没有对应的载体。 | 不是错误。 要添加其他运营商的估计值，请扩展`scripts/delivery-estimates.js`中的`CARRIER_MAP`并在后端扩展中配置该运营商。 |

{style="table-layout:auto"}

### Commerce SaaS沙盒

| 症状 | 原因 | 修复 |
|---------|-------|-----|
| Webhook返回`429 Too Many Requests` | [!DNL App Builder]工作区处于调试模式，该模式具有严格的每分钟速率限制。 [!DNL Commerce]在结账期间频繁地重新计算运费，从而耗尽配额。 | 部署到生产工作区（`aio app use`以切换，然后`aio app deploy`）。 生产工作区没有调试速率限制。 |
| Webhook软超时警告（>1000毫秒） | shipping-methods webhook操作花费的时间超过[!DNL Commerce] 1000毫秒软超时。 | 在`aio-lib-state`中更积极地启用服务器端缓存，或者在[!DNL Commerce Admin]中增加webhook超时（Commerce Webhooks配置）。 |

{style="table-layout:auto"}

## 教程回顾

以下是本教程涵盖的主题摘要：

- **模拟API设置：**&#x200B;使用Pipedream或[!DNL App Builder]运行时操作创建模拟投放估算API。
- **BFF模式：**&#x200B;正在生成一个封装外部API、保留凭据服务器端并集中缓存的后端for-frontend操作。
- **Webhook扩充：**&#x200B;扩展配送方式webhook以在结账时将交货日期注入每个配送选项。
- **管理员UI可配置性：**&#x200B;使用[!DNL Admin UI SDK]添加配置页面，以便商家无需重新部署即可管理API设置、源地址和运营商映射。
- **服务合同：**&#x200B;正在创建桥接后端扩展和店面实施的API合同。
- **店面集成：**&#x200B;使用共享客户端模块在PDP（“获取方式”）、购物车（日期范围）和结账（每种配送方式）上显示预计投放。
- **非阻塞UX：**&#x200B;确保投放估算从不阻止购买流程 — 页面首先呈现，估算异步显示。

## 后续步骤

使用以下建议来扩展您的投放估计服务：

- **连接实际运营商API：**&#x200B;通过更改[!DNL Admin UI]中的服务URL和API密钥，将模型替换为UPS、FedEx或USPS等实时送货API。
- **支持匿名购物者：**&#x200B;在PDP和购物车页面上添加邮政编码输入，以便未登录的购物者也可以看到估计送达次数。
- **扩展运营商映射：**&#x200B;将更多运营商代码添加到`CARRIER_MAP`以显示其他配送方法的交货日期。
- **添加服务器端缓存：**&#x200B;在BFF操作中实施`aio-lib-state`缓存，以减少对重复源与目标对的外部API的调用。
- **在订单确认中显示预计：**&#x200B;在订单确认页面和事务性电子邮件中显示预计的交货日期。
