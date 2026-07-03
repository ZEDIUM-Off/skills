---
name: plan-writer
description: "Plan subagent execution after grilling: draft, finalize, or revise a self-contained implementation blueprint with phases, waves, fresh subagent prompts, exact file scopes, validation gates, and handoffs."
---

# Plan Writer

Produce an implementation blueprint: a final Markdown plan that a fresh orchestrator can execute with fresh subagents, without knowing this skill.

For the full rules, gates, assignable-unit contract, validation policy, and revision mode, read [`REFERENCE.md`](REFERENCE.md) before planning.

## Process

### 1. Freeze intake

Capture the post-grilling goal, non-goals, decisions, constraints, and initial review flags.

Completion criterion: the objective and boundaries are explicit enough to start technical resolution.

### 2. Resolve uncertainty

Do the legwork before the final plan: inspect code, load relevant skills, read docs, and use focused subagents/chains when useful.

Completion criterion: every planned implementation unit has exact file scope; remaining uncertainties are only human/product decisions, real contradictions, or accepted risks.

### 3. Shape the task graph

Define phases, orchestration waves, tasks, and optional subtasks. Mark only bounded, fresh-executable units as `Assignable: yes`.

Completion criterion: every assignable unit has dependencies, parallelization constraints, exact files, validation responsibility, output contract, acceptance criteria, handoff notes, and a subagent prompt.

### 4. Review the draft

Run or simulate feasibility, sequencing, and scope-isolation reviews. Use parallel subagents when useful.

Completion criterion: required review changes are applied; any remaining concern is an explicit review flag.

### 5. Finalize the blueprint

Only after the gates pass and the user has approved finalization:

1. Create `.agents/plans` if needed.
2. If `.agents/plans/<slug>.md` exists, ask before updating or creating a variant.
3. Copy `templates/implementation-plan.md` to `.agents/plans/<slug>.md` or update the approved existing file.
4. Fill only the variable sections; keep invariant template text when possible.
5. Run:

```bash
node /Users/matissechenavas/.agents/skills/plan-writer/scripts/finalize-plan-lines.mjs .agents/plans/<slug>.md
```

6. Read the generated `Canonical Line References` table and verify it.
7. Report the plan path and remaining review flags.

Completion criterion: the saved Markdown contains stable anchors, generated line references, orchestration waves, and self-contained fresh-subagent prompts.

## Hard rules

- Drafts and iterations stay in chat; persist only the final approved plan.
- All implementation subagents are `fresh`; never rely on forked context.
- The final blueprint is not a scratchpad: include only verified facts, decisions, accepted constraints, actionable orchestration, exact scopes/references, and review flags.
- Do not recommend splitting merely because a plan is large; split only assignable units that are not bounded.
- Do not include generic provenance; attach references where execution needs them.
- Prevent legacy/workaround patches unless explicitly planned.
