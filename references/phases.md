# ZAIA Phases & Quality Gates

This reference describes the six operational phases (0-5), their procedures, and the quality gates between them.

## Table of Contents

1. [Phase 0: Initiative Qualification](#phase-0-initiative-qualification)
2. [Phase 1: Discovery](#phase-1-discovery)
3. [Phase 2: Target Analysis](#phase-2-target-analysis)
4. [Phase 3: Specification & Validation](#phase-3-specification--validation)
5. [Phase 4: Implementation Support](#phase-4-implementation-support)
6. [Phase 5: Organizational Learning](#phase-5-organizational-learning)
7. [Quality Gates Summary](#quality-gates-summary)

---

## Phase 0: Initiative Qualification

**Purpose**: Classify the change, assess complexity, and determine the analytical pathway before investing effort in deep analysis.

**Entry criteria**: A change request, project proposal, or business need has been identified.

**Activities**:

1. **Classify the change type**: Is this a new capability, process improvement, system integration, regulatory compliance, or something else?
2. **Assess complexity**: Low (single process, known domain), Medium (cross-process, partial unknowns), High (cross-domain, significant uncertainty)
3. **Identify sponsors and stakeholders**: Who requested this? Who will be affected? Who must approve?
4. **Determine uncertainty level**: What do we know? What don't we know? Where are the biggest risks?
5. **Select analytical pathway**: Based on complexity and uncertainty, decide which phases to emphasize and which artifacts are mandatory vs. optional
6. **Create initiative card**: Summarize the above in a structured document

**Artifacts to produce**:
- `initiative-card.md` — Change type, complexity, sponsors, stakeholders, uncertainty assessment, proposed analytical pathway
- `qualification-assessment.md` — Detailed assessment with rationale for the chosen approach

**Initiative card template**:
```markdown
# Initiative Card: <Name>

**Date:** <date>
**Sponsor:** <name, role>
**Analyst:** <name>

## Change Classification
- **Type:** <New capability | Process improvement | System integration | Regulatory compliance | Other>
- **Complexity:** <Low | Medium | High>
- **Uncertainty:** <Low | Medium | High>

## Objectives
1. <objective>

## Scope
- **In scope:** <what's included>
- **Out of scope:** <what's explicitly excluded>
- **Assumptions:** <key assumptions>

## Stakeholders
| Name | Role | Interest | Influence | Engagement Level |
|------|------|----------|-----------|-----------------|

## Analytical Pathway
- **Mandatory phases:** <which phases>
- **Mandatory artifacts:** <which artifacts>
- **Estimated effort:** <rough estimate>

## Key Risks
1. <risk>
```

### Quality Gate 1
- [ ] Initiative classified (type + complexity + uncertainty)
- [ ] Objectives defined and approved by sponsor
- [ ] Scope boundaries set (in/out/assumptions)
- [ ] Key stakeholders identified with roles
- [ ] Analytical pathway selected

**Present this checklist to the analyst. All items must be confirmed before proceeding to Phase 1.**

---

## Phase 1: Discovery

**Purpose**: Process source materials, extract structured information, identify gaps, and build an understanding of the current state (AS-IS).

**Entry criteria**: Gate 1 passed. Initiative card exists.

**Activities**:

1. **Process source materials**: Read all provided documents, transcripts, meeting notes. Extract key information using the Discovery Agent role.
2. **Build stakeholder map**: Identify all actors, their roles, responsibilities, influence levels, and interests. Visualize as Mermaid diagram.
3. **Model AS-IS processes**: For each major process in scope, create BPMN and Mermaid models showing current state. Include happy path, exception paths, and decision points.
4. **Extract business rules**: Identify conditions, constraints, and rules embedded in current processes.
5. **Identify information gaps**: What's missing? What needs validation? What are the hypotheses?
6. **Search for related analyses**: Check if similar initiatives have been analyzed before (ask the analyst about prior work).

**Artifacts to produce**:
- `stakeholder-map.md`
- `as-is-process.bpmn` + `as-is-process.md` (for each major process)
- `discovery-findings.md`
- `information-gaps.md`
- `hypothesis-log.md` (if hypotheses exist)

**Working approach**: Process sources incrementally. After each source, present findings to the analyst and ask if the interpretation is correct. This catches misunderstandings early.

### Quality Gate 2
- [ ] All provided source materials processed
- [ ] AS-IS state described (processes, actors, rules)
- [ ] Stakeholder map complete
- [ ] Information gaps identified and documented
- [ ] Hypotheses formulated for unknowns
- [ ] Analyst has validated discovery findings

---

## Phase 2: Target Analysis

**Purpose**: Design the target state (TO-BE), explore solution variants, decompose capabilities, and model the target domain and integrations.

**Entry criteria**: Gate 2 passed. AS-IS understanding exists.

**Activities**:

1. **Generate TO-BE process models**: Design target state processes based on objectives and constraints. Show how the process will work after the change.
2. **Capability decomposition**: Break down the target solution into logical capabilities/components. Show hierarchy and dependencies.
3. **Variant analysis**: If multiple solution approaches exist, document each variant with pros/cons/risks/effort. Help the analyst compare, but let them decide.
4. **Domain modeling**: Create entity-relationship model for the target domain. Define entities, attributes, relationships.
5. **Integration catalog**: Map all system integrations needed for the target state. Document interfaces, protocols, data flows.
6. **Delta analysis**: Compare AS-IS vs TO-BE — what changes, what stays, what's new, what's removed.

**Artifacts to produce**:
- `to-be-process.bpmn` + `to-be-process.md`
- `capability-decomposition.md` (Mermaid mindmap or hierarchy)
- `variant-analysis.md` (if multiple approaches)
- `domain-model.md` (Mermaid ERD)
- `integration-catalog.md`
- `delta-analysis.md`

**Iterative validation**: Present each TO-BE model to the analyst for feedback before finalizing. Target analysis is the most creative phase — expect multiple revision cycles.

### Quality Gate 3
- [ ] TO-BE process model is coherent and complete
- [ ] Capability decomposition covers all objectives
- [ ] Solution variants evaluated (if applicable)
- [ ] Domain model defined with key entities
- [ ] Integration points identified
- [ ] Delta from AS-IS clearly documented
- [ ] Analyst has approved the target direction

---

## Phase 3: Specification & Validation

**Purpose**: Formalize requirements, develop acceptance criteria, build NFR catalog, and ensure traceability from business need to testable requirement.

**Entry criteria**: Gate 3 passed. Approved TO-BE design exists.

**Activities**:

1. **Structure requirements**: Organize into Business → Functional → System levels. Each requirement gets an ID, description, rationale, priority, and source reference.
2. **Write user stories**: Convert functional requirements into GWT-format stories with acceptance criteria.
3. **Define business rules**: Formalize all business rules as structured conditions.
4. **Build NFR catalog**: Generate non-functional requirements with measurable criteria.
5. **Create glossary**: Compile all business terms with precise definitions.
6. **Build traceability matrix**: Map: business need → requirement → user story → acceptance criterion.
7. **Cross-validation**: Use the Artifact Quality Agent role to verify consistency across all artifacts.
8. **Architectural review**: Check that requirements are technically feasible and don't conflict with architectural constraints.
9. **Security review**: Identify security implications and ensure appropriate controls are specified.

**Artifacts to produce**:
- `requirements/business-requirements.md`
- `requirements/functional-requirements.md`
- `requirements/system-requirements.md`
- `requirements/nfr-catalog.md`
- `user-stories.md` (or in `requirements/`)
- `business-rules.md`
- `glossary.md`
- `acceptance-criteria.md`
- `traceability-matrix.md`
- `quality-report.md` (from cross-validation)

### Quality Gate 4
- [ ] All requirements structured with IDs, descriptions, priorities
- [ ] Traceability built: need → requirement → story → test
- [ ] ≥95% user stories have acceptance criteria
- [ ] NFR catalog complete with measurable criteria
- [ ] Glossary covers all domain terms
- [ ] Cross-artifact consistency validated
- [ ] No unresolved contradictions between requirements
- [ ] Analyst has approved the specification

---

## Phase 4: Implementation Support

**Purpose**: Support the development team during implementation — clarify requirements, analyze change requests, and validate that implementation matches intent.

**Entry criteria**: Gate 4 passed. Approved specification exists.

**Activities**:

1. **Transform to backlog**: Use the Backlog Agent role to decompose requirements into Epics → Features → User Stories with dependencies.
2. **Prepare refinement packages**: Bundle stories with context, acceptance criteria, relevant process models, and domain definitions — everything the team needs for sprint refinement.
3. **Clarify during sprints**: When the team has questions, trace back to source requirements and provide precise answers with context.
4. **Analyze change requests**: When new requirements or scope changes emerge, assess impact on existing artifacts and recommend adjustments.
5. **Validate implementation**: Compare delivered functionality against requirements and acceptance criteria.

**Artifacts to produce**:
- `backlog/epics.md`
- `backlog/user-stories.md`
- `backlog/dependencies.md` (Mermaid dependency graph)
- `refinement-package.md` (per sprint)
- `sprint-clarifications/` (as needed)
- `change-impact/` (per change request)

### Quality Gate 5
- [ ] Backlog created with epics, stories, and acceptance criteria
- [ ] Story dependencies mapped
- [ ] Stories ready for sprint refinement
- [ ] Analyst has approved the backlog structure

---

## Phase 5: Organizational Learning

**Purpose**: Capture what worked, identify reusable patterns, and improve the analytical process for future initiatives.

**Entry criteria**: Implementation completed (or a significant milestone reached).

**Activities**:

1. **Quality assessment**: Review all artifacts produced during the initiative. What was useful? What was unnecessary? What was missing?
2. **Pattern identification**: What analytical approaches worked well? What templates should be reused?
3. **Lessons learned**: What would we do differently? What surprised us?
4. **Update knowledge base**: Index all materials, catalog decisions, update pattern library.
5. **Metric collection**: If possible, compare planned vs actual: effort, artifact revision rate, requirement change rate.

**Artifacts to produce**:
- `lessons-learned.md`
- `pattern-catalog.md`
- `quality-assessment.md`
- Updated `README.md` with final status and artifact index
- Updated `decision-register.md` with post-implementation reflections

---

## Quality Gates Summary

| Gate | Phase Transition | Key Criteria |
|------|-----------------|--------------|
| Gate 1 | 0 → 1 | Initiative classified, objectives defined, scope set, stakeholders identified |
| Gate 2 | 1 → 2 | AS-IS described, gaps identified, findings validated by analyst |
| Gate 3 | 2 → 3 | TO-BE coherent, variants evaluated, analyst approved direction |
| Gate 4 | 3 → 4 | Requirements complete, traceability built, cross-validated |
| Gate 5 | 4 → (implementation) | Backlog ready, stories have acceptance criteria, dependencies mapped |

**Gate enforcement**: Present the checklist to the analyst when you believe a phase is complete. All items must be confirmed. If items fail, identify what's missing and help address the gaps before re-checking.
