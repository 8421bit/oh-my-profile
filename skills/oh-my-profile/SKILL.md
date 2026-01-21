---
name: oh-my-profile
description: |
  Personal AI profile system - reads ~/oh-my-profile/ to understand user's complete digital self.
  Contains my-profile.md (identity/preferences/goals), my-knowledge.md (knowledge index), my-skills.md (skills index).
  Use when:
  (1) Starting any conversation - auto-load user profile for personalized context
  (2) User says "初始化"/"initialize"/"setup my profile"/"创建档案" - first-time setup
  (3) User says "同步档案"/"sync profile"/"更新画像"/"profile changed" - sync user data
  (4) User says "规划技能"/"plan skills"/"我需要什么技能"/"skill gap analysis" - analyze and recommend skills
  (5) User asks "who am I"/"了解我"/"我的档案" - show user profile summary
  (6) Auto-sync when ~/oh-my-profile/ files changed since last read
  Covers: profile initialization, Socratic dialogue guidance, skill gap analysis, open-source skill recommendations.
license: MIT
metadata:
  author: 8421bit
  version: "1.0.0"
---

# oh-my-profile - Your Personal Agent Profile

> 你的数字自我，AI 读取此 skill 即可完整了解你。

## 核心文件

| 文件 | 作用 | 位置 |
|------|------|------|
| `my-profile.md` | 我是谁（身份、偏好、目标） | `references/` + `~/oh-my-profile/` |
| `my-knowledge.md` | 我知道什么（知识索引+学习规划） | `references/` + `~/oh-my-profile/` |
| `my-skills.md` | 我能做什么（技能索引+发展路径） | `references/` + `~/oh-my-profile/` |

---

## 何时使用

- 首次安装 oh-my-profile 后
- 用户说「初始化」「setup my profile」「创建我的档案」
- 用户说「我更新了 profile」「sync profile」「同步画像」
- 用户说「规划技能」「plan my skills」「我需要什么技能」
- 发现 `~/oh-my-profile/my-profile.md` 有更新

---

## 读取用户画像

每次对话开始时：

### 步骤 0: 自动同步检查

```
1. 检查 ~/oh-my-profile/ 目录是否存在
2. 如果存在，比较用户目录文件与 references/ 的修改时间
3. 如有变化，静默同步更新 references/
4. 无需用户主动触发，自动保持同步
```

### 步骤 1: 读取核心文件

```
1. 读取 references/my-profile.md    → 了解用户身份
2. 读取 references/my-knowledge.md  → 了解用户知识
3. 读取 references/my-skills.md     → 了解用户技能
```

基于这些信息提供个性化服务。

---

## 首次初始化

如果 `~/oh-my-profile/` 目录不存在，执行初始化：

### 步骤 1: 检查并创建目录

```
1. 检查 ~/oh-my-profile/ 是否存在
2. 如果不存在，创建以下结构：
   ~/oh-my-profile/
   ├── my-profile.md     (从模板复制)
   ├── my-knowledge.md   (从模板复制)
   ├── my-skills.md      (从模板复制)
   ├── knowledge/        (空目录)
   └── skills/           (空目录)
3. 如果已存在，告知用户并询问是否重新初始化
```

### 步骤 2: 引导填写 Profile

读取 `~/oh-my-profile/my-profile.md` 模板，引导用户填写以下必要信息：

**必填项**：
- 姓名/称呼
- 角色/职业
- 语言偏好（中文/英文/双语）
- 沟通风格偏好

**选填项**：
- 决策风格
- 技能专长
- 学习偏好
- AI 交互偏好
- 当前项目
- 职业目标

**使用苏格拉底式对话引导，不要一次问太多问题。**

### 步骤 3: 生成索引文件

基于 my-profile.md 生成初始的：
- `my-knowledge.md` - 知识索引（含学习规划）
- `my-skills.md` - 技能索引（含发展路径 + Gap 分析）

### 步骤 4: 个人技能规划

基于 my-profile.md 中的信息，分析用户可能需要的技能：

#### 分析维度

| 维度 | 分析内容 | 示例提案 |
|------|----------|----------|
| **角色/职业** | 该角色常用的工作技能 | PM → PRD撰写、竞品分析 |
| **技能专长** | 可以沉淀为 skill 的专长 | AI领域 → AI工具评测 |
| **当前项目** | 项目相关的重复工作 | 电商 → 数据报表生成 |
| **学习目标** | 学习过程的辅助技能 | 学Python → 代码审查 |
| **日常工作** | 高频重复的任务 | 会议 → 会议纪要生成 |

