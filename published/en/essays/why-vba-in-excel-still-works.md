---
title: Why VBA-in-Excel Still Works — and What AI-in-Excel Must Preserve
date: 2026-02-03
---

# Why VBA-in-Excel Still Works — and What AI-in-Excel Must Preserve

_On the operational properties that outlast every modernization wave_

---

## The macro that would not die

Every few years, someone proposes replacing it.

The workbook is old. The VBA is tangled. The named ranges have names that only one person understands. A consultant draws a clean architecture diagram with REST endpoints and a proper database, and everyone nods. Then the project stalls, or ships something that covers 70% of the cases, and the old workbook quietly returns to service.

I have watched this cycle three times in my career. Each time the replacement was technically superior. Each time the original survived — not because people were stubborn, but because the replacement could not do what the spreadsheet actually did: keep decisions moving while preserving enough context for someone else to check them later.

This essay is not a defense of VBA. It is an attempt to name the properties that make VBA-in-Excel unexpectedly durable at the operational front line — the place where design, manufacturing, purchasing, and inspection meet — and to ask what AI-in-Excel must preserve if it wants to occupy the same ground.

---

## 1. The product is not a spreadsheet. It is a chain of decisions.

In most organizations, the spreadsheet is treated as the artifact. But the artifact is not what matters. What matters is the chain of decisions that the artifact represents.

A typical front-line workflow is not "enter inputs, compute output." It is closer to:

1. Read something — a customer drawing, a prior job, a specification.
2. Derive candidates — run calculations, call a macro, or now, ask an AI.
3. Compare and judge — check differences, validate constraints, consult references.
4. Commit — issue a drawing, send a purchase order, register an inspection result, update master data.

Before commit, work is reversible. After commit, correction becomes coordination, rework, and explanation. In practice, a single job includes multiple commits; each commit creates a new irreversible boundary. That boundary is where operational cost concentrates. And it is exactly at that boundary where VBA-in-Excel has proven surprisingly reliable.

The output of this chain is not a number. It is a defensible decision: a result that can be rechecked later, by someone else, under changed tools, and still be accepted as the same judgment.

---

## 2. Four properties architects should respect

VBA is easy to dismiss because it looks old. But age is not the question. The question is why it keeps running where cleaner designs do not. The answer lies in four properties that are architectural, not linguistic.

### Data proximity

VBA runs where the operational truth already lives. The macro reads the exact sheet the operator is looking at, transforms data in the same conceptual frame, and writes results back into the same artifact. There is no serialization layer that strips context. The moment you move logic away from the sheet, you create boundaries — extraction, mapping, validation, synchronization — and each boundary introduces new failure modes and new human work.

### Deployment simplicity

A macro-enabled workbook can be copied, shared, and executed in environments where no one has admin privileges and every extra dependency is a political burden. Front-line automation rarely fails on algorithmic complexity. It fails on distribution, support, and drift. The single-artifact packaging keeps those costs low enough that the organization can tolerate gradual improvement. When you propose a replacement, you must beat this operational advantage, not just runtime performance.

### Human-in-the-loop by default

Many macros are not end-to-end pipelines. They are stepwise procedures with intentional pauses: verify inputs, confirm selections, review outputs, approve before writing back. The system allows stop-and-recover without losing state. This is not a limitation. It is a design for ambiguity, incomplete requirements, and constraints that only experienced operators can interpret.

### Implicit contracts

Most VBA workbooks rely on unstated assumptions: named ranges must exist, columns must carry specific meanings, reference tables must be current, certain cells must be filled before execution. These assumptions are rarely documented, but they are enforced through code that checks and stops. In other words, many macros operate as validators and gatekeepers as much as calculators. They encode "what must be true before we proceed" and reduce variation across operators and across time.

These four properties are not VBA features. They are operational invariants. Any replacement that discards them will be technically superior and operationally fragile.

---

## 3. AI changes the failure mode

Classic Excel risk is familiar: wrong formulas, wrong references, silent copy mistakes. These are correctness failures. They can be painful, but they are diagnosable. A formula is visible. A cell can be traced. A macro can be stepped through. The artifact carries some internal explanation of how it got its result.

AI embedded in Excel shifts the dominant failure. The problem is no longer "the sheet computed the wrong value." It becomes "the sheet cannot explain why this value is acceptable."

This is concrete, not hypothetical:

- The same prompt yields different answers on different days. Model nondeterminism and silent updates make the output a moving target.
- Input context and tool identity are not preserved. Sources, assumptions, reference tables, and even the model version may be missing, so drift cannot be bounded or explained.
- An operator commits a result but cannot later reconstruct what was read, under what conditions, and with what authority.

The downstream effect is predictable. When provenance is weak, organizations compensate with more human work: extra reviews, more meetings, more send-backs, more approvals, and ultimately more delay. The sheet looks faster. The workflow becomes slower.

The core problem is not intelligence. It is comparability — the ability to say, under the same declared conditions, "this result and that result can be accepted as equivalent, even though the tools or operators changed."

Industry signals confirm the problem is real: some cloud analytics products already package data sources, instructions, and verified definitions together to stabilize conversational workflows.
Those solutions are typically platform-scoped; the approach described here focuses on the portable discipline—explicit gates, check artifacts, and ordered evidence that let workflows stop and recover across heterogeneous tools.

---

## 4. Failures that illustrate the pattern

The argument becomes clearer through examples. Each of these is a real pattern, not a single incident.

**Template drift.**
A team reuses a past workbook as a template. A reference table inside is outdated, but no one notices because the outputs still look reasonable. Two weeks later, another operator runs the same file after updating one lookup table, and the outputs differ. Both results "make sense." No one can explain which is acceptable. The result is a meeting and a quiet rewrite.

