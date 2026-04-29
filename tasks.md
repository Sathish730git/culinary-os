## 1. Foundation: Extend Existing Module Schemas

- [ ] 1.1 Identify existing data models and implement additive schema changes for new fields (ingredients brand/branch, dish stage steps, chef note, side-dish accompaniments, festival menu mapping, tool category, publish authorization flags)
- [ ] 1.2 Update API request/response DTOs and validation rules for all enhanced modules
- [ ] 1.3 Extend media upload handling for stage-step videos and premium ingredient media (photos/videos)
- [ ] 1.4 Add server-side role/authorization helpers needed for Test Kitchen publishing control

## 2. Ingredients Enhancements

- [ ] 2.1 Enforce mandatory brand selection on ingredient create/update
- [ ] 2.2 Enforce mandatory branch mapping on ingredient create/update
- [ ] 2.3 Implement alternative ingredients (substitute) mapping UI/API and persistence
- [ ] 2.4 Implement premium imported ingredient tagging with associated brand metadata and media attachments
- [ ] 2.5 Add tests covering validation (missing brand/branch), alternatives, and premium media tagging

## 3. Dishes Enhancements

- [ ] 3.1 Add Stage Steps tab to dish authoring and persist ordered stage steps
- [ ] 3.2 Implement ingredient checklist for each stage step with checkbox completion state
- [ ] 3.3 Implement per-step video upload and ensure it is associated with the correct stage step
- [ ] 3.4 Implement per-stage-step “What can go wrong” guidance storage and rendering in overview
- [ ] 3.5 Implement Chef Note field and ensure it is displayed in dish overview
- [ ] 3.6 Set default portion value to `2` for newly created dishes
- [ ] 3.7 Update accompaniment handling so it is mapped/rendered as side dish with overview text: `Served with <name> as a side dish`
- [ ] 3.8 Add tests covering end-to-end dish enhancements (stages, checklist, videos, guidance, chef note, side dish mapping, default portion)

## 4. Tools Enhancements

- [ ] 4.1 Add tool category classification options: `cutlery`, `cooking tools`, `others`
- [ ] 4.2 Implement category selection persistence on tool create/edit
- [ ] 4.3 Implement tools filtering by category in the Tools module
- [ ] 4.4 Add tests for category persistence and filtering behavior

## 5. Dish Categories Enhancements

- [ ] 5.1 Add Festival Menu tab under Dish Categories and implement tab-level controls
- [ ] 5.2 Implement mapping between dishes and festival menu categories
- [ ] 5.3 Ensure switching between standard categories and Festival Menu preserves independent UI state (where applicable)
- [ ] 5.4 Add tests for festival menu tab navigation and dish mapping/unmapping

## 6. Dish Proposals: Publishing Workflow

- [ ] 6.1 Enforce publish restriction: only users with Test Kitchen role can publish after R&D completion
- [ ] 6.2 Record publish audit details (actor and timestamp) in existing History/audit workflow
- [ ] 6.3 Add tests for authorization gating and publish transition correctness

## 7. Integration, Migration, and Verification

- [ ] 7.1 Implement data migration/backfill strategy for existing records (defaults for required fields like portion, and safe handling for new mandatory fields)
- [ ] 7.2 Add end-to-end scenario tests covering: Ingredients -> Dishes stages -> accompaniment side dish -> Festival Menu mapping -> publishing workflow
- [ ] 7.3 Document updated API contracts and provide a concise rollout/rollback plan (feature flags or route gating if needed)
