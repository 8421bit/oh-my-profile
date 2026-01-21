# oh-my-profile - 你的个人 AI 档案

> 构建你的数字自我，让 AI 真正了解你是谁、你知道什么、你能做什么。

[English](README.md)

---

## 安装

**推荐：克隆到主目录**

```bash
# 克隆到 ~/oh-my-profile/
git clone https://github.com/8421bit/oh-my-profile.git ~/oh-my-profile

# 添加为本地市场
/plugin marketplace add ~/oh-my-profile/.claude-plugin/marketplace.json

# 安装技能
/skills install oh-my-profile
```

---

## 快速开始

安装后，尝试对 AI 说：

| 场景 | 你说 | AI 会做 |
|------|------|---------|
| **初始化** | "帮我初始化 oh-my-profile" | 创建 ~/oh-my-profile/ 目录，引导填写档案 |
| **知识沉淀** | "帮我记一下" / "Save this" | 提取洞察，保存到 knowledge/ |
| **整理内容** | "整理这个" + 网址/文本 | 解析并结构化保存 |
| **技能发现** | "这个可以做成技能吗" / "Create skill" | 引导创建个人技能 |
| **技能规划** | "规划我的技能" / "Plan my skills" | Gap 分析 + 推荐开源 skill |
| **同步档案** | "同步档案" / "Sync profile" | 手动同步用户目录到 skill references |

**提示**：AI 会自动读取你的档案提供个性化服务，无需每次手动触发。

---

## 什么是 oh-my-profile？

**oh-my-profile** 是一个**个人 AI 档案**系统 —— 你完整的**数字自我**，AI 可以理解的格式。

它不仅仅是知识库，不仅仅是记忆系统。它是一个帮助 AI 真正了解你的系统化方法：

| 组件 | 回答什么问题 | 性质 |
|------|-------------|------|
| `my-profile.md` | **你是谁？** | 身份 + 偏好 + 目标 |
| `my-knowledge.md` | **你知道什么？** | 知识索引 + 学习规划 |
| `my-skills.md` | **你能做什么？** | 技能索引 + 发展路径 |
| `knowledge/` | 积累的洞察 | 经验 + 学习 |
| `skills/` | 个人技能 | 能力 + 方法 |

安装 oh-my-profile 后，会在你的主目录创建 `~/oh-my-profile/` 目录：

```
~/oh-my-profile/
├── my-profile.md     # 你的身份（你是谁、偏好、目标）
├── my-knowledge.md   # 知识索引 + 学习规划
├── my-skills.md      # 技能索引 + 发展路径
├── knowledge/        # 你的洞察和经验（Obsidian 兼容）
└── skills/           # 你的 Agent Skills（可复用能力）
```

**AI 读取这些内容来提供个性化服务。**

---

## 核心理念

**在 AI 时代，什么让一个人独特？**

```
信息
  ↓
思考 / 消化 / 整理
  ↓
知识  →  my-knowledge.md + knowledge/
  ↓
技能 (Agent Skills)  →  my-skills.md + skills/
  ↓
可复用的能力
```

**档案 + 知识 + 技能 = 你在 AI 世界的数字自我**

从被动接收到主动创造 —— 这是持续的个人进化。

---

## 3 个元技能

oh-my-profile 包含 3 个内置的「元技能」，帮助你构建和维护数字自我：

| 技能 | 功能 | 触发示例 |
|------|------|----------|
| **oh-my-profile** | 核心入口 + 初始化 + 档案同步 | 任何对话、"初始化"、"同步档案" |
| **oh-my-knowledge** | 从对话、网址、文件中捕获洞察 | "帮我记一下"、"整理这个"、"Save this" |
| **oh-my-skills** | 发现模式并创建可复用技能 | "创建技能"、"分析知识库"、"Create skill" |

### oh-my-profile（核心入口）

AI 读取的中心技能，完整了解你。

