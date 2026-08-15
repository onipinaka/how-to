---
name: playbook-creator
description: Convert any PRD, app concept, or project request into an end-to-end, zero-code execution playbook with copy-paste prompts for AI tools (Claude, Antigravity, Cursor, v0, Bolt). Triggers on 'create playbook', 'spoonfeed playbook', 'generate build prompts', 'step by step prompts', or 'create execution guide'.
version: 1.0.0
author: onipinaka
category: development
---

# Playbook Creator Skill

## Overview
This skill generates an **exhaustive, highly granular, step-by-step, zero-code execution Playbook** for building any software project or application.

The playbook breaks the entire project down into **tiny, atomic, copy-paste prompts** tailored for AI tools (Claude, Antigravity, Cursor, v0, Bolt.new, ChatGPT) so that the user can build complex applications one small, manageable step at a time without getting overwhelmed or hitting token/context limits.

**Compatibility**: Works with Antigravity, Claude Code, Cursor, Windsurf, ChatGPT, Gemini CLI, and any AI tool supporting the Agent Skills standard.

---

## 🛑 MANDATORY MANDATES

### Mandate 1: Ultra-Granular Micro-Prompts
- **DO NOT BUNDLE ENTIRE MODULES INTO SINGLE HUGE PROMPTS.**
- **ONE PROMPT = ONE TASK**: Separate prompt for folder structure. Separate prompt for `tailwind.config`. Separate prompt for Navbar. Separate prompt for Footer. Separate prompt for each SQL migration. Separate prompt for each API route. Separate prompt for each form component. Separate prompt for each integration.
- A complete playbook for a standard SaaS application must contain a **MINIMUM of 20–40 sequential prompts**.

### Mandate 2: Zero Application Code in Playbook
- Do NOT write actual application source code (no TypeScript files, no React components, no SQL) inside the playbook text.
- DO write **engineered copy-paste prompts** inside codeblocks that instruct an AI tool to write that exact code when executed.

### Mandate 3: No Bracket Placeholders
- **NEVER output bracket placeholders** like `[Detailed prompt for...]`, `[Add specifics here]`, or `[Core action]` in any prompt block.
- Every single prompt must be **fully written out** with specific, actionable, complete instructions.

### Mandate 4: Tailor to Domain
- ALL example prompts in this schema are illustrative templates for a generic SaaS. When generating a real playbook, **every prompt must be tailored to the user's specific product domain, features, and tech stack**.
- Do NOT copy generic SaaS landing page patterns when the product is an IoT dashboard, a mobile game backend, a CRM, a marketplace, or any other domain.

### Mandate 5: Context Passing Between Prompts
- Each prompt after Phase 1 must include a **Context line** at the top that references relevant prior work so the AI tool receiving the prompt has continuity.
- Format: `Context: You have already created [X] in [file]. Now build [Y] that uses/extends it.`

### Mandate 6: Output as a Saved Document — Not Chat Text
- **ALWAYS save the Playbook as a markdown file**, not as inline chat text.
- Use the best available method depending on the AI tool:
  1. **Antigravity**: Save as an **artifact** markdown file (e.g., `playbook_[product-name].md`). Set `UserFacing: true`.
  2. **Claude Code / Cursor / Windsurf**: Write to a file in the project workspace (e.g., `docs/PLAYBOOK.md` or `PLAYBOOK.md` in the project root).
  3. **ChatGPT / Other**: If file creation is not possible, output the full playbook in a single markdown codeblock so the user can copy-paste it into a `.md` file.
- **Naming convention**: `PLAYBOOK_[ProductName]_v1.md` (e.g., `PLAYBOOK_MealPlannerAI_v1.md`).
- **Never split** the playbook across multiple files. It must be one complete, sequential document.

### Mandate 7: Extreme Detail in EVERY Prompt
- **NEVER output a short, 1-sentence prompt.** 
- EVERY prompt must be highly detailed (100-200+ words). You must explicitly list all files to create, specific UI components to import, exact state variables needed, specific error handling logic, and specific Tailwind layout classes. 
- **DO NOT meta-comment** like "Generate similarly detailed prompts for the rest". You must actually generate the full text for EVERY prompt in the entire project.

