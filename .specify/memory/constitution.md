<!--
Sync Impact Report
- Version change: 0.0.0 → 1.0.0
- Modified principles: (template → project-specific)
	- [PRINCIPLE_1_NAME] → Angular 21 First-Class
	- [PRINCIPLE_2_NAME] → Type Safety & Explicit 3D Contracts
	- [PRINCIPLE_3_NAME] → Performance Budgeted 3D Rendering
	- [PRINCIPLE_4_NAME] → Thin Components, Strong Services
	- [PRINCIPLE_5_NAME] → Spec Kit-Gated Delivery
- Added sections:
	- Technology & Architecture Constraints
	- Development Workflow & Quality Gates
- Removed sections: None (template sections specialized, not removed)
- Templates requiring updates:
	- ✅ .specify/templates/plan-template.md (Constitution Check aligned)
	- ✅ .specify/templates/spec-template.md (success criteria + scenarios compatible)
	- ✅ .specify/templates/tasks-template.md (phase structure compatible with Spec Kit flow)
- Follow-up TODOs:
	- TODO(RATIFICATION_DATE): Set actual original ratification date when known.
-->

# wesley-dusell-3d Constitution

## Core Principles

### I. Angular 21 First-Class (NON-NEGOTIABLE)

All production code MUST be idiomatic Angular 21 using standalone components,
the modern router APIs, Angular Signals for local reactive state, and strict
TypeScript typing. Components MUST declare `ChangeDetectionStrategy.OnPush`,
avoid `@HostBinding` and `@HostListener` in favor of `host` configuration, and
prefer inline templates for small, focused components. Routing MUST be
lazy-loaded for feature areas, and templates MUST use Angular's native control
flow (`@if`, `@for`, `@switch`) and the `async` pipe for observable bindings.

**Rationale**: Enforcing idiomatic Angular 21 keeps the codebase modern,
predictable, and aligned with the official framework direction, which reduces
maintenance cost and makes it easier to onboard new contributors.

### II. Type Safety & Explicit 3D Contracts (NON-NEGOTIABLE)

The TypeScript compiler MUST run in strict mode with zero `any` usage in
production code. All scene data, camera configuration, materials, animation
loops, and interaction handlers MUST be modeled with explicit interfaces or
types. When types are uncertain, `unknown` MUST be used and narrowed explicitly
before use. Public APIs for 3D utilities, services, and components MUST accept
and return well-typed contracts.

**Rationale**: A strictly typed 3D stack dramatically reduces runtime errors in
complex rendering and interaction flows and makes refactoring safe as the
portfolio evolves.

### III. Performance-Budgeted 3D Rendering (NON-NEGOTIABLE)

The 3D experience MUST target 60 fps on modern laptops under normal usage.
Every 3D feature MUST respect an explicit performance budget for draw calls,
geometry complexity, material count, and shader work. New 3D features MUST be
evaluated for impact on frame time; where necessary, level-of-detail
techniques, culling, instancing, or simplification MUST be applied. Debug-only
instrumentation MAY be used to track frame rate and frame time.

**Rationale**: A portfolio that stutters undermines its purpose. Explicit
performance budgets protect the user experience as visuals and interactions
grow.

### IV. Thin Components, Strong Services

Angular components MUST remain small and focused on orchestration and view
composition. Three.js scene setup, cameras, render loops, loaders, and shared
interaction logic MUST live in dedicated services or utility modules with
clear, typed APIs. Components MAY bind Signals and observables and delegate
work to services, but they MUST NOT accumulate low-level Three.js imperative
logic.

**Rationale**: Separating orchestration (components) from core behavior
(services/utilities) improves testability, reuse across routes, and keeps the
component tree understandable.

### V. Spec Kit-Gated Delivery (NON-NEGOTIABLE)

All new features and materially changed behaviors MUST go through the full
Spec Kit flow in this order: constitution → spec → plan → tasks →
implementation → tests. No feature work MAY begin without a drafted spec and
plan, and no feature MAY be considered complete until the corresponding tasks
are checked off and core tests are implemented and passing. Exceptions MUST be
explicitly recorded in the Complexity Tracking section of the plan.