**能力：**
- 自动同步：检测 ~/oh-my-profile/ 的变化并更新 references
- 从 `references/` 加载你的完整档案
- 首次运行时初始化 `~/oh-my-profile/` 目录
- 通过苏格拉底式对话引导填写档案
- 分析档案规划技能（Gap 分析）

### oh-my-knowledge（知识沉淀）

你的思维搭档，帮助捕获和整理洞察。

**触发条件：**
- "帮我记一下" / "Save this" → 保存对话洞察
- "整理这个" + 网址/文本 → 整理提供的内容
- "整理这些文件" + 文件夹 → 批量处理文件
- 对话产生有价值洞察时主动建议

**人格特质：**
- 倾听者 - 真正倾听，不打断
- 鼓励但不谄媚 - "这个有意思"，而非"太棒了！"
- 挑战但不挑刺 - 有价值的质疑
- 睿智而谦虚 - 有见解，但知道你是专家

### oh-my-skills（技能发现）

知识到技能的进化系统。

**触发条件：**
- "这个可以做成技能" / "Create skill" → 捕获当前模式
- "从知识创建技能" / "分析知识库" → 分析知识提取模式
- 自动：检测重复工作（3次以上）
- 发现非显而易见的解决方案（调查超过10分钟）

**质量门控：**
- 可复用？能帮助未来任务？
- 非平凡？不是简单查文档？
- 具体？有明确触发条件？
- 已验证？确实有效？

---

## 如何工作

### 阶段 1：档案设置

```
1. 安装 oh-my-profile → 创建 ~/oh-my-profile/
2. AI 通过苏格拉底式对话引导填写档案
3. 生成 my-knowledge.md（学习规划）和 my-skills.md（技能缺口）
4. 同步到 oh-my-profile/references/ 供 AI 读取
```

### 阶段 2：知识沉淀

```
你的对话 → AI 倾听并确认理解
        → 选择思维方法（苏格拉底、第一性原理等）
        → 提问，你发现洞察
        → 建议："要我帮你沉淀一下吗？"
        → 保存到 ~/oh-my-profile/knowledge/
        → 更新 my-knowledge.md 索引
```

### 阶段 3：技能发现

```
检测到重复工作 → AI 建议："这个可以做成技能吗？"
              → 通过对话引导技能定义
              → 创建 ~/oh-my-profile/skills/[skill-name]/
              → 更新 my-skills.md 索引
```

### 阶段 4：持续进化

```
my-profile.md（你的目标）
       ↓
my-knowledge.md（学什么）+ my-skills.md（掌握什么）
       ↓
knowledge/（积累）+ skills/（创建）
       ↓
你越来越接近档案中的目标
```

---

## 核心差异化

| 传统 AI | oh-my-profile |
|---------|---------------|
| "用完即弃" | "留下痕迹" |
| 直接给答案 | 通过问题引导 |
| 通用回复 | 个性化到你的档案 |
| 工具导向 | 关系导向 |
| 无记忆 | 持续进化 |
| ❌ 从零开始 | ✅ 了解你的历史 |
| ❌ 通用建议 | ✅ 基于你的目标 |

---

## 用户工作区

oh-my-profile 的输出保存在你的主目录，独立于任何项目：

```
~/oh-my-profile/
├── my-profile.md           # 你的身份 + 偏好 + 目标
├── my-knowledge.md         # 知识索引 + 学习规划
├── my-skills.md            # 技能索引 + 发展路径 + Gap 分析
├── knowledge/              # 知识文件（Obsidian 兼容）
│   └── YYYY-MM-DD_topic.md
└── skills/                 # 个人技能
    └── [skill-name]/
        └── SKILL.md
```

**数据在这里，用户可以手动编辑。这是数据源。**

---

## 双轨设计：Obsidian + AI

`~/oh-my-profile/` 同时是 **Obsidian 知识库** 和 **AI 可读的档案**：