---

## 🎯 When to Trigger
Trigger this skill when the user requests:
- "Create a playbook for this PRD"
- "Give me step-by-step copy-paste prompts to build [app]"
- "Spoon-feed me detailed micro-prompts to build [idea]"
- "Break down this app into copy-paste prompts for AI editors"

---

## 📋 Exhaustive Playbook Structure & Schema

Structure the playbook across deep, micro-segmented phases. The output must begin with a header block, tool matrix, and then progress through sequential phases with checkpoint verification between each major phase.

### Playbook Header Block

```markdown
# 🗺️ Master Execution Playbook: [Project / Product Name]

> **Goal**: Exhaustive, step-by-step guide to build [Product Name] using AI tools from zero to live deployment.
> **Total Prompts**: [Count] sequential micro-prompts.
> **Instruction**: Execute each step sequentially. Do not skip steps. Copy-paste each prompt into the specified AI tool. After each checkpoint, verify before continuing.
```

### Tool & Model Assignment Matrix

Assign a specific AI tool and model to every task category in a table format:

| Task Category | Recommended AI Tool | Recommended Model | Why This Tool |
| :--- | :--- | :--- | :--- |
| Project scaffolding & config | Antigravity / Cursor / Claude Code | Claude Sonnet 4 | Best for multi-file generation |
| UI component creation | v0.dev / Bolt.new | Claude Sonnet 4 | Specialized for React/Tailwind UI |
| Complex UI screens with logic | Antigravity / Cursor | Claude Sonnet 4 / Gemini 2.5 Pro | Handles state + layout together |
| Database schema & migrations | Antigravity / Cursor | Claude Sonnet 4 | SQL generation and RLS policies |
| API routes & server logic | Antigravity / Cursor | Claude Sonnet 4 / Gemini 2.5 Pro | Backend logic + validation |
| Third-party SDK integration | Antigravity / Cursor | Claude Sonnet 4 | API key handling + webhook setup |
| Debugging & error fixing | Antigravity / Cursor / Claude Code | Claude Sonnet 4 | Context-aware fixes |
| Final audit & deployment | Antigravity / Cursor | Claude Sonnet 4 | Build validation |

---

## 🚀 PHASE 1: Project Initialization & Architecture Scaffolding

### Step 1.1: Create Project Directory (Manual)
**Type**: Manual Action
1. Open your terminal.
2. Create project folder:
   ```bash
   mkdir my-app && cd my-app
   git init
   ```

### Step 1.2: Framework & Dependency Scaffolding
**Tool**: Antigravity / Cursor / Claude Code | **Model**: Claude Sonnet 4

```text
PROMPT 1.2: FRAMEWORK SCAFFOLDING
--------------------------------------------------
Initialize a new Next.js 14+ (App Router) project in the current directory using TypeScript and TailwindCSS.

Install these exact dependencies:
- `lucide-react` (icons)
- `framer-motion` (animations)
- `@supabase/supabase-js` and `@supabase/ssr` (database & auth)
- `zod` (validation)
- `stripe` (payments)
- `resend` (transactional email)
- `sonner` (toast notifications)
- `zustand` (state management)

Set up this exact directory structure (create empty directories with a .gitkeep file):
- /app (pages & route groups)
- /components/ui (reusable primitives: Button, Input, Card, Modal, Badge, Skeleton)
- /components/layout (Navbar, Sidebar, Footer)
- /components/features (domain-specific feature components)
- /lib (utility functions, API clients, constants)
- /lib/supabase (Supabase client & server helpers)
- /hooks (custom React hooks)
- /types (TypeScript type definitions)
- /supabase/migrations (SQL migration files)

Do not start the dev server. Just generate all config files and the directory structure.
```

