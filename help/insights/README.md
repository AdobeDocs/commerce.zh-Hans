---
title: Commerce文档管理
description: 了解Commerce Insights的内部治理模型。 未发布到Experience League — 有意置于TOC.md之外。
source-git-commit: 1da6d9753acbeadf3a0df5fae86a9386643c6d6d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Commerce文档管理

这是文档团队的内部参考。 `TOC.md`中未列出它，因此它未生成或发布到Experience League。 将其保留在此处，以便与它管理的内容保持接近。

## 所有权

Commerce Insights文章由负责维护文章准确性和货币性的发布作者或团队拥有。 这些文章当前托管在`commerce.en`存储库中。 Commerce文档团队协助确保内容质量并将文章发布到生产环境。

## 什么属于Commerce Insights

- **属于此处**：Commerce解决方案的战略指导和白皮书，其中涵盖基于现实场景的实施指导。 包含指向相关Commerce文档页面的链接以获取支持。

- **改为属于产品存储库**：逐步配置、教程、参考资料（API/CLI/配置参考）和故障排除。 如果这里的帖子开始积累此类详细信息，请将其移至相关的产品指南，然后链接到相应的产品指南。

## 添加新内容

为要发布的文章创建COMDOX JIRA票证。 将`[templates/comdox-intake-template.md](templates/comdox-intake-template.md)`复制到票证描述中并填写 — 它会要求请求者识别受众，标记内容是否为临时内容（包含过期日期），并确认它属于“分析指南”而非Commerce产品文档中。

在票证限定范围后，从`templates/`中的模板启动文章（`whitepaper-template.md`、`security-guidance-template.md`、`insight-perspective-template.md` — 未发布，将相关文章复制到目标文件中并删除模板自己的frontmatter占位符注释）。 在内容准备发布后添加`TOC.md`条目。

- **新的顶级节**（例如，“分析”>“目录管理”）在添加之前需要IA审核，因为它更改了指南的导航形状。 在拥有Commerce IA审阅故事或任务的人中循环。

- **添加到目录** — 在发布之前将新主题添加到目录。 如果需要，请使用隐藏元数据发布隐藏文章，只有拥有该链接的用户才能访问。 请参阅ExL作者指南中的[隐藏内容](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files)。

## 审核节奏

在重命名或更新新的Commerce解决方案，或分析不再相关时，查看文章内容。
