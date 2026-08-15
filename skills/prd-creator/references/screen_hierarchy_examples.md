# Screen Hierarchy & Interface States Examples Reference

This file contains the full example screen hierarchy with 5-state breakdowns for the PRD Creator skill. The agent loads this on demand when generating Section 6 of a PRD.

---

## Example: Complete Screen Hierarchy for a Standard SaaS Application

For **EVERY screen/view** in the application, write out the full entry. Define every screen — do not list routes without the state breakdown.

**Format per screen (mandatory)**:

### Screen: `/` — Landing Page
- **Route**: `/`
- **Auth Required**: No
- **Key Components**: Navbar, HeroSection, FeatureGrid, PricingCards, TestimonialCarousel, FAQAccordion, Footer.
- **States**:
  - **Default**: Full marketing page rendered with animated hero, feature cards, pricing tiers.
  - **Loading**: Progressive skeleton — hero loads first, feature grid shimmer below.
  - **Empty**: N/A (static page).
  - **Error**: If CMS/pricing data fails to load, show fallback static content with "Refresh" button.
  - **Success**: N/A (no mutations on this page).

### Screen: `/login` — User Login
- **Route**: `/auth/login`
- **Auth Required**: No (redirect to `/dashboard` if already authenticated)
- **Key Components**: LoginForm (email + password fields), OAuthButtons (Google, GitHub), ForgotPasswordLink.
- **States**:
  - **Default**: Clean centered form with email/password inputs, OAuth divider, and submit button.
  - **Loading**: Submit button shows spinner, inputs disabled during API call.
  - **Empty**: N/A.
  - **Error**: Inline field errors (red border + helper text) for validation; toast alert for "Invalid credentials" or "Account locked."
  - **Success**: Redirect to `/dashboard` with welcome toast.

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

### Screen: `/settings/profile` — Profile Settings
- **Route**: `/settings/profile`
- **Auth Required**: Yes
- **Key Components**: AvatarUploader, ProfileForm (name, bio, email display), SaveButton, DangerZone (delete account).
- **States**:
  - **Default**: Pre-filled form with current user data, avatar preview.
  - **Loading**: Save button shows spinner during PATCH request.
  - **Empty**: N/A (always pre-filled from session).
  - **Error**: Inline validation errors on fields + toast for server errors.
  - **Success**: Toast "Profile updated successfully."

Continue for EVERY route in the application: `/settings/billing`, `/settings/team`, `/projects/[id]`, `/projects/[id]/edit`, `/admin`, etc.

**RULE**: List a minimum of 8-12 screens for a standard SaaS app. Every screen gets the full 5-state breakdown shown above. No abbreviated entries.