### Step 1.3: Global Design System & CSS Tokens
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 1.3: DESIGN SYSTEM & CSS TOKENS
--------------------------------------------------
Context: You have already initialized the Next.js project with TailwindCSS. Now configure the design system.

Update `tailwind.config.ts` to extend the theme with:
- Custom colors using HSL CSS variables: `--background`, `--foreground`, `--primary`, `--primary-foreground`, `--secondary`, `--accent`, `--muted`, `--muted-foreground`, `--border`, `--input`, `--ring`, `--destructive`.
- Custom border radius tokens: `--radius-sm`, `--radius-md`, `--radius-lg`.
- Font family: 'Inter' from Google Fonts as the sans-serif default.

Update `app/globals.css` to:
- Define `:root` (light) and `.dark` (dark) CSS variable palettes. Use a modern dark theme as default with indigo/violet primary palette.
- Add utility classes: `.glass-card` (backdrop-blur + semi-transparent bg), `.gradient-text` (bg-clip-text with gradient), `.hover-lift` (translateY(-2px) on hover with shadow).
- Smooth global transitions on all interactive elements.

Update `app/layout.tsx` to:
- Import 'Inter' from `next/font/google`.
- Apply the font class to `<html>`.
- Set default `<html>` class to `dark`.
- Add `<meta>` tags for SEO (title, description, viewport, theme-color).
```

### Step 1.4: Environment Variables Template
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 1.4: ENVIRONMENT CONFIGURATION
--------------------------------------------------
Context: Project scaffolded with Supabase, Stripe, and Resend dependencies installed.

Create `.env.local` with placeholder values for all required environment variables.
Create `.env.example` with the same keys but empty values (for other developers).
Add `.env.local` to `.gitignore` if not already present.
Create `lib/env.ts` with a Zod schema that validates all required env vars at build time and exports typed constants.
```

---

## ✅ CHECKPOINT 1: Verify Foundation

1. **Manual**: Run `npm run dev` and open `http://localhost:3000`.
2. **Verify**: Default Next.js page with dark theme and Inter font applied.
3. If errors, use this prompt:

```text
CHECKPOINT PROMPT 1: FIX FOUNDATION ERRORS
--------------------------------------------------
Context: I just scaffolded a Next.js 14+ project with TailwindCSS, Inter font, and a dark theme design system.

Run `npm run dev` and check for errors. Fix any:
- Missing dependency errors
- TailwindCSS configuration issues
- TypeScript config issues
- Import path errors

Confirm the dev server starts cleanly on localhost:3000.
```

---

## 🎨 PHASE 2: UI Component Library (Atomic Micro-Prompts)

Every UI component gets its own dedicated prompt. Here are representative examples showing the expected depth. **Generate ALL component prompts at this same level of detail.**

### Step 2.1: Button Component
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.1: BUTTON COMPONENT
--------------------------------------------------
Context: Design system configured in globals.css and tailwind.config.ts with HSL CSS variables.

Create `components/ui/Button.tsx` — a reusable button component with:
- Variants: `primary` (gradient bg), `secondary` (outline border), `ghost` (transparent), `destructive` (red).
- Sizes: `sm`, `md`, `lg`.
- States: disabled (opacity + pointer-events-none), loading (spinner icon replaces text).
- Props: variant, size, isLoading, disabled, children, onClick, className, type, and all standard HTML button attributes via React.ButtonHTMLAttributes.
- Smooth hover transitions with subtle scale and shadow elevation.
- Use `cva` (class-variance-authority) or manual className merging pattern.
```

### Step 2.7: Navigation Bar
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.7: NAVIGATION BAR
--------------------------------------------------
Context: UI primitives (Button, Input, Badge) exist in components/ui/. Design tokens configured in globals.css.

Create `components/layout/Navbar.tsx`:
- Fixed top position with `backdrop-blur-md` and `bg-background/80` transparency.
- Left: Logo icon + app name with gradient text.
- Center (desktop): Navigation links specific to the product — e.g., Features, Pricing, Docs, Blog.
- Right: "Log In" button (ghost variant) and "Get Started" button (primary variant with subtle glow).
- Mobile: Hamburger icon that toggles a full-height drawer overlay from the right with Framer Motion slide animation. Drawer contains same nav links + CTA buttons stacked vertically.
- Active link indicator: bottom border highlight on current route.
- Scroll behavior: slight shadow appears on Navbar after scrolling 50px.
```

