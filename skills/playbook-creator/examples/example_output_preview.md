# Example Output Preview

This is a **truncated preview** of what the Playbook Creator generates. The actual output contains 20-40+ sequential prompts across 6 phases.

---

```markdown
# 🗺️ Master Execution Playbook: MealPlannerAI

> **Goal**: Exhaustive, step-by-step guide to build MealPlannerAI using AI tools from zero to live deployment.
> **Total Prompts**: 34 sequential micro-prompts.
> **Instruction**: Execute each step sequentially. Do not skip steps. Copy-paste each prompt into the specified AI tool. After each checkpoint, verify before continuing.

---

## 🧰 Tool & Model Assignment Matrix

| Task Category | Recommended AI Tool | Recommended Model | Why This Tool |
| :--- | :--- | :--- | :--- |
| Project scaffolding & config | Antigravity / Cursor | Claude Sonnet 4 | Best for multi-file generation |
| UI component creation | v0.dev / Bolt.new | Claude Sonnet 4 | Specialized for React/Tailwind UI |
| Database schema & migrations | Antigravity / Cursor | Claude Sonnet 4 | SQL generation and RLS policies |
| API routes & server logic | Antigravity / Cursor | Gemini 2.5 Pro | Backend logic + validation |
| AI integration (OpenAI) | Antigravity / Cursor | Claude Sonnet 4 | API key handling + structured output |

---

## 🚀 PHASE 1: Project Initialization

### Step 1.1: Create Project Directory (Manual)
**Type**: Manual Action
1. Open your terminal.
2. Create project folder:
   ```bash
   mkdir meal-planner-ai && cd meal-planner-ai
   git init
   ```

### Step 1.2: Framework & Dependency Scaffolding
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

\```text
PROMPT 1.2: FRAMEWORK SCAFFOLDING
--------------------------------------------------
Initialize a new Next.js 14+ (App Router) project in the current directory using TypeScript and TailwindCSS.

Install these exact dependencies:
- `lucide-react` (icons)
- `framer-motion` (animations)
- `@supabase/supabase-js` and `@supabase/ssr` (database & auth)
- `openai` (AI meal generation)
- `zod` (validation)
- `stripe` (payments)
- `resend` (transactional email)
- `sonner` (toast notifications)
- `zustand` (state management)

Set up this exact directory structure:
- /app (pages & route groups)
- /components/ui (Button, Input, Card, Modal, Badge, Skeleton)
- /components/layout (Navbar, Sidebar, Footer)
- /components/features (MealCard, GroceryList, PreferenceQuiz, NutritionBadge)
- /lib (utilities, API clients, constants)
- /lib/supabase (client & server helpers)
- /lib/openai (AI generation helpers)
- /hooks (custom React hooks)
- /types (TypeScript type definitions)
- /supabase/migrations (SQL migration files)

Do not start the dev server.
\```

### Step 1.3: Design System & CSS Tokens
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

\```text
PROMPT 1.3: DESIGN SYSTEM
--------------------------------------------------
Context: You have already initialized the Next.js project with TailwindCSS.

Configure a fresh, food-themed design system:
- Primary palette: Warm green (#22c55e) to emerald gradient for health/freshness
- Accent: Amber (#f59e0b) for highlights and CTAs
- Dark mode as default with rich, appetizing color tones
...
\```

[...continues for 34 total prompts across 6 phases + 4 checkpoints...]
```

> **Note**: This preview shows the first 3 prompts. The full playbook contains 34 sequential prompts covering UI components, landing page, authentication, database, AI meal generation, grocery list logic, billing, settings, and deployment.
