---
name: obsidian-knowledge-rules
description: Obsidian Markdown 知识文件创建规范 - Nio 创建 knowledge 文件时必须遵循的格式规则
---

# Obsidian Markdown 知识文件创建规范

## 核心：Nio 创建 Knowledge 文件时必须遵循

## 1. 文件命名

```markdown
~/oh-my-profile/knowledge/[YYYYMMDD]-[topic].md
```

## 2. Frontmatter（必需）

每个 Knowledge 文件必须包含以下 properties：

```yaml
---
title: [主题名称]
date: [YYYY-MM-DD]
tags:
  - knowledge
  - [类别标签]
type: knowledge
status: new
---
```

### 标签建议

| 类别 | 标签示例 |
|------|----------|
| 洞察类 | insight, epiphany, realization |
| 思考路径 | thinking-path, reasoning, logic |
| 行动 | action, todo, next-step |
| 方法论 | method, framework, approach |
| 模式 | pattern, heuristic |
| 问题 | problem, challenge, obstacle |

## 3. 文档结构

### 必需章节

```markdown
# [主题]

> [!info] 背景
> 简要说明这个知识点的来源或上下文。

## 核心洞察

> [!tip] 关键要点 1
> 详细说明

> [!tip] 关键要点 2
> 详细说明

> [!tip] 关键要点 3
> 详细说明

## 思考路径

- [步骤 1]：[描述]
- [步骤 2]：[描述]
- [步骤 3]：[描述]

> [!note] 关键转折点

## 下一步行动

- [ ] [行动项 1]
- [ ] [行动项 2]

## 相关链接

- [[相关知识1]]
- [[相关技能1|技能描述]]
```

## 4. Obsidian 特性使用规则

### 4.1 Wikilinks（内部链接）

| 用法 | 语法 | 示例 |
|------|------|----------|
| 链接到其他知识 | `[[Note Name]]` | `[[产品决策20240115]]` |
| 带显示文本 | `[[Note|Display]]` | `[[策略|如何做产品决策]]` |
| 链接到标题 | `[[Note#Heading]]` | `[[产品#市场分析]]` |
| 链接到块 | `[[Note#^block-id]]` | `[[会议#^action-items]]` |

### 4.2 Callouts（引用块）

| 类型 | 语法 | 场景 |
|------|------|----------|
| 要点 | `> [!tip] ...` | 关键洞察 |
| 重要 | `> [!important] ...` | 核心结论 |
| 警告 | `> [!warning] ...` | 注意事项 |
| 疑问 | `> [!question] ...` | 待解决问题 |
| 信息 | `> [!info] ...` | 背景信息 |
| 成功 | `> [!success] ...` | 已验证方案 |

### 4.3 任务列表

```markdown
- [ ] 未完成任务
- [x] 已完成任务
- [ ] 带子任务
  - [ ] 子任务 1
  - [x] 子任务 2
```

### 4.4 Tags（标签）

```markdown
#主标签/子标签
#knowledge/insight
#pattern/socratic
#project/项目名
```

### 4.5 代码块

```markdown
`行内代码`

```
代码块
```

```javascript
// 带语法高亮
function example() {}
```
```

### 4.6 数学公式

```
行内公式：$x^2$
块级公式：$$
\begin{vmatrix} x y \\ c d \end{vmatrix} = ad - bc
$$
```

### 4.7 高亮

```markdown
==高亮文本==    背景色高亮
```

## 5. 特殊规则

### 5.1 嵌入笔记

Nio 可以在其他知识中嵌入当前知识：

```markdown
![[当前知识]]
```

### 5.2 引用块

```markdown
> 来自对话记录
> 具体内容或洞察
```

### 5.3 隐藏注释

```markdown
%%
这是给 Nio 看的注释，对用户不可见
%%
```

## 6. 必须避免的格式错误

| 错误类型 | 错误示例 | 正确示例 |
|----------|----------|----------|
| 链接空格 | `[[Note Name]]` | `[[Note-Name]]`（不允许空格） |
| 嵌套列表层级 | 用 `-` 或 `*` | 不要混用 `1.` 和 `-` |
| Frontmatter 格式 | 使用 `---` 分隔符 | YAML 语法正确 |
| 标题层级 | 只用 `#` 到 `######` | 不用 `#######` |

## 7. 文件模板

完整的 Knowledge 文件模板：

```markdown
---
title: [主题]
date: [YYYY-MM-DD]
tags:
  - knowledge
  - insight
type: knowledge
status: new
---

# [主题]

> [!info] 背景
> 简要说明这个知识点的来源或上下文。

## 核心洞察

> [!tip] [洞察 1]
> [详细说明]

> [!tip] [洞察 2]
> [详细说明]

## 思考路径

- [步骤 1]：[描述]
- [步骤 2]：[描述]

> [!note] [关键转折点]

## 下一步行动

- [ ] [行动项 1]
- [ ] [行动项 2]

## 相关链接

- [[相关知识1]]
- [[相关技能1|技能描述]]
```

## 8. Nio 创建时的注意事项

1. **文件命名**：使用 `[YYYYMMDD]-[topic].md` 格式
2. **Frontmatter**：必须包含 title、date、tags、type
3. **标签使用**：至少包含 `#knowledge` 标签
4. **链接验证**：wikilinks 必须指向存在的文件
5. **任务状态**：用 `- [ ]` 和 `- [x]` 区分未完成和已完成
6. **Callouts 使用**：关键信息用 callout 标记
7. **代码块**：语言指定要准确（`javascript` 不是 `js`）
8. **隐藏注释**：用 `%% %%` 包裹 Nio 内部说明

---

**创建顺序**：参考本规范 → 创建文件 → 验证格式 → 保存到 `~/oh-my-profile/knowledge/`