#### 搜索开源 Skills

对于每个规划的技能，搜索是否已有开源实现：

```
搜索关键词：
- "claude code skill [功能关键词]"
- "agent skill [功能关键词] github"
- "anthropics/skills [功能关键词]"

优先检查：
- https://github.com/anthropics/skills
- https://github.com/topics/claude-code-skill
```

#### 更新 my-skills.md

将分析结果写入 `my-skills.md` 的「技能缺口分析」部分：

```markdown
## 技能缺口分析

| 目标技能 | 当前状态 | 建议路径 |
|----------|----------|----------|
| [技能1] | ❌ 缺失 | 推荐安装: [开源仓库链接] |
| [技能2] | ⚠️ 部分 | 引导创作 |
| [技能3] | ✅ 已有 | - |

## 学习任务清单

- [ ] 安装 [技能1]
- [ ] 创建 [技能2]
```

#### 询问用户

```
基于你的档案，我规划了以下技能建议：

1. **[技能1]** - [描述]
2. **[技能2]** - [描述]
3. **[技能3]** - [描述]

这些已保存到 my-skills.md。
你想现在就创建或安装其中某个技能吗？
```

### 步骤 5: 同步到 references

将用户目录的 3 个文件同步到 skill 的 `references/`：

```
~/oh-my-profile/my-profile.md    → references/my-profile.md
~/oh-my-profile/my-knowledge.md  → references/my-knowledge.md
~/oh-my-profile/my-skills.md     → references/my-skills.md
```

### 步骤 6: 确认完成

```
oh-my-profile 初始化完成！

已创建：
✅ ~/oh-my-profile/my-profile.md
✅ ~/oh-my-profile/my-knowledge.md（含学习规划）
✅ ~/oh-my-profile/my-skills.md（含技能规划）
✅ ~/oh-my-profile/knowledge/
✅ ~/oh-my-profile/skills/

现在你可以：
- 使用 oh-my-knowledge 沉淀对话中的知识
- 使用 oh-my-skills 创建个人技能
- 查看 my-skills.md 中的技能建议
- AI 会读取你的档案提供个性化服务
```

---

## Profile 同步更新

当检测到 `~/oh-my-profile/` 中的文件有更新时：

### 触发条件

- 用户说「我更新了 profile」「profile 变了」「sync profile」
- 用户说「同步画像」「更新我的画像」
- 在对话中发现用户目录内容与 references 不一致

### 同步流程

```
1. 读取 ~/oh-my-profile/my-profile.md
2. 读取 ~/oh-my-profile/my-knowledge.md
3. 读取 ~/oh-my-profile/my-skills.md
4. 更新 references/ 中的对应文件
5. 检查是否有新的技能规划机会
6. 如有新规划，更新 my-skills.md
7. 确认同步完成
```

### 同步确认

```
Profile 同步完成！

已更新：
✅ references/my-profile.md
✅ references/my-knowledge.md
✅ references/my-skills.md

变更摘要：
- [列出主要变更项]
```

---

## 技能规划（独立功能）

用户可随时触发技能规划：

### 触发条件
- 用户说「规划技能」「plan my skills」
- 用户说「我需要什么技能」「帮我分析需要的技能」

### 执行流程
```
1. 读取 ~/oh-my-profile/my-profile.md
2. 分析角色、专长、项目、目标
3. 搜索开源 skills 推荐
4. 更新 ~/oh-my-profile/my-skills.md
5. 同步到 references/my-skills.md
6. 询问用户是否立即创建或安装
```

---

## 模板引用

首次安装时，references/ 中的 3 个文件为模板结构。
初始化后，它们会被替换为用户的真实数据。

- `references/my-profile.md` - 个人档案模板/数据
- `references/my-knowledge.md` - 知识索引模板/数据
- `references/my-skills.md` - 技能索引模板/数据

---

## 注意事项

- 如果用户中途退出，保存已填写的内容
- 可以随时运行再次初始化来更新 profile
- **用户目录是数据源**：`~/oh-my-profile/` 中的文件用户可手动编辑
- **references 是同步副本**：供大模型快速读取
- **my-profile.md 和 references/my-profile.md 应保持同步**
- **技能规划是建议性的，用户决定是否创建或安装**
