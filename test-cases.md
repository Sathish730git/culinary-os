# Test Cases: Culinary OS Enhancement (Existing Modules)

## Ingredients Module

### TC-ING-001: Update legacy ingredient without validation failure
**Scenario:** Editing an ingredient created before the enhancement should remain functional.  
**Steps:**
1. Open an existing legacy ingredient record.
2. Modify a non-mandatory field (e.g., name/notes).
3. Save changes.
**Expected result:**
- The ingredient saves successfully.
- No migration/validation errors occur.

### TC-ING-002: Save ingredient without branch mapping (validation)
**Scenario:** Brand may be selected but Branch is mandatory.  
**Steps:**
1. Open Ingredients -> Create (or Edit).
2. Select a Brand.
3. Leave Branch mapping empty.
4. Click Save.
**Expected result:**
- Save is blocked.
- The system prompts for Branch selection.

### TC-ING-003: Save ingredient without brand selection (validation)
**Scenario:** Branch may be selected but Brand is mandatory.  
**Steps:**
1. Open Ingredients -> Create (or Edit).
2. Select a Branch.
3. Leave Brand selection empty.
4. Click Save.
**Expected result:**
- Save is blocked.
- The system prompts for Brand selection.

### TC-ING-004: Add substitute (alternative ingredient) mapping
**Scenario:** Alternatives can be defined for a primary ingredient.  
**Steps:**
1. Open Ingredients -> Edit a primary ingredient.
2. Add an alternative ingredient mapping (substitute).
3. Save.
4. Re-open the ingredient.
**Expected result:**
- The alternative mapping is persisted.
- The substitute mapping is returned/displayed when reopening.

### TC-ING-005: View premium imported ingredient details (media + brand)
**Scenario:** Premium/imported tagging shows metadata and media.  
**Steps:**
1. Open a premium/imported ingredient record.
2. Navigate to its media/details section.
**Expected result:**
- The record displays imported/premium status.
- Brand metadata is shown.
- Photos/videos are displayed as attached media.

## Dishes Module

### TC-DIS-001: Edit an existing dish remains compatible
**Scenario:** Existing dish records must remain editable after enhancements.  
**Steps:**
1. Open a dish created before the enhancement.
2. Edit basic fields (e.g., title/description).
3. Save.
**Expected result:**
- The dish saves without breaking existing data.

### TC-DIS-002: Stage Steps tab shows and persists ordered stages
**Scenario:** Dish supports Stage Steps tab with ordered stage steps.  
**Steps:**
1. Open an existing/new dish in edit mode.
2. Navigate to **Stage Steps** tab.
3. Add Stage Step A, then Stage Step B (in that order).
4. Save dish.
5. Re-open the dish and navigate back to Stage Steps.
**Expected result:**
- Stage steps are displayed in the same order (A then B).
- Saved data persists across reopen.

### TC-DIS-003: Stage step ingredient checklist checkboxes persist completion
**Scenario:** Checklist items are represented as checkboxes and completion persists.  
**Steps:**
1. In Stage Steps tab, open/edit Stage Step 1.
2. Ensure checklist items are present.
3. Check one or more checklist items.
4. Save.
5. Re-open the dish and return to Stage Step 1.
**Expected result:**
- Checklist items show the same completion state after reopen.

### TC-DIS-004: Upload per-step video and ensure association with correct stage step
**Scenario:** Video upload is associated to the specific stage step.  
**Steps:**
1. In Stage Steps tab, open/edit Stage Step 1.
2. Upload a video for Stage Step 1.
3. Open/edit Stage Step 2.
4. Upload a different video for Stage Step 2 (or leave Stage Step 2 without video).
5. Save.
6. Return to each stage step and verify videos.
**Expected result:**
- Stage Step 1 shows only its uploaded video.
- Stage Step 2 shows only its uploaded video (or shows none if left empty).

### TC-DIS-005: “What can go wrong” guidance per stage step is visible in overview
**Scenario:** Failure guidance is stored per stage step and displayed in dish overview.  
**Steps:**
1. Add “What can go wrong” content in Stage Step 1.
2. Save.
3. Open dish overview (view mode).
**Expected result:**
- Overview displays the “what can go wrong” content for Stage Step 1.

### TC-DIS-006: Chef Note is displayed in dish overview
**Scenario:** Chef Note field is persisted and visible in overview.  
**Steps:**
1. Enter a Chef Note for a dish.
2. Save.
3. Open dish overview.
**Expected result:**
- Overview shows the exact Chef Note text.

