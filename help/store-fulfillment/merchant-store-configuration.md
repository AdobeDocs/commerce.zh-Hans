---
title: 商家商店配置
description: 将增强的Inventory management源设置为商户商店。
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# 商户商店(Source)配置

此解决方案通过为商家使用面向操作的功能扩展库存来源，增强了原生Inventory management功能。

- 添加商店位置的地理坐标
- 将源指定为[!DNL Store Pickup Location]并指定可用的送货功能（“收货商店”、“发货商店”）
- 指定可用的取车选项（店内或路边）、自定义的取车说明和其他信息，以将取车详细信息和说明传达给客户

术语&#x200B;_源_&#x200B;和&#x200B;_商家商店位置_&#x200B;可互换使用。 所有记录都是库存来源，但来源也可以是商家商店位置，具体取决于配置设置。

从管理员管理商户商店配置： **[!UICONTROL Stores > Inventory > Sources >  Edit Source]**。

>[!NOTE]
>
>在设置过程中，可能必须在创建源或更新现有源之后刷新缓存。

## **常规**

<table>
<tbody>
<tr>
<th>字段</th>
<th>描述</th>
<th>范围</th>
<th>必填</th>
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>商家商店位置的纬度坐标。 此必需信息用于店面体验的位置搜索和地图放置。 该值必须与存储区的确切地址匹配才能通过验证。</td>
<td>全局</td>
<td>是</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>商户商店位置的纵向坐标。 此必需信息用于店面体验的位置搜索和地图放置。 该值必须与存储区的确切地址匹配才能通过验证。</td>
<td>全局</td>
<td>是</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>将来源指定为可用的商店取货地点。 此设置确定是否同步源并向访客显示。</td>
<td>全局</td>
<td>否</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong><br><code>Extension Attribute: allow_ship_to_store</code></td>
<td>在源级别配置收货到存储功能。 有关详细信息，请参阅[常规配置](enable-general.md)选项<strong>[!UICONTROL Enable Ship To Store]
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>商家商店位置的纬度坐标。 此必需信息用于店面体验的位置搜索和地图放置。 该值必须与存储区的确切地址匹配才能通过验证。</td>
<td>全局</td>
<td>是</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>商户商店位置的纵向坐标。 此必需信息用于店面体验的位置搜索和地图放置。 该值必须与存储区的确切地址匹配才能通过验证。</td>
<td>全局</td>
<td>是</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>将来源指定为可用的商店取货地点。 此设置确定是否同步源并向访客显示。</td>
<td>全局</td>
<td>否</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong></br> <code>Extension Attribute: [!DNL allow_ship_to_store]</code></td>
<td>在源级别配置收货到存储功能。 有关详细信息，请参阅[常规配置](enable-general.md)选项<strong>[!UICONTROL Enable Ship To Store]</strong>。</td>
<td>全局</td>
<td>否</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
 <td>在源级别配置ship-from-store功能。 有关详细信息，请参阅[常规配置](enable-general.md)选项[!UICONTROL Enable Ship From Store]。</td>
<td>全局</td>
<td>否</td>
</tr>
<tr>
<td>全局</td>
<td>否</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong><code></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
<td>在源级别配置ship-from-store功能。 有关详细信息，请参阅[常规配置](enable-general.md)选项[!UICONTROL Enable Ship From Store]。</td>
<td>全局</td>
<td>否</td>
</tr>
</tbody>
</table>



| **字段** | **描述** | **作用域** | **必需** |
|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Latitude]**</br>`Base Attribute: latitude` | 商家商店位置的纬度坐标。 此必需信息用于店面体验的位置搜索和地图放置。 该值必须与存储区的确切地址匹配才能通过验证。 | 全局 | 是 |
| **[!UICONTROL Longitude]**</br>`Base Attribute: Longitude` | 商户商店位置的纵向坐标。 此必需信息用于店面体验的位置搜索和地图放置。 该值必须与存储区的确切地址匹配才能通过验证。 | 全局 | 是 |
| **[!UICONTROL Use as Pickup Location]**</br>`Base Attribute:[!DNL is_pickup_location_active]` | 将来源指定为可用的商店取货地点。 此设置确定是否同步源并向访客显示。 | 全局 | 否 |
| **[!UICONTROL Enable Ship to Store]**</br>`Extension Attribute: [!DNL allow_ship_to_store]` | 在源级别配置收货到存储功能。 有关详细信息，请参阅[常规配置](enable-general.md)选项&#x200B;**[!UICONTROL Enable Ship To Store]**。 | 全局 | 否 |
| **[!UICONTROL Enable Ship From Store]**</br>`Extension Attribute: [!DNL use_as_shipping_source]` | 在源级别配置ship-from-store功能。 有关详细信息，请参阅[常规配置](enable-general.md)选项[!UICONTROL Enable Ship From Store] | 全局 | 否 |

{style="table-layout:auto"}

## 取车地点配置

