---
name: omp-init
description: Initialize oh-my-profile system or sync profile updates. Creates ~/oh-my-profile/ directory with my-profile.md, knowledge/, skills/, docs/ folders. Guides user through profile setup and generates omp-myprofile skill. Also triggers when my-profile.md is updated to sync omp-myprofile. Run this when user first installs oh-my-profile, says "setup my profile", "初始化", or when my-profile.md changes.
license: MIT
metadata:
  author: 8421bit
  version: "1.1"
---

# omp-init - Initialize Your Personal Agent Profile

## 何时使用

- 首次安装 oh-my-profile 后
- 用户说「初始化」「setup my profile」「创建我的档案」
- **用户说「我更新了 profile」「sync profile」「同步画像」**
- **发现 `~/oh-my-profile/my-profile.md` 有更新**

## 执行流程

### 第一步：检查并创建目录

```
1. 检查 ~/oh-my-profile/ 是否存在
2. 如果不存在，创建以下结构：
   ~/oh-my-profile/
   ├── my-profile.md     (从模板复制)
   ├── knowledge/        (空目录)
   ├── skills/           (空目录)
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

### 第四步：确认完成

```
初始化完成！

已创建：
✅ ~/oh-my-profile/my-profile.md
✅ ~/oh-my-profile/knowledge/
✅ ~/oh-my-profile/skills/omp-myprofile/
✅ ~/oh-my-profile/docs/

现在你可以：
- 使用 omp-thinker 进行思考对话
- 让 AI 读取 omp-myprofile 了解你
```

---

## Profile 同步更新

当检测到 `my-profile.md` 有更新时（用户主动告知或发现文件变化），执行以下流程：

### 触发条件

- 用户说「我更新了 profile」「profile 变了」「sync profile」
- 用户说「同步画像」「更新我的画像」
- 在对话中发现 `my-profile.md` 内容与 `omp-myprofile/SKILL.md` 不一致

### 同步流程

```
1. 读取 ~/oh-my-profile/my-profile.md
2. 提取关键信息：
   - 姓名/称呼
   - 角色/职业
   - 语言偏好
   - 沟通风格
   - 技能专长
   - AI 交互偏好
3. 更新 ~/oh-my-profile/skills/omp-myprofile/SKILL.md
   - 更新 description 字段
   - 更新内容摘要
4. 确认同步完成
```

### 同步确认

```
Profile 同步完成！

已更新：
✅ ~/oh-my-profile/skills/omp-myprofile/SKILL.md

变更摘要：
- [列出主要变更项]

AI 现在可以读取最新的个人画像了。
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
- **建议用户更新 profile 后主动告知以触发同步**
