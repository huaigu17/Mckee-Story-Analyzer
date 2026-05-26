# Mckee-Story-Analyzer

An AI skill that analyzes scripts, novels, and short fiction through the lens of Robert McKee's Story trilogy (Story, Dialogue, Character). Works like a professional literary critic — diagnostic analysis backed by theory, then actionable rewrite suggestions.

## What makes it different

- **Theory-grounded, not vague** — every critique cites McKee's specific concepts (the Gap, the Inciting Incident, Subtext, the Principle of Antagonism)
- **Prescriptive, not just critical** — each problem gets a concrete rewrite demo
- **Format-adaptive** — built-in three-tier scaling system prevents judging short stories by feature-film standards

## Five dimensions of analysis

| Dimension | What it examines |
|-----------|-----------------|
| Story Structure | Inciting incident, progressive complications, crisis/climax/resolution |
| Character Design | Characterization vs true character, conscious vs unconscious desire, arc |
| Dialogue & Text | Three functions of dialogue, subtext, show vs tell, narrative rhythm |
| Genre | Genre conventions, innovation within the contract, value change |
| Scene Design | Beats, turning points, value change, sequence architecture |

## Format-adaptive analysis

McKee's original framework assumes a 90-120 minute feature film. This skill scales its criteria to match the work's actual length:

- **Feature / Novel (>50k words)** — full McKee five-part structure standard
- **Novella / Episode (10k-50k)** — simplified structure, condensed arc allowed
- **Short fiction / Flash (<10k words)** — single-effect principle, type characters and lens narrators recognized as valid devices

The format tier is determined before analysis begins. Every dimension note declares which scale is in use.

## Workflow

1. Receive and classify — format, genre, length tier
2. Diagnose across dimensions — load reference material on demand
3. Prescribe — actionable revision with rewrite demonstration
4. Summarize — strengths, prioritized issues, overall direction

## Use cases

- Submit a story or script for professional critique
- Identify core strengths and weaknesses
- Get McKee-grounded revision suggestions with before/after demos
- Discuss structural, character, or dialogue problems



---


## V2.0 Update

### Overview

McKee Story Analyzer v2 is a major upgrade. It retains the original 5-dimension diagnostic framework (Story Structure, Character Design, Dialogue & Text, Genre & Form, Scene Design) and the format-adaptation system, while introducing three core new capabilities.

### What's New

#### 1. Three Analytical Tones

Users select their preferred tone before analysis begins. The entire output adjusts accordingly:

| Mode | Description | Best For |
|------|-------------|----------|
| **Sharp** | Direct, blunt, skips the "praise-first" convention | Experienced writers who want fast, actionable criticism |
| **Objective** | Balanced, professional, theory-backed diagnoses | Writers seeking comprehensive, even-handed evaluation **[Default]** |
| **Encouraging** | Gentle, constructive, positive-first framing (≥2:1 ratio) | Beginners or writers needing confidence support |

A selection interface appears at the start of each session with brief descriptions of each mode.

#### 2. RAG Knowledge Base System

**1,828 structured knowledge entries** automatically extracted from McKee's trilogy (STORY, DIALOGUE, CHARACTER) EPUB, tagged across **24 concept dimensions** (Inciting Incident, The Gap, Character Arc, Subtext, Value Change, etc.).

During analysis, Claude retrieves original McKee quotations via keyword search to ensure every diagnosis is grounded in precise theory. A companion `query_mckee_kb.ps1` script provides RAG-style querying.

#### 3. Two Modes: Critique Only + Co-Creation

The original single workflow has been split into two independent modes:

| Mode | Workflow | Output |
|------|----------|--------|
| **Critique Only** | Diagnose → Recommend → Report | Professional diagnostic report without rewriting |
| **Co-Create** | Diagnose → Discuss → Iterative Rewrite → Review | Collaborative revision through iterative dialogue |

Both modes are dispatched automatically via the main skill's routing system to dedicated sub-agents.

### Additional Improvements

- **6 Deep Reference Files**: 12 inciting incident variants, 3-layer gap model, 7 subtext techniques, 14 arc subtypes, 60+ value shifts, 15×5 genre matrix
- **9 Classic Case Studies**: 3 movies, 3 TV series, 3 novels—works McKee himself analyzed, serving as reference coordinates
- **All existing reference files updated** with cross-references to deep files and the knowledge base

### File Structure

