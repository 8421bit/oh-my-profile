# oh-my-profile - Your Personal Agent Profile

> Build your Digital Self for AI — so it truly understands who you are, what you know, and what you can do.

[中文文档](README_CN.md)

---

## Installation

**Recommended: Clone to home directory**

```bash
# Clone to ~/oh-my-profile/
git clone https://github.com/8421bit/oh-my-profile.git ~/oh-my-profile

# Add as local marketplace
/plugin marketplace add ~/oh-my-profile/.claude-plugin/marketplace.json

# Install skills
/skills install oh-my-profile
```

---

## Quick Start

After installation, try saying to AI:

| Scenario | You Say | AI Does |
|----------|---------|---------|
| **Initialize** | "帮我初始化 oh-my-profile" | Creates ~/oh-my-profile/, guides profile setup |
| **Save Knowledge** | "帮我记一下" / "Save this" | Extracts insights, saves to knowledge/ |
| **Organize Content** | "整理这个" + URL/text | Parses and structures content |
| **Create Skill** | "这个可以做成技能吗" / "Create skill" | Guides personal skill creation |
| **Plan Skills** | "规划我的技能" / "Plan my skills" | Gap analysis + recommends open-source skills |
| **Sync Profile** | "同步档案" / "Sync profile" | Manual sync user directory to references |

**Note**: AI automatically reads your profile for personalized service — no manual trigger needed.

---

## What is oh-my-profile?

**oh-my-profile** is a **Personal Agent Profile** system — your complete **Digital Self** that AI can understand.

It's not just a knowledge base, not just a memory system. It's a systematic approach to help AI truly know you:

| Component | What It Answers | Nature |
|-----------|-----------------|--------|
| `my-profile.md` | **Who you are?** | Identity + Preferences + Goals |
| `my-knowledge.md` | **What you know?** | Knowledge Index + Learning Plan |
| `my-skills.md` | **What you can do?** | Skills Index + Development Path |
| `knowledge/` | Accumulated insights | Experience + Learnings |
| `skills/` | Personal skills | Capabilities + Methods |

When you install oh-my-profile, it creates a `~/oh-my-profile/` directory in your home folder:

```
~/oh-my-profile/
├── my-profile.md     # Your identity (who you are, preferences, goals)
├── my-knowledge.md   # Knowledge index + learning plan
├── my-skills.md      # Skills index + development path
├── knowledge/        # Your insights & experiences (Obsidian-compatible)
└── skills/           # Your Agent Skills (reusable capabilities)
```

**AI reads this to provide personalized service.**

---

## The Core Concept

**In the AI era, what makes an individual unique?**

```
Information
     ↓
Thinking / Digestion / Organization
     ↓
Knowledge  →  my-knowledge.md + knowledge/
     ↓
Skills (Agent Skills)  →  my-skills.md + skills/
     ↓
Reusable Capabilities
```

**Profile + Knowledge + Skills = Your Digital Self in AI World**

From passive receiving to active creating — this is continuous personal evolution.

---

## 3 Meta Skills

oh-my-profile includes 3 built-in "Meta Skills" that help you build and maintain your digital self:

| Skill | Function | Trigger Examples |
|-------|----------|------------------|
| **oh-my-profile** | Core entry point + Initialize + Profile sync | Any conversation, "初始化", "同步档案" |
| **oh-my-knowledge** | Capture insights from conversations, URLs, files | "帮我记一下", "整理这个", "Save this" |
| **oh-my-skills** | Discover patterns and create reusable skills | "创建技能", "分析知识库", "Create skill" |

### oh-my-profile (Core Entry Point)

The central skill that AI reads to understand you completely.

**Capabilities:**
- Auto-sync: Detects changes in ~/oh-my-profile/ and updates references
- Load your complete profile from `references/`
- Initialize `~/oh-my-profile/` directory on first run
- Guide profile setup through Socratic dialogue
- Analyze profile to plan skills (Gap analysis)

### oh-my-knowledge (Knowledge Capture)

Your thinking partner that helps capture and organize insights.

**Triggers:**
- "帮我记一下" / "Save this" → Save conversation insights
- "整理这个" + URL/text → Organize provided content
- "整理这些文件" + folder → Batch process files
- Proactive suggestion after insightful conversation

**Personality:**
- Listener - Truly listens, doesn't interrupt
- Encouraging not fawning - "That's interesting," not "Amazing!"
- Challenging not nitpicking - Valuable questioning
- Wise but humble - Has insights, knows you're the expert

### oh-my-skills (Skill Discovery)

Knowledge-to-Skill evolution system.

**Triggers:**
- "这个可以做成技能" / "Create skill" → Capture current pattern
- "从知识创建技能" / "分析知识库" → Analyze knowledge for patterns
- Automatic: Detects repetitive work (3+ times)
- Non-obvious solution discovered after >10min investigation

**Quality Gates:**
- Reusable? Can help future tasks?
- Non-trivial? Not just documentation lookup?
- Specific? Clear trigger conditions?
- Verified? Actually works?

---

## How It Works

### Phase 1: Profile Setup

```
1. Install oh-my-profile → Creates ~/oh-my-profile/
2. AI guides you through profile setup (Socratic dialogue)
3. Generates my-knowledge.md (learning plan) and my-skills.md (skill gaps)
4. Syncs to oh-my-profile/references/ for AI to read
```

### Phase 2: Knowledge Capture

```
Your conversation → AI listens and confirms understanding
                 → Chooses thinking method (Socratic, First Principles, etc.)
                 → Asks questions, you discover insights
                 → Suggests: "Should I save this insight?"
                 → Saves to ~/oh-my-profile/knowledge/
                 → Updates my-knowledge.md index
```

### Phase 3: Skill Discovery

