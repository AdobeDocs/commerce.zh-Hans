---
title: 将Adobe Experience Platform Mobile SDK与Commerce集成
description: 了解如何将Adobe Experience Platform Mobile SDK与Headless或自定义Commerce店面结合使用。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 02d07abb-8d7f-4f0a-9f96-f42654cd79d3
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# 将Adobe Experience Platform Mobile SDK与Commerce集成

>[!IMPORTANT]
>
>适用于iOS的Adobe Experience Platform Mobile SDK支持iOS 11或更高版本。

将[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)与Commerce Mobile应用程序集成后，商家可以将Commerce [事件数据](events.md)发送到Experience Platform Edge。

当Commerce事件数据在边缘可用时，其他Adobe Experience Cloud应用程序即可访问该数据。 例如，您可以使用此数据在Real-Time CDP中构建受众，然后[使用这些受众](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=zh-Hans)个性化您的Commerce移动应用程序。

## 配置

要开始将Adobe Experience Platform Mobile SDK与Commerce结合使用，请在Experience Platform中安装和配置SDK。 然后，在Commerce中完成配置。

### Experience Platform

1. 通过查看移动设备应用程序中的[Adobe Experience Cloud教程](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=zh-Hans)了解移动设备应用程序功能。

1. [在Experience Platform中安装和配置](https://developer.adobe.com/client-sdks/documentation/getting-started/)SDK。

   >[!NOTE]
   >
   >您在Experience Platform中创建和配置的架构，与您在Commerce移动设备应用程序中的应用程序代码中使用的架构相同。

### Commerce

完成适用于Experience Platform的SDK配置后，请将SDK配置添加到Commerce。

1. 要通过SDK将Commerce事件数据发送到Experience Platform，您必须在应用程序代码中提供XDM架构。 此架构必须与Experience Platform中为SDK配置的[架构](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/)匹配。

   以下示例显示如何使用电子邮件字段跟踪`web.webpagedetails.pageViews`事件并设置`identityMap`。

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. 连接到Commerce Cloud环境。

   在您的项目构建设置中，将URL添加到Commerce GraphQL端点。 例如：

   - 调试： http://_debug_.commercesite.cloud/graphql/
   - 发行版本： http://_发行版本_.commercesite.cloud/graphql/

1. 要从Commerce GraphQL端点检索数据，请先使用[Apollo代码生成器](https://www.apollographql.com/docs/ios/)在项目中生成必要的文件和目录。

   1. 从项目目录[安装](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOS。

   1. [初始化](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize) Apollo Codegen CLI。

      这将创建一个`apollo-codegen-configuration.json`文件。

   1. 使用以下内容替换`apollo-codegen-configuration.json`文件的内容，以在项目中生成必要的GraphQL文件和目录：

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. [提取](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema) Commerce GraphQL架构。

      确保路径为`./apollo-codegen-config.json`文件，该文件包含对Commerce GraphQL架构的引用。

   1. [生成](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate)源代码。

      确保路径指向`./apollo-codegen-config.json`文件，该文件包含用于生成所需文件和目录的配置信息。

   1. 在新创建的&#x200B;**GraphQLGenerated**&#x200B;文件夹内，添加或编辑GraphQL类型。 例如，您可以添加具有以下内容的`DynamicBlocks.graphql`类型：

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   您现在已将Adobe Experience Platform Mobile SDK与Commerce移动应用程序集成。 事件数据从您的应用程序流向Experience Platform Edge。

## 如何区分从移动应用程序生成的Commerce事件

所有[事件](events.md)都包含一个名为`channel`的字段。 `channel`字段包含`channel._id`和`channel._type`，对于Luma店面，这两个字段的命名空间值分别为`"https://ns.adobe.com/xdm/channels/web"`和`"https://ns.adobe.com/xdm/channel-types/web"`。 但是，对于移动店面，命名空间值分别为`"https://ns.adobe.com/xdm/channels/mobile-app"`和`"https://ns.adobe.com/xdm/channel-types/mobile"`。

## 后续步骤

要了解如何从移动Real-Time CDP应用程序中检索Commerce受众以告知购物车价格规则、动态块和相关产品规则，请参阅[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=zh-Hans#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk)。
