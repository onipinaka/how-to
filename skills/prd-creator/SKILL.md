---
name: prd-creator
description: Generate an exhaustive, ultra-detailed, production-ready Product Requirement Document (PRD) from any app concept, prompt, or requirements (from 2 lines to 500 lines). Triggers on 'create PRD', 'generate PRD', 'write product requirements', 'spec out app', or when asked to design product requirements.
version: 1.0.0
author: onipinaka
category: product-design
---

# PRD Creator Skill

## Overview
This skill instructs the AI agent to take any app idea, concept draft, or feature request (regardless of how brief or verbose—whether 2 lines or 500 lines) and expand it into an **exhaustive, ultra-detailed, highly granular Product Requirement Document (PRD)**.

**Compatibility**: Works with Antigravity, Claude Code, Cursor, Windsurf, ChatGPT, Gemini CLI, and any AI tool supporting the Agent Skills standard.

---

## 🛑 CRITICAL QUALITY MANDATES

### Mandate 1: No Truncation or High-Level Summaries
- **NEVER generate generic, brief 2-3 page summaries.**
- The final PRD must be comprehensive enough to serve as the **sole engineering handoff document**. Target depth: **8–15+ pages equivalent**. Every section must contain substantive, specific detail — not summaries.

### Mandate 2: No Placeholders or Ellipsis
- **NEVER write** `(similar for other endpoints...)`, `...and so on`, `[add more here]`, `(repeat for remaining tables)`, or any form of abbreviated placeholder.
- Write out EVERY item explicitly — every feature, every endpoint, every table, every screen.

### Mandate 3: Repeat Depth Uniformly Across All Modules
- If a section template shows a detailed example for one module (e.g., Authentication), apply the **exact same depth and format** to every other module. Do not write one module in detail and summarize the rest.

### Mandate 4: Output as a Saved Document — Not Chat Text
- **ALWAYS save the PRD as a markdown file**, not as inline chat text.
- Use the best available method depending on the AI tool:
  1. **Antigravity**: Save as an **artifact** markdown file (e.g., `prd_[product-name].md`). Set `UserFacing: true`.
  2. **Claude Code / Cursor / Windsurf**: Write to a file in the project workspace (e.g., `docs/PRD.md` or `PRD.md` in the project root).
  3. **ChatGPT / Other**: If file creation is not possible, output the full PRD in a single markdown codeblock so the user can copy-paste it into a `.md` file.
- **Naming convention**: `PRD_[ProductName]_v1.md` (e.g., `PRD_MealPlannerAI_v1.md`).
- **Never split** the PRD across multiple files. It must be one complete document.

---

## 🎯 When to Trigger
Trigger this skill when the user requests:
- "Create a PRD for [app idea]"
- "Write product requirements for..."
- "Spec out this project in deep detail"
- "I have an app idea: [brief description], make a full PRD"
- Any request asking to turn a product concept into an exhaustive specification.

---

## 📋 Comprehensive PRD Generation Workflow

### Phase 1: Requirements Expansion (Mind-Mapping)
Before writing anything, silently infer and expand ALL implicit dimensions:
- **User Roles & Authorization Matrix** (Guest, Free, Pro, Team Admin, Super Admin, API Integration Key).
- **Page & View Hierarchy** (Landing, Onboarding, Auth, Core Dashboards, Settings, Billing, Analytics, Workspace Management, Modals, Drawer Views).
- **Complete Data Models & Fields** (Database tables, exact data types, constraints, relations).
- **Complete API Endpoint Index** (HTTP Method, Route Path, Parameters, Auth level, Request/Response payloads).
- **UI States per Screen** (Default State, Loading Skeleton, Empty State, Error Alert State, Success Toast State).
- **Edge Cases & Failure Recovery** (Rate limit exceeded, offline queue, token expiration, webhook retries).

### Phase 2: Generate the Full PRD Using the Schema Below

---

## 📄 Exhaustive PRD Output Schema

The AI must output the PRD using this exact structure, filling every section completely for the user's specific product.

---

### Section 1: Header & Metadata

```markdown
# 📄 Exhaustive Product Requirement Document (PRD): [App / Product Name]

> **Version**: 1.0 (Production Blueprint)
> **Status**: Deep Spec / Ready for Engineering
> **Author**: AI Lead Product Architect
> **Date**: [Current Date]
```

