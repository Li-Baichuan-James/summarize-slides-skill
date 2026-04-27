# Summarize Slides Skill

<div align="center">

## 课件.skill

---

> "哎哟 真复习不过来了我艹"
> 
> --考试周破防哥


<img src="assets/summarize-slides-readme.jpg" alt="考试周破防哥" width="220" />

---

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-green)](https://agentskills.io)
[![Bilingual](https://img.shields.io/badge/README-%E4%B8%AD%E6%96%87%20%7C%20English-4c9a2a)](#中文)

[中文](#中文) | [English](#english)

---

</div>

---

## 中文

还在对着几百页的课件发愁，不知如何下手？别慌，你不是一个人在崩溃。毕竟谁也不想把宝贵的摸鱼时间，浪费在逐页扒 PPT、抄重点这种无效内卷上，更不想对着满屏废话，熬得头发比 PPT 页数还少。

`课件.skill` 是一款专为“不想费脑子总结课件”的懒人（哦不，是高效人士）量身打造的 agent skill，主打一个“躺平式总结”。甭管你的 PPT 多冗长、多杂乱，哪怕是讲师凑数的废话合集，它都能帮你拆解、提炼、梳理，让你告别手动逐页抠内容的痛苦。

### 安装

复制给 OpenCode / Claude Code / 其他支持 skills 的 LLM agent：

```text
Fetch and follow instructions from:
https://raw.githubusercontent.com/Li-Baichuan-James/summarize-slides-skill/main/INSTALL.md
```

### 快速开始

1. 按 `INSTALL.md` 完成安装与环境检查：

```text
https://raw.githubusercontent.com/Li-Baichuan-James/summarize-slides-skill/main/INSTALL.md
```

2. 在会话中直接描述你的需求即可，例如：

```text
把这个课件整理成考试前看的复习资料，并生成文件。
```

3. 也可以自然说明范围与风格，例如：

```text
只总结第 3 讲到第 5 讲，中文为主，保留英文术语，做成公式和概念速查表。
```

### 默认交付物

- 默认交付物是 `.tex` 加编译后的 `.pdf`；默认编译 PDF 的工作流依赖本地可用且工作正常的 `xelatex`
- 如果缺少 `xelatex`，默认需要的 PDF 输出应视为被环境阻塞，而不是把仅有 `.tex` 视为正常成功；只有用户明确表示不需要 PDF 时，仅产出 `.tex` 才算成功
- 除非用户明确要求不生成文件，否则聊天内摘要不算默认成功交付
- 默认输出目录为源 PDF 同级的 `Summary - <pdf-stem>`
- 默认文风为中文主写，重要术语保留英文括注
- 默认内容应尽量带页码或紧凑页码范围，便于回查原课件

### 它适合做什么

- 课件复习资料
- 考点总结
- 公式 / 概念速查表
- 考前用的 cheat sheet
- 带页码引用的 lecture PDF 精简总结

### 与 `pdf` companion skill 的关系

- `summarize-slides` 必须与 `pdf` 配合使用
- `pdf` 负责 PDF 读取、提取、OCR 与页面内容确认等输入侧工作
- `summarize-slides` 负责全局通读、按讲次或主题分段、合并总结、覆盖性核查、写出 LaTeX，并在本地 LaTeX 环境可用时尝试编译最终 PDF
- 简单说：`pdf` 负责把课件读清楚，`summarize-slides` 负责把复习文档做完整

### 仓库内容

- `SKILL.md`：技能的权威说明，包含触发条件、工作流、边界与交付要求
- `INSTALL.md`：安装入口与环境检查说明
- `LICENSE`：本仓库当前发布版本附带的许可文件
- `README.md`：面向公开发布的中英双语介绍与使用说明

### 许可说明

本仓库的分发、复用与镜像以仓库内现有的 `LICENSE` 文件为准。

---

## English

`summarize-slides` is a skill for turning lecture PDFs, exported slide decks, and course handout PDFs into exam-oriented study materials. Its default outcome is a saved LaTeX source file and a compiled PDF, and that default compiled-PDF path depends on locally available `xelatex` rather than just falling back to an inline chat summary.

This repository is meant for users who want a publication-quality review artifact: key points, formulas, concepts, representative examples, and practical study guidance, with page references wherever the source quality allows.

### Installation

Tell your LLM agent:

```text
Fetch and follow instructions from:
https://raw.githubusercontent.com/Li-Baichuan-James/summarize-slides-skill/main/INSTALL.md
```

### Quick Start

1. Install and validate through `INSTALL.md`:

```text
https://raw.githubusercontent.com/Li-Baichuan-James/summarize-slides-skill/main/INSTALL.md
```

2. Then ask naturally for the output you want. For example:

```text
Summarize this lecture PDF into an exam-review cheat sheet and generate the files.
```

3. You can also specify scope and style directly. For example:

```text
Summarize only Lectures 3 to 5, keep Chinese as the main language, retain English terms, and focus on formulas and core concepts.
```

### Default Deliverables

- The default deliverables are `.tex` plus a compiled `.pdf`; the default compiled-PDF workflow depends on locally available and working `xelatex`
- If the required PDF output cannot be produced because `xelatex` is missing, that default workflow is blocked by the environment rather than successfully completed as `.tex`-only, unless the user explicitly opts out of PDF output
- Unless the user explicitly opts out of file creation, a chat-only summary is not the default successful outcome
- The default output folder is `Summary - <pdf-stem>` alongside the source PDF
- The default writing style is Chinese-first, with important technical terms preserved in English parentheses
- Summarized points should carry page citations or tight page ranges whenever extraction quality permits

### Intended Use

- Exam review sheets
- Key-point summaries for course slides
- Formula and concept cheat sheets
- Concise review PDFs generated from lecture materials
- Page-cited summaries of long lecture decks

### How It Works With the `pdf` Companion Skill

- `summarize-slides` is designed to be used together with `pdf`
- `pdf` handles PDF intake, extraction, OCR, and page-level source recovery
- `summarize-slides` governs the summarization workflow: global read, segmentation by lecture or topic, draft merge, coverage verification, LaTeX writing, and final PDF compilation when the local LaTeX environment is available
- In short: `pdf` helps the agent read the source correctly, and `summarize-slides` governs how the final study artifact is produced

### Repository Contents

- `SKILL.md`: canonical skill specification, workflow, boundaries, and required outputs
- `INSTALL.md`: installation entry point and environment validation guide
- `LICENSE`: license file included with the current published repository
- `README.md`: publication-facing bilingual overview and usage guide

### License Note

Distribution, reuse, and mirroring of this repository are governed by the `LICENSE` file included in the repository.
