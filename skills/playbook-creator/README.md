# 🗺️ Playbook Creator

**Convert any PRD or app concept into step-by-step, copy-paste build prompts for AI tools.**

Works in **Antigravity**, **Claude Code**, **Cursor**, **Windsurf**, **ChatGPT**, and **Gemini CLI**.

---

## What It Does

You give it a PRD (Product Requirements Document) or an app concept, and it generates an **end-to-end execution playbook** — a sequence of **20-40+ micro-prompts** that you copy-paste one at a time into your AI tool of choice.

Each prompt is:
- 🎯 **One task, one prompt** — no bundled mega-prompts that overwhelm the AI
- ✍️ **Fully written out** — no `[add details here]` placeholders
- 🔗 **Context-aware** — each prompt references what was built in prior steps
- 🛠️ **Tool-assigned** — specifies which AI tool and model to use
- ✅ **Checkpoint-gated** — verification prompts between phases catch errors early

### Why This Matters

Large prompts that ask an AI to "build the entire app" fail because:
1. They exceed context limits
2. They produce inconsistent, hallucinated code
3. Errors cascade without checkpoints

The Playbook Creator solves this by breaking everything into tiny, atomic steps that any AI tool can execute reliably.

---

## How to Install

### Via skills.sh
```bash
npx skills add onipinaka/howto-skills/skills/playbook-creator
```

### Manual
Copy this folder into your project's `.agents/skills/` directory:
```bash
mkdir -p .agents/skills
cp -r playbook-creator .agents/skills/
```

---

## How to Use

Once installed, trigger the skill with any of these phrases:

- **"Create a playbook for this PRD"**
- **"Give me step-by-step copy-paste prompts to build [app]"**
- **"Spoon-feed me detailed micro-prompts to build [idea]"**
- **"Break down this app into copy-paste prompts for AI editors"**

### Execution Flow

1. Copy-paste the first prompt into your AI tool
2. Let the AI execute it
3. Verify the output
4. Copy-paste the next prompt
5. At checkpoints, test everything before continuing
6. Repeat until deployment

---

## What's in a Playbook?

A typical playbook contains **6 phases** with **20-40+ sequential prompts**:

| Phase | What It Covers | Prompts |
| :--- | :--- | :--- |
| 🚀 Phase 1 | Project scaffolding, design system, environment setup | 4 |
| 🎨 Phase 2 | UI component library + full landing page | 10-15 |
| ⚡ Phase 3 | Authentication, database schema, middleware | 5-6 |
| 🔗 Phase 4 | Dashboard layout, core CRUD features | 5 |
| 💳 Phase 5 | Settings, billing, integrations | 4 |
| 🚢 Phase 6 | Audit, polish, production deployment | 3 |

Plus **4 checkpoint prompts** between phases to catch and fix errors.

---

## Pairs Well With

Use the **[PRD Creator](../prd-creator/)** skill first to generate the exhaustive specification, then feed it to the Playbook Creator:

```
Your idea → PRD Creator → Exhaustive PRD → Playbook Creator → 20-40 copy-paste build prompts
```

See the [examples/](./examples/) directory for a preview of input and output.
