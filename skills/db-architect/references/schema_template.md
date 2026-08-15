# 📄 Complete PostgreSQL Schema Template

This is a reference example demonstrating the extreme depth required when outputting Section 3, 4, and 5.

```sql
-- ENUMS
CREATE TYPE user_role AS ENUM ('member', 'admin', 'super_admin');
CREATE TYPE subscription_tier AS ENUM ('free', 'pro', 'enterprise');
CREATE TYPE task_status AS ENUM ('todo', 'in_progress', 'done');

-- 1. USERS TABLE
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  full_name VARCHAR(255) NOT NULL,
  avatar_url TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- 2. ORGANIZATIONS (MULTI-TENANCY)
CREATE TABLE organizations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  slug VARCHAR(255) UNIQUE NOT NULL,
  owner_id UUID NOT NULL REFERENCES users(id) ON DELETE RESTRICT,
  tier subscription_tier DEFAULT 'free',
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- 3. MEMBERSHIPS (MANY-TO-MANY)
CREATE TABLE memberships (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  org_id UUID NOT NULL REFERENCES organizations(id) ON DELETE CASCADE,
  role user_role DEFAULT 'member',
  joined_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  UNIQUE(user_id, org_id)
);

-- 4. TASKS (CORE DOMAIN ENTITY)
CREATE TABLE tasks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  org_id UUID NOT NULL REFERENCES organizations(id) ON DELETE CASCADE,
  created_by UUID NOT NULL REFERENCES users(id) ON DELETE SET NULL,
  assigned_to UUID REFERENCES users(id) ON DELETE SET NULL,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  status task_status DEFAULT 'todo',
  due_date TIMESTAMP WITH TIME ZONE,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- ROW LEVEL SECURITY (RLS)
ALTER TABLE users ENABLE ROW LEVEL SECURITY;
ALTER TABLE organizations ENABLE ROW LEVEL SECURITY;
ALTER TABLE memberships ENABLE ROW LEVEL SECURITY;
ALTER TABLE tasks ENABLE ROW LEVEL SECURITY;

-- POLICIES
-- Users can read their own profile
CREATE POLICY "Users can view own profile" 
ON users FOR SELECT USING (auth.uid() = id);

-- Users can read orgs they belong to
CREATE POLICY "Users can view own orgs" 
ON organizations FOR SELECT USING (
  EXISTS (SELECT 1 FROM memberships WHERE user_id = auth.uid() AND org_id = organizations.id)
);

-- Users can read tasks in their org
CREATE POLICY "Users can view org tasks" 
ON tasks FOR SELECT USING (
  EXISTS (SELECT 1 FROM memberships WHERE user_id = auth.uid() AND org_id = tasks.org_id)
);

-- Users can insert tasks in their org
CREATE POLICY "Users can insert org tasks" 
ON tasks FOR INSERT WITH CHECK (
  EXISTS (SELECT 1 FROM memberships WHERE user_id = auth.uid() AND org_id = tasks.org_id)
);

-- INDEXES
CREATE INDEX idx_memberships_user_id ON memberships(user_id);
CREATE INDEX idx_memberships_org_id ON memberships(org_id);
CREATE INDEX idx_tasks_org_id ON tasks(org_id);
CREATE INDEX idx_tasks_assigned_to ON tasks(assigned_to);
CREATE INDEX idx_tasks_status ON tasks(status);
```