### TC-DIS-007: Accompaniment mapping renders as side dish in overview
**Scenario:** Accompaniments must be mapped as side dishes and rendered with required text.  
**Steps:**
1. Edit a dish.
2. Map an accompaniment as a side dish.
3. Save.
4. Open dish overview.
**Expected result:**
- Overview includes the text: `Served with <name> as a side dish`.

### TC-DIS-008: Default portion is 2 for newly created dishes
**Scenario:** Portion defaults to 2 when not explicitly set.  
**Steps:**
1. Create a new dish.
2. Do not modify the portion field.
3. Save dish.
**Expected result:**
- Saved dish shows portion value `2`.

## Tools Module

### TC-TOOL-001: Access/edit an existing tool (backward compatibility)
**Scenario:** Tools created before enhancements remain editable.  
**Steps:**
1. Open an existing pre-enhancement tool record.
2. Edit a field (unrelated to category).
3. Save.
**Expected result:**
- Tool saves successfully.
- No data loss occurs.

### TC-TOOL-002: Assign category while creating a tool
**Scenario:** Category values include cutlery/cooking tools/others.  
**Steps:**
1. Create a new tool.
2. Select category `cutlery`.
3. Save.
4. Re-open tool record.
**Expected result:**
- Tool record shows category `cutlery`.

### TC-TOOL-003: Filter tools list by category
**Scenario:** Tools can be filtered by category.  
**Steps:**
1. Open Tools module.
2. Select filter `cooking tools`.
**Expected result:**
- Only tools assigned to `cooking tools` are displayed.

## Dish Categories Module

### TC-CAT-001: Open Festival Menu tab
**Scenario:** Festival Menu tab exists and loads festival controls.  
**Steps:**
1. Navigate to Dish Categories.
2. Select the **Festival Menu** tab.
**Expected result:**
- Festival Menu tab loads festival category management controls.

### TC-CAT-002: Switching tabs preserves independent UI state
**Scenario:** Standard vs Festival tabs maintain independent state.  
**Steps:**
1. On Dish Categories, set a standard tab filter/selection (if applicable).
2. Switch to Festival Menu tab.
3. Set a Festival tab filter/selection (if applicable).
4. Switch back to standard categories tab.
5. Switch back to Festival Menu tab.
**Expected result:**
- Standard tab state remains unchanged when returning.
- Festival tab state remains unchanged when returning.

### TC-CAT-003: Map a dish to a festival category
**Scenario:** Dishes can be mapped under festival groupings.  
**Steps:**
1. Open Dish Categories -> Festival Menu.
2. Select a festival category.
3. Map/associate a dish to that festival category.
4. View the festival grouping listing.
**Expected result:**
- The dish appears under that festival grouping.

### TC-CAT-004: Remove dish from festival category
**Scenario:** Unmapping should immediately reflect in festival grouping.  
**Steps:**
1. In Festival Menu, remove/unmap an existing dish from a festival category.
2. Refresh/re-open the festival grouping view.
**Expected result:**
- The dish no longer appears in that festival grouping.

## Dish Proposals Publishing Workflow

### TC-PROP-001: R&D progression history remains intact
**Scenario:** Existing proposal progression through R&D stages records history transitions.  
**Steps:**
1. Open a dish proposal.
2. Move the proposal status through existing R&D stages.
3. Navigate to History/audit view.
**Expected result:**
- History includes status transitions recorded as per existing behavior.

### TC-PROP-002: Non-Test Kitchen user cannot publish
**Scenario:** Authorization gating for publishing is enforced.  
**Steps:**
1. Log in as a user without Test Kitchen role.
2. Open a dish proposal with R&D status complete (or publish-ready state).
3. Attempt to click Publish.
**Expected result:**
- Publish action is blocked.
- User receives authorization feedback/message.

### TC-PROP-003: Test Kitchen user can publish only after R&D completion
**Scenario:** Publishing is allowed only when R&D is complete and user is Test Kitchen.  
**Steps:**
1. Log in as a Test Kitchen user.
2. Open a dish proposal with R&D status complete.
3. Click Publish.
4. Verify dish/proposal status becomes published.
5. Check History/audit view for publish audit details.
**Expected result:**
- Proposal is published successfully.
- History contains publish audit details (actor and timestamp).

