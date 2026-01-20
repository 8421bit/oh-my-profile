---
name: omp-skill-creator
description: |
  Knowledge to Skill evolution system. Identifies reusable patterns from work sessions and knowledge base,
  creates skills proposals for user decision. Triggers: (1) User says "分析知识库" or "create skill",
  (2) "这个我经常做" or repetitive work detected, (3) Non-obvious solutions discovered after >10min investigation,
  (4) Periodic review of ~/oh-my-profile/knowledge/ for extractable patterns.
license: MIT
metadata:
  author: 8421bit
  version: "2.1"
---

# omp-skill-creator - Knowledge to Skill Evolution

> 从知识沉淀到技能进化的持续学习系统

---

## 核心设计原则

### 精简是关键

**Context window 是公共资源。** 每个 skill 都要与系统提示、对话历史、其他 Skills 共享上下文空间。

- **默认假设：llm 已经很聪明**
- 只添加 llm 不知道的内容
- 对每段信息质疑：「llm 真的需要这个？」「这段内容值得它的 token 成本吗？」
- **偏好简洁的示例，而非冗长的解释**

### 自由度匹配

根据任务的脆弱性选择不同的指令详细程度：

| 自由度 | 适用场景 | 表现形式 |
|--------|----------|----------|
| **高** | 多种方法都可行、依赖上下文判断 | 文字描述指引 |
| **中** | 有首选模式、允许一定变化 | 伪代码或带参数的模板 |
| **低** | 操作脆弱易错、一致性关键 | 具体步骤、少参数 |

> 把执行者想象成在探索路径：悬崖窄桥需要具体护栏（低自由度），开阔田野允许多条路线（高自由度）。

---

## 何时启动

### 被动触发（用户主动调用）
- 用户说「分析知识库」「从知识创建技能」
- 用户说「我总是在做这件事，帮我自动化」
- 用户说「查看技能提案」

### 主动触发（自动识别 → 静默提案）
完成任务后，如果符合以下条件，启动**静默提案模式**：
- **重复模式**：第 3 次执行相似任务
- **非显而易见解决方案**：需要 >10 分钟调查
- **变通方案发现**：通过实验找到限制的解决方法
- **工作流优化**：发现更高效的多步骤流程

### 定期触发
- 每周分析 `~/oh-my-profile/knowledge/` 目录
- 发现 ≥3 个相似主题的知识文档时

---

## 静默提案模式

主动触发时**不直接创建 skill**，而是记录提案供用户决策：

### 流程

```
1. 识别到可提取模式
2. 静默记录提案到 ~/oh-my-profile/skills-proposals.md
3. 提示用户："发现一个可能值得创建的技能，查看提案？"
4. 用户确认后再执行创建流程
```

### skills-proposals.md 格式

```markdown
# 技能提案

## [YYYY-MM-DD] [提案名称]
- **识别来源**：[知识文档名/工作会话描述]
- **建议技能**：[一句话描述]
- **触发场景**：[何时使用这个技能]
- **状态**：待处理 | 已创建 | 已拒绝
```

---

## 执行流程（6 步）

### 第一步：用具体示例理解需求

```
问用户：
- "这个技能应该支持什么功能？"
- "能给一些这个技能如何使用的例子吗？"
- "什么情况会触发这个技能？"
```

避免一次问太多问题，从最重要的开始。

### 第二步：规划可复用内容

分析每个示例，识别需要的资源：

| 资源类型 | 用途 | 何时使用 |
|----------|------|----------|
| `scripts/` | 可执行脚本，确定性操作 | 反复编写相同代码、需要确定性 |
| `references/` | 按需加载的参考文档 | 需要引用的文档、schema、API |
| `assets/` | 输出用资源（不加载到 context） | 模板、图标、样板代码 |

### 第三步：扫描知识库

```
1. 读取 ~/oh-my-profile/knowledge/ 下的所有文件
2. 提取每个文件的：
   - 标题和主题
   - 标签 (tags)
   - 核心洞察
   - 下一步行动
3. 构建知识图谱概览
```

### 第四步：识别模式

| 模式类型 | 识别信号 | 示例 |
|---------|---------|------|
| **重复工作流** | 多个文件描述相似步骤 | 「每次写 PRD 我都会...」 |
| **方法论** | 多次提及同一思考框架 | 「我用 MECE 分析问题」 |
| **工具链** | 固定的工具使用组合 | 「先用 X，再用 Y，最后 Z」 |
| **决策规则** | 条件判断模式 | 「如果...就...」 |
| **错误解决** | 误导性错误的真实原因 | 「这个报错实际上是...」 |

### 第五步：Web 搜索验证（技术类主题）

当识别到技术相关的技能主题时：

```
1. 执行 Web 搜索收集最佳实践
   - 搜索：「[技术] [问题] best practices」
   - 搜索：「[技术] [功能] official docs」
2. 询问用户确认是否保存搜索结果
3. 如确认，保存摘要至 ~/oh-my-profile/knowledge/[YYYYMMDD]-[topic].md
4. 在后续创建的 skill 中引用该知识
```

### 第六步：质量门控 + 创建

#### 质量门控（创建前必须检查）

