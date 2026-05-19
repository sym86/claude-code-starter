# /refactor-plan — Propose a refactor before writing any code

## Inputs
A file, module, or area of code I want refactored. If I haven't given
a clear goal ("make X testable", "reduce coupling between A and B",
"prepare for feature Y"), ask before producing the plan.

## Steps

### 1. Understand the current state
- Read the target code and its direct callers/imports.
- Identify the **3–5 specific pain points** the refactor should fix
  (not a general "improve code quality"). Quote file:line for each.
- State what the code currently does well — refactors that lose existing
  strengths are net-negative.

### 2. Set the goal
- Restate the refactor goal in one sentence. If it's wider than that
  sentence allows, the scope is too big — split it.
- List what's explicitly **out of scope**. This is the single most
  important step.

### 3. Propose phased steps
Output 3–7 numbered phases. For each:
- **Title** — what changes in this phase
- **Why** — which pain point it addresses
- **Scope** — files/symbols touched
- **Behavior change** — should be "none" for refactor phases; flag
  any phase that actually changes behavior
- **Test strategy** — which existing tests cover it, which new tests
  are needed *before* the change
- **Rollback** — how to revert if it goes wrong

Order phases so each one is independently mergeable and reversible.
No phase should depend on a later phase to compile.

### 4. Risks
- List the 3 highest risks (e.g. "callers in package X may depend on
  current ordering", "this method is called from a cron we don't have
  tests for").
- For each, propose how the plan mitigates it.

### 5. Estimate
- Rough size per phase: S (under 1 hour), M (1–4 hours), L (half day+).
- Total. If total is L+, recommend splitting.

### 6. Stop
End with: "Approve this plan or tell me what to change. I'll only
start coding once you confirm."

## Constraints
- Do not write any production code in this command. Plan only.
- Never propose "rewrite from scratch" without an explicit
  current-vs-rewrite cost/risk comparison.
- If the refactor would be easier *after* a small prerequisite change,
  make that change phase 1 and call it out.
- Behavior changes hidden inside refactor phases are forbidden — they
  must be their own phase, clearly labeled.