This is not a calculation error. It is a missing prerequisite: the reference table version was not declared or checked.

**AI summary shipped without provenance.**
AI-in-Excel generates a summary of a customer drawing and proposes parameter values. The operator copies them into the sheet. Later, an engineer asks why a particular tolerance was chosen. The prompt is not saved, the input drawing is not linked, the model version is unknown. The only thing left is the final number.

This is not primarily an "AI hallucination" problem. It is a provenance failure: the decision was committed without the references that make it defensible.

**Same part number, different conditions.**
Two operators generate the same inspection instruction for the same part. One assumes horizontal mounting, the other assumes vertical. Both documents look correct internally. Only during inspection does someone realize the measurement axis differs, and the results are not comparable.

Nothing is "wrong" with either document. The mounting condition was not bound to the decision.

**External dependency changed silently.**
A workbook uses a lookup table on a shared drive. The path remains the same, but the contents were updated. A job created last month cannot be reproduced today. The team sees drift and assumes "someone made a mistake," but the real cause is dependency drift.

**Approvals were assumed.**
A junior engineer updates a master sheet because the macro allows it. A week later, a senior engineer asks why the master changed. The junior says "the tool let me." The senior says "you were not supposed to commit that." The organization adds a manual rule. The tool remains unchanged.

In every case, the failure is not in the computation. It is in the boundary — something that should have traveled with the decision got separated from it.

---

## 5. Five things that must travel together

I call this minimal semantics layer Between: a way to keep decisions comparable across tools and time. The pattern across these failures is consistent. A decision becomes unverifiable when it gets separated from its references. To stay comparable, a decision needs a bundle:

- **Basis** — what was read: source drawing, customer spec, prior job ID. Missing: cannot justify the choice.
- **Conditions** — under which assumptions: mount direction, measurement axis, environment, selected rule set. Missing: same part, different results.
- **Effects** — which external dependencies influenced the result: tables, dictionaries, models, tool versions. Missing: drift looks like human error.
- **Evidence** — enough of the above recorded so the decision can be rechecked later and accepted as equivalent. Missing: recheck becomes impossible. Minimal: store pointers (IDs/paths/URLs) to basis/inputs, versions (or as-of dates) of dependencies, and a short commit rationale in one place.
- **Approvals** — who approved the commit, and at what stage. Missing: commit authority becomes ambiguous.

(In the Observation Point Design essay, preconditions and external factors are introduced at a more compact level. The split here into Conditions and Effects reflects front-line practice, where mounting direction or measurement axis and lookup-table version fail differently and must be diagnosed separately.)

If these are scattered, you get plausible outputs that cannot be compared. If these travel together, you can re-examine the workflow and accept results as equivalent under the same declared conditions.

A **contract** is the declaration of what a bundle must contain for a given decision type. A **gate** is a stop point that checks the bundle before commit and routes the operator into recovery when it is incomplete. Recovery means answering four questions: what is missing, where to obtain it, the minimum edit to proceed, and the escalation route if it cannot be obtained.

These are not new ideas. Most experienced operators already carry versions of them in their heads. The point is to make them explicit, checkable, and portable — so they survive staff turnover, tool migration, and the introduction of AI.

---

## 6. Connecting the properties to the design

The link between "why VBA works" and "what to design next" can be drawn directly:

| VBA-in-Excel property | Design primitive       | Question it answers                                              |
|-----------------------|------------------------|------------------------------------------------------------------|
| Data proximity        | Reference bundle       | Is the required basis attached to the decision, not scattered?   |
| Deployment simplicity | Contract (packaging)   | Can the tool and its prerequisites ship as one verifiable unit?   |
| Human-in-the-loop     | Gate + recovery path   | Can humans stop before commit and resume with guidance?           |
| Implicit contracts    | Contract (explicit)    | Are prerequisites declared and auto-checkable?                    |

The goal is not to preserve VBA. It is to preserve the operational invariants that VBA-in-Excel enforced — sometimes by accident, sometimes by the accumulated wisdom of the people who maintained it.

---

## 7. Measuring what matters

If you measure AI by how fast it produces an answer, you will optimize the wrong thing. The front line does not pay for answers. It pays for stable decisions.

Two metrics cut through the noise:

**Comparability rate** — under the same declared basis and conditions, how often do results come back equivalent? You do not need perfect reproducibility. You need bounded drift that is visible. When drift is detected, the system should stop and require re-approval, not silently continue.

**Human-in-the-loop cost** — the total overhead of hesitation, explanation, and rework. In legacy environments, start with what is easy to record:

- Send-backs — formal rejection requiring re-submission.
- Reason-hunting time — time spent reconstructing why a result is acceptable.
- Approval waiting — time stalled at the approval-to-commit boundary.
- Post-generation edits — manual corrections after automated output.

Even tracking send-backs alone gives a leading indicator of where semantics is unstable. That makes the problem actionable without a platform rebuild.

---

## Closing: speed comes after comparability

VBA-in-Excel keeps working not because it is modern, but because it quietly enforces what modern systems often forget: decisions must be stoppable, recoverable, and comparable.

AI-in-Excel will earn its place when it can do the same — not by being smarter, but by carrying the bundle, checking the contract, and stopping at the gate when something is missing.

If you want to start tomorrow, do three things:

1. Pick one failure-prone commit boundary and write down its prerequisites as a contract.
2. Add a gate that stops before commit and tells operators what is missing and how to recover.
3. Log one metric you can record today — send-backs or post-generation edits — and review it weekly.

Start small. Speed comes after comparability.

---

## Related essays

- **Observation Points and Comparability** — why comparison breaks, and the five questions that restore it.
- **Origin** — the two files that started Between: an Excel sheet, an AutoCAD block library, and the boundary in between.

---
