---
name: omp-skill-creator
description: Analyze user's knowledge base and create new skills from patterns. Reads ~/oh-my-profile/knowledge/ to identify reusable workflows, methods, and patterns, then generates new skills in ~/oh-my-profile/skills/. Use when user says "分析知识库" or "create skill from knowledge" or wants to automate repetitive work.
license: MIT
metadata:
  author: 8421bit
  version: "1.0"
---

# omp-skill-creator - Knowledge to Skill Evolution

## 何时使用

- 用户说「分析我的知识库」「从知识创建技能」
- 用户说「我总是在做这件事，帮我自动化」
- 定期回顾知识库，识别可复用模式

## 执行流程

### 第一步：扫描知识库

```
1. 读取 ~/oh-my-profile/knowledge/ 下的所有文件
2. 提取每个文件的：
   - 标题和主题
   - 标签 (tags)
   - 核心洞察
   - 下一步行动
3. 构建知识图谱概览
```

### 第二步：识别模式

分析以下可复用模式：

| 模式类型 | 识别信号 | 示例 |
|---------|---------|------|
| **重复工作流** | 多个文件描述相似步骤 | 「每次写 PRD 我都会...」 |
| **方法论** | 多次提及同一思考框架 | 「我用 MECE 分析问题」 |
| **工具链** | 固定的工具使用组合 | 「先用 X，再用 Y，最后 Z」 |
| **决策规则** | 条件判断模式 | 「如果...就...」 |

### 第三步：提议新技能

向用户展示识别到的模式：

```
我在你的知识库中发现了以下可复用模式：

1. **[模式名称]**
   - 出现频率：X 次
   - 相关知识：[[知识1]], [[知识2]]
   - 可以创建为技能：[技能描述]

2. **[模式名称]**
   ...

你想把哪个模式创建为技能？
```

### 第四步：生成技能

用户确认后，在 `~/oh-my-profile/skills/` 创建新技能：

```markdown
---
name: [skill-name]
description: [基于知识库模式的描述，包含触发条件]
---

# [技能名称]

## 来源
此技能由 omp-skill-creator 从以下知识中提炼：
- [[知识1]]
- [[知识2]]

## 何时使用
[触发条件]

## 执行步骤
[具体步骤，从知识中提取]

## 注意事项
[从知识中提取的注意事项]
```

### 第五步：确认完成

```
技能已创建：~/oh-my-profile/skills/[skill-name]/SKILL.md

✅ 已关联源知识
✅ 已提取执行步骤
✅ 已生成触发条件

下次当你 [触发条件] 时，可以使用这个技能。
```

## 分析维度

### 频率分析
- 相似主题出现 3 次以上
- 相似标签聚类
- 相似动作序列

### 结构分析
- 输入 → 处理 → 输出 模式
- 条件分支逻辑
- 循环/迭代步骤

### 价值分析
- 节省时间的潜力
- 减少错误的潜力
- 提高一致性的潜力

## 参考

- `references/agent-skills-spec.md` - Agent Skills 规范
- 用户的 `~/oh-my-profile/knowledge/` - 知识源
