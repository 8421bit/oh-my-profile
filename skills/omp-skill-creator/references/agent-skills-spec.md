---
name: skill-specification
description: Agent Skills 技术规范参考
---

# Agent Skills 规范

> Agent Skills 是一种轻量级、开放的格式，用于扩展 AI agent 的能力。

## 什么是 Skill

Skill 是一个包含 `SKILL.md` 文件的文件夹。这个文件包含元数据（至少有 `name` 和 `description`）和指导 agent 如何执行特定任务的说明。

```
my-skill/
├── SKILL.md          # 必需：指令 + 元数据
├── scripts/          # 可选：可执行代码
├── references/       # 可选：参考文档
└── assets/           # 可选：模板、资源
```

## 渐进式加载

Skills 使用三级加载来高效管理上下文：

1. **发现阶段**：启动时只加载 `name` 和 `description`（~100 tokens）
2. **激活阶段**：任务匹配时加载完整 `SKILL.md`（<5000 tokens）
3. **执行阶段**：按需加载 scripts/references/assets

## SKILL.md 格式

### 必需的 Frontmatter

```yaml
---
name: skill-name
description: 描述这个 skill 做什么以及何时使用它
---
```

### 可选字段

```yaml
---
name: pdf-processing
description: 从 PDF 文件提取文本和表格，填写表单，合并文档。
license: Apache-2.0
compatibility: 需要 pdfplumber，需要网络访问
metadata:
  author: example-org
  version: "1.0"
allowed-tools: Bash(git:*) Read Write
---
```

### 字段约束

| 字段 | 必需 | 约束 |
|------|------|------|
| `name` | 是 | 1-64字符，小写字母+数字+连字符，不能以连字符开头结尾 |
| `description` | 是 | 1-1024字符，描述做什么+何时使用 |
| `license` | 否 | 许可证名称或引用 |
| `compatibility` | 否 | 1-500字符，环境要求 |
| `metadata` | 否 | 任意键值对 |
| `allowed-tools` | 否 | 空格分隔的预授权工具列表 |

## 目录结构

### scripts/
包含 agent 可以运行的可执行代码。应该：
- 自包含或清晰说明依赖
- 包含有用的错误消息
- 优雅处理边缘情况

### references/
包含 agent 需要时可以读取的额外文档：
- `REFERENCE.md` - 详细技术参考
- 领域特定文件（`finance.md`, `legal.md` 等）

### assets/
包含静态资源：
- 模板
- 图片
- 数据文件

## 最佳实践

### 1. description 字段是关键

这是主要的触发机制，必须全面：

**好的例子**：
```yaml
description: 从 PDF 文件提取文本和表格，填写 PDF 表单，合并多个 PDF。当用户需要处理 PDF 文档或提到 PDF、表单、文档提取时使用。
```

**差的例子**：
```yaml
description: 处理 PDF。
```

### 2. 保持 SKILL.md 精简

- 主体内容 < 500 行
- 详细内容移到 references/ 目录
- Claude 已经很聪明，只添加它不知道的上下文

### 3. 使用祈使句

```markdown
## 如何使用

1. 识别用户请求的类型
2. 加载相应的参考文件
3. 按照具体指令操作
```

### 4. 渐进式披露

高层指南 + 引用：
```markdown
# PDF 处理

## 快速开始
使用 pdfplumber 提取文本：[代码示例]

## 高级功能
- 表单填写：见 [FORMS.md](references/FORMS.md)
- API 参考：见 [REFERENCE.md](references/REFERENCE.md)
```

## 创建新 Skill 的步骤

1. **理解需求**：明确 skill 要解决什么问题
2. **规划内容**：决定需要哪些 scripts、references、assets
3. **创建目录**：`skills/[skill-name]/`
4. **编写 SKILL.md**：核心指令，< 500 行
5. **添加参考**：详细内容放入 references/
6. **测试迭代**：基于实际使用改进

## 验证清单

- [ ] name 符合命名规范（小写、连字符）
- [ ] description 清晰描述功能和触发条件
- [ ] SKILL.md < 500 行
- [ ] 详细内容在 references/ 中
- [ ] 使用祈使句
- [ ] 包含使用示例
