---
title: 设置
description: 配置 [!DNL Live Search] 服务的设置。
exl-id: 6387a365-7e23-4023-95ac-27908164d81c
source-git-commit: 70ff444afbe7ddf41e966e479e03975a02f4e10f
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 设置

使用&#x200B;*设置*&#x200B;工作区配置价格方面范围和间隔以及索引的默认语言。

价格彩块化指定价格范围组的数量以及价格值在它们之间的分配方式。

语言设置告知[!DNL Live Search]服务在写入索引时应该使用哪种语言。

![设置](assets/settings.png)

## 价格刻面

您可以指定价格范围组的数量以及价格值在它们之间的分配方式。 每个价格范围与上一组价目表各一重叠。 例如，间隔为20的五个组将创建以下价格范围：0-20、20-40、40-60、60-80和>80。 如果目录中没有足够的产品来填满所有定义的范围，则会相应地调整可用组的显示。 例如：0-20、60-80、>80。

1. 在管理员中，转到&#x200B;**营销** > *SEO和搜索* > **[!DNL Live Search]**。
1. 在&#x200B;**价格分面**&#x200B;下的&#x200B;*设置*&#x200B;工作区上，执行以下操作：
   * 输入&#x200B;**选择的数量**&#x200B;或可用的价格分组。 使用[!DNL Live Search] 4.4.0，您最多可以定义100个价格分组。 早期版本允许50个价格分组。
   * 输入每个组的&#x200B;**间隔值**&#x200B;或价格范围。 最大值为40,000,000。
1. 单击&#x200B;**保存**。

   更新后的设置大约需要15分钟才能在店面中提供。

### 字段描述

| 字段 | 描述 |
|--- |--- |
| 选择数量 | 指定可在店面中用作搜索过滤器的价格范围分组的数量。 默认值： 8，最大值： 100（截至[!DNL Live Search] 4.4.0） |
| 间隔值 | 指定每个组的价格范围间隔。 例如，间隔值为20的五个选择将创建0-20、20-40、40-60、60-80和>80的五个分组。 默认值：5，最大值：40,000,000 |

## 语言

Language设置告知[!DNL Live Search]在读取目录和写入索引时应该使用哪种语言。

语言有不同的语法规则集：例如单词的分隔、动词句子和单词形式。
语言设置可确保将正确的规则集应用于索引机制。

将语言设置设置为目录的主要语言。 更改索引的语言时，根据目录的大小和复杂性，可能需要5到60分钟才能在店面反映更改。

| 语言 | 代码 |
|----|----|
| 阿拉伯语 | ar |
| 亚美尼亚语 | hy |
| 巴斯克语 | 欧盟 |
| 孟加拉语 | bn |
| 巴西语 | pt-br |
| 保加利亚语 | bg |
| 加泰罗尼亚语 | ca |
| 中文（简体） | zh-cn |
| 繁体中文 | zh-tw |
| 捷克语 | cs |
| 丹麦语 | da |
| 荷兰语 | nl |
| 英语 | en |
| 爱沙尼亚语 | et |
| 芬兰语 | fi |
| 法语 | fr |
| 加利西亚语 | gl |
| 德语 | de |
| 希腊语 | el |
| 印地语 | 您好 |
| 匈牙利语 | 胡 |
| 印尼语 | id |
| 爱尔兰语 | ga |
| 意大利语 | it |
| 日语（片假名） | ja |
| 朝鲜语 | ko |
| 拉脱维亚语 | lv |
| 立陶宛语 | lt |
| 挪威语 | 否 |
| 波斯语 | fa |
| 葡萄牙语 | pt |
| 罗马尼亚语 | ro |
| 俄语 | ru |
| 索拉尼 | ku |
| 西班牙语 | es |
| 瑞典语 | sv |
| 土耳其语 | tr |
| 泰语 | th |