```
┌─────────────────────────────────────────────────┐
│              ~/oh-my-profile/                   │
│                                                 │
│   ┌───────────────┐     ┌───────────────┐      │
│   │   AI 轨道     │     │  用户轨道     │      │
│   │               │     │               │      │
│   │ oh-my-*       │     │  Obsidian     │      │
│   │ skills        │     │  直接编辑     │      │
│   │ 读写          │     │               │      │
│   └───────┬───────┘     └───────┬───────┘      │
│           │                     │              │
│           └──────────┬──────────┘              │
│                      │                         │
│           同一个 Obsidian 知识库               │
│           (Markdown + Wikilinks + Tags)        │
└─────────────────────────────────────────────────┘
```

### AI 轨道
- **oh-my-profile**：读取完整档案，初始化目录，自动同步变化
- **oh-my-knowledge**：捕获洞察，创建知识文件
- **oh-my-skills**：发现模式，创建技能文件

### 用户轨道
- 将 `~/oh-my-profile/` 作为 **Obsidian 知识库** 打开
- 使用 Obsidian 的可视化编辑器直接编辑文件
- 使用 **wikilinks** `[[note]]` 连接知识
- 使用 **Graph View** 可视化知识结构
- 使用 **Tags** 和 **Properties** 组织内容

### 为什么这样设计？

| 优势 | 说明 |
|------|------|
| **两全其美** | AI 捕获，用户策展 |
| **无锁定** | 标准 markdown，无需 AI 也能用 |
| **可视化管理** | Obsidian 的图谱视图、搜索、反向链接 |
| **持续进化** | AI 和用户共同贡献 |

**推荐工作流：**
1. AI 在对话中捕获洞察 → `knowledge/`
2. 用户在 Obsidian 中审阅和整理
3. AI 基于知识模式建议技能
4. 用户决定保留和优化什么

---

## 项目结构

```
oh-my-profile/                          # 插件仓库
├── skills/
│   ├── oh-my-profile/                  # 核心入口
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── my-profile.md           # 模板 → 用户数据
│   │       ├── my-knowledge.md         # 模板 → 用户数据
│   │       └── my-skills.md            # 模板 → 用户数据
│   ├── oh-my-knowledge/                # 知识沉淀
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── obsidian-knowledge-rules.md
│   └── oh-my-skills/                   # 技能发现
│       ├── SKILL.md
│       └── references/
│           └── agent-skills-spec.md
├── .claude-plugin/
├── README.md
├── README_CN.md
└── .gitignore
```

---

## 开始使用

安装后：

1. **首次运行** - AI 检测到 `~/oh-my-profile/` 不存在
2. **创建结构** - 带模板文件的目录
3. **引导档案** - 苏格拉底式对话填写 my-profile.md
4. **规划成长** - 生成学习规划和技能缺口
5. **就绪** - AI 现在了解你，可用于所有未来对话

---

## 进化哲学

你的数字自我随着你进化：
- 更多对话 → 知识积累
- 识别模式 → 技能提取
- 优化目标 → 规划相应更新

**oh-my-profile 促进这种进化：**
- 主动捕获你可能错过的洞察
- 识别重复工作模式
- 建议技能自动化工作流
- 跟踪向目标的进展

---

## 适合谁？

### 知识工作者
构建一个 AI 可以利用的**个人知识库**，获得更好的帮助。

### 开发者
创建可复用 Agent Skills 的**个人技能库**。

### 终身学习者
用结构化的知识和技能发展跟踪你的**学习旅程**。

### AI 深度用户
建立真正的 **AI 伙伴关系**，让 AI 随时间理解你的上下文。

**配合 Obsidian 使用效果最佳**，可以链接笔记并构建知识图谱。

---

## 规范合规

**Agent Skills 规范：**
- 遵循官方 Agent Skills 格式
- 支持渐进式披露和动态加载
- 参见 `oh-my-skills/references/agent-skills-spec.md`

**Obsidian 知识规范：**
- 遵循 Obsidian Flavored Markdown 格式
- 支持 wikilinks、callouts、properties 等所有 Obsidian 特性
- 参见 `oh-my-knowledge/references/obsidian-knowledge-rules.md`

---

## 许可证

MIT
