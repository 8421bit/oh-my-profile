---
name: omp-init
description: |
  Initialize oh-my-profile system, sync profile updates, and plan personal skills.
  Creates ~/oh-my-profile/ directory with my-profile.md, knowledge/, skills/, docs/.
  Guides user through profile setup, generates omp-myprofile skill, and plans personalized skills based on profile.
  Triggers: (1) First install, (2) "setup my profile" or "初始化", (3) my-profile.md updated, (4) "规划技能" or "plan my skills".
license: MIT
metadata:
  author: 8421bit
  version: "1.2"
---

# omp-init - Initialize Your Personal Agent Profile

## 何时使用

- 首次安装 oh-my-profile 后
- 用户说「初始化」「setup my profile」「创建我的档案」
- 用户说「我更新了 profile」「sync profile」「同步画像」
- **用户说「规划技能」「plan my skills」「我需要什么技能」**
- 发现 `~/oh-my-profile/my-profile.md` 有更新

---

## 执行流程

### 第一步：检查并创建目录

```
1. 检查 ~/oh-my-profile/ 是否存在
2. 如果不存在，创建以下结构：
   ~/oh-my-profile/
   ├── my-profile.md     (从模板复制)
   ├── knowledge/        (空目录)
   ├── skills/           (空目录)
   ├── skills-proposals.md (技能提案)
   └── docs/             (空目录)
3. 如果已存在，告知用户并询问是否重新初始化
```

### 第二步：引导填写 Profile

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

使用苏格拉底式对话引导，不要一次问太多问题。

### 第三步：生成 omp-myprofile 技能

基于用户填写的信息，在 `~/oh-my-profile/skills/omp-myprofile/` 生成 SKILL.md：

```markdown
---
name: omp-myprofile
description: [用户名称] 的个人画像。[角色/职业]。偏好：[语言]，[沟通风格]。[其他关键信息摘要]。AI 读取此技能可快速了解用户。
---

# [用户名称] 的个人画像

[基于 my-profile.md 的结构化摘要]
```

### 第四步：个人技能规划（新功能）

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

#### 生成技能提案

将分析结果保存到 `~/oh-my-profile/skills-proposals.md`：

```markdown
# 技能提案

## [YYYY-MM-DD] 基于个人档案的技能规划

### 基于角色：[角色名]
- **[技能名]**：[一句话描述]
  - 触发场景：[何时使用]
  - 开源推荐：[skill-name](https://github.com/xxx/skill-name) ✅ 或 无 ❌

### 基于技能专长：[专长领域]
- **[技能名]**：[一句话描述]
  - 触发场景：[何时使用]
  - 开源推荐：[skill-name](https://github.com/xxx/skill-name) ✅ 或 无 ❌

### 基于当前项目：[项目名]
- **[技能名]**：[一句话描述]
  - 触发场景：[何时使用]
  - 开源推荐：无 ❌（需自建）

### 基于日常工作
- **[技能名]**：[一句话描述]
  - 触发场景：[何时使用]
  - 开源推荐：[skill-name](https://github.com/xxx/skill-name) ✅

---
状态：待处理
```

#### 询问用户

```
基于你的档案，我规划了以下技能建议：

1. **[技能1]** - [描述]
2. **[技能2]** - [描述]
3. **[技能3]** - [描述]
...

这些提案已保存到 skills-proposals.md。
你想现在就创建其中某个技能吗？
```

### 第五步：确认完成

```
初始化完成！

已创建：
✅ ~/oh-my-profile/my-profile.md
✅ ~/oh-my-profile/knowledge/
✅ ~/oh-my-profile/skills/omp-myprofile/
✅ ~/oh-my-profile/skills-proposals.md（含个人技能规划）
✅ ~/oh-my-profile/docs/

现在你可以：
- 使用 omp-thinker 进行思考对话
- 查看 skills-proposals.md 中的技能建议
- 让 AI 读取 omp-myprofile 了解你
```

---

## Profile 同步更新

当检测到 `my-profile.md` 有更新时，执行以下流程：

### 触发条件

- 用户说「我更新了 profile」「profile 变了」「sync profile」
- 用户说「同步画像」「更新我的画像」
- 在对话中发现 `my-profile.md` 内容与 `omp-myprofile/SKILL.md` 不一致

### 同步流程

```
1. 读取 ~/oh-my-profile/my-profile.md
2. 提取关键信息
3. 更新 ~/oh-my-profile/skills/omp-myprofile/SKILL.md
4. 检查是否有新的技能规划机会
5. 如有新规划，追加到 skills-proposals.md
6. 确认同步完成
```

### 同步确认

```
Profile 同步完成！

已更新：
✅ ~/oh-my-profile/skills/omp-myprofile/SKILL.md
✅ ~/oh-my-profile/skills-proposals.md（如有新规划）

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
3. 生成技能建议
4. 追加到 ~/oh-my-profile/skills-proposals.md
5. 询问用户是否立即创建
```

---

## 模板引用

- `references/my-profile-template.md` - 个人档案模板
- `references/omp-myprofile-template.md` - 用户画像技能模板

## 注意事项

- 如果用户中途退出，保存已填写的内容
- 可以随时运行再次初始化来更新 profile
- 生成的 omp-myprofile 应包含足够信息让 AI 快速理解用户
- **my-profile.md 和 omp-myprofile/SKILL.md 应保持同步**
- **技能规划是建议性的，用户决定是否创建**
- **规划会追加到 skills-proposals.md，不会覆盖已有提案**
