# DB Architect

Act as a Principal Database Architect. This skill takes any app idea or PRD and designs an exhaustive, production-ready PostgreSQL database schema.

## Features
- Defaults to PostgreSQL (Supabase-flavored).
- Enforces `UUID` primary keys and `created_at`/`updated_at` timestamps.
- Generates comprehensive `CREATE TABLE` and `CREATE INDEX` statements.
- Writes strict Row Level Security (RLS) policies for multi-tenant isolation.
- Automatically generates a visual Mermaid.js ER diagram.

## How to use

1. Ensure the skill is installed in your project.
2. Ask your AI tool:
   > "Design a database for a B2B SaaS habit tracking app"
3. The AI will output a massive `schema_[name].md` file containing the complete SQL architecture.
