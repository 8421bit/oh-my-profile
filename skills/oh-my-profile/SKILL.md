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

## 运行流程与 omp-my-profile 的关系

### 正确的执行顺序
1. **初始化目录结构**
   - 创建 `~/oh-my-profile/` 目录
   - 创建 `knowledge/` 和 `skills/` 子目录

2. **创建/更新三个核心文件**
   - `~/oh-my-profile/my-profile.md` - 个人档案
   - `~/oh-my-profile/my-knowledge.md` - 知识索引
   - `~/oh-my-profile/my-skills.md` - 技能索引

3. **构建 omp-my-profile 技能**
   - 基于三个核心文件的内容创建简化画像
   - 生成 `~/oh-my-profile/skills/omp-my-profile/SKILL.md`

### 目录结构规范
- **`~/oh-my-profile/skills/oh-my-profile/references/`**: 只包含模板文件（带 `-template` 后缀）
  - `my-profile-template.md`
  - `my-knowledge-template.md`
  - `my-skills-template.md`

- **`~/oh-my-profile/`**: 只包含生成的用户数据文件（不带 `-template` 后缀）
  - `my-profile.md`
  - `my-knowledge.md`
  - `my-skills.md`

### 技能分工
- **oh-my-profile**: 完整的 profile 管理系统
  - 负责步骤 1-2：初始化和管理三个核心文件
  - **不直接用于 AI 上下文提供**

- **omp-my-profile**: 个人简化画像技能
  - 在步骤 3 中基于三个核心文件创建
  - 专门为 AI 提供快速上下文
  - 位于 `~/oh-my-profile/skills/omp-my-profile/`

### 更新流程
当您需要更新个人画像时，有以下两种情况：

#### 情况1：通过 oh-my-profile 技能更新
- 运行 oh-my-profile 技能（如 `/初始化`、`/setup my profile` 等）
- 技能会生成/更新三个核心文件，并自动构建 omp-my-profile 技能

#### 情况2：通过其他渠道更新核心文件
- 您可能直接编辑了 `~/oh-my-profile/` 目录下的三个核心文件
- 当您明确要求更新画像时（如说「更新我的 profile」、「重新生成画像」等）
- oh-my-profile 技能会**基于现有的三个核心文件重新构建 omp-my-profile 技能**

这样确保 omp-my-profile 技能始终与您的最新核心文件保持同步。

## 核心文件

| 文件 | 作用 | 位置 |
|------|------|------|
| `my-profile.md` | 我是谁（身份、偏好、目标） | `~/oh-my-profile/my-profile.md` |
| `my-knowledge.md` | 我知道什么（知识索引+学习规划） | `~/oh-my-profile/my-knowledge.md` |
| `my-skills.md` | 我能做什么（技能索引+发展路径） | `~/oh-my-profile/my-skills.md` |
| `*-template.md` | 模板文件（首次安装时创建） | `~/oh-my-profile/skills/oh-my-profile/references/` |

---

## 何时使用

- 首次安装 oh-my-profile 后
- 用户说「初始化」「setup my profile」「创建我的档案」
- 用户说「我更新了 profile」「profile 变了」「更新我的画像」
- 用户说「重新生成画像」「重建 omp-my-profile」
- 用户说「规划技能」「plan my skills」「我需要什么技能」

---

## 读取用户画像

oh-my-profile 技能**不直接用于 AI 上下文提供**。AI 上下文由 omp-my-profile 技能提供。

oh-my-profile 技能的主要作用是：
- 管理 `~/oh-my-profile/` 目录下的三个核心文件
- 初始化项目目录结构
- 构建或更新 omp-my-profile 技能

当 oh-my-profile 技能运行时，它会：
1. 生成/更新三个核心文件
2. 确保目录结构正确
3. 基于核心文件构建 omp-my-profile 技能

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

基于 my-profile.md 生成初始的索引文件：

- `my-knowledge.md` - **知识索引文件**（不是知识内容），包含：
  - 对 `~/oh-my-profile/knowledge/` 目录中所有知识文件的链接和摘要
  - 基于个人档案的学习规划和待补充知识清单
  - 使用 Obsidian 双链语法 `[[filename|display name]]` 链接到具体知识文件