```
Repetitive work detected → AI suggests: "Can we make this a skill?"
                        → Guides skill definition through dialogue
                        → Creates ~/oh-my-profile/skills/[skill-name]/
                        → Updates my-skills.md index
```

### Phase 4: Continuous Evolution

```
my-profile.md (your goals)
       ↓
my-knowledge.md (what to learn) + my-skills.md (what to master)
       ↓
knowledge/ (accumulated) + skills/ (created)
       ↓
You grow closer to your profile goals
```

---

## Key Differentiators

| Traditional AI | oh-my-profile |
|----------------|---------------|
| "Use once, discard" | "Leave a trace" |
| Give answers immediately | Guide through questions |
| Generic responses | Personalized to your profile |
| Tool-focused | Relationship-focused |
| No memory | Continuous evolution |
| ❌ Starts from zero | ✅ Knows your history |
| ❌ Generic advice | ✅ Based on your goals |

---

## User Workspace

oh-my-profile's outputs live in your home directory, independent of any project:

```
~/oh-my-profile/
├── my-profile.md           # Your identity + preferences + goals
├── my-knowledge.md         # Knowledge index + learning plan
├── my-skills.md            # Skills index + development path + Gap analysis
├── knowledge/              # Knowledge files (Obsidian-compatible)
│   └── YYYY-MM-DD_topic.md
└── skills/                 # Personal skills
    └── [skill-name]/
        └── SKILL.md
```

**Data lives here, user can manually edit. This is the source of truth.**

---

## Dual-Track Design: Obsidian + AI

`~/oh-my-profile/` is simultaneously **an Obsidian vault** and **an AI-readable profile**:

```
┌─────────────────────────────────────────────────┐
│              ~/oh-my-profile/                   │
│                                                 │
│   ┌───────────────┐     ┌───────────────┐      │
│   │   AI Track    │     │  User Track   │      │
│   │               │     │               │      │
│   │ oh-my-*       │     │  Obsidian     │      │
│   │ skills        │     │  Direct Edit  │      │
│   │ read/write    │     │               │      │
│   └───────┬───────┘     └───────┬───────┘      │
│           │                     │              │
│           └──────────┬──────────┘              │
│                      │                         │
│           Same Obsidian Vault                  │
│           (Markdown + Wikilinks + Tags)        │
└─────────────────────────────────────────────────┘
```

### AI Track
- **oh-my-profile**: Reads your complete profile, initializes directory, auto-syncs changes
- **oh-my-knowledge**: Captures insights, creates knowledge files
- **oh-my-skills**: Discovers patterns, creates skill files

### User Track
- Open `~/oh-my-profile/` as an **Obsidian vault**
- Edit files directly with Obsidian's visual editor
- Use **wikilinks** `[[note]]` to connect knowledge
- Use **Graph View** to visualize knowledge structure
- Use **Tags** and **Properties** for organization

### Why This Design?

| Benefit | Description |
|---------|-------------|
| **Best of both worlds** | AI captures, user curates |
| **No lock-in** | Standard markdown, works without AI |
| **Visual management** | Obsidian's graph view, search, backlinks |
| **Continuous evolution** | AI and user both contribute |

**Recommended workflow:**
1. AI captures insights during conversations → `knowledge/`
2. User reviews and organizes in Obsidian
3. AI suggests skills based on knowledge patterns
4. User decides what to keep and refine

---

## Project Structure

```
oh-my-profile/                          # Plugin repository
├── skills/
│   ├── oh-my-profile/                  # Core entry point
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── my-profile.md           # Template → User data
│   │       ├── my-knowledge.md         # Template → User data
│   │       └── my-skills.md            # Template → User data
│   ├── oh-my-knowledge/                # Knowledge capture
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── obsidian-knowledge-rules.md
│   │       ├── socratic.md
│   │       ├── first-principles.md
│   │       ├── brainstorming.md
│   │       └── reverse-thinking.md
│   └── oh-my-skills/                   # Skill discovery
│       ├── SKILL.md
│       └── references/
│           └── agent-skills-spec.md
├── .claude-plugin/
├── README.md
└── .gitignore
```

---

## Getting Started

After installation:

1. **First run** - AI detects `~/oh-my-profile/` doesn't exist
2. **Creates structure** - Directory with template files
3. **Guides profile** - Socratic dialogue to fill my-profile.md
4. **Plans growth** - Generates learning plan and skill gaps
5. **Ready** - AI now understands you for all future conversations

---

## Evolution Philosophy

Your digital self evolves as you:
- Have more conversations → Knowledge accumulates
- Recognize patterns → Skills get extracted
- Refine your goals → Plans update accordingly

**oh-my-profile facilitates this by:**
- Proactively capturing insights you might miss
- Recognizing repetitive work patterns
- Suggesting skills to automate workflows
- Tracking progress toward your goals

---

## Who is This For?

### For Knowledge Workers
Build a **personal knowledge base** that AI can leverage for better assistance.

### For Developers
Create a **personal skill library** of reusable Agent Skills.

### For Lifelong Learners
Track your **learning journey** with structured knowledge and skill development.

### For AI Power Users
Build a true **AI partnership** where the AI understands your context over time.

**Works best with Obsidian** for linking notes and building a knowledge graph.

---

## Specifications Compliance

**Agent Skills Specification:**
- Follows the official Agent Skills format
- Supports progressive disclosure and dynamic loading
- See `oh-my-skills/references/agent-skills-spec.md`

**Obsidian Knowledge Specification:**
- Follows Obsidian Flavored Markdown format
- Supports wikilinks, callouts, properties, and all Obsidian features
- See `oh-my-knowledge/references/obsidian-knowledge-rules.md`

---

## License

MIT
