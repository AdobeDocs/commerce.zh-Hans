---
source-git-commit: 4ddab6bbd62a3cc7c6dff089745c1b5ef5c20f70
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---
# 投稿

感谢您选择投稿！

以下是为该项目做贡献时应遵循的一套准则。

## 行为准则

此项目遵循 Adobe [行为准则](code-of-conduct.md)。通过参与，
您应遵守本准则。 向报告不可接受的行为
[Grp-opensourceoffice@adobe.com](mailto:Grp-opensourceoffice@adobe.com)。

## 参与者指南文档

请参阅[参与者指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=zh-Hans)。

## 有疑问吗？

首先，提交问题。 该项目的现有参与者需要工作以达到
在适当的情况下，就项目方向和问题线程中的问题解决方案达成共识。

## 参与者许可协议

所有参与到该项目的第三方稿件都必须附有已签署的投稿人
许可协议。 这将允许Adobe重新分发您投稿的内容
作为项目的一部分。 [签署我们的CLA](https://opensource.adobe.com/cla.html)。 您
只需提交一次Adobe CLA即可。 如果您之前提交了一个，
一切准备就绪！

## 代码审阅

所有提交都应采用拉取请求的形式，并且需要审核
按项目参与者。 阅读[GitHub的拉取请求文档](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)
以了解有关发送拉取请求的更多信息。

最后，请在以下情况下遵循[拉取请求模板](PULL_REQUEST_TEMPLATE.md)：
提交拉取请求！

## 从参与者到提交者

我们欢迎来自社区的投稿！ 如果您想在投稿人之外更进一步
并成为具有完全写入权限且在项目中具有发言权的提交者，您必须
受邀加入该项目。 现有参与者采用内部提名
在邀请之前必须达成懒惰共识（沉默即表示同意）的进程
已颁发。 如果你觉得自己有资格，希望更深入地参与进来，
欢迎您随时联系现有的撰稿人，以便就此展开讨论。

## 安全问题

要报告安全问题，[请向我们的安全专家提出问题](https://helpx.adobe.com/cn/security/alertus.html)。

## 新增功能亮点

如果您的更改引入新主题、重大更新或需要突出显示的更正，则可以在拉取请求正文的[新增功能部分](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/home#whats-new)中添加简短描述。

添加“新增功能”高亮显示：

1. 在结尾处的拉取请求正文中包含带有相应描述的`whatsnew`标记。 说明应提供有关更改的上下文以及指向一个或多个目标主题的链接。 使用以下格式（代码块引号仅用于表示法，请勿将其包含在拉取请求正文中）：

   ```text
   whatsnew
   Short description of the change in the [target topic](https://experienceleague.adobe.com/en/docs/commerce/target-topic.html).
   ```

   或者，如果有多个主题：

   ```text
   whatsnew
   Short description of the changes in the [first target topic](https://experienceleague.adobe.com/en/docs/commerce/target-topic.html), [second target topic](https://experienceleague.adobe.com/en/docs/commerce/second-target-topic.html), and [third target topic](https://experienceleague.adobe.com/en/docs/commerce/third-target-topic.html).
   ```

   您还可以将列表用于多个高亮：

   ```text
   whatsnew
   - Short description of the first change in the [first topic](https://experienceleague.adobe.com/en/docs/commerce/first-topic.html).
   - Short description of the second change in the [second topic](https://experienceleague.adobe.com/en/docs/commerce/second-topic.html).
   ```

   ```text
   whatsnew
   The following changes were made to the documentation:
   - Short description of the first change in the [first topic](https://experienceleague.adobe.com/en/docs/commerce/first-topic.html).
   - Short description of the second change in the [second topic](https://experienceleague.adobe.com/en/docs/commerce/second-topic.html).
   ```

1. 添加受支持的标签以指示更改类型。 支持的标签包括适用于每种更改类型的标签，例如：

   - `new-topic` — 新主题
   - `major-update` — 对于可能包括内容、结构或功能方面重大更改的主要更新
   - `technical` — 对于不被视为主要更新但仍需要关注的技术更改

**重要信息：**

1. `whatsnew`部分必须从`whatsnew`标记开始，并且位于拉取请求正文的最末尾。
1. 对更改的描述必须包含工作链接。 请确保链接正确无误并指向预期的主题。 如果主题是新主题，请在合并拉取请求并发布新主题后，验证链接是否正常工作。 可以在合并拉取请求后修复链接。

例如，在存储库的已关闭拉取请求中搜索以查看现有高亮的格式设置，并将它们与[新增功能部分](https://experienceleague.adobe.com/zh-hans/docs/commerce/user-guides/home#whats-new)进行比较，以查看它们在文档中的显示方式。
