## Context

This change is an enhancement of the existing Culinary OS application. The system already contains operational modules for Dishes, Ingredients, Tools, Dish Categories, Dish Proposals, and History. The design focus is to extend these current modules with additional behaviors from the proposal while keeping existing workflows intact.

Primary constraints are: (1) preserve backward compatibility for current records and UI flows, (2) extend existing module schemas without introducing unrelated new domains, and (3) keep authorization and audit behavior consistent with existing Dish Proposals and History flows.

## Goals / Non-Goals

**Goals:**
- Extend the Dishes module with stage steps, checklist/video support, accompaniment enforcement, failure guidance, chef note visibility, and default portion value.
- Extend the Ingredients module with brand selection, mandatory branch mapping, substitutes, and premium ingredient media metadata.
- Extend the Tools module with category classification and category-based filtering.
- Extend Dish Categories with festival-menu organization and dish-to-festival mapping.
- Extend Dish Proposals publishing flow with Test Kitchen-only publish control after R&D completion.

**Non-Goals:**
- Creating new standalone domains such as grocery, pantry, meal planning, or guided-cooking systems.
- Replacing existing module architecture or rewriting established CRUD workflows.
- Introducing unrelated features (AI generation, social features, marketplace integrations).

## Decisions

1. Extend existing module boundaries, do not add unrelated domains
   - Decision: keep enhancement work inside current modules only: Dishes, Ingredients, Tools, Dish Categories, and Dish Proposals.
   - Rationale: aligns with current application architecture and avoids unnecessary domain sprawl.
   - Alternative considered: introduce additional workflow modules; rejected because proposal scope is enhancement of existing application behavior.

2. Incremental schema extension for existing entities
   - Decision: extend existing entity structures with additive fields (for example, ingredient branch mapping, tool category, dish stage metadata) while preserving legacy compatibility.
   - Rationale: enables rollout with minimal migration risk and no disruption to existing records.
   - Alternative considered: hard schema replacement; rejected due to high regression risk.

3. Workflow-first extension inside Dishes module
   - Decision: add stage-step workflow, checklist support, and stage media upload to existing dish authoring flow instead of introducing a separate execution module.
   - Rationale: keeps authoring and preparation context in one module and reuses current dish lifecycle.
   - Alternative considered: independent guided execution subsystem; rejected as outside requested module scope.

4. Role-based publish control in existing proposal lifecycle
   - Decision: enforce Test Kitchen role and R&D completion checks at publish transition point in Dish Proposals.
   - Rationale: introduces controlled publishing without changing existing proposal stages or history tracking model.
   - Alternative considered: create a new publish pipeline service; rejected to avoid duplicating existing lifecycle ownership.

## Risks / Trade-offs

- [Legacy data compatibility] -> Mitigation: use additive schema changes and default values to keep old records valid.
- [UI complexity from added dish-stage fields] -> Mitigation: gate new fields behind clear sections and retain existing defaults.
- [Role misconfiguration for publishing] -> Mitigation: enforce server-side role checks with explicit authorization feedback and audit logs.
- [Scope creep into unrelated domains] -> Mitigation: constrain implementation strictly to existing modules listed in proposal.

## Migration Plan

1. Add required fields and validations incrementally to existing module models and APIs.
2. Release enhancements module-by-module: Ingredients and Tools updates first, then Dishes and Dish Categories UX updates, then Dish Proposals publish control.
3. Validate existing records against new constraints using fallback defaults where required (for example, default portion value).
4. Rollback strategy: disable new validation/feature flags while preserving pre-existing module behavior.

## Open Questions

- Should branch mapping be mandatory for all legacy ingredients immediately, or phased in on edit/update?
- Are tool categories centrally managed (admin-defined) or free-form with validation?
- Should Test Kitchen publish restriction include optional second-level approval in later phases?
