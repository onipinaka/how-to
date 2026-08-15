<p align="center">
  <h1 align="center">🚀 HowTo AI Skills Collection</h1>
  <p align="center">
    <strong>Turn any app idea into a production-ready PRD, then into step-by-step build prompts.</strong>
  </p>
</p>

<p align="center">
  <a href="./LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License"></a>
  <a href="https://skills.sh/onipinaka/howto-skills"><img src="https://img.shields.io/badge/skills.sh-indexed-8A2BE2" alt="skills.sh"></a>
  <a href="#-compatibility"><img src="https://img.shields.io/badge/works_with-6_AI_tools-green" alt="Compatibility"></a>
  <a href="./CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome"></a>
</p>

---

## What's a Skill?

A **skill** is a set of instructions you give to your AI coding agent. Think of it like a job description for a specific task. Once installed, you trigger it with a phrase and the AI knows exactly how to handle it — producing consistent, high-quality output every time.

This collection contains two production-grade skills that work as a **pipeline**:

```
💡 Your app idea → 📄 PRD Creator → Exhaustive PRD → 🗺️ Playbook Creator → Step-by-step build prompts
```

---

## 📦 Included Skills

### 📄 PRD Creator (`prd-creator`)

Turn **any** app idea — from a 2-line napkin sketch to a 500-line feature dump — into an **exhaustive, production-ready Product Requirements Document**.

Not a generic 3-page summary. A **deep, granular 8-15+ page engineering handoff document** with:
- Detailed personas & RBAC permission matrix
- Atomic feature breakdown with unique IDs (`FEAT-X.Y`), user stories, and acceptance criteria
- Complete screen hierarchy with 5 interface states per screen
- Full API endpoint specification (15-25+ endpoints)
- Complete SQL database schema (CREATE TABLE statements)
- Edge cases, failure modes, NFRs, and integrations

**Trigger phrases:**
```
"Create a PRD for [app idea]"
"Write product requirements for..."
"Spec out this project in deep detail"
```

---

### 🗺️ Playbook Creator (`playbook-creator`)

Convert any PRD or app concept into an **end-to-end, zero-code execution playbook** — a sequence of **20-40+ copy-paste micro-prompts** designed for AI tools.

Each prompt is:
- **One task, one prompt** — no bundled mega-prompts
- **Fully written out** — no `[add details here]` placeholders
- **Context-aware** — each prompt references what was built in prior steps
- **Tool-assigned** — specifies which AI tool and model to use

Built-in **checkpoints** between phases to catch errors before they cascade.

**Trigger phrases:**
```
"Create a playbook for this PRD"
"Give me step-by-step copy-paste prompts to build [app]"
"Spoon-feed me detailed micro-prompts to build [idea]"
```

---

### 🗄️ DB Architect (`db-architect`)

Act as a Principal Database Architect. Take any app idea or PRD and design an exhaustive, production-ready PostgreSQL database schema.

Output includes:
- Executive Summary & Design Decisions
- Mermaid.js Entity-Relationship (ER) Diagram
- Master SQL Schema (`CREATE TABLE` with UUIDs & Timestamps)
- Strict Row Level Security (RLS) Policies
- Recommended Indexes
- Example Analytical Queries

**Trigger phrases:**
```
"Design a database for [app idea]"
"Create a schema for..."
"DB schema for..."
```

---

## ⚡ Quick Installation

### Install the Entire Collection
```bash
npx skills add onipinaka/howto-skills
```

### Install Individual Skills
```bash
# PRD Creator only
npx skills add onipinaka/howto-skills/skills/prd-creator

# Playbook Creator only
npx skills add onipinaka/howto-skills/skills/playbook-creator

# DB Architect only
npx skills add onipinaka/howto-skills/skills/db-architect
```

### Manual Installation
Copy skill folders directly into your project's `.agents/skills/` directory:
```bash
mkdir -p .agents/skills
cp -r skills/* .agents/skills/
```

---

## 🎯 Compatibility

These skills follow the open **[Agent Skills](https://agentskills.io)** standard and work across all major AI coding tools:

| AI Tool | Status | Notes |
| :--- | :---: | :--- |
| **Antigravity** | ✅ | Saves output as artifact (recommended) |
| **Claude Code** | ✅ | Writes to project workspace |
| **Cursor** | ✅ | Writes to project workspace |
| **Windsurf** | ✅ | Writes to project workspace |
| **ChatGPT** | ✅ | Outputs in markdown codeblock for copy-paste |
| **Gemini CLI** | ✅ | Writes to project workspace |

---

## 🔄 The Pipeline: Idea → PRD → Playbook → Working App

These two skills are designed to work together as a complete pipeline:

**Step 1: Start with any idea**
> "Create a PRD for an AI-powered meal planning app that generates weekly grocery lists"

The PRD Creator generates an exhaustive specification document covering every aspect of the product.

**Step 2: Feed the PRD to the Playbook Creator**
> "Create a playbook for this PRD"

The Playbook Creator breaks the entire project into 20-40+ sequential, copy-paste prompts you execute one at a time in your AI tool of choice.

**Step 3: Execute the playbook**

Copy-paste each prompt sequentially. Build your app one atomic step at a time without getting overwhelmed.

---

## 📁 Repository Structure

```
howto-skills/
├── README.md                          # You are here
├── LICENSE                            # MIT License
├── CONTRIBUTING.md                    # How to contribute
├── .gitignore
└── skills/
    ├── prd-creator/
    │   ├── SKILL.md                   # Core skill instructions
    │   ├── README.md                  # Skill-specific docs
    │   ├── references/                # Templates & examples (loaded on demand)
    │   │   ├── prd_template.md
    │   │   ├── schema_examples.md
    │   │   ├── api_endpoint_examples.md
    │   │   └── screen_hierarchy_examples.md
    │   └── examples/                  # Input/output examples
    │       ├── example_input.md
    │       └── example_output_preview.md
    ├── playbook-creator/
    │   ├── SKILL.md                   # Core skill instructions
    │   ├── README.md                  # Skill-specific docs
    │   ├── references/                # Templates & examples (loaded on demand)
    │   │   ├── playbook_template.md
    │   │   └── example_prompts.md
    │   └── examples/                  # Input/output examples
    │       ├── example_input.md
    │       └── example_output_preview.md
    └── db-architect/
        ├── SKILL.md                   # Core skill instructions
        ├── README.md                  # Skill-specific docs
        └── references/                # Templates & examples (loaded on demand)
            └── schema_template.md
```

---

## 🤝 Contributing

Contributions are welcome! See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## 📜 License

MIT License — free for commercial and personal use. See [LICENSE](./LICENSE).

---

## 👤 Author

Built by [@onipinaka](https://github.com/onipinaka).
