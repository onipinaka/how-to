# Example Prompts Reference: Phases 2-6

This file contains fully worked example prompts for Phases 2-6 of a standard SaaS playbook. The agent loads this file on demand to understand the expected depth, style, and format of micro-prompts before generating the actual playbook.

**CRITICAL**: When generating a real playbook, tailor ALL prompts to the user's specific product domain and tech stack. These are format/depth references, not copy-paste templates.

---

## 🎨 PHASE 2: UI Component Library (Atomic Micro-Prompts)

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

### Step 2.2: Input & Form Field Component
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.2: INPUT & FORM FIELD COMPONENT
--------------------------------------------------
Context: Button component exists at components/ui/Button.tsx.

Create `components/ui/Input.tsx` — a styled input component with:
- Support for: text, email, password (with show/hide toggle eye icon), number, search.
- Props: label, error (string for error message), helperText, icon (left icon), required, and all standard HTML input attributes.
- Visual states: default (border-border), focused (ring-2 ring-primary), error (border-destructive + red error text below), disabled (muted bg).
- Smooth focus ring animation.
```

### Step 2.3: Card Component
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.3: CARD COMPONENT
--------------------------------------------------
Context: Button and Input components exist in components/ui/.

Create `components/ui/Card.tsx` with sub-components:
- `Card` (wrapper with rounded border, subtle bg, hover-lift animation)
- `CardHeader` (title + optional description + optional action button slot)
- `CardContent` (padded body area)
- `CardFooter` (bottom action bar, right-aligned)
- Variant: `default`, `glass` (glassmorphism with backdrop-blur).
```

### Step 2.4: Modal / Dialog Component
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.4: MODAL DIALOG COMPONENT
--------------------------------------------------
Context: Card component exists at components/ui/Card.tsx.

Create `components/ui/Modal.tsx`:
- Overlay backdrop with blur + dark scrim (click to close).
- Centered modal panel with entrance animation (fade + scale up via Framer Motion).
- Props: isOpen, onClose, title, description, children, size (sm/md/lg/full).
- Close button (X icon) in top-right corner.
- Focus trap: when modal is open, Tab key cycles only through modal elements.
- Escape key closes modal.
- Prevent body scroll when modal is open.
```

### Step 2.5: Skeleton Loader Component
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.5: SKELETON LOADER COMPONENT
--------------------------------------------------
Context: UI component library growing in components/ui/.

Create `components/ui/Skeleton.tsx`:
- A shimmer animation component for loading states.
- Variants: `text` (single line), `avatar` (circle), `card` (rectangle), `table-row` (row of cells).
- Props: width, height, className, variant.
- Smooth pulse/shimmer animation using TailwindCSS animate-pulse or a custom CSS shimmer keyframe.
```

### Step 2.6: Badge & Status Indicator
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.6: BADGE COMPONENT
--------------------------------------------------
Context: UI component library in components/ui/.

Create `components/ui/Badge.tsx`:
- Variants: `default`, `success` (green), `warning` (amber), `error` (red), `info` (blue), `outline`.
- Sizes: `sm`, `md`.
- Props: variant, size, children, className.
- Subtle rounded pill shape with semi-transparent backgrounds matching each variant color.
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
- Mobile: Hamburger icon that toggles a full-height drawer overlay from the right with Framer Motion slide animation.
- Active link indicator: bottom border highlight on current route.
- Scroll behavior: slight shadow appears on Navbar after scrolling 50px.
```

### Step 2.8: Footer Component
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.8: FOOTER COMPONENT
--------------------------------------------------
Context: Navbar exists at components/layout/Navbar.tsx.

Create `components/layout/Footer.tsx`:
- 4-column grid layout (responsive: 1 column mobile, 2 tablet, 4 desktop).
- Column 1: Logo, one-line tagline, social media icon links (Twitter/X, GitHub, LinkedIn).
- Column 2: Product links (Features, Pricing, Changelog, Roadmap).
- Column 3: Resources (Documentation, Blog, API Reference, Status Page).
- Column 4: Company (About, Careers, Contact, Privacy Policy, Terms of Service).
- Bottom bar: Copyright line + stack attribution.
- Muted color palette with hover:text-foreground transitions on links.
```