### Step 2.10: Landing Page — Hero Section
**Tool**: v0.dev / Antigravity | **Model**: Claude Sonnet 4

```text
PROMPT 2.10: HERO SECTION
--------------------------------------------------
Context: Navbar exists. Design system with dark theme, gradient utilities, and glass-card class configured.

Create `components/landing/HeroSection.tsx`:
- Centered layout with max-width container.
- Announcement badge at top: small pill badge with link to changelog.
- Primary headline: Large (text-5xl md:text-7xl) bold heading with `.gradient-text` class on the key phrase. Text specific to the product's value prop.
- Subtitle: text-lg muted-foreground paragraph (2-3 lines) expanding on the value prop.
- CTA row: Two buttons side by side:
  - "Get Started Free" (primary gradient button with subtle pulse glow animation).
  - "Watch Demo" (secondary outline button with Play icon).
- Below CTAs: Social proof line: "Trusted by 1,000+ teams" with small avatar stack (5 overlapping circles).
- Hero visual: Large container (rounded-xl, glass border) showing a mock screenshot or dashboard preview. Apply subtle floating animation (translateY oscillation via Framer Motion).
- Background: Radial gradient glow behind the hero visual (indigo/violet, opacity 20%).
```

**CRITICAL AI INSTRUCTION**: You must actually generate the full, exhaustive text for EVERY remaining UI component prompt (Input, Card, Modal, Skeleton, Badge, Footer, Sidebar, Features Grid, Pricing Section, Testimonials, FAQ Accordion, and Landing Page Assembly). Do NOT output a summary sentence here. Write out the actual PROMPT blocks for each one with the same extreme detail as shown above.

> 📎 See `references/example_prompts.md` for fully worked examples of ALL Phase 2 component prompts plus Phases 3-6.

---

## ✅ CHECKPOINT 2: Verify Landing Page

```text
CHECKPOINT PROMPT 2: FIX LANDING PAGE ERRORS
--------------------------------------------------
Context: I assembled the landing page from components in components/landing/ and components/layout/.

Run `npm run dev` and check the browser console and terminal for errors. Fix any:
- Component import errors or missing exports
- TailwindCSS classes not applying
- Framer Motion animation errors
- Hydration mismatch warnings
- Layout or spacing issues

List every error you find and fix each one. The landing page should render perfectly with all sections visible.
```

---

## ⚡ PHASE 3: Authentication & Database Setup

### Step 3.2: Supabase Client Helpers
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 3.2: SUPABASE CLIENT SETUP
--------------------------------------------------
Context: Supabase dependencies (@supabase/supabase-js, @supabase/ssr) installed. Env vars configured in .env.local.

Create three files:
1. `lib/supabase/client.ts` — Browser client using `createBrowserClient` from @supabase/ssr. Export a function `createClient()`.
2. `lib/supabase/server.ts` — Server client using `createServerClient` from @supabase/ssr with cookie handling via next/headers. Export async function `createClient()`.
3. `lib/supabase/admin.ts` — Admin client using service role key for server-only operations. Export function `createAdminClient()`.

