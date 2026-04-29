# BRD: Culinary OS Enhancement + Organization & Access Control

## 1. Existing System Overview

The Culinary OS application is already live and provides a set of modules to manage culinary content and publishing workflows.

### Dashboard
- Shows counts for: Brands, Branches, Users, Dishes, Ingredients, and Tools.

### Current available modules
- `Dishes`
- `Feedback`
- `Dish Categories`
- `Ingredients`
- `Tools`
- `Media Library`
- `Dish Proposals`
- `History`

### Current behavior (baseline limitations)
- `Dishes` can be created, but cooking guidance is not represented as structured stage steps.
- `Ingredients` exist but are not fully structured (brand/branch linkage is incomplete).
- Accompaniments are not strictly enforced as side dishes.
- `Tools` are not categorized (e.g., cutlery vs other tools).
- `Dish Categories` do not support festival-based classification.
- Chef notes and “what can go wrong” guidance are not clearly visible in the dish overview.
- Publishing exists via `Dish Proposals`, but controlled publishing (Test Kitchen role gating after R&D completion) is not enforced.

## 2. Goals of this BRD

Provide a production-ready definition of product requirements to:
1. Enhance existing culinary modules (Dishes, Ingredients, Tools, Dish Categories, Dish Proposals).
2. Add a new **Organization & Access Control** capability for hierarchy, RBAC, branch-scoped visibility, and login-time alerts.

## 3. Scope

### In scope

#### 3.1 Enhancements to existing modules
1. **Ingredients module**
   - Mandatory Brand selection
   - Mandatory Branch mapping (ingredient belongs to a branch)
   - Alternative ingredients (substitutes)
   - Premium imported tagging with media (photos/videos)

2. **Dishes module**
   - Add **Stage Steps** tab (stage-wise checklist, per-step video, per-step failure guidance)
   - Ingredient checklist with checkbox completion
   - Video upload per step
   - “What can go wrong” per stage step
   - Chef Note surfaced in dish overview
   - Default portion value = `2`
   - Accompaniments mapped and displayed as side dishes: `Served with <name> as a side dish`

3. **Tools module**
   - Category classification: `cutlery`, `cooking tools`, `others`
   - Persist and filter by category

4. **Dish Categories module**
   - Add **Festival Menu** tab
   - Map/unmap dishes to festival menu categories

5. **Dish Proposals module (publishing workflow)**
   - Publish allowed only for **Test Kitchen**
   - Publish allowed only after **R&D completion**
   - Publish audit trail recorded in `History`

#### 3.2 Organization & Access Control (new module)
Define organizational hierarchy and enforce access rules across modules:
- Hierarchy: Company → Brand → Branch → Profile → Role → User
- Profiles: Kitchen, Service, Culinary Leadership, Operations
- Role mapping and permissions (RBAC)
- Profile-based module visibility
- Branch-level data restriction (users can access only their assigned branch data)
- Token-based login with unread feedback and alerts at login

### Out of scope (explicitly not introduced)
- Grocery list generation
- Pantry inventory management
- Meal planning calendar systems
- Guided-cooking execution subsystems
- Unrelated domains outside Culinary OS and access control

## 4. Functional Requirements

### 4.1 Ingredients (existing module)
1. **Mandatory Brand**
   - Ingredient create/update MUST require Brand.
2. **Mandatory Branch**
   - Ingredient create/update MUST require Branch mapping.
3. **Alternative ingredients**
   - Support substitutes/alternative ingredients mapping for a primary ingredient.
4. **Premium imported tagging**
   - Support premium/imported tagging with associated brand and media attachments (photos/videos).

### 4.2 Dishes (existing module)
1. **Stage Steps tab**
   - Add a Stage Steps tab to dish authoring.
   - Store stage steps in ordered sequence.
2. **Ingredient checklist with checkboxes**
   - Each stage step includes ingredient checklist items.
   - Each checklist item MUST be represented as a checkbox with completion tracking.
3. **Video upload per step**
   - Each stage step supports uploading a video.
   - Video MUST be associated with the correct stage step.
4. **“What can go wrong” per step**
   - Each stage step includes failure guidance (“what can go wrong”).
   - Dish overview MUST display the failure guidance.
5. **Chef Note in overview**
   - Dish includes a Chef Note field.
   - Dish overview MUST display the Chef Note.
6. **Default portion**
   - Newly created dishes default portion MUST be `2`.
7. **Accompaniment mapping as side dish**
   - Accompaniments MUST be mapped as side dishes.
   - Overview MUST render: `Served with <name> as a side dish`.

### 4.3 Tools (existing module)
1. **Tool categories**
   - Tool create/edit MUST support categories: `cutlery`, `cooking tools`, `others`.
2. **Persist category**
   - Selected category MUST be saved with tool records.
3. **Filtering**
   - Tools list supports filtering by category.

### 4.4 Dish Categories (existing module)
1. **Festival Menu tab**
   - Add a Festival Menu tab within Dish Categories.
2. **Dishes mapping**
   - Map/unmap dishes to festival menu categories.
3. **Unmapping**
   - Unmapped dishes MUST no longer appear in the festival grouping.

### 4.5 Dish Proposals (existing module)
1. **Test Kitchen-only publishing**
   - Publishing is allowed only for users with Test Kitchen role.
