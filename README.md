# Study Guy · 小镇做题家学案

**把 PPT 和 lecture 一股脑丢进来，带走一份能拿起笔做的预习／复习学案。**

从“这页好像看懂了”，走到“合上课件也会做”。Study Guy 是一个可复用的 AI Agent Skill：整理材料、搭知识框架、讲典型例题、出分层练习、分开给解析，再根据实际作答安排错题回炉。

## 它会做什么

| 场景 | 交付内容 |
| --- | --- |
| 明天上课，先预习 | 前置诊断、核心概念、引导填空、示范例题、独立练习、课堂问题 |
| 学完一讲，巩固一下 | 知识结构、公式条件、易混点、A/B/C 分层训练、答案与错因 |
| 考前材料太多 | 全量材料台账、按依据排序的复习重点、限时自测、速查清单、时间计划 |
| 做错了，帮我补 | 保留真实作答、定位错误步骤、补概念、练新变式、延迟复测 |

默认中文讲解，保留英文术语。支持数理、编程、理论和人文课程的不同训练形式。不会把所有课程都套成选择题，也不会把原创题包装成老师的真题。

## 安装和使用

在支持技能安装的 Codex 会话中，可以发送：

```text
$skill-installer 从 https://github.com/ccyyll11/study-guy 安装 skills/study-guy。
```

也可以下载本仓库，将 `skills/study-guy` 整个目录放到你的技能目录。当前官方文档列出的项目级位置是 `.agents/skills/`，用户级位置是 `~/.agents/skills/`；具体宿主也可能使用自己的技能安装目录，优先使用其安装器。见 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)。

安装后，把材料作为附件提供，或指定已授权的本地目录，再说：

```text
$study-guy 这些是本周 PPT、lecture notes 和 tutorial。
帮我做预习学案，中文解释、保留英文术语，控制在 45 分钟，答案单独放。
```

```text
$study-guy 把这个文件夹里所有 lecture 整理成期末复习学案。
先列材料和覆盖范围，再按知识依赖组织。给我基础题、变式题、综合题，
每题附知识点和预计时间，解析分开。每天能学 2 小时，还有 5 天考试。
```

```text
$study-guy 我做完了，这是我的答案。
请按错误步骤判断问题，保留错题记录，再给同知识点的新变式；先不要展示答案。
```

不需要先填长问卷。缺少非关键偏好时会说明假设并继续；缺少原材料或无法辨认的公式时会说明缺口。

## 一次完整输出

```text
study-guide/
├── 00-课程导航.md         材料清单、覆盖状态、知识点和题目映射
├── 01-学案.md             学习目标、讲解、例题、独立练习
├── 02-答案与解析.md       关键步骤、建议评分、错因和检查方法
└── 03-错题与复习计划.md   真实作答记录、重练条件和复测安排
```

多讲课程按讲次拆分。默认输出 Markdown；请求 Word 或 PDF 时，需宿主具备相应生成和检查能力。

## 看一份实际示例

仓库包含一套原创的“条件概率与独立性”迷你课程，不使用真实课程课件：

1. [原始讲义](examples/conditional-probability/source-lecture.md)
2. [课程导航与覆盖表](examples/conditional-probability/00-course-map.md)
3. [学生学案：预习＋复习](examples/conditional-probability/01-study-guide.md)
4. [独立答案与解析](examples/conditional-probability/02-solutions.md)
5. [错题表与复习安排](examples/conditional-probability/03-review-plan.md)

先读学案再看解析。示例用于展示交付质量，不是某门真实课程的考试范围。

## 读取能力与边界

这是学习工作流技能，不是自带文件解析、OCR 或转录服务的软件。PPT/PPTX、PDF、DOCX、图片和音视频能读到什么，取决于宿主工具；没有音视频转录能力时，需要已有转录稿。扫描页、图片公式、讲者备注等会单独检查或标注缺口。

讲解保留实际来源，分清原材料、补充解释和原创练习。不从一份课件推断“必考”，不把未作答写成已掌握。默认间隔复习安排可以调整，不承诺成绩提升。

使用时只处理用户指定材料。此公开仓库仅存技能、模板和原创示例；技能不会自动发布用户课件、学案或作答记录。

## 仓库结构

```text
skills/study-guy/
├── SKILL.md
├── agents/openai.yaml
├── references/ingestion.md
├── references/practice-and-feedback.md
└── assets/
    ├── preview-template.md
    └── review-template.md
examples/conditional-probability/
```

技能本身无必装 Python 依赖或 API key。运行它需要一个能加载技能并读取所提供材料的 AI Agent；单独下载文件不会自动开始学习任务。