All clients should use the SUPABASE_URL and SUPABASE_ANON_KEY from env vars.
```

### Step 3.3: Database Schema Migration
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 3.3: DATABASE MIGRATION SQL
--------------------------------------------------
Context: Supabase project created. Client helpers in lib/supabase/.

Create `supabase/migrations/001_initial_schema.sql` with complete SQL for:

1. `users` table: id (UUID PK), email (unique), full_name, avatar_url, bio, role (enum: member/admin/super_admin), email_verified (bool), oauth_provider, last_login_at, created_at, updated_at. Add indexes on email and role.

2. `organizations` table: id (UUID PK), name, slug (unique), logo_url, owner_id (FK → users), plan (enum: free/pro/team), stripe_customer_id, stripe_subscription_id, created_at, updated_at. Add indexes on owner_id and slug.

3. `memberships` table: id (UUID PK), user_id (FK → users ON DELETE CASCADE), org_id (FK → organizations ON DELETE CASCADE), role (enum: member/admin/owner), invited_by (FK → users), joined_at. Add UNIQUE constraint on (user_id, org_id).

4. Core domain entity table (adapt to the user's specific product): id (UUID PK), org_id (FK → organizations), created_by (FK → users), title, description (TEXT), status (enum), tags (TEXT array), metadata (JSONB), created_at, updated_at. Add indexes.

5. `notifications` table and `audit_logs` table with appropriate columns, FKs, and indexes.

Enable Row Level Security (RLS) on all tables. Create policies ensuring users can only access data within their organization.
```

### Step 3.5: Login Page
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 3.5: LOGIN PAGE
--------------------------------------------------
Context: Auth middleware protecting /dashboard routes. Supabase client helpers in lib/supabase/. Button, Input, Card components in components/ui/.

Create `app/(auth)/login/page.tsx`:
- Centered card layout on a dark background with subtle gradient.
- Card contains:
  - Heading: "Welcome back" with subtitle "Log in to your account."
  - Email input field with label and validation.
  - Password input field with show/hide toggle.
  - "Forgot password?" link (text-primary, right-aligned above submit button).
  - Submit button "Log In" (full-width, primary variant, shows loading spinner during API call).
  - Divider: "or continue with"
  - OAuth buttons row: "Continue with Google" and "Continue with GitHub" (outline buttons with provider icons).
  - Bottom text: "Don't have an account? Sign up" with link to /signup.
- Form submission calls Supabase `signInWithPassword`. On success redirect to /dashboard. On error show toast with error message.
- OAuth buttons call Supabase `signInWithOAuth` with appropriate provider.
```

**CRITICAL AI INSTRUCTION**: Do not summarize! You must write out the actual full-length PROMPT blocks for the Auth middleware, Signup page, and any remaining auth flows. Every prompt must have exact logic, UI states, and routing rules.

---

## ✅ CHECKPOINT 3: Verify Auth Flow

```text
CHECKPOINT PROMPT 3: FIX AUTH FLOW
--------------------------------------------------
Context: Login at app/(auth)/login/page.tsx. Signup at app/(auth)/signup/page.tsx. Middleware at middleware.ts.

The auth flow should work: signup → email verification → login → redirect to /dashboard. Unauthenticated /dashboard access should redirect to /login.

Check for and fix: Supabase client errors, middleware routing, cookie handling, OAuth redirects, form validation, redirect loops.
```

---

## 🔗 PHASE 4: Dashboard & Core Features

**CRITICAL AI INSTRUCTION**: Write out the full, exhaustive PROMPT blocks for EVERY step in Phase 4: Dashboard layout shell, Dashboard home page, Core entity list page (with filters/pagination), Create/Edit form (with Zod validation), and Detail/View page (with delete confirmation). Do not summarize this phase. Write the actual prompts! Each prompt must specify exact state variables, DB queries, loading skeletons, and error toasts.

---

## ✅ CHECKPOINT 4: Verify Core CRUD

```text
CHECKPOINT PROMPT 4: FIX DASHBOARD & CRUD ERRORS
--------------------------------------------------
Context: Dashboard home and CRUD pages created.

