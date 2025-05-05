---
title: 测试和部署商店履行
description: 测试计划，以验证“商店履行”功能。 测试包括“库存同步API”、已取消订单的端到端履行工作流、“商店履行”应用程序用户管理以及“客户签入”体验。
role: User, Admin
level: Intermediate
feature: Shipping/Delivery, User Account, Roles/Permissions
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 0%

---

# 测试和部署Adobe Commerce商店履行

在开发环境中完成载入流程后，您可以启动该流程以测试存储履行解决方案并将其部署到生产环境。

**先决条件**

在测试或同步任何信息、存储或订单之前，请验证您已完成以下任务：

- 已完成存储履行服务的[常规配置](enable-general.md)。

- [添加并验证沙盒和生产环境的帐户凭据和连接详细信息](connect-set-up-service.md#configure-store-fulfillment-account-credentials)

- 确认Store Fulfillment解决方案的[Adobe Commerce集成](connect-set-up-service.md#configure-store-fulfillment-account-credentials)可用并已获得授权。

## 准备测试

在创建任何测试订单或执行集成测试之前，必须完成连接配置。 在测试之前，还必须验证存储区数据是否已同步。

1. 同步存储履行来源。

   - 转到&#x200B;**[!UICONTROL Stores > Sources]**。

   - 选择&#x200B;**[!UICONTROL Synchronize Store Fulfillment Sources]**。

1. 在创建测试订单之前，从商店网格中验证是否已将商店标记为`Synced`。

## 示例测试计划

零售商在部署的配置和测试阶段验证Store Fulfillment解决方案的基本功能。 此示例测试计划提供了测试的起点。 根据您的要求添加其他方案。

>[!NOTE]
>
>在完成Store Fulfillment解决方案的初始载入或更新现有安装后，始终在部署到生产环境之前在非生产环境中测试应用程序。

此测试计划示例包括以下功能区域：

| 功能区 | 函数 | 角色 |
|-------------------------------------|------------------------------------------|----------------------------------|
| 库存和订单同步 | 清单API同步 | Adobe Commerce管理员 |
| 端到端 | 订单取消工作流 | 客户、管理员、商店关联 |
| 管理员 | 商店履行应用程序权限 | 管理员 |
| Adobe Commerce前端 | 产品类型 | 客户、管理员 |
| 前端签出</br>签入表单 | 签到体验 | 客户、管理员 |
| 商店协助应用程序 | 订单</br>挑选</br>阶段</br>和移交 | 存储关联 |

### 清单API同步

测试计划的此部分涵盖库存和订单同步，以验证提货源和库存的更新是否在Adobe Commerce和“商店履行”解决方案之间正确同步。

**功能区**：库存和订单同步</br>
**角色：**&#x200B;管理员</br>
**测试类型：**&#x200B;全部为正

<table>
<thead>
<tr>
<th>函数</th>
<th>测试方案</th>
<th>预期结果</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>添加提货库存来源</strong></td>
<td>保存新的提货库存来源。</td>
<td>实时同步会在5分钟内将源详细信息发送到沃尔玛GIF服务。</td>
</tr>
<tr>
<td><strong>更新现有的提货库存来源</strong></td>
<td>将更新保存到现有的取车库来源。</td>
<td>实时同步操作会在5分钟内将详细信息发送到沃尔玛GIF</td>
</tr>
<tr>
<td><strong>取车库来源</br><code>Is Synced</code>状态</strong></td>
<td>将更新保存到现有的取车库来源。</td>
<td>成功操作后，“管理Source”页面的<code>Is Synced</code>列将从<code>No</code>更新为<code>Yes</code>。</td>
</tr>
<tr>
<td><strong>已修改的库存预留流程</strong></td>
<td>创建并提交产品的新订单。</td>
<td>产品的可销售数量会相应减少。</td>
</tr>
<tr>
<td><strong>新订单推送、API同步 — 客户订单</strong></td>
<td>客户提交商店取货订单。</td>
<td><ul><li>在“管理员订单”视图中，<strong>Adobe Commerce管理员用户</strong>看到订单同步状态更新为 <code>Sent</code></li><li>订单详细信息日志包含消息 <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>新订单推送、API同步 — 管理员提交订单</strong></td>
<td>Adobe Commerce <strong>管理员</strong>提交取车订单。</td>
<td><ul><li>在“管理订单”视图中，“订单同步”状态更新为<code>Sent</code>。</li><li>订单详细信息日志包含消息 <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>新订单推送，例外队列<strong></td>
<td>确定Adobe Commerce管理员中的多个虚拟和可下载产品，这些产品可以通过Adobe Commerce完成，而无需与履行服务(FaaS)交互。</td>
<td>这些产品在导出中将被适当移除或标记，以防止下游与FaaS发生冲突。</td>
</tr>
</tbody>
</table>

### 订单取消工作流

测试计划的此部分包含一些场景，用于测试通过Adobe Commerce取消的订单的端到端工作流。

**功能区域：** Adobe Commerce管理员</br>
**角色：**&#x200B;端到端（管理员、商店关联、客户）</br>
**测试结果类型：**&#x200B;对于所有方案为正

<table style="table-layout:fixed">
<tr>
<th>函数</th>
<th>方案</th>
<th>预期结果</th>
</tr>
<tr>
<td><strong>完全订单取消</strong></td>
<td><ol>
<li>下单。</li>
<li>等待订单同步。</li>
<li>验证发票创建（如果授权并捕获）发票电子邮件的接收。</li>
<li>从“发票”视图创建包含所有已订购产品的贷项通知单。</li>
</ol>
</td>
<td>
<ul>
<li>已使用<code>We refunded $X online. Transaction ID: transactionID</code>和更新订单历史记录 <code>Received Cancel acknowledgment from the BOPIS solution.</code></li>
<li>订单状态为<code>Closed</code>。 （我们已经设置了“付款审核”。）</li>
<li>在Adobe Commerce中创建的贷项通知单。 （请等待cron正常工作。）</li>
<li>如果所有已选取项目，则准备好接收电子邮件<code>DISPLAY COMMENT HISTORY</code>将显示<code>Order is ready for pickup</code> （<code>CUSTOMER NOTIFIED</code>标志为<code>true</code>。）</li>
<li>如果未挑选所有项目，则会显示取消电子邮件和显示备注历史记录 <code>Order has been canceled - all items were not available</code></li>
<li><code>CUSTOMER NOTIFIED</code> 标志为<code>true</code>。)</li>
</ul>
</td>
</tr>
<tr><td><strong>部分订单取消<strong></td>
<td>
<ol>
<li>订购至少两种产品。</li>
<li>等待订单同步。</li>
<li>检查是否已创建发票（如果授权并捕获）以及是否已收到发票电子邮件。</li>
<li>等待两个小时进行交易记录结算。</li>
<li>从“发票”视图创建仅含部分订购产品的贷项通知单。</li>
</td>
<td>
<ul>
<li>订单历史记录更新： <code>We refunded $X online. Transaction ID: transactionID</code></li>
<li>订单历史记录更新： <code>Order notified as partly canceled at: Date and Hour</code></li>
<li>收到订单退款电子邮件： <code>$x amount was refunded</code></li>
<li>订单状态为<code>Processing</code>。</li>
<li>在Adobe Commerce中创建的贷项通知单（等待cron正常工作）。</li>
<li>如果某些项目未领料，请确认显示带有nil领料或退款部分的[!UICONTROL Ready for Pickup]电子邮件。 <code>DISPLAY COMMENT HISTORY</code>显示<code>Order is ready for pickup, but some items not available.</code>。</li>
<li><code>CUSTOMER NOTIFIED</code> 标志为<code>true</code>。</li>
</ul>
</td>
</tr>
<td><strong>准备提货</br></br>完全取消</br>（所有产品均设置为0数量提货）</strong></td>
<td>
<ol>
<li>下订单。</li>
<li>等待订单同步。</li>
<li>检查是否已创建发票（如果授权并捕获）以及是否已收到发票电子邮件。</li>
<li>转到Postman并运行准备收取请求，其中所有产品均设置为<code>picked</code>并设置<code>0 qty</code>。</li>
</ol>
</td>
<td>
<ul>
<li>已更新订单历史记录： <code>We refunded $X offline</code></li>
<li>订单状态为<code>CLOSED</code>。
<li>创建贷项通知单。 （请等待cron正常工作。）</li>
<li>已收到退款电子邮件： <code>$x amount was refunded</code></li>
<li>已发送“订单取消”电子邮件。</li>
</ul>
</td>
</tr>
<tr>
<td><strong>准备提货 — 部分取消</strong></br></br><strong>（某些产品已提货，而某些产品已与<code>0 qty</code>一起提货）</strong>
</td>
<td>
<ol>
<li>下订单。</li>
<li>等待订单同步。</li>
<li>检查是否已创建发票（如果授权并捕获）以及是否已收到发票电子邮件。</li>
<li>转到Postman并运行准备提货请求，其中部分产品设置为0数量，其余产品设置为0数量。</li>
</ol>
</td>
<td>
<ul>
<li><code>Your order is ready for pickup</code> 包含[!UICONTROL Ready for Pickup Items]和[!UICONTROL Canceled Items]个表。 </li>
<li>订单状态为“准备提货”。 </li>
<li>已更新订单历史记录： <code>We refunded $X offline.</code>
<li>已更新订单历史记录： <code>Order notified as partly canceled at: Date and hour</code>
<li>已收到退款电子邮件： <code>$x amount was refunded</code>
<li>已创建贷项通知单。 （请等待cron正常工作。）</li>
</ul>
</td>
</tr>
<tr>
<td><strong>准备提货 — 部分取消</br></br>某些产品已提货，而某些产品已与<code>0 qty</code>一起提货</strong>
</td>
<td><ol>
<li>下订单。</li>
<li>等待订单同步。</li>
<li>检查是否已创建发票（如果授权并捕获）以及是否已收到发票电子邮件。</li>
<li>转到Postman并运行准备提货请求，其中部分产品设置为0数量，其余产品设置为0数量。</li>
</ol>
</td>
<td><ul>
<li><code>Your order is ready for pickup</code> 包含[!UICONTROL Ready for Pickup Items]和[!UICONTROL Canceled Items]个表。 </li>
<li>订单状态为“准备提货”。 </li>
<li>已更新订单历史记录： <code>We refunded $X offline.</code>
<li>已更新订单历史记录： <code>Order notified as partly canceled at: Date and hour</code>
<li>已收到退款电子邮件： <code>$x amount was refunded</code>
<li>已创建贷项通知单。 （请等待cron正常工作。）</li>
</ul>
</td>
</tr>
<tr>
<td><strong>已分配（在分配期间） </br></br>完全取消（所有产品都设置为已拒绝）</strong>
</td>
<td>
<ol>
<li>下订单。</li>
<li>等待订单同步。</li>
<li>检查是否已创建发票（如果授权并捕获）以及是否已收到发票电子邮件。</li>
<li>转到Postman并运行准备收取请求，将所有产品都设置为已收取。</li>
<li>打开邮箱，找到“准备好取货”电子邮件。 然后单击&#x200B;**[!UICONTROL Confirm Arrival]**。</li>
<li>签到。</li>
<li>转到Postman并运行Dispensed请求，将所有产品都设置为已拒绝。</li>
</ol>
<td><ul>
<li>已更新订单历史记录： <code>We refunded $X offline.</code></li>
<li>已收到退款电子邮件： <code>$x amount was refunded</code></li>
<li>状态设置为<code>CLOSED</code>。</li>
<li>已创建贷项通知单。 （请等待cron正常工作。）</li>
</ul>
</td>
</tr>
<tr>
<td><strong>已分配（分配期间）</br></br>部分取消</br>（某些产品已分配；某些产品已被拒绝。）</strong>
</td>
<td>
<ol>
<li>下订单。</li>
<li>等待订单同步。</li>
<li>检查是否已创建发票（如果授权并捕获）以及是否已收到发票电子邮件。</li>
<li>转到Postman，运行准备收取请求，并将所有产品设置为已收取。</li>
<li>打开您的邮箱。 找到“准备好取车”电子邮件，然后选择<code>Confirm Arrival</code>。</li>
<li>签到。</li>
<li>转到Postman，然后运行Dispensed请求，其中某些产品设置为dispensed，而某些产品设置为rejected</li>
</ol>
</td>
<td>
<li>已更新订单历史记录： <code>We refunded $X offline</code></li>
<li><code>Order notified as partly canceled at: Date and Hour</code>
<li>已收到退款电子邮件： <code>$x amount was refunded</code>
<li>订单状态设置为<code>Ready for pickup Dispensed</code>
<li>已创建贷项通知单。 （请等待cron正常工作。）</li>
</td>
</tr>
<tr>
<td> 返回<strong>新的RMA （完整）</strong>
</td>
<td>
<ol>
<li>下订单。</li>
<li>等待订单同步。</li>
<li>如果已配置授权和捕获选项，请验证是否已创建发票，以及客户是否已收到发票电子邮件。</li>
<li>选择Postman的所有产品。</li>
<li>签到。</li>
<li>进行分配。</li>
<li>转到订单，然后选择<strong>[!UICONTROL Create returns]=
<li>创建RMA。</li>
</ol>
</td>
<td>
<ul>
<li>已创建RMA，RMA显示在“订单”视图的<strong>[!UICONTROL Returns]</b>选项卡下方。</li>
<li>客户收到了RMA确认电子邮件。</li>
</ul>
</td>
</tr>
<tr>
<td>返回后<strong>新RMA — 部分</strong>
</td>
<td>
<ol>
<li>下订单。</li>
<li>等待订单同步。</li>
<li>检查是否已创建发票（如果授权并捕获）以及是否已收到发票电子邮件。</li>
<li>选择Postman的所有产品。</li>
<li>签到。</li>
<li>进行分配。</li>
<li>转到订单，然后选择  <strong>[!UICONTROL Create returns]</strong></li>
<li>创建包含部分订购产品的RMA。</li>
</ol>
<td>
<ul>
<li>RMA已创建并显示在订单视图的<strong>[!UICONTROL Returns]</strong>选项卡下方。</li>
<li>客户收到了RMA确认电子邮件。</li>
<li>创建RMA后，获取RMA授权：从管理员转到<strong>[!UICONTROL Sales > Returns]</strong>。 选择您创建的RMA并授权它。</li>
<li>验证客户是否收到了RMA授权确认电子邮件。</li>
<li>检查退款是否已添加至交易和订单历史记录。</li>
</ul>
</td>
</tr>
</table>


### 商店履行应用程序权限

测试计划的此部分涵盖商店履行应用程序用户的帐户管理。

- 确认应用商店关联可以使用从Adobe Commerce管理员创建的新用户帐户进行身份验证。
- 确认已成功应用对现有帐户的更新。

**功能区域：** Adobe Commerce管理员</br>
**角色：**&#x200B;管理员，存储关联</br>
**测试类型：**&#x200B;全部为正

<table style="table-layout:auto">
<tr>
<th>函数</th>
<th>方案</th>
<th>预期结果</th>
</tr>
<tr>
<td><strong>用户帐户管理 — 创建帐户</strong></br></br>
</td>
<td>
<ol>
<li><strong>管理员</strong> — 登录Adobe Commerce管理员</li>
<li>转至<strong>[!UICONTROL System] &gt;商店履行应用权限&gt;所有商店履行应用用户</strong></li>
<li><strong>添加新用户。</strong></li>
</ol>
<td>
<ul>
<li>已成功创建帐户。</li>
<li>新用户帐户显示在[!UICONTROL Store Fulfillment Users]仪表板上。</li>
<li><strong>应用商店关联</strong>使用新用户帐户登录到应用商店助手应用。</li>
</ul>
</td>
</tr>
<tr>
<td><strong>用户帐户管理 — 更新现有用户帐户</strong>
</td>
<td>
<ol>
<li>使用管理员用户帐户登录Adobe Commerce管理员。</li>
<li>转至<strong>[!UICONTROL System] &gt;商店履行应用权限&gt;所有商店履行应用用户</strong>。</li>
<li>在“用户帐户”列表中，通过选择<strong>[!UICONTROL Edit]</strong>打开现有的活动用户帐户。
<li>通过将<strong>[!UICONTROL Is Active]</strong>更改为<strong>否</strong>禁用该帐户。</li>
</ol>
</td>
<td>
<ul>
<li>在<strong>[!UICONTROL Store Fulfillment App Users]</strong>仪表板上，已更新帐户的状态更改为<strong>[!UICONTROL Inactive]</strong>。</li>
<li>应用商店关联无法使用非活动帐户凭据登录到“应用商店助手”应用程序。</li>
</ul>
</td>
</tr>
</table>

## Adobe Commerce产品类型

Adobe Commerce产品类型的测试方案将验证客户能否看到不同产品类型的正确产品、库存和交付方法信息：

- [!UICONTROL Configurable]
- [!UICONTROL Grouped]
- [!UICONTROL Virtual]
- [!UICONTROL Bundle products]在Adobe Commerce店面。

**功能区：** Adobe Commerce前端</br>
**角色：**&#x200B;商店助理应用用户（商店关联）</br>
**测试类型：**&#x200B;全部为正

<table style="table-layout:auto">
<tr>
<th>函数</th>
<th>方案</th>
<th>评论</th>
</tr>
<tr>
<td><strong>可配置的产品</strong>
</td>
<td>
<ul>
<li>验证用户是否只能看到这些可配置选项（已启用来源、已分配库存以及库存中有某些项目），并检查子产品。</li>
<li>验证在选择其他存储时，不可用的选项是否显示为已划出。</li>
<li>验证如果用户选择不同的商店，则会取消选择可配置的选项。</li>
<li>验证当可配置产品已在购物车中，并且用户选择其他商店时，该产品将显示为缺货。</li>
</ul>
</td>
<td></td>
</td>
</tr>
<tr>
<td><strong>已分组的产品</strong>
</td>
<td>
<ul>
<li>验证当所有子产品都具有
<code>qty</code>设置为<code>0</code>。[!UICONTROL Add to cart]</li>
<li>验证当至少有一个子产品将<code>qty</code>设置为时，是否为客户启用传递方法 <code>0.</code></li>
<li>验证[!UICONTROL Store Pickup Delivery]方法是否仅对启用了[!UICONTROL Available for Store Pickup]的产品可见和有效。 （检查子产品。）</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td><strong>虚拟产品</strong>
</td>
<td>
验证虚拟产品是否不提供[!UICONTROL In-store Pickup]交付方法。
<td></td>
</td>
</tr>
<tr>
<td><strong>捆绑产品</strong>
</td>
<td>
<ul>
<li>验证是否至少有一个子产品禁用了[!UICONTROL Available for Store Pickup]，则客户无法使用“商店见面交货”选项。</li>
<li>验证如果至少有一个子产品禁用了[!UICONTROL Available for Home Delivery]，则客户无法使用“主页交付”选项。</li>
<li>验证捆绑包中是否至少有一个子产品缺货，捆绑包（父产品）也会显示
作为[!UICONTROL Out of stock]。</li>
</ul>
</td>
<td></td>
</tr>
<tbody>
</table>

## 签到体验

测试计划的此部分涵盖以下功能的商店提货订单登记体验：

- 备用提货联系人 — 验证用于添加[!UICONTROL Alternate Pickup Contact]和为商店提货订单选择[!UICONTROL Preferred Contact]的工作流。

- 签入表单 — 验证用于提交商店提货单的签入请求的工作流。

**功能区域：**&#x200B;购物车结帐，商店提货单的登记表</br>
**角色：**&#x200B;管理员、客户、商店联系人</br>
**测试类型：**&#x200B;全部为正

### 备用代答联系人


**功能区：**&#x200B;购物车结帐</br>
**角色：**&#x200B;客户</br>
**测试类型：**&#x200B;全部为正

<table style="table-layout:auto">
<tr>
<th>函数</th>
<th>方案</th>
<th>预期结果</th>
</tr>
<tr>
<td><strong>备用代答联系人</br>
签入<strong>
</td>
<td>
客户提交具有“店内提货”选项的订单。</td>
<td>在结账过程中，客户在送货步骤中看到[!UICONTROL Alternate Pickup Contact]选项。
</td>
</tr>
<tr>
<td><strong>备用代答首选联系人，签到</strong>
<td>
客户提交具有“店内提货”选项的订单。 在结账过程中，客户添加了[!UICONTROL Alternate Pickup Contact]。</td>
<td>在结账过程中，客户在送货步骤中看到[!UICONTROL Preferred Contact]选项。</td>
</td>
</tr>
<tr>
<td><strong>备用代答联系人详细信息，签到</strong>
</td>
<td>
客户提交具有“店内提货”选项的订单。 在结账过程中，客户在送货步骤中选择[!UICONTROL Alternate Pickup Contact]。
</td>
<td>客户看到用于输入联系人详细信息的输入选项： [!UICONTROL First name]、[!UICONTROL Last name]、[!UICONTROL Phone]和[!UICONTROL Email]。</td>
</tr>
<tr>
<td><strong>备用接送，签到电子邮件</strong>
</td>
<td>客户提交具有“店内提货”选项的订单。 在结账过程中，客户在送货步骤中选择[!UICONTROL Alternate Pickup Contact]，添加联系人详细信息，并提交订单。</td>
<td>客户和备用联系人都会收到订单的“签入”电子邮件。</td>
</tr>
<td><strong>替代装货，订单详细信息</strong></td>
<td>客户提交具有“店内提货”选项的订单。 在结账过程中，客户在送货步骤中选择[!UICONTROL Alternate Pickup Contact]，添加联系人详细信息，并提交订单。</td>
<td>管理员会看到已保存订单上的其他联系信息。</td>
</tr>
<tr>
<td><strong>备用代答联系人，商店关联订单视图</strong>
</td>
<td>客户提交具有“店内提货”选项的订单。 在结账过程中，客户在送货步骤中选择[!UICONTROL Alternate Pickup Contact]，添加联系人详细信息，并提交订单。</td>
<td>“商店关联”可以在FaaS/ChaaS中查看有关订单的其他联系信息。</td>
</td>
</tr>
</tbody>
</table>

### 签到表单


**功能区：**&#x200B;签入表单</br>
**角色：**&#x200B;客户</br>
**测试类型：**&#x200B;全部为正

<table style="table-layout:auto">
<tr>
<th>函数</th>
<th>方案</th>
<th>预期结果</th>
</tr>
<tr>
<td><strong>签入操作 — 提交请求</strong>
</td>
<td>在签到表单中，客户填写所有必填字段，并提交请求。</td>
<td>客户收到成功响应。</td>
</tr>
<tr>
<td><strong>签入操作 — 查看请求详细信息</strong></td>
<td>客户已成功提交签到请求。</td>
<td>订单状态会在FaaS系统中更新，而“商店关联”可以在FaaS中查看签入请求详细信息。
</td>
</tr>
<tr>
<td><strong>签入操作 — 仅提交请求一次</strong></td>
<td>在提交订单签到请求后，客户会选择再次签到的链接。</td>
<td>在签入表单上，客户看不到编辑或重新提交表单的选项。</td>
</tr>
<tr>
<td><strong>签入操作 — 确认到达</strong></td>
<td>店内提货单已标记为可在FaaS中提货。 客户收到“准备好取货”电子邮件，并选择[!UICONTROL Confirm Arrival]。</td>
<td>客户看到订单的“签到”表格。</td>
</tr>
</tbody>
</table>

## 商店协助应用程序

测试计划的此部分介绍了应用商店助手应用程序中测试订单、挑选和移交工作流的场景。

**功能区：**&#x200B;商店助理应用</br>
**角色：**&#x200B;存储关联</br>
**测试类型：**&#x200B;全部为正

<table style="table-layout:auto">
<tr>
<th>函数</th>
<th>方案</th>
<th>预期结果</th>
</tr>
<tr>
<td>
<strong>单个订单领料 — 快乐路径，路边领料</strong></td>
<td>挑选单个和多数量物料。 无nil pick，路边取车（带暂存功能）。
</td>
<td>
</td>
</tr>
<tr>
<td><strong>多订单领料 — 快乐路径，路边领料</strong></td>
<td>单个和多数量物料。 无nil pick，路边取车（带暂存功能）</td>
<td></td>
</tr>
<tr>
<td><strong>单订单提货 — 店内提货的快乐路径</strong></td>
<td>单个和多数量物料。 无Nil Pick和店内取货（带暂存）</td>
<td>
</td>
</tr>
<tr>
<td><strong>多订单领料 — 快乐路径，店内领料</strong></td>
<td>挑选单个和多数量物料。 无nil pick，路边取车（带暂存功能）。</td>
<td></td>
</tr>
<tr>
<td><strong>单一订单领料 — 路径不愉快，店内领料</strong></td>
<td>挑选单个和多数量物料，包括部分挑库和零挑库以及店内提货（具有暂存）</td>
</td>
<td></td>
</tr>
<td><strong>多订单领料 — 不满意路边领料</strong></td>
<td>挑选单个和多数量物料，包括部分挑库和零挑库以及店内提货（具有暂存）</td>
<td></td>
</tr>
<td><strong>单订单提货 — 路径不愉快，路边提货</strong></td>
<td>挑选单个和多数量物料，包括部分挑库和分段挑库（具有暂存）</strong></td>
</td>
<td></td>
</tr>
<tr><td><strong>下单 — 领料前已取消</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>下单 — 移交前已取消</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>下订单 — 按订单搜索模块</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>下单 — 搜索和手动签入以进行移交</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>订单已下达 — 选取器未选取或标记的所有项目不可用</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>与捆绑项目一起下达的订单 — 领料和移交</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>已下达订单 — 已拒绝的交货</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>已下达订单 — 在拒绝所有物料的情况下交货</strong></td>
<td></td>
<td></td></tr>
</tbody>
</table>

## 部署

在验证解决方案已配置并且已按照您的规范进行测试后，您就可以准备从暂存部署到生产。

部署和测试因您的基础架构和功能而异。

>[!TIP]
>
>有关Adobe Commerce在云基础架构项目中的部署准则、核对表和最佳实践，请参阅Adobe Commerce开发人员文档中的[部署您的应用商店](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production)。
