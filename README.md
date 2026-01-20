# oh-my-profile - Your Personal Agent Profile

> Build your Digital Self for AI — so it truly understands who you are, what you know, and what you can do.

---

## Installation

```bash
# Add marketplace
/plugin marketplace add 8421bit/oh-my-profile

# Install oh-my-profile
/skills install oh-my-profile@oh-my-profile
```

Or directly from GitHub:
```bash
/skills install oh-my-profile@github.com/8421bit/oh-my-profile
```

---

## What is oh-my-profile?

**oh-my-profile** is a **Personal Agent Profile** system.

It's not just a knowledge base, not just a memory system — it's your complete **Digital Self** that AI can understand:

| Component | What It Answers | Nature |
|-----------|-----------------|--------|
| `my-profile.md` | **Who you are?** | Identity + Preferences |
| `knowledge/` | **What you know?** | Experience + Insights |
| `skills/` | **What you can do?** | Capabilities + Methods |
| `docs/` | **What you create?** | Deliverables + Outputs |

When you install oh-my-profile, it creates a `~/oh-my-profile/` directory in your home folder:

```
~/oh-my-profile/
├── my-profile.md     # Your personal profile (identity, preferences, AI interaction style)
├── knowledge/        # Your insights & experiences (Obsidian-compatible markdown)
├── skills/           # Your Agent Skills (reusable capabilities)
└── docs/             # Your deliverables (PRDs, reports, etc.)
```

**AI tools like Claude Code read this directory to understand:**
- Who you are → Personalized responses
- What you know → Leverage your expertise
- What you can do → Use your methods
- What you create → Consistent output style

**Technical:** `oh-my-profile` is a **Claude Code Skill** that complies with both **Agent Skills specification** and **Obsidian Knowledge Rules**. Best used with **Obsidian** for knowledge organization and linking.

---

## The Core Concept

**In the AI era, what makes an individual unique?**

```
Information
     ↓
Thinking/Digestion/Organization
     ↓
Knowledge
     ↓
Skills (Agent Skills)
     ↓
Reusable Capabilities
```

**Profile + Knowledge + Skills = Your Digital Self in AI World**

This is the essence: **从「被动接收」到「主动创造」的递进成长** (From passive receiving to active creating).

---

## Key Differentiators

| Other AI Assistants | oh-my-profile |
|-------------------|---------------|
| "Use once, discard" | "Leave a trace" |
| Give answers immediately | Guide through questions |
| Generic responses | Personalized thinking |
| Tool-focused | Relationship-focused |
| No memory | Continuous evolution |
| Generic format | ✅ Obsidian Markdown spec |
| ❌ Not unique | ✅ Your digital self |

---

## How oh-my-profile Works

### Phase 1: Active Listening

```
You speak → oh-my-profile listens (really listens, doesn't interrupt)
            → oh-my-profile confirms understanding ("I get what you mean...")
            → Ensures we're on the same channel
```

### Phase 2: Choose Thinking Method

Based on your situation, oh-my-profile selects the right approach:

| Your State | Method | Reference |
|-------------|--------|-----------|
| "I have an idea..." | Socratic questioning | `references/socratic.md` |
| "I don't know how to choose..." | First principles | `references/first-principles.md` |
| "I want new directions..." | Brainstorming | `references/brainstorming.md` |
| "This process I do often..." | Create Skill | `references/agent-skills-spec.md` |
| "Help me write a PRD..." | Product Documentation | `assets/prd-template.md` |

### Phase 3: Socratic Dialogue

```
oh-my-profile asks a question (not giving answers)
  → You discover new insights
  → oh-my-profile digs deeper
  → Repeat until you say "Enough" or "I get it"
```

### Phase 4: Leave a Trace

When our conversation generates valuable insights:

**Knowledge沉淀**
- Trigger: You say "Let me save this" or oh-my-profile proactively suggests "要我帮你沉淀一下吗？"
- Save: `~/oh-my-profile/knowledge/[YYYYMMDD]-[topic].md`
- Format: Follows **Obsidian Markdown Rules** (see `references/obsidian-knowledge-rules.md`)

**Skills沉淀**
- Trigger: You repeatedly do something, oh-my-profile suggests automation
- Save: `~/oh-my-profile/skills/[skill-name]/SKILL.md`
- Format: Follows **Agent Skills规范** (see `references/agent-skills-spec.md`)

**My Profile**
- Trigger: You say "Update my profile" or need to update your profile
- Save: `~/oh-my-profile/my-profile.md`
- Format: Follows **Obsidian Markdown Rules** (see `references/obsidian-knowledge-rules.md`)

---

## oh-my-profile's Personality

| Trait | How it manifests |
|--------|------------------|
| **倾听者 (Listener)** | Listens first, truly listens, doesn't rush to answers |
| **鼓励但不谄媚 (Encouraging not fawning)** | Says "That's an interesting perspective," not "That's amazing!" |
| **挑战但不挑刺 (Challenging not nitpicking)** | Offers valuable questioning, not fault-finding |
| **睿智而谦虚 (Wise but humble)** | Has insights, but knows you're the expert |
| **隐形的情绪支持 (Invisible emotional support)** | You may not feel it, but it's always there |

---

## User Workspace

oh-my-profile's outputs live in your home directory, independent of any project:

```
~/oh-my-profile/
├── my-profile.md           # Your personal profile
├── knowledge/              # Insights (Obsidian spec)
│   └── [YYYYMMDD]-[topic].md
├── skills/
│   └── omp-myprofile/       # AI reads this to understand you
└── docs/                   # Deliverables
       └── [YYYYMMDD]-[name]-prd.md
```

**无论在哪个项目目录运行，oh-my-profile 的产出物都保存在同一个地方。**

---

## Project Structure

```
oh-my-profile/                          # Plugin repository
├── skills/
│   ├── omp-init/                       # Initialize your profile
│   │   ├── SKILL.md
│   │   └── references/
│   ├── omp-thinker/                    # Thinking Partner
│   │   ├── SKILL.md
│   │   ├── references/                 # Thinking methods
│   │   └── assets/                     # Templates
│   └── omp-skill-creator/              # Knowledge → Skill evolution
│       ├── SKILL.md
│       └── references/
├── .claude-plugin/
├── README.md
└── .gitignore
```

---

## Getting Started

After installation, run `omp-init` to set up your profile:

1. Creates `~/oh-my-profile/` directory
2. Guides you through filling your profile
3. Generates `omp-myprofile` skill so AI understands you

---

## Evolution Philosophy

**进化 = 随着时间增长，知识积累，技能扩展**

Your profile evolves as you:
- Have more conversations
- Accumulate unique insights
- Build reusable skills
- Discover your thinking patterns

**oh-my-profile helps this evolution by:**
- Proactively capturing insights you might miss
- Recognizing patterns in your work
- Suggesting new skills to automate repetitive workflows

---

## Who is This For?

### For Developers

Build your own **personal skill library** based on `references/agent-skills-spec.md`.

### For Product Managers

Create a structured **personal knowledge base** for product decisions and strategies.

### For Thinkers

Enhance your **digital avatar** by continuously refining your thinking patterns and communication style.

**Works best with Obsidian** for linking notes and building a knowledge graph.

### For Everyone

Build a relationship with your **digital self**—a thinking partner that grows with you over time.

---

## Specifications Compliance

**Agent Skills Specification**:
- Follows the official Agent Skills format defined in `references/agent-skills-spec.md`
- Supports progressive disclosure and dynamic loading

**Obsidian Knowledge Specification**:
- Follows the Obsidian Flavored Markdown format defined in `references/obsidian-knowledge-rules.md`
- Supports wikilinks, callouts, properties, and all Obsidian features

---

## License

MIT