| **字段** | **描述** | **作用域** | **必需** |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Allow In-Store Pickup]**</br>`Extension Attribute: [!DNL store_pickup_enabled]` | 两个取车选项之一。 [!DNL In-Store Pickup]指的是允许客户输入商家商店位置以检索其订单的功能。 </br></br>启用后，在结帐期间可能会向客户显示此选项。 </br></br>此选项还将覆盖在[!UICONTROL Delivery Method]上为[!UICONTROL In-store Pickup]配置的[!UICONTROL Enable In-store Pickup]全局配置 | 全局 | 否 |
| **店内取货说明**</br>`Extension Attribute: store_pickup_instructions` | 在&#x200B;**Order Ready For Pick In Store**&#x200B;电子邮件通知中向客户传递的可自定义消息。 | 全局 | 否 |
| **允许路边**</br>`Extension Attribute: curbside_enabled` | 两个取车选项之一。 路边交付允许客户将其车辆停放在商铺地点的指定位置。 在此方案中，订单由商店关联交付给客户。 </br></br>启用后，可在结帐期间向客户显示此选项。 此外，在办理登记入住手续时，客户可能会被要求描述自己的车辆和停车位。 </br></br>此选项还将覆盖&#x200B;**店内取货**&#x200B;的&#x200B;**交货方法**&#x200B;上配置的&#x200B;**启用路边取货**&#x200B;的全局配置 | 全局 | 否 |
| **[!UICONTROL Curbside Instructions]**</br>`Extension Attribute: curbside_instructions` | 在[!UICONTROL Order Ready For Pickup in Store]电子邮件通知中传递给客户的可自定义消息。 | 全局 | 否 |
| **[!UICONTROL Estimated Pickup Lead Time]**</br>`Extension Attribute: pickup_lead_time` | 接收、领料和准备领料订单前所需的分钟数。 </br></br>此信息用于在网站上向客户显示订单提货的估计时间。</br></br>设置此选项将覆盖为&#x200B;**店内收货**&#x200B;配置中的&#x200B;**交货方法**&#x200B;配置的&#x200B;**预计提货提前期**&#x200B;的全局配置。 | 全局 | 否 |
| **[!UICONTROL Estimated Pickup Time Label]**</br>`Extension Attribute: pickup_time_label` | 显示订单准备接受前所经过分钟数的标签。</br></br>在自定义此标签时，您可以使用代码%1插入您的&#x200B;**预计提货提前期**。</br></br>设置此选项将覆盖[!UICONTROL In-store Pickup]中为[!UICONTROL Delivery Method]配置的[!UICONTROL Estimated Pickup Time Label]的全局配置。 | 全局 | 否 |

### **营业时间**

| **字段** | **描述** | **作用域** | **必需** |
|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Location Timezone]**</br>`Extension Attribute: timezone` | 商家存储位置的时区。 对于每一天，设置开始和结束时间。</br></br>这些设置用于优化预计取车时间和履行服务报表。 | 全局 | 是 |
| **[!UICONTROL Opening Hours]**</br>`Internal Attribute: inventory_source_opening_hours_dynamic_rows` | 商家商店位置的营业时间。 </br></br>此信息可用于优化预计取车时间，以及履行服务报表。 | 全局 | 是 |

### 配置“签入”Experience界面选项



| **字段** | **描述** | **作用域** | **必需** |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Use Parking Spots]**</br>`Extension Attribute: parking_spots_enabled` | 指定商户商店位置是否具有指定路边取车的停车位。 </br></br>启用后，您可以配置可用的停车位。 | 全局 | 否 |
| **[!UICONTROL Is Parking Spot a Mandatory Field?]**</br>`Extension Attribute: parking_spot_mandatory` | 指定客户在购物体验期间是否需要停车位识别。</br></br>如果启用，将提示客户在到达时指定其停车位。 如果禁用，客户可以跳过此输入。 | 全局 | 否 |
| **[!UICONTROL Parking Spots List]**</br> `Internal Attribute: inventory_source_parking_spot_dynamic_rows` | 这家商店提供路边取车的停车位。 使用提供的界面为每个点命名。</br></br>您无需为每个停车位命名，只需为指定路边的停车位命名。 例如，您可能有可供停车的A-G行，但只有行A的前8个点被指定用于路边取车。 在此方案中，您可以定义8个位置；例如：A1、A2、A3等。 | 全局 | 否 |
| **[!UICONTROL Allow "Other" Parking Spot Field]**</br>`Extension Attribute: custom_parking_spot_enabled` | 启用后，此设置允许客户在登记入住期间描述其停车位。 | 全局 | 否 |
| **[!UICONTROL Use Car Color]**</br>`Extension Attribute: use_car_color` | 指定在登记入住期间是否支持从客户收集车辆颜色。 </br></br> [!UICONTROL Car Color]的可用选择已在签入体验](check-in-experience-setup.md)的管理员[系统设置中配置。 | 全局 | 否 |
| **[!UICONTROL Is Car Color a Mandatory Field?]**</br>`Extension Attribute: car_color_mandatory` | 指定客户在登记入住期间是否需要车辆颜色标识。</br></br>如果启用，将提示客户在到达时指定其车辆的颜色。 如果禁用，客户可以跳过此输入。 | 全局 | 否 |
| **[!UICONTROL Use Car Make]** </br>`Extension Attribute: use_car_make` | 指定在登记入住期间是否支持从客户处收集车辆。</br></br> [!UICONTROL Car Make]的可用选择已在签入体验](check-in-experience-setup.md)的管理员[系统设置中配置。 | 全局 | 否 |
| **[!UICONTROL Is Car Make a Mandatory Field?]**</br>`Extension Attribute: car_make_mandatory` | 指定客户在登记入住期间是否需要车辆制造标识。</br></br>如果启用，将提示客户在到达时指定其车辆的厂牌。 如果禁用，客户可以跳过此输入。 | 全局 | 否 |
| **[!UICONTROL Use Additional Information]**</br> `Extension Attribute: use_additional_information` | 指定在签到期间是否支持从客户收集其他信息。 | 全局 | 否 |
| **[!UICONTROL Is Additional Information a Mandatory Field?]**</br>`Extension Attribute: additional_information_mandatory` | 指定客户在签入期间是否需要其他信息。 </br></br>如果启用，则提示客户在到达时输入其他信息。 如果禁用，客户可以跳过此输入。 | 全局 | 否 |