Test full CRUD flow: List → Create → View → Edit → Delete. Fix: Supabase query errors, RLS blocking, form validation, redirects, pagination, TypeScript mismatches.
```

---

## 💳 PHASE 5: Settings, Billing & Integrations

**CRITICAL AI INSTRUCTION**: Write out the full, exhaustive PROMPT blocks for EVERY step in Phase 5: Settings layout with tab navigation, Profile settings page (avatar upload, form, danger zone), Security settings, Stripe checkout & webhook API routes, and Billing settings page. Do not write a summary. Write the full 100+ word prompt for each task detailing API endpoints, payloads, and UI updates.

---

## 🚢 PHASE 6: Final Audit, Polish & Deployment

### Step 6.1: TypeScript & Build Audit
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 6.1: FULL CODEBASE AUDIT
--------------------------------------------------
Context: Complete application built with all pages, components, API routes, and integrations.

Run `npx tsc --noEmit` and `npm run build`. Fix every single error: missing type annotations, unused imports, incorrect prop types, missing return types on API handlers, ESLint warnings. Confirm zero errors and zero warnings.
```

### Step 6.2: Accessibility & SEO Audit
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 6.2: ACCESSIBILITY & SEO AUDIT
--------------------------------------------------
Context: Full application built and type-checked.

Audit for: aria-labels on all interactive elements, form input labels, image alt text, WCAG 2.1 AA color contrast, visible focus states, page metadata (title, description), Open Graph tags, semantic HTML, single h1 per page. Fix all issues found.
```

### Step 6.3: Production Deployment (Manual)
**Type**: Manual Action
1. Push to GitHub: `git add . && git commit -m "Complete application" && git push origin main`
2. Import to Vercel, configure env vars, deploy.
3. Update Stripe webhook URL and Supabase redirect URLs for production domain.
4. Test full flow on production: Signup → Login → CRUD → Billing → Settings.

---

## Required Phases & Minimum Prompts Summary

| Phase | Contents | Min Prompts |
| :--- | :--- | :--- |
| **Phase 1**: Scaffolding | Directory, framework, design system, env vars | 4 |
| **Checkpoint 1** | Verify dev server starts | 1 |
| **Phase 2**: UI Components | Button, Input, Card, Modal, Skeleton, Badge, Navbar, Footer, Sidebar, Hero, Features, Pricing, Testimonials, FAQ, Assembly | 10-15 |
| **Checkpoint 2** | Verify landing page renders | 1 |
| **Phase 3**: Auth & Database | Supabase setup, clients, SQL migration, middleware, login, signup | 5-6 |
| **Checkpoint 3** | Verify auth flow | 1 |
| **Phase 4**: Dashboard & CRUD | Layout shell, home, list, create/edit, detail | 5 |
| **Checkpoint 4** | Verify CRUD works | 1 |
| **Phase 5**: Settings & Billing | Settings layout, profile, Stripe API, billing page | 4 |
| **Phase 6**: Audit & Deploy | TypeScript check, a11y audit, deployment | 3 |

**Total minimum: 20-40 prompts + 4 checkpoint prompts.**

**RULE**: Adapt phases based on the user's specific product. Add phases as needed (e.g., real-time features, file uploads, AI integration). Remove inapplicable phases (e.g., no Stripe if no billing). Always maintain atomic prompt granularity and checkpoint pattern.

> 📎 See `references/example_prompts.md` for fully worked examples of remaining component prompts (Input, Card, Modal, Skeleton, Badge, Footer, Sidebar, Features Grid, Pricing, Testimonials, FAQ) and Phases 4-5 detail.
> 📎 See `references/playbook_template.md` for the mandatory phase checklist and anti-patterns to avoid.

---

## 💡 Micro-Prompt Quality Guarantee Checklist
- Every prompt focuses on **ONE logical task** (1 component, 1 route, 1 migration, 1 integration).
- Every prompt is **fully self-contained** with exact filenames, import context, and styling expectations.
- Every prompt includes a **Context line** referencing prior work.
- **No bracket placeholders** (`[...]`) — every prompt is fully written out.
- **Checkpoint prompts** between phases to catch and fix errors before continuing.
- **Manual action steps** clearly separated from copy-paste prompts.
- **Tool & model recommendations** on every prompt block.
- Minimum **20-40 prompts** for a standard SaaS playbook.