**Rationale**: A personal portfolio can evolve quickly and experimentally.
Spec Kit ensures each change is intentional, traceable, and testable.

## Technology & Architecture Constraints

The project is a personal 3D resume/portfolio built with Angular 21 and
Three.js.

- **Frontend stack**: Angular 21, standalone components, Angular Router, SCSS.
- **3D layer**: Three.js integrated into Angular via dedicated services or a
  thin wrapper; imperative Three.js code MUST NOT leak into templates.
- **Reactivity**: Angular Signals for local UI state; RxJS observables for
  streams (user interaction, time-based effects, router events, async data);
  the `async` pipe MUST be used for observable bindings.
- **TypeScript**: Strict mode enabled and maintained; tsconfig changes MUST NOT
  weaken strictness.
- **Testing**: Vitest + jsdom for unit tests, with a focus on 3D scene setup,
  interaction logic, and performance-sensitive code paths.
- **Tooling**: Angular CLI 21 and npm define the canonical build and test
  workflows.

## Development Workflow & Quality Gates

All work MUST follow the Spec Kit-driven workflow and respect these gates:

1. **Spec Gate**

   - A feature specification in `/specs/[###-feature-name]/spec.md` MUST define
     user stories, edge cases, functional requirements, and success criteria
     before any implementation work.
   - Performance expectations (especially 60 fps target and any memory or load
     constraints) MUST be captured in the spec's success criteria.

2. **Plan Gate**

   - An implementation plan in `/specs/[###-feature-name]/plan.md` MUST be
     generated from the spec using the Spec Kit command.
   - The plan's **Constitution Check** MUST explicitly confirm compliance with
     this constitution or list violations in the Complexity Tracking table with
     justification.

3. **Tasks Gate**

   - A task list in `/specs/[###-feature-name]/tasks.md` MUST decompose the
     feature into independently testable slices aligned to user stories.
   - Tasks for 3D work MUST clearly indicate which services/utilities and which
     components are touched, and MUST include Vitest coverage for core scene
     setup and interaction logic.

4. **Implementation & Testing Gate**

   - Implementation MUST follow the structure in plan and tasks, keep
     components thin, and place 3D setup and loops into services/utilities.
   - New code MUST compile with strict TypeScript and pass Vitest test suites.
   - Critical 3D interactions and scene setup MUST have unit tests or
     integration-style tests in Vitest (as feasible in jsdom).

5. **Review Gate**
   - Code review MUST verify:
     - Compliance with Angular 21 idioms, Signals, and strict typing.
     - Absence of `any` in new or modified TypeScript.
     - Respect for performance budgets (no obvious 60 fps regressions).
     - Traceability from implementation back to spec, plan, and tasks.

## Governance

This constitution governs all technical work in `wesley-dusell-3d` and
supersedes informal preferences or ad-hoc practices.

- **Authority**: In case of conflict, this constitution overrides other
  documentation. Specs, plans, and tasks MUST conform to these principles.
- **Amendments**:
  - Any change to principles, constraints, or workflow MUST be proposed via a
    dedicated spec that explains the motivation and impact.
  - Upon approval, this file MUST be updated with a new semantic version,
    rationale captured in a Sync Impact Report comment, and `Last Amended` set
    to the amendment date.
- **Versioning**:
  - MAJOR: Backward-incompatible governance changes (e.g., removing or
    redefining a NON-NEGOTIABLE principle).
  - MINOR: Adding new principles, sections, or material expansions.
  - PATCH: Clarifications that do not change obligations.
- **Compliance Review**:
  - All PRs MUST include a brief note confirming which Spec Kit artifacts are
    linked (spec/plan/tasks) and whether this constitution remains satisfied.
  - Violations MUST be recorded in the plan's Complexity Tracking table with a
    clear exit strategy.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): set initial adoption date | **Last Amended**: 2025-12-04