---

### Section 2: Key Assumptions & Inferred Scope
If the user input was short (under 50 lines), explicitly list every architectural and product assumption made to expand the idea. Format as a numbered list. Example:

```markdown
## ⚠️ Key Assumptions & Inferred Scope
1. Assumed web-first SaaS with responsive mobile support (not native apps).
2. Assumed freemium monetization model with Stripe billing integration.
3. Assumed multi-tenant workspace model where users belong to organizations.
4. Assumed PostgreSQL via Supabase for database and auth.
5. Assumed deployment on Vercel with edge functions.
```

---

### Section 3: Executive Summary & Core Value Proposition
- **Problem Statement**: Deep, specific breakdown of the pain point — not a generic sentence, but **3-5 lines** explaining the user's frustration, current workarounds, and market gap.
- **Core Value Proposition**: Why this solution wins over existing alternatives. Specific differentiators.
- **Primary Goals & KPIs**: Minimum 4 quantified KPIs (e.g., `<100ms API response time p95`, `40% user activation within first 24 hours`, `<2% monthly churn`, `99.9% uptime SLA`).

---

### Section 4: Target Audience, Personas & RBAC Matrix

Write **2-3 detailed personas** (not one-liners — each persona gets 5+ attributes: Demographics, Goals, Pain Points, Workflow, Willingness to Pay). Then produce a full RBAC permission matrix table:

```markdown
### Role-Based Access Control (RBAC) Matrix
| Permission | Guest | Free Member | Pro Member | Team Admin | Super Admin |
| :--- | :---: | :---: | :---: | :---: | :---: |
| View public content | ✅ | ✅ | ✅ | ✅ | ✅ |
| Create projects | ❌ | ✅ (limit 3) | ✅ (unlimited) | ✅ | ✅ |
| Edit own projects | ❌ | ✅ | ✅ | ✅ | ✅ |
| Invite team members | ❌ | ❌ | ❌ | ✅ | ✅ |
| Manage billing | ❌ | ❌ | ❌ | ✅ | ✅ |
| Access admin panel | ❌ | ❌ | ❌ | ❌ | ✅ |
| API key access | ❌ | ❌ | ✅ | ✅ | ✅ |
```

---

### Section 5: Atomic Feature Breakdown (Granular Module Specs)

**CRITICAL RULE**: Use the EXACT format shown below for EVERY module. Each module MUST contain all 5 parts. Here is the mandatory format demonstrated with one module:

```markdown
### 3.1 Module: Authentication & User Lifecycle
- **Overview**: Complete user authentication system with email/password, OAuth, session management, and account recovery flows.
- **Priority**: P0 — Must Have
- **Atomic Features**:
  - `FEAT-1.1`: Email/Password registration with real-time field validation.
  - `FEAT-1.2`: Email verification via 6-digit OTP (expires after 10 min).
  - `FEAT-1.3`: OAuth 2.0 login (Google, GitHub) with automatic account linking.
  - `FEAT-1.4`: Session JWT in HTTP-Only cookie + refresh token rotation.
  - `FEAT-1.5`: "Forgot Password" flow with email reset link (expires 1 hour).
  - `FEAT-1.6`: Account deletion with 30-day grace period and data export.
  - `FEAT-1.7`: Rate limiting: max 5 failed login attempts per IP per 15 minutes.
- **User Stories**:
  - "As a new user, I want to sign up with my email and verify it via OTP so I know my account is secure."
  - "As a returning user, I want to log in with Google SSO so I don't have to remember a password."
  - "As a user who forgot my password, I want to receive a reset email within 30 seconds so I can regain access quickly."
- **Acceptance Criteria**:
  - [ ] Password field enforces minimum 8 chars, 1 uppercase, 1 number, 1 special char with real-time validation indicator.
  - [ ] OTP email delivered within 30 seconds via Resend/SendGrid.
  - [ ] OAuth login creates user record if first time, merges if email matches existing account.
  - [ ] JWT access token expires in 15 minutes, refresh token in 7 days.
  - [ ] After 5 failed login attempts, IP is blocked for 15 minutes with a clear error message.
```