```
mckee-story-analyzer/
├── SKILL.md                          ← Main router (tone selection + dual mode)
├── references/
│   ├── tone-guide.md                 ← [NEW] Tone specifications
│   ├── mckee-knowledge-base.json     ← [NEW] RAG knowledge base (1,828 entries)
│   ├── deep/ (6 files)               ← [NEW] Deep concept breakdowns
│   └── case-studies/ (9 files)       ← [NEW] Classic work analyses
├── sub-skills/
│   ├── critique-only/SKILL.md        ← [NEW] Critique-only sub-skill
│   └── co-create/SKILL.md            ← [NEW] Co-creation sub-skill
└── scripts/
    ├── query_mckee_kb.ps1            ← [NEW] RAG query script
    └── extract_mckee_kb.ps1          ← [NEW] EPUB extraction script
```


## McKee Story Analyzer v2.1 — Changelog

**Core change: New three-layer work suitability classifier (Step 0)**

Previous versions applied McKee analysis to all "scripts/novels" without checking whether the work was actually suitable for McKee's dramatic narrative framework. v2.1 inserts a pre-filter before routing and tone selection, with three layers:

1. **Gate check** — Three questions: does it have a clear protagonist? Is the plot driven by character choices? Is there a value-turning point (positive/negative shift)? All three pass → enter McKee pipeline; two or more fail → deemed unsuitable, alternative frameworks recommended (Campbell's monomyth, kishōtenketsu, Chinese zhanghui narrative, etc.); borderline cases (two pass, one ambiguous) → allowed entry but marked "partial elements missing."

2. **Plot type classification** — Distinguishes archplot/minimalism/antiplot. Archplot → full McKee standards; minimalism → entry with caveats (no requirement for complete five-part structure, active protagonist, etc.); antiplot → skip to alternatives.

3. **Medium classification** — Screenplay/film → McKee's native domain, strongest applicability; novel → applicable with noted limitations (McKee's system is based on 90–120 minute films); short story → deferred to format-adaptation standards; poetry/atmospheric works → not applicable.

Existing workflow steps renumbered: old Step 0 (routing + tone) → Step 1, old Step 1 (format classification) → Step 2, and so on. All internal cross-references have been updated accordingly.




    
# McKee Story Analyzer

基于罗伯特·麦基《故事》《对白》《人物》三部曲的理论框架，对剧本、小说等文学创作进行专业点评与修改优化的 AI skill。

像一个文学评论家那样工作——先做冷静的理论诊断，再给出可操作的修改方案。

## 它不是什么

- ❌ 不是泛泛的"写得不错"——每个诊断引用麦基理论中的具体概念
- ❌ 不是只会批评的鉴赏家——每个问题附带示范改写
- ❌ 不是拿长片标准量一切的教条主义者——内置格式自适应系统

## 五大分析维度

| 维度 | 关注什么 |
|------|---------|
| 故事结构 | 激励事件、鸿沟原理、高潮的必然性与意外性 |
| 人物设计 | 人物塑造 vs 真人物、自觉/不自觉欲望、人物弧光 |
| 对白与文本 | 对白三功能、潜文本、展示 vs 讲述、叙述节奏 |
| 类型与体裁 | 类型约定、类型创新、核心价值的不可逆转变 |
| 场景设计 | 节拍分析、转折点、价值转变、序列设计 |

## 格式自适应

麦基的理论建立在长片剧本上。直接套在极短篇上会产生误判。本 skill 内置三档标准：

| 篇幅 | 字数 | 适用尺度 |
|------|------|---------|
| 长片/长篇 | >5万 | 完整麦基五部分结构标准 |
| 中篇 | 1-5万 | 简化结构 |
| 极短篇/短片 | <1万 | 单一效果原则，放宽结构/人物要求 |

分析前强制判定级别。每个维度标注使用了哪一级标准。

## 工作流

1. 接收与归类 — 格式、类型、篇幅
2. 五维诊断 — 逐维度引用理论点评优缺点
3. 修改方案 — 可操作的修改建议 + 示范改写
4. 综合总结 — 优势、问题优先级、总体方向



# McKee Story Analyzer v2 — 更新说明 / Release Notes

## 中文

### 概述

McKee Story Analyzer v2 是一次重大升级。在保留原有五维诊断（故事结构、人物设计、对白与文本、类型与体裁、场景设计）和格式自适应系统的基础上，新版本引入了三大核心新能力。