### Step 2.9: Sidebar Navigation (Dashboard Layout)
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.9: DASHBOARD SIDEBAR
--------------------------------------------------
Context: Navbar and Footer exist in components/layout/. All UI primitives available.

Create `components/layout/Sidebar.tsx`:
- Fixed left sidebar (width: 240px desktop, collapsible to 64px icon-only mode).
- Top: Workspace/org name with dropdown switcher.
- Navigation sections with Lucide icons: Main (Dashboard, Core Pages, Analytics), Management (Team, Settings), Account (Billing, Help).
- Active route highlighting with primary color left border + bg-muted.
- Bottom: User avatar, name, role badge, and sign-out button.
- Collapse toggle with Framer Motion layout animation.
- Mobile: Hidden by default, toggled via hamburger, slides in as overlay.
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
- Primary headline: Large (text-5xl md:text-7xl) bold heading with gradient text on the key phrase, tailored to the product's value prop.
- Subtitle: text-lg muted-foreground paragraph (2-3 lines).
- CTA row: "Get Started Free" (primary gradient button) + "Watch Demo" (secondary outline button with Play icon).
- Social proof line with small avatar stack.
- Hero visual: Large container with mock screenshot/dashboard preview and subtle floating animation.
- Background: Radial gradient glow (indigo/violet, opacity 20%).
```

### Step 2.11-2.14: Landing Page Sections (Features Grid, Pricing, Testimonials, FAQ)

Follow the same atomic pattern shown above for each landing section. Each prompt creates ONE component with specific, domain-tailored content. See Steps 2.11-2.14 in the playbook template reference for the exact format.

### Step 2.15: Assemble Landing Page
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 2.15: ASSEMBLE LANDING PAGE
--------------------------------------------------
Context: All landing page sections exist in components/landing/. Navbar and Footer exist in components/layout/.

Update `app/page.tsx` to compose the full landing page:
- Import and render in order: Navbar, HeroSection, FeaturesGrid, PricingSection, TestimonialsSection, FAQSection, Footer.
- Add proper spacing between sections (py-20 or py-24).
- Wrap in a main tag with smooth-scroll behavior enabled.
- Add SEO metadata in a `generateMetadata` export: title, description, open graph tags.
```

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

List every error you find and fix each one.
```

---

## ⚡ PHASE 3: Authentication & Database Setup

### Step 3.1: Supabase Project Setup (Manual)
**Type**: Manual Action
1. Go to supabase.com and create a new project.
2. Copy Project URL, anon key, and service role key into `.env.local`.

### Step 3.2: Supabase Client Helpers
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 3.2: SUPABASE CLIENT SETUP
--------------------------------------------------
Context: Supabase dependencies installed. Env vars configured.

Create three files:
1. `lib/supabase/client.ts` — Browser client using `createBrowserClient`.
2. `lib/supabase/server.ts` — Server client using `createServerClient` with cookie handling.
3. `lib/supabase/admin.ts` — Admin client using service role key for server-only operations.
```

### Step 3.3: Database Schema Migration
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 3.3: DATABASE MIGRATION SQL
--------------------------------------------------
Context: Supabase project created. Client helpers in lib/supabase/.

Create `supabase/migrations/001_initial_schema.sql` with complete SQL for all domain entities. Include: tables with all columns/types/constraints, PRIMARY KEYs, FOREIGN KEYs with ON DELETE CASCADE, INDEXes, Row Level Security policies.

Cover all entities from the PRD: users, organizations, memberships, core domain entity, notifications, audit_logs, and any domain-specific tables.
```

### Step 3.4: Auth Middleware & Route Protection
**Tool**: Antigravity / Cursor | **Model**: Claude Sonnet 4

```text
PROMPT 3.4: AUTH MIDDLEWARE
--------------------------------------------------
Context: Supabase server client exists.