**Apply this EXACT depth and format to EVERY module.** Common modules to include (add/remove based on the user's product):
- Core Application Workflow & Domain Logic (minimum 5 atomic features)
- Dashboard, Analytics & Data Visualization
- Workspace, Team Collaboration & Permissions
- Billing, Subscriptions & Monetization
- Notifications & Communication
- Settings & Account Management
- Search, Filtering & Discovery

**RULE**: Minimum 5 modules total. Every module gets the same treatment as the Authentication example above. Never write one module in detail and summarize the rest.

---

### Section 6: Complete Screen Hierarchy & Interface States

For **EVERY screen/view** in the application, write the full entry. Here is the mandatory format:

```markdown
### Screen: `/dashboard` — Main User Hub
- **Route**: `/dashboard`
- **Auth Required**: Yes
- **Key Components**: Sidebar, TopBar (search + user avatar dropdown), ProjectGrid/ProjectList, QuickActionButtons, RecentActivityFeed.
- **States**:
  - **Default**: Grid of project cards showing title, status badge, last edited timestamp, and quick-action dots menu.
  - **Loading**: Skeleton grid of 6 placeholder cards with shimmer animation.
  - **Empty**: Centered illustration with heading "No projects yet" and CTA button "Create Your First Project."
  - **Error**: Red banner at top "Failed to load projects — please try again" with Retry button.
  - **Success**: Toast "Project created successfully" on new project creation.
```

**RULE**: Minimum 8-12 screens. Every screen gets the full 5-state breakdown shown above. No abbreviated entries. Include: Landing Page, Login, Signup, Dashboard, Core Entity List, Core Entity Detail, Core Entity Create/Edit, Settings Profile, Settings Billing, Settings Team, and any domain-specific screens.

> 📎 See `references/screen_hierarchy_examples.md` for additional fully worked screen examples.

---

### Section 7: Exhaustive API Endpoint Specification

**RULE**: Minimum 15–25 endpoints covering ALL CRUD operations for every entity. Format as a table:

```markdown
| # | HTTP Method | Endpoint Route | Description | Auth | Request Payload | Response Payload |
| :--- | :--- | :--- | :--- | :---: | :--- | :--- |
| 1 | `POST` | `/api/v1/auth/register` | Register new user | No | `{ email, password, name }` | `{ user_id, message }` |
| 2 | `POST` | `/api/v1/auth/login` | Authenticate user | No | `{ email, password }` | `{ access_token, refresh_token, user }` |
| 3 | `POST` | `/api/v1/auth/logout` | Invalidate session | Yes | — | `{ message }` |
| 4 | `GET` | `/api/v1/users/me` | Get current user | Yes | — | `{ id, email, name, avatar_url, role }` |
| 5 | `PATCH` | `/api/v1/users/me` | Update profile | Yes | `{ name?, avatar_url? }` | `{ updated_user }` |
```

Continue for ALL entities: auth (7 endpoints), users (3), domain entities (5 CRUD), organizations (4), billing (3), webhooks (1), notifications (2). Write out EVERY row — never abbreviate with "continue for all..."

> 📎 See `references/api_endpoint_examples.md` for a complete 25-row example table.

---

### Section 8: Full Database Schema & Data Dictionary

**RULE**: Write complete `CREATE TABLE` statements for **EVERY entity**. Each table must include all columns with data types, `PRIMARY KEY`, `FOREIGN KEY` references, `INDEX` definitions, and `DEFAULT` values. Here is the mandatory format:

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash TEXT,
  full_name VARCHAR(255) NOT NULL,
  avatar_url TEXT,
  bio TEXT,
  role VARCHAR(50) NOT NULL DEFAULT 'member' CHECK (role IN ('member', 'admin', 'super_admin')),
  email_verified BOOLEAN DEFAULT FALSE,
  oauth_provider VARCHAR(50),
  oauth_provider_id VARCHAR(255),
  last_login_at TIMESTAMP WITH TIME ZONE,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_role ON users(role);
```

Apply this EXACT level of detail to EVERY table. Minimum 5-6 tables. No comment-only placeholders like `-- Projects table (add columns)`.

> 📎 See `references/schema_examples.md` for fully worked examples of all baseline tables (users, organizations, memberships, projects, notifications, audit_logs).

---

### Section 9: Third-Party Integrations & SDK Architecture

Table with columns: Service Category, Provider, SDK/Library, Purpose, Webhook Events.

```markdown
| Service Category | Provider | SDK / Library | Purpose | Webhook Events |
| :--- | :--- | :--- | :--- | :--- |
| **Auth** | Supabase Auth | `@supabase/supabase-js` | User auth, OAuth, session mgmt | N/A |
| **Database** | PostgreSQL via Supabase | `@supabase/supabase-js` | Data storage, RLS policies | N/A |
| **Payments** | Stripe | `stripe` Node SDK | Checkout, subscriptions, invoices | `checkout.session.completed`, `invoice.payment_succeeded`, `customer.subscription.deleted` |
| **Email** | Resend | `resend` | OTP, welcome, reset, receipts | N/A |
| **Analytics** | PostHog | `posthog-js` | Product analytics, feature flags | N/A |
| **Error Tracking** | Sentry | `@sentry/nextjs` | Runtime error capture | N/A |
```

Cover ALL integrations relevant to the product.

---

### Section 10: Non-Functional Requirements (NFRs)

Cover all categories with specific, quantified targets:
- **Performance**: API response latency (`< 150ms p95` reads, `< 300ms p95` writes), page load LCP (`< 1.5s` on 4G), database query time (`< 50ms` indexed).
- **Security**: OWASP Top 10 compliance, Zod input validation, CSRF via SameSite cookies, XSS via CSP headers, AES-256 encryption at rest, TLS 1.3 in transit.
- **Scalability**: Horizontal scaling via serverless, connection pooling (PgBouncer), Redis caching, CDN for static assets.
- **Accessibility**: WCAG 2.1 AA, keyboard navigation, screen reader labels, color contrast ratio ≥ 4.5:1.
- **Monitoring & Observability**: Sentry for errors, PostHog for session replay, uptime monitoring.

---

### Section 11: Comprehensive Edge Cases & Failure Modes

Table with minimum 12-15 edge cases:

```markdown
| Category | Edge Case | Expected Behavior |
| :--- | :--- | :--- |
| **Auth** | User submits expired OTP | Show "OTP expired, request a new one" with resend button. |
| **Auth** | OAuth provider is temporarily down | Fallback to email/password with notice. |
| **Data** | Network disconnect mid-form-submit | Client-side retry with exponential backoff (max 3). |
| **Data** | Concurrent edits on same resource | Last-write-wins with optimistic locking (version column). |
| **Billing** | Stripe webhook delayed/dropped | Idempotent handler + cron reconciliation every 6 hours. |
| **Billing** | Card declined on renewal | Dunning emails Day 1, 3, 7. Downgrade to Free after Day 7. |
| **Performance** | DB connection pool exhaustion | PgBouncer + queue with timeout. Return 503 with Retry-After. |
| **Security** | SQL injection attempt | Parameterized queries via ORM. Input sanitized and logged. |
| **Security** | Brute force login attack | Rate limit 5/15min per IP + CAPTCHA after 3 failures. |
| **UX** | Session expires during long form | Auto-save to localStorage every 30s. Restore on re-auth. |
```

Write out ALL edge cases explicitly — never abbreviate.

---

### Section 12: Out of Scope (v1.0)

Explicitly list features NOT included in v1 to maintain focus:
- Native mobile apps (iOS/Android) — web responsive only for v1.
- Real-time collaborative editing (multiplayer cursors).
- AI-powered features beyond basic automation.
- Multi-language / i18n support.
- Custom domain mapping for workspaces.
- Marketplace / plugin ecosystem.
- Advanced analytics dashboards (custom report builder).

---

## 💡 Guidelines for Handling Minimal (2-Line) Inputs
If the user provides a minimal prompt (e.g., *"Make a PRD for an AI meal planner app"*):
1. **Never ask the user 20 questions first.** Generate the complete v1.0 PRD immediately with sensible, industry-standard defaults.
2. Highlight all assumptions in the `## ⚠️ Key Assumptions & Inferred Scope` section.
3. Infer the most logical tech stack, user roles, and monetization model based on the domain.
4. Still produce the FULL depth across all sections — minimal input does NOT mean minimal output.