### 三大更新

#### 1. 三种分析语气

用户可在分析前选择语气，系统将据此调整整个输出的措辞风格：

| 模式 | 说明 | 适合谁 |
|------|------|--------|
| **尖刻模式** (Sharp) | 直指缺陷，不绕弯子，跳过"先扬后批" | 已有一-基础、想快速找到致命问题的创作者 |
| **客观模式** (Objective) | 优缺点并重，专业持平，每诊断必有理论引用 | 希望获得平衡专业评估的创作者 **[默认]** |
| **鼓励模式** (Encouraging) | 温和建设，肯定比例 ≥ 2:1，问题包裹在正向框架中 | 新手作者、需要信心支持的创作阶段 |

选择界面在分析开始时弹出，附各模式简介，用户一目了然。

#### 2. RAG 知识库系统

从《故事》《对白》《人物》三部曲 EPUB 中自动提取了 **1,828 条结构化理论文本**，按 **24 个概念维度**（激励事件、鸿沟原理、人物弧光、潜文本、价值转变等）标注。分析时可通过关键词检索获取麦基原著原文引用，确保每个诊断都有精确的理论支撑。

配套 `query_mckee_kb.ps1` 脚本提供 RAG 式查询。

#### 3. 双模式：纯点评 + 共创修改

将原有的"点评+修改"拆分成了两个独立工作流：

| 模式 | 工作流 | 产出 |
|------|--------|------|
| **纯点评** (Critique Only) | 诊断 → 建议方向 → 报告 | 专业诊断报告，不参与改写 |
| **共创修改** (Co-Create) | 诊断 → 讨论 → 逐轮改写 → 复审 | 在迭代对话中完成修改 |

两种模式通过主 skill 的路由系统自动派发到对应的子 agent。

### 其他改进

- **6 个深度参考文件**：激励事件 12 种变体、鸿沟三层递进模型、潜文本 7 种技术、弧光 14 种子类型、价值图谱 60+ 种、类型矩阵 15×5
- **9 个经典案例**：麦基本人重点分析过的电影×3、剧集×3、小说×3，提供"参考坐标"
- **更新了所有现有参考文件**，添加了与深度文件和知识库的交叉引用

### 文件结构

```
mckee-story-analyzer/
├── SKILL.md                          ← 主路由（含语气选择 + 双模式）
├── references/
│   ├── tone-guide.md                 ← [NEW] 语气规范
│   ├── mckee-knowledge-base.json     ← [NEW] RAG 知识库
│   ├── deep/ (6 files)               ← [NEW] 深度概念拆解
│   └── case-studies/ (9 files)       ← [NEW] 经典案例
├── sub-skills/
│   ├── critique-only/SKILL.md        ← [NEW] 纯点评子 skill
│   └── co-create/SKILL.md            ← [NEW] 共创修改子 skill
└── scripts/
    ├── query_mckee_kb.ps1            ← [NEW] RAG 查询脚本
    └── extract_mckee_kb.ps1          ← [NEW] EPUB 提取脚本
```
## McKee Story Analyzer v2.1 — 更新说明

**核心变更：新增作品适用性三层分类器（Step 0）**

之前的版本对所有"剧本/小说"类作品统一启动麦基分析，未区分作品是否真的适合用麦基的戏剧叙事理论框架。v2.1 在路由和语气选择之前插入了一层前置过滤，分三步判断：

1. **门控检查** — 三个问题：有无明确主角、情节是否由角色选择驱动、有无正负价值转折点。全通过才进入麦基管道；两项不通过则判定为不适合，推荐替代框架（Campbell 神话理论、起承转合、章回体叙事等）；边界情况（两绿一黄）允许进入但标注"部分要素缺失"。

2. **情节类型判断** — 区分大情节/小情节/反情节。大情节完整适用麦基标准；小情节进入但标注限制（不要求完整五部分结构、不要求主动主人公等）；反情节跳至替代方案。

3. **媒介判断** — 剧本/电影为麦基原生领域最强适用；长篇小说标注局限性（麦基体系基于 90-120 分钟电影）；短篇转至格式自适应标准；诗歌/氛围型不适用。

现有工作流步骤顺延：原 Step 0（路由+语气）→ Step 1，原 Step 1（格式归类）→ Step 2，以此类推。所有内部交叉引用已同步更新。
---
