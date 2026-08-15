# 📄 PRD Creator

**Turn any app idea into an exhaustive, production-ready Product Requirements Document.**

Works in **Antigravity**, **Claude Code**, **Cursor**, **Windsurf**, **ChatGPT**, and **Gemini CLI**.

---

## What It Does

You give it an app idea — anything from a 2-line napkin sketch to a 500-line feature dump — and it generates a **comprehensive PRD** that can serve as the sole engineering handoff document.

This is not a generic 3-page summary. The PRD Creator produces **8-15+ page equivalent documents** covering:

- 🎯 Executive summary & core value proposition with KPIs
- 👥 Detailed personas (5+ attributes each) & RBAC permission matrix
- 🧩 Atomic feature breakdown with unique IDs, user stories, and acceptance criteria
- 📱 Complete screen hierarchy with 5 interface states per screen
- 🔌 Full API endpoint specification (15-25+ endpoints)
- 🗄️ Complete SQL database schema with CREATE TABLE statements
- 🔗 Third-party integrations & SDK architecture
- ⚡ Non-functional requirements (performance, security, scalability)
- 🚨 Edge cases & failure modes (12-15+ scenarios)
- 📋 Out of scope (v1.0 vs v2.0)

---

## How to Install

### Via skills.sh
```bash
npx skills add onipinaka/howto-skills/skills/prd-creator
```

### Manual
Copy this folder into your project's `.agents/skills/` directory:
```bash
mkdir -p .agents/skills
cp -r prd-creator .agents/skills/
```

---

## How to Use

Once installed, trigger the skill with any of these phrases:

- **"Create a PRD for [app idea]"**
- **"Write product requirements for..."**
- **"Spec out this project in deep detail"**
- **"I have an app idea: [brief description], make a full PRD"**

### Minimal input works great
Even a 2-line prompt like *"Make a PRD for an AI meal planner app"* will produce a full-depth PRD. The skill infers sensible defaults and lists all assumptions explicitly.

---

## Example

**Input:**
> Create a PRD for an AI-powered meal planning app that generates personalized weekly meal plans and grocery lists based on dietary preferences.

**Output:** An exhaustive PRD document saved as `PRD_MealPlannerAI_v1.md` containing all sections listed above, fully tailored to the meal planning domain.

See the [examples/](./examples/) directory for a preview of input and output.

---

## Pairs Well With

Use the output from PRD Creator as input to the **[Playbook Creator](../playbook-creator/)** skill to generate step-by-step build prompts:

```
Your idea → PRD Creator → Exhaustive PRD → Playbook Creator → 20-40 copy-paste build prompts
```