- `my-skills.md` - 技能索引（含发展路径 + Gap 分析）

### 重要说明
- `my-knowledge.md` 是**索引文件**，不是知识内容文件
- 所有具体知识必须保存为单独的 `.md` 文件在 `~/oh-my-profile/knowledge/` 目贯中
- 索引文件通过 Obsidian 双链链接到具体知识文件
- 当使用 oh-my-knowledge 技能沉淀新知识时，会自动：
  1. 创建新的知识文件到 `~/oh-my-profile/knowledge/` 目录
  2. 更新 `my-knowledge.md` 索引文件，添加对应的链接

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

将用户目录的 3 个文件同步到技能的 references 目录：

```
~/oh-my-profile/my-profile.md    → ~/oh-my-profile/skills/oh-my-profile/references/my-profile.md
~/oh-my-profile/my-knowledge.md  → ~/oh-my-profile/skills/oh-my-profile/references/my-knowledge.md
~/oh-my-profile/my-skills.md     → ~/oh-my-profile/skills/oh-my-profile/references/my-skills.md
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

## Profile 更新检测

当用户明确要求更新个人画像时，oh-my-profile 技能会执行以下操作：

### 触发条件
- 用户说「我更新了 profile」「profile 变了」「更新我的画像」
- 用户说「重新生成画像」「重建 omp-my-profile」
- 用户明确要求同步或更新个人画像

### 更新流程
```
1. 读取 ~/oh-my-profile/my-profile.md
2. 读取 ~/oh-my-profile/my-knowledge.md
3. 读取 ~/oh-my-profile/my-skills.md
4. 基于三个核心文件的内容重新构建 omp-my-profile 技能
5. 确保简化画像与核心文件保持同步
6. 确认更新完成
```

### 更新确认
```
Profile 更新完成！

已重新构建：
✅ ~/oh-my-profile/skills/omp-my-profile/SKILL.md

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

### 文件位置规范
- **模板文件**（带 `-template` 后缀）：`~/oh-my-profile/skills/oh-my-profile/references/`
  - `my-profile-template.md`
  - `my-knowledge-template.md`
  - `my-skills-template.md`

- **用户数据文件**（不带 `-template` 后缀）：`~/oh-my-profile/`
  - `my-profile.md`
  - `my-knowledge.md`
  - `my-skills.md`

- **AI 上下文技能**：`~/oh-my-profile/skills/omp-my-profile/SKILL.md`

### 执行流程
1. AI 参考模板文件创建或验证用户数据文件结构
2. 用户数据文件保存在 `~/oh-my-profile/` 目录
3. 基于三个核心文件的内容生成 omp-my-profile 技能
4. omp-my-profile 技能的 description 字段包含详细的用户画像信息，便于 AI 快速了解用户

### 注意事项
- **不要直接修改 references 目录中的文件**
- **所有用户数据必须保存在 `~/oh-my-profile/` 目录**
- **omp-my-profile 技能基于用户数据文件创建，description 字段特别详细友好**
- **AI 优先使用 omp-my-profile 技能获取上下文，需要更多详情时再加载完整系统**

---

## 注意事项

- 如果用户中途退出，保存已填写的内容
- 可以随时运行再次初始化来更新 profile
- **用户目录是数据源**：`~/oh-my-profile/` 中的文件用户可手动编辑
- **references 是同步副本**：位于 `~/oh-my-profile/skills/oh-my-profile/references/`，供大模型快速读取
- **my-profile.md 和 ~/oh-my-profile/skills/oh-my-profile/references/my-profile.md 应保持同步**
- **技能规划是建议性的，用户决定是否创建或安装**

### 验证规则
- `my-knowledge.md` 必须是索引文件，不能包含详细知识内容
- 所有具体知识必须保存在 `~/oh-my-profile/knowledge/` 目录中
- 索引文件必须使用 Obsidian 双链语法链接到具体知识文件
- 索引文件必须包含正确的 YAML frontmatter
- `my-knowledge.md` 中的知识目录部分应按领域组织，并链接到实际知识文件