- [ ] **可复用性**：能帮助未来的任务吗？
- [ ] **非平凡性**：需要发现的知识，非文档查询即得？
- [ ] **具体性**：能描述确切的触发条件吗？
- [ ] **已验证**：方案实际有效？
- [ ] **精简**：内容是否足够精简？删除了冗余？
- [ ] Description 包含具体触发条件
- [ ] 不与现有 skill 重复
- [ ] 不包含敏感信息

#### 创建 Skill

在 `~/oh-my-profile/skills/` 创建新技能目录和 SKILL.md。

---

## Skill 结构规范

### 目录结构

```
skill-name/
├── SKILL.md          (必需)
│   ├── YAML frontmatter (name + description)
│   └── Markdown 指令
└── 可选资源/
    ├── scripts/      - 可执行脚本
    ├── references/   - 按需加载的参考文档
    └── assets/       - 输出用资源（不读入 context）
```

### 资源分类说明

| 目录 | 何时加载 | 用途示例 |
|------|----------|----------|
| `scripts/` | 执行时 | 自动化脚本、数据处理 |
| `references/` | Claude 判断需要时 | schema、API 文档、详细指南 |
| `assets/` | **不加载**，仅用于输出 | 模板、样板代码、图片 |

### SKILL.md 模板

```markdown
---
name: [skill-name]
description: |
  [功能描述]。当以下情况使用：
  (1) [触发条件1]
  (2) [触发条件2]
  覆盖 [能力范围]。
version: "1.0"
date: YYYY-MM-DD
status: active
---

# [技能名称]

## 溯源
> 此技能从以下知识中提炼：
> - [[知识1]]
> - [[知识2]]

## 何时使用
[具体的触发条件和场景]

## 执行步骤
[清晰的步骤指引 - 根据自由度选择详细程度]

## 验证
[如何确认执行成功]

## 注意事项
[边缘情况、警告]

## 参考资料
[外部链接，如果有]
```

---

## Description 撰写指南

Description 是**语义匹配的关键**，决定 skill 何时被触发。

### 必须包含
1. **功能描述**：做什么
2. **触发条件**：何时使用（用编号列出）
3. **覆盖范围**：能处理什么

### 示例

❌ **差的 description**：
```yaml
description: 处理产品需求相关的问题
```

✅ **好的 description**：
```yaml
description: |
  产品需求文档(PRD)撰写技能。当以下情况使用：
  (1) 用户说「帮我写 PRD」或「需求文档」
  (2) 需要结构化描述产品功能
  (3) 需要包含用户故事、验收标准
  覆盖背景分析、目标定义、功能清单、数据需求、上线计划。
```

---

## 渐进加载模式

当 skill 支持多种变体、框架或选项时，只在 SKILL.md 中保留核心流程，详细内容分离到 references/。

### 模式 1：高层指南 + 引用

```markdown
# PDF 处理

## 快速开始
使用 pdfplumber 提取文本：[简短示例]

## 高级功能
- 表单填写：见 [FORMS.md](references/FORMS.md)
- API 参考：见 [REFERENCE.md](references/REFERENCE.md)
```

### 模式 2：领域组织

```
bigquery-skill/
├── SKILL.md (概览 + 导航)
└── references/
    ├── finance.md (财务指标)
    ├── sales.md (销售数据)
    └── product.md (产品数据)
```

查询销售时只加载 sales.md。

### 模式 3：条件详情

```markdown
## 创建文档
使用 docx-js。见 [DOCX-JS.md](references/DOCX-JS.md)

## 编辑文档
简单编辑直接修改 XML。
**需要修订追踪**: 见 [REDLINING.md](references/REDLINING.md)
```

---

## 反模式：不该做的事

### 不该包含的文件
- ❌ README.md
- ❌ INSTALLATION_GUIDE.md
- ❌ CHANGELOG.md
- ❌ 用户文档

Skill 只包含 AI agent 完成任务所需的信息。

### 不该做的事
- ❌ **过度提取**：不是每个任务都值得一个 skill
- ❌ **模糊 description**：「帮助处理问题」无法触发
- ❌ **未验证方案**：只提取实际有效的
- ❌ **重复文档**：不要复制官方文档，链接即可
- ❌ **深层嵌套引用**：references 保持一层深度

---

## 技能生命周期

### 状态定义

| 状态 | 含义 |
|------|------|
| `active` | 当前有效，正常使用 |
| `deprecated` | 已过时，不建议使用 |
| `archived` | 已归档，保留历史 |

### 迭代工作流

```
1. 在实际任务中使用 skill
2. 发现困难或低效之处
3. 识别需要更新的部分
4. 实施更改，再次测试
```

---

## 自省提示

使用这些问题识别 skill 提取机会：

### 发现时机
- "我刚刚学到了什么在开始前不明显的东西？"
- "如果再次遇到这个问题，我希望提前知道什么？"

### 价值判断
- "这个知识对类似项目都有帮助吗？"
- "如果告诉遇到相同问题的同事，我会说什么？"

### 模式识别
- "我是第几次做类似的事情了？"
- "这个流程有固定的步骤吗？"

---

## 参考

- `references/agent-skills-spec.md` - Agent Skills 规范
- 用户的 `~/oh-my-profile/knowledge/` - 知识源
- 用户的 `~/oh-my-profile/skills-proposals.md` - 技能提案