Create `middleware.ts`: Protect dashboard/settings/API routes, redirect to /login if no session.
Create `hooks/use-user.ts`: Custom hook returning { user, isLoading, error, signOut } with reactive auth state.
```

### Step 3.5-3.6: Login & Signup Pages
One prompt per page. Same centered card layout. Login includes OAuth buttons and forgot password link. Signup includes real-time password strength indicator. Both use Supabase auth methods.

---

## ✅ CHECKPOINT 3: Verify Auth Flow

```text
CHECKPOINT PROMPT 3: FIX AUTH FLOW
--------------------------------------------------
Context: Login, Signup, Middleware, and Supabase clients created.

Test: signup → email verification → login → redirect to /dashboard. Unauthenticated /dashboard should redirect to /login.
Fix: Supabase init errors, middleware routing, cookie handling, OAuth redirects, redirect loops.
```

---

## 🔗 PHASE 4: Dashboard & Core Features

### Step 4.1: Dashboard Layout Shell
Layout with sidebar + main content area + top bar (breadcrumb, search, notification bell, user avatar dropdown).

### Step 4.2: Dashboard Home Page
Welcome heading, stats row (3-4 metric cards with trend indicators), project grid from Supabase, recent activity feed, loading/empty states.

### Step 4.3: Core Domain CRUD — List Page
Page title + "Create New" CTA, filters row (search, status, date, sort), table/grid view toggle, pagination, loading/empty states, server-side data fetching.

### Step 4.4: Core Domain CRUD — Create/Edit Form
Full-page form with Zod validation, create (POST) and edit (PATCH) variants, loading/success/error states.

### Step 4.5: Core Domain — Detail/View Page
Header with metadata, action buttons (edit/delete/share), full content rendering, delete confirmation modal, 404 handling.

---

## ✅ CHECKPOINT 4: Verify Core CRUD

```text
CHECKPOINT PROMPT 4: FIX DASHBOARD & CRUD ERRORS
--------------------------------------------------
Context: Dashboard home and CRUD pages created.

Test full CRUD flow: List → Create → View → Edit → Delete.
Fix: Supabase query errors, RLS blocking, form validation, redirects, pagination, TypeScript mismatches.
```

---

## 💳 PHASE 5: Settings, Billing & Integrations

### Step 5.1: Settings Layout & Profile Page
Sub-navigation tabs (Profile, Security, Team, Billing, Notifications). Profile page with avatar upload, form fields, danger zone (delete account). Security page with change password and connected accounts.

### Step 5.2: Stripe Integration Setup (Manual)
Create Stripe account, copy API keys to .env.local, set up webhook endpoint.

### Step 5.3: Stripe Checkout & Billing API
`lib/stripe.ts` helper, checkout API route, portal API route, webhook handler (checkout.completed, subscription.updated, subscription.deleted, payment.failed).

### Step 5.4: Billing Settings Page
Current plan card, upgrade CTAs, Stripe Customer Portal link, invoice history table.

---

## 🚢 PHASE 6: Final Audit, Polish & Deployment

### Step 6.1: TypeScript & Build Audit

```text
PROMPT 6.1: FULL CODEBASE AUDIT
--------------------------------------------------
Context: Complete application built.

Run `npx tsc --noEmit` and `npm run build`. Fix every error: missing types, unused imports, incorrect props, missing return types, ESLint warnings. Confirm zero errors and zero warnings.
```

### Step 6.2: Accessibility & SEO Audit

```text
PROMPT 6.2: ACCESSIBILITY & SEO AUDIT
--------------------------------------------------
Context: Full application built and type-checked.

Audit for: aria-labels on interactive elements, form input labels, image alt text, WCAG 2.1 AA color contrast, focus states, page metadata, Open Graph tags, semantic HTML, single h1 per page. Fix all issues.
```

### Step 6.3: Production Deployment (Manual)
Push to GitHub, import to Vercel, configure env vars, deploy, update Stripe webhook URL and Supabase redirect URLs, test full flow on production.
