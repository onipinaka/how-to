# Contributing to HowTo AI Skills

Thank you for your interest in contributing! This collection thrives on community input.

---

## Ways to Contribute

### 🐛 Report Issues
- Found a skill generating incomplete output? Open an issue with the trigger phrase you used and a description of what went wrong.
- Include the AI tool and model you were using (e.g., Antigravity + Claude Sonnet 4, Cursor + Gemini 2.5 Pro).

### 💡 Suggest Improvements
- Have ideas for new PRD sections, playbook phases, or quality mandates? Open an issue with the `enhancement` label.

### 🔧 Submit a Pull Request

#### For Existing Skills
1. Fork the repository.
2. Create a feature branch: `git checkout -b improve-prd-edge-cases`
3. Make your changes.
4. Ensure SKILL.md stays **under 500 lines** — move examples and large templates to `references/`.
5. Submit a PR with a clear description of what changed and why.

#### For New Skills
1. Create a new directory under `skills/your-skill-name/`.
2. Add a `SKILL.md` with proper YAML frontmatter:
   ```yaml
   ---
   name: your-skill-name
   description: Clear description with explicit trigger phrases.
   version: 1.0.0
   author: your-github-username
   category: one-of (product-design | development | testing | communication | other)
   ---
   ```
3. Add a `references/` directory for templates and large examples.
4. Add an `examples/` directory with sample input and output previews.
5. Add a `README.md` explaining the skill to non-technical users.
6. Submit a PR.

---

## Formatting Rules

- **SKILL.md must stay under 500 lines.** Use `references/` for anything beyond that.
- **No hardcoded paths or local-only config.** Skills must work for anyone who installs them.
- **No bracket placeholders** in instructions (e.g., `[add more here]`). Write everything out explicitly.
- **Include trigger phrases** in the YAML description field so agents can discover the skill.

---

## Code of Conduct

Be respectful, constructive, and helpful. We're all here to make AI tools more useful.