2. **R&D completion gate**
   - Publishing is allowed only after R&D status is complete.
3. **Audit trail**
   - Publish MUST record actor and timestamp in `History`.

### 4.6 Organization & Access Control (new module)
1. **Hierarchy & inheritance**
   - Company → Brand → Branch → Profile → Role → User.
   - User’s effective Branch scope is derived from Role → Profile → Branch path.
2. **Profiles (module visibility)**
   - Profile type determines which modules are visible and which actions are permitted.
3. **RBAC (role-based actions)**
   - Protected actions require the appropriate permission granted by the user’s Role.
   - Protected actions include at minimum: create, read, update, delete, approve, and (where applicable) publish.
4. **Branch-level data restriction**
   - Users can access only data belonging to their effective Branch scope.
   - Cross-branch access must be denied without disclosing record existence.
5. **Login-time behavior**
   - Login uses secure token-based authentication.
   - After login, system shows unread feedback and access-related alerts based on Profile/Role/Branch state.

## 5. User Roles, Profiles, and Permissions

### 5.1 Profile types
- **Kitchen**: execution-focused authoring within dish-related workflows
- **Service**: limited visibility and actions
- **Culinary Leadership**: higher authoring control (e.g., full recipe/dish control)
- **Operations**: monitoring/control capability

### 5.2 Role mapping (RBAC)

| Role | Profile | Role intent | Key permissions (high level) |
|---|---|---|---|
| Waiter | Service | Limited visibility | Read access; no create/edit stages; no approvals/publishing |
| Chef | Kitchen | Execution rights | Create/edit dish stage content within branch scope |
| Master Chef | Culinary Leadership | Full dish control | Read & modify dishes/recipe content within branch scope; publish eligibility if gated by R&D |
| Director | Operations | Monitoring and control | Read + monitoring; approve/control where explicitly permitted |
| System Admin | (All) | Full access | All modules and protected actions across applicable scope |

## 6. Workflows

### 6.1 Login workflow (token-based + alerts)
1. User authenticates using a token.
2. System determines Profile/Role and effective Branch scope.
3. System loads:
   - Unread feedback/notifications the user can see
   - Access-related alerts (e.g., missing effective permissions, invalid/inactive branch linkage)
4. UI navigation and accessible API endpoints are filtered accordingly.

### 6.2 Ingredients setup workflow
1. User opens Ingredients create/edit.
2. Selects mandatory Brand and mandatory Branch mapping.
3. Optionally adds alternative ingredients.
4. Optionally tags as premium/imported and attaches media.
5. Save validates required fields and persists.

### 6.3 Dish creation workflow (with stage steps)
1. User creates/edits a dish.
2. User sets Chef Note.
3. User adds stage steps in Stage Steps tab (ordered).
4. For each stage step:
   - marks ingredient checklist items using checkboxes
   - uploads a stage video
   - enters “what can go wrong” guidance
5. User maps accompaniments as side dishes.
6. Dish overview displays:
   - Chef Note
   - stage-level “what can go wrong”
   - `Served with <name> as a side dish`
7. Default portion remains `2` for new dishes unless changed.

### 6.4 Festival Menu workflow (Dish Categories)
1. User navigates to Dish Categories.
2. Opens Festival Menu tab.
3. Maps/unmaps dishes to festival categories.
4. UI reflects dish placement instantly.

### 6.5 Publishing workflow (Test Kitchen + R&D gate)
1. Content progresses dish proposal through R&D stages.
2. When R&D is complete, publish becomes available (subject to RBAC).
3. Only Test Kitchen can publish.
4. System records publish actor and timestamp in `History`.

### 6.6 Organization & Access Control workflow (setup/administration)
1. Admin creates Company → Brand → Branch.
2. Admin creates Profile under a Branch.
3. Admin creates Role under a Profile (permission set).
4. Admin assigns User to Role (effective Branch scope derived).

## 7. UI Expectations

### 7.1 Ingredients UI
- Ingredient form includes required fields:
  - Brand (mandatory)
  - Branch mapping (mandatory)
- Alternative ingredients section for substitutes.
- Premium/imported tagging with media attachments (photos/videos).

### 7.2 Dishes UI
- Stage Steps tab is visible in dish authoring.
- Stage Steps supports:
  - ordered stage steps
  - ingredient checklist with checkbox controls
  - per-step video upload
  - “What can go wrong” per stage step
- Dish overview shows:
  - Chef Note
  - per-step failure guidance
  - side dish text: `Served with <name> as a side dish`
- New dishes show default portion value `2`.

### 7.3 Tools UI
- Tool create/edit includes category selection:
  - `cutlery`, `cooking tools`, `others`
- Tools list includes category filter.

### 7.4 Dish Categories UI
- Festival Menu tab available under Dish Categories.
- Map/unmap dishes from festival groupings.

### 7.5 Dish Proposals UI
- Publish action visibility/enabling follows:
  - Test Kitchen role
  - R&D completion state
- Publish triggers audit recording in History.

### 7.6 Organization & Access Control UI
- Admin screens for Company/Brand/Branch/Profile/Role/User management.
- Users see only modules/actions permitted by Profile/Role.
- Users receive login-time alerts for unread feedback and access state.

