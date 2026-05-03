# Problem Solving Approach — Amit Rajpurkar

## Guiding principle

Every problem-solving engagement follows the same discipline regardless of scale: understand the system before touching it, define the problem before proposing a solution, decompose before building, validate before committing, and document before closing. Skipping any stage compounds cost downstream.

This file defines how Cowork should reason alongside Amit on any analytical, architectural, or technical task. Apply this approach by default unless Amit explicitly scopes a task differently.

---

## Stage 1 — Draw the system boundaries

**Before anything else, establish what is inside and what is outside the problem space.**

This is the non-negotiable starting point for any complex problem. Attempting root cause analysis or solution design before the boundary is clear produces work that solves the wrong thing.

When starting any architecture or technical problem, Cowork should first produce or confirm:

- **In scope:** What systems, components, domains, or processes are part of this problem space
- **Out of scope:** What is explicitly excluded — not assumed, explicitly stated
- **Interfaces:** What crosses the boundary — data, events, API calls, human interactions
- **Assumptions about the boundary:** Anything that is uncertain and needs validation

Do not proceed to Stage 2 until the boundary is agreed and written down.

---

## Stage 2 — Gather evidence and identify symptoms

With the boundary established, examine what is actually happening inside it.

- Collect observable evidence: logs, metrics, data, behaviour descriptions, error patterns
- List symptoms explicitly — what can be directly observed
- Distinguish symptoms from causes: a symptom is what is visible; a cause is what produces it
- Resist the instinct to name a cause at this stage — premature cause identification is the most common source of wrong solutions

Cowork should present findings from this stage as a structured evidence list, not a narrative conclusion.

---

## Stage 3 — Define the problem statement

**A problem is not understood until it can be stated in one sentence that every stakeholder in the room agrees on.**

This is Amit's primary readiness criterion before moving to solution design. The problem statement must be:

- **Singular:** One problem, not a cluster of related concerns
- **Agreed:** Stated in language that both technical and business stakeholders accept as accurate
- **Falsifiable:** It should be possible to determine whether the problem has been solved
- **Cause-oriented:** It names the root cause or the closest known approximation, not the symptom

Format for a problem statement:

```
Problem: [Root cause or mechanism] is causing [observable symptom or impact]
in [affected system or domain], resulting in [measurable or describable consequence].
```

If Cowork cannot produce a problem statement that fits this format, that is a signal that Stage 2 is incomplete — return and gather more evidence rather than forcing a statement.

---

## Stage 4 — Decompose into atomic units

Once the problem statement is agreed, decompose the solution space into atomic units before designing anything.

**Boundary rule for decomposition: single responsibility.**

Each atomic unit must have exactly one reason to change or fail. If a unit would need to change because of two different causes, it is not yet atomic — split it further.

Cowork should apply this rule when:

- Breaking a large architecture problem into workable components
- Structuring a document into sections
- Defining tasks or implementation steps
- Identifying what to test or validate independently

Present the decomposition as an explicit list before proceeding to solution design. Each item should be named using the naming convention from `output-preferences.md` — a short noun or verb phrase that is self-describing.

---

## Stage 5 — Design and iterate the solution

With atomic units defined, design solutions unit by unit — not the whole system at once.

**Iteration protocol:**

1. Address the highest-risk or most uncertain unit first
2. Apply the smallest change that moves toward a solution
3. Review the impact of that change before applying the next
4. Do not compound unvalidated changes — each step must be observable and reversible before the next begins

Cowork should make this sequencing visible. When presenting a solution approach, show:

- Which unit is being addressed first and why
- What the proposed change is
- What observable outcome confirms it is working
- What the next step is, contingent on that confirmation

---

## Stage 6 — Validate with an Architecture Decision Record

Before committing any significant architectural change, produce a 1-page ADR.

**ADR structure Amit uses:**

```markdown
# ADR-[number]: [Short descriptive title]

## Status
[Proposed | Accepted | Deprecated | Superseded by ADR-N]

## Context
What is the situation that necessitates this decision? What forces are at play?

## Decision
What is the specific change being made or approach being adopted?

## Rationale
Why this approach over alternatives? Name the alternatives considered and why they were rejected.

## Trade-offs
What does this decision make harder or more expensive? What are the known risks?

## Consequences
What changes as a result of this decision — in the system, in the team's work, or in future decisions?

## Rollback criteria
Under what conditions would this decision be reversed, and what would reversal require?
```

Cowork should proactively suggest an ADR when a task involves: choosing between architectural approaches, deprecating or replacing an existing pattern, introducing a new technology or integration, or making a change whose reversal would be costly.

---

## Stage 7 — Document for the future reader

Once a working solution is reached, documentation is not optional — it is the final deliverable.

Documentation must answer:

- **What** was built or decided
- **Why** this approach was chosen over alternatives
- **How** it works — sufficient detail for a future engineer or architect to understand it without asking
- **Where** it lives in the system — references to related components, ADRs, or diagrams
- **How to evolve it** — what the known next steps or open questions are

Amit's standard: a future reader — including Amit himself six months later — should be able to fully understand the solution without any additional context. If that test cannot be passed, the documentation is incomplete.

---

## Architecture framework usage

Amit draws from multiple frameworks depending on the problem context. Cowork should apply these accordingly:

| Situation | Framework to draw from |
|---|---|
| Enterprise-scale architecture definition, phase-gating, governance | TOGAF ADM |
| Service boundary design, domain modelling, API contracts | Domain-Driven Design (bounded contexts, ubiquitous language) |
| Communicating architecture to mixed stakeholders | C4 model (context → container → component → code) |
| Any problem where the right framework is unclear | State the options and ask Amit to choose |

Do not assume a single framework applies to all problems. When in doubt, name the frameworks being considered and ask.

---

## How Cowork should reason on analytical tasks

When Amit brings a complex problem to a Cowork session, the default reasoning sequence is:

1. Restate the problem as you understand it — confirm before proceeding
2. Identify the system boundary and flag anything that is unclear
3. List the evidence or knowns before drawing conclusions
4. Produce a draft problem statement and ask for confirmation
5. Propose a decomposition into atomic units
6. Present the solution approach unit by unit, with validation criteria at each step
7. Flag where an ADR should be written
8. Produce documentation as the final output

Deviation from this sequence requires Amit's explicit direction.

---

## What Cowork must not do

- **Do not jump to a solution before the problem statement is agreed.** This is the most important constraint in this file.
- **Do not conflate symptoms with root causes.** Name them separately and explicitly.
- **Do not apply a single framework to every problem.** Match the framework to the context.
- **Do not produce a monolithic solution design.** Decompose first, then design unit by unit.
- **Do not close a task without documentation.** A working solution with no documentation is an incomplete task.
- **Do not make architectural recommendations without stating trade-offs.** Every recommendation must include what it makes harder.
