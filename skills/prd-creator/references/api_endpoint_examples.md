# API Endpoint Examples Reference

This file contains the full example API endpoint specification for the PRD Creator skill. The agent loads this on demand when generating Section 7 of a PRD.

---

## Example: Exhaustive API Endpoint Table for a Standard SaaS Application

**RULE**: The API table must contain a **minimum of 15–25 endpoints** covering ALL CRUD operations for every entity in the database schema. Include auth endpoints, user endpoints, domain entity endpoints, billing endpoints, webhook endpoints, and admin endpoints.

| # | HTTP Method | Endpoint Route | Description | Auth | Request Payload | Response Payload |
| :--- | :--- | :--- | :--- | :---: | :--- | :--- |
| 1 | `POST` | `/api/v1/auth/register` | Register new user | No | `{ email, password, name }` | `{ user_id, message }` |
| 2 | `POST` | `/api/v1/auth/login` | Authenticate user | No | `{ email, password }` | `{ access_token, refresh_token, user }` |
| 3 | `POST` | `/api/v1/auth/logout` | Invalidate session | Yes | — | `{ message }` |
| 4 | `POST` | `/api/v1/auth/refresh` | Rotate refresh token | Yes (Refresh) | `{ refresh_token }` | `{ access_token, refresh_token }` |
| 5 | `POST` | `/api/v1/auth/forgot-password` | Send password reset email | No | `{ email }` | `{ message }` |
| 6 | `POST` | `/api/v1/auth/reset-password` | Reset password with token | No | `{ token, new_password }` | `{ message }` |
| 7 | `POST` | `/api/v1/auth/verify-otp` | Verify email OTP | No | `{ email, otp_code }` | `{ verified: true }` |
| 8 | `GET` | `/api/v1/users/me` | Get current user profile | Yes | — | `{ id, email, name, avatar_url, role }` |
| 9 | `PATCH` | `/api/v1/users/me` | Update profile | Yes | `{ name?, avatar_url?, bio? }` | `{ updated_user }` |
| 10 | `DELETE` | `/api/v1/users/me` | Delete account (soft) | Yes | `{ confirmation: "DELETE" }` | `{ message, grace_period_ends }` |
| 11 | `GET` | `/api/v1/projects` | List user projects | Yes | `?page=1&limit=20&sort=created_at` | `{ data: [...], total, page }` |
| 12 | `POST` | `/api/v1/projects` | Create new project | Yes | `{ title, description, tags[] }` | `{ id, title, created_at }` |
| 13 | `GET` | `/api/v1/projects/:id` | Get single project | Yes | — | `{ project }` |
| 14 | `PATCH` | `/api/v1/projects/:id` | Update project | Yes | `{ title?, description?, status? }` | `{ updated_project }` |
| 15 | `DELETE` | `/api/v1/projects/:id` | Delete project | Yes | — | `{ message }` |
| 16 | `GET` | `/api/v1/orgs` | List user organizations | Yes | — | `{ data: [...] }` |
| 17 | `POST` | `/api/v1/orgs` | Create organization | Yes | `{ name, slug }` | `{ id, name, slug }` |
| 18 | `POST` | `/api/v1/orgs/:id/invite` | Invite member | Yes (Admin) | `{ email, role }` | `{ invite_id, status }` |
| 19 | `DELETE` | `/api/v1/orgs/:id/members/:uid` | Remove member | Yes (Admin) | — | `{ message }` |
| 20 | `POST` | `/api/v1/billing/checkout` | Create Stripe checkout | Yes | `{ plan_id }` | `{ checkout_url }` |
| 21 | `POST` | `/api/v1/billing/portal` | Stripe customer portal | Yes | — | `{ portal_url }` |
| 22 | `GET` | `/api/v1/billing/invoices` | Invoice history | Yes | — | `{ invoices: [...] }` |
| 23 | `POST` | `/api/v1/webhooks/stripe` | Stripe webhook handler | Stripe Sig | Stripe Event Payload | `200 OK` |
| 24 | `GET` | `/api/v1/notifications` | List notifications | Yes | `?unread=true` | `{ data: [...], unread_count }` |
| 25 | `PATCH` | `/api/v1/notifications/:id/read` | Mark as read | Yes | — | `{ message }` |

Continue for ALL domain-specific endpoints. Do NOT stop at generic examples. Add endpoints for every entity defined in the database schema section.
