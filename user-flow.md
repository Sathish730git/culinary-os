# User Flows: Culinary OS Enhancements

## 1) Dish Creation Flow

### Goal
Create a new dish in the existing Dishes module with required defaults and mappings.

### Actors
- Content Creator / Chef

### Preconditions
- User has access to `Dishes` module.
- Required master data is available (ingredients, tools, categories).

### Flow
1. User opens `Dishes` and clicks **Create Dish**.
2. User enters core dish information (name, category, summary, etc.).
3. System initializes `Default Portion = 2`.
4. User selects ingredients for the dish.
5. User maps accompaniment as a **side dish**.
6. User adds optional Chef Note (or later in Stage Steps flow).
7. User saves dish draft.
8. System validates required fields and stores the dish.
9. Dish overview displays side-dish text as: `Served with <name> as a side dish`.

### Alternate / Validation Paths
- If required core fields are missing, system blocks save and highlights validation errors.
- If accompaniment is not mapped correctly as side dish, system blocks save and requests valid mapping.

### Outcome
- Dish draft is created successfully and is available for stage-level authoring and proposal workflow.

---

## 2) Stage Steps Flow

### Goal
Add structured stage-wise preparation details to a dish.

### Actors
- Content Creator / Chef

### Preconditions
- Dish record already exists (draft or editable state).

### Flow
1. User opens an existing dish and navigates to **Stage Steps** tab.
2. User adds ordered stage steps (Step 1, Step 2, ...).
3. For each stage step, user:
   - adds ingredient checklist items,
   - marks checklist items using checkboxes,
   - uploads a video for that step,
   - enters **What can go wrong** guidance.
4. User updates/adds **Chef Note** for the dish.
5. User saves changes.
6. System persists stage order, checklist state, media links, and failure guidance.
7. Dish overview reflects:
   - Chef Note,
   - per-step “What can go wrong” content.

### Alternate / Validation Paths
- If video upload fails, system shows upload error and allows retry without losing step draft data.
- If stage data is partially complete, system allows draft save and flags incomplete items for final review.

### Outcome
- Dish includes complete stage-wise preparation data and is ready for R&D/proposal progression.

---

## 3) Publishing Workflow Flow

### Goal
Publish a dish proposal using controlled authorization in the existing Dish Proposals lifecycle.

### Actors
- Content Creator / Chef
- Test Kitchen

### Preconditions
- Dish proposal exists in `Dish Proposals`.
- Proposal has progressed through R&D stages.

### Flow
1. Content Creator advances proposal through existing R&D statuses.
2. When R&D is complete, proposal enters publish-ready state.
3. User attempts **Publish** action.
4. System validates:
   - user role is `Test Kitchen`,
   - R&D status is complete.
5. If validation passes, system publishes the dish.
6. System records publish audit trail (actor, timestamp) in existing `History` workflow.

### Alternate / Validation Paths
- Non-Test Kitchen user attempts publish:
  - system denies action with authorization message.
- Test Kitchen user attempts publish before R&D completion:
  - system denies action with status precondition message.

### Outcome
- Only authorized Test Kitchen users can publish completed proposals, with full auditability.

