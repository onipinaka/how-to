---
name: tracker-creator
description: Convert any Playbook and PRD into a living, interactive Markdown Execution Tracker. Creates a comprehensive checklist mapping all phases and prompts with status badges, assignees, and blocker logs. Triggers on 'create tracker', 'generate project tracker', or 'build checklist for this playbook'.
version: 1.0.0
author: onipinaka
category: project-management
---

# Tracker Creator Skill

## Overview
This skill instructs the AI agent to act as a **Project Manager**. It reads a generated Execution Playbook (and its parent PRD) and outputs a comprehensive, interactive **Markdown Execution Tracker**. 

This tracker serves as a living document where developers can check off tasks, log blockers, and track overall progress across all phases of development without having to read through the massive playbook every time.

**Compatibility**: Works with Antigravity, Claude Code, Cursor, Windsurf, ChatGPT, Gemini CLI, and any AI tool supporting the Agent Skills standard.

---

## 🛑 MANDATORY RULES

### Mandate 1: Exhaustive Extraction
- **DO NOT skip any prompts.** You must extract every single prompt from the Playbook and turn it into a trackable checklist item. If the Playbook has 46 prompts, the tracker must have 46 checkboxes.

### Mandate 2: Interactive Checklists
- Use strict GitHub Flavored Markdown (GFM) task lists: `- [ ]` for incomplete, `- [x]` for complete.
- When generating the tracker initially, all tasks must be incomplete (`- [ ]`).

### Mandate 3: Status Badges & Metadata
- Every checklist item MUST include a status badge, assignee placeholder, and a link/pointer to the specific prompt ID in the Playbook.
- Format: `- [ ] **Prompt 1.2: Framework Scaffolding** 🟡 [To Do] | 👤 @unassigned | 📝 Notes: `

### Mandate 4: Output as a Saved Document
- **ALWAYS save the Tracker as a markdown file**, not as inline chat text.
- Use the best available method:
  1. **Antigravity**: Save as an **artifact** markdown file (e.g., `tracker_[app-name].md`). Set `UserFacing: true`.
  2. **Claude Code / Cursor**: Write to `docs/TRACKER.md`.
  3. **ChatGPT**: Output in a single large code block.

---

## 🎯 When to Trigger
Trigger this skill when the user requests:
- "Create a tracker for this playbook"
- "Generate a project tracker"
- "Build a checklist for this PRD/Playbook"
- "Give me a Kanban board in markdown"

---

## 📄 Tracker Output Format

You must output the exact structure below.

### Section 1: Project Dashboard
A high-level summary of the project and current progress.

```markdown
# 📊 Execution Tracker: [Project Name]

**Status**: 🔴 Not Started
**Overall Progress**: 0% (0 / [Total Prompts] Completed)
**Last Updated**: [Current Date]
```

### Section 2: Phase Progress Summary
A table showing the breakdown of progress per phase.

| Phase | Description | Progress | Status |
| :--- | :--- | :---: | :---: |
| 1. Scaffolding | Framework, DB, Env | 0/4 | 🔴 To Do |
| 2. UI Components | Design system primitives | 0/12 | 🔴 To Do |
| ... | ... | ... | ... |

### Section 3: The Execution Backlog
**CRITICAL AI INSTRUCTION**: This is the core of the document. You must iterate through EVERY phase and EVERY step from the provided playbook. Do not summarize. Do not write "Repeat for rest of prompts". 

Write out the nested markdown lists exactly like this for EVERY prompt:

```markdown
### 🚀 Phase 1: Project Initialization
- [ ] **Prompt 1.1: Create Project Directory**
  - 🚦 **Status**: ⚪ To Do
  - 👤 **Owner**: @unassigned
  - 🛠️ **Tool**: Manual
  - 📝 **Notes**: [Add PR link or blocker notes here]

- [ ] **Prompt 1.2: Framework Scaffolding**
  - 🚦 **Status**: ⚪ To Do
  - 👤 **Owner**: @unassigned
  - 🛠️ **Tool**: Cursor / Antigravity
  - 📝 **Notes**: 
```

### Section 4: Blocker Log
A dedicated section at the bottom for the team to log critical issues that are holding up progress.

```markdown
## 🚧 Blocker Log
| Date | Blocker Description | Impacted Prompts | Owner | Resolution |
| :--- | :--- | :--- | :--- | :--- |
| YYYY-MM-DD | Example: Supabase API down | Prompts 3.2, 3.3 | @name | Pending... |
```

> 📎 See `references/tracker_template.md` for a fully worked example of the expected tracker structure.
