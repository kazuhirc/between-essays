# Why 5W1H Breaks in Software Architecture, and What to Use Instead

Most architecture documents quietly inherit a habit from everyday explanation: 5W1H.
Who did what, when, where, why, and how. It feels complete, because it mirrors how humans tell stories.

In real systems, this habit eventually produces a familiar kind of fatigue. Documents grow, diagrams proliferate, and alignment meetings multiply. Not because people are careless, but because the coordinate system is unstable. The same fact can land in multiple buckets, and one change triggers edits across everything.

This essay argues that 5W1H is a convenient narrative scaffold, not a structural basis for complex systems. As systems become dynamic, distributed, and operationally accountable, architecture needs a different primitive: three independent axes: Structure, Dynamics, and Observation, plus a way to define "how we look" at them: View.

---

## 1. 5W1H is good narration, weak structure

5W1H helps you explain a situation to another human. It encourages coverage and reduces the chance you forget something. But it does not behave like an orthogonal model. The categories are not independent, and they do not compose well as systems evolve.

In architecture, the failure modes are consistent.

First, categories overlap. "Who" often encodes responsibility boundaries, which shape "what," which constrains "how." "Where" implies latency and failure domains, which rewrite "when" and "how." You can write a tidy 5W1H paragraph, but you cannot prevent the same information from reappearing under different headings.

Second, granularity drifts. One "what" is a single API endpoint; another "what" is an entire subsystem. One "when" is a nightly batch; another "when" is an event-driven state transition. 5W1H does not enforce level consistency, so documents oscillate between microscopic and panoramic without warning.

Third, time becomes underspecified. "When" is not the same as behavior. Real systems require ordering, branching, retries, idempotency, and timeouts. These are not add-ons; they are the system.

Fourth, observation becomes an afterthought. 5W1H has no explicit place for "how we know." Logs, metrics, traces, SLOs, and alert policies get bolted on late, because the primary narrative categories never demanded them.

The result is predictable: documents are large but fragile. They decay under change, and every edit threatens consistency.

---

## 2. How 5W1H fails in practice

The break is not philosophical. It is operational.

### 2.1 Duplicate truth in many places

A typical architecture set includes:

- a component diagram (who talks to whom),
- a sequence diagram (in what order),
- an operations runbook (what to do when it fails),
- a dashboard description (what to watch).

All are legitimate. The problem is that they often restate the same facts with different vocabulary and different implied assumptions. Over time, they diverge. You end up with multiple "truths" that must be reconciled by memory and meetings.

### 2.2 Organizational change rewrites technical meaning

When a team boundary shifts, or ownership changes, a 5W1H-style document forces edits everywhere because "who" is entangled with "what" and "how." The architecture itself may not have changed, but the documentation coordinate system did. This is a key source of hidden cost: the meaning remains, yet the text must be rewritten.

### 2.3 "Why" disappears into "what"

5W1H encourages you to answer "what we built" and "how it works". The design intent—the tradeoffs, constraints, and alternatives that justify the current structure—often dissolves into the "what" narrative. Months later, you can read the document and still not recover the decision. The system is present, but the reasoning has evaporated.

This is one of the most expensive forms of loss. It forces re-litigation. It also invites "optimizations" that accidentally destroy the conditions the system relied on.

### 2.4 Automation fails because the structure is not machine-readable

Many teams want "architecture as code" in some form: generated diagrams, validated configurations, reproducible deployments, enforced contracts. But 5W1H is a human-facing categorization, not a typed model. The language is too ambiguous and the granularity too inconsistent for reliable tooling.

When architecture cannot be projected into machine-checkable forms, regression protection becomes cultural rather than technical. That is not sustainable.

---

## 3. A stable basis: Structure, Dynamics, Observation

Across engineering disciplines, complex artifacts repeatedly collapse into three kinds of description:

- what exists and how it is arranged,
- how it changes over time,
- how it is observed and judged.

These map cleanly to:

- Structure
- Dynamics
- Observation

This is not a new framework in the sense of a proprietary method. It is closer to a minimum coordinate system that keeps reappearing whenever people must build, operate, and verify systems.

### 3.1 Structure

Structure is the static layout of what exists and how it connects.

Examples:

- modules, services, and their dependencies,
- data structures and schemas,
- network topology and failure domains,
- trust boundaries and interfaces.

Structure answers: what are the parts, where are the boundaries, and what references what.

### 3.2 Dynamics

Dynamics is how the system evolves in time.

Examples:

- sequences and causal flows,
- state machines and transitions,
- retries, timeouts, backpressure,
- periodic and event-driven scheduling.

Dynamics answers: what happens next, under what conditions, and what must be true for the next step to be valid.

### 3.3 Observation

Observation is how the system is made legible.

Examples:

- logs, metrics, traces,
- alerts, SLOs, health checks,
- inspection points and validation gates,
- evidence for success, failure, and recovery.

Observation answers: what we can know, when we can know it, and what we consider sufficient evidence.

A key claim of this essay is that Observation is not optional. Modern systems are defined as much by their observability as by their computation. If "how we know" is missing from architecture, the architecture is incomplete.

---

## 4. Mapping 5W1H onto the three axes

5W1H does not become "wrong." It becomes derivative.

You can treat each 5W1H element as a partial projection onto the three axes:

| 5W1H element | Primary mapping | Role |
|--------------|-----------------|------|
| What / Where | Structure | existence, placement, connectivity |
| When | Dynamics | timing, ordering, conditions, periodicity |
| How | Dynamics / Observation | control logic and how it is verified |
| Who | Structure / View | responsibility boundaries and access scope |
| Why | Constraints (acts on all axes) | requirements, tradeoffs, intent, prohibitions |

Two notes matter here.

First, "Why" is better treated as Constraints rather than a peer category. Intent and constraints are not a fourth axis; they constrain choices across all axes. Constraints are closer to the "laws of physics" of the system: semantic ground rules that act on every axis. In systems that touch the physical world, this includes invariants like spatial exclusivity and temporal causality; in software, it often appears as consistency models, safety constraints, and non-negotiable interface contracts. Put simply, these rules define what is admissible in structure and dynamics, and what is minimally required in observation to trust the system.

Second, "Who" is ambiguous by nature. Sometimes it describes organizational responsibility (a structural boundary). Sometimes it describes perspective, permissions, or exposure (a view problem). Treating "Who" as a single bucket is one reason 5W1H causes document churn.

---

## 5. View: architecture outputs as projections, not separate truths

Once you accept a stable basis, you can define something more useful than a pile of documents: View.

A View is a purpose-driven projection of Structure, Dynamics, and Observation. The word "view" is overloaded in English, so this essay draws a hard boundary: Observation produces and justifies evidence; a View selects and presents the basis for a specific audience and goal.

This reframes familiar artifacts:

- A component diagram is a View emphasizing Structure.
- A sequence diagram is a View emphasizing Dynamics.
- A dashboard is a View emphasizing Observation.
- A runbook is a View combining Dynamics and Observation under recovery constraints.

Crucially, Views should not become independent sources of truth. They should be projections that can be regenerated or validated against the underlying model.

This yields a practical design rule:

Architecture does not rot because people are lazy; it rots because Views are treated as independent truths and drift apart.

When you treat documents and diagrams as Views, you gain a way to reason about consistency. You can ask:

- Which axis does this View rely on?
- What constraints does it assume?
- What evidence does it require?
- What must remain stable for this View to stay valid?

---

## 6. Why source code is also a View

Engineers often treat code as "the truth." That is partly correct and partly dangerous.

Source code is a View that expresses Structure and Dynamics in a specific language. It is powerful, but incomplete. It usually does not contain an explicit, reviewable Observation model: what must be logged, what must be measured, what constitutes failure, how recovery should be decided.

This explains a common operational pain:

When code becomes the only truth, observation becomes a retrofit.

Teams then rebuild observability by reading code, reconstructing intent, and guessing constraints. That work repeats during every incident.

In a View-based architecture, you want the opposite: code remains central, but observation and operational evidence are treated as first-class views, constrained by the same basis. Code stays legible because the other Views stay anchored.

---

## 7. How to adopt this without rewriting everything

You do not have to rebuild your documentation set from scratch. You can introduce the coordinate system gradually.

### 7.1 Inventory existing artifacts as Views

List what you already have:

- diagrams,
- documents,
- runbooks,
- dashboards,
- deployment configurations.

Assign each item:

- which axis it emphasizes (Structure, Dynamics, Observation),
- what purpose it serves,
- what constraints it assumes.

This alone reveals two useful patterns: duplicates and gaps.

### 7.2 Identify gaps by axis

Common gaps include:

- Structure exists, but Dynamics is implicit (only "it should work").
- Dynamics exists, but Observation is missing (no explicit evidence).
- Observation exists, but is unmoored (alerts without a model of "what matters").

Treat these as architectural defects, not documentation defects.

### 7.3 Choose a single truth per axis where possible

Decide where the truth lives:

- OpenAPI, schema files, dependency manifests for Structure,
- state machines, workflow specs, or tested sequences for Dynamics,
- telemetry specs, SLO definitions, and evidence policies for Observation.

Then treat prose documents and diagrams as Views derived from these sources. Even partial derivation (links, references, checklists) reduces drift.

### 7.4 Enforce View integrity through review questions

A lightweight review rubric can be:

- What is the Structure change?
- What Dynamics does it introduce or modify?
- What Observation is required to detect failure and verify success?
- Which Views must be updated, and which can be regenerated?

This turns "documentation discipline" into an engineering workflow.

---

## 8. What you gain

### 8.1 Change becomes localized

When team boundaries shift or systems split, the underlying basis can remain stable. You update the Views that depend on organizational perspective, not the entire architectural narrative.

### 8.2 Observability becomes architectural, not cosmetic

Observation is no longer a late-stage add-on. It becomes part of the minimal description of the system. This aligns architecture with real-world operation, where failures are inevitable and recovery must be engineered.

### 8.3 Tooling becomes realistic

Once you can state what belongs to which axis, it becomes feasible to validate and regenerate. You can build checkers, produce reports, and guard against regressions without relying on memory.

### 8.4 Review becomes simpler

Instead of debating document style, you can debate the model:

- Is the structure coherent?
- Are the dynamics safe and complete?
- Is the observation sufficient to operate the system?
- Is this View the right projection for its audience?

That shifts effort from coordination to engineering.

---

## Closing

5W1H is a great way to explain a system in conversation. It is not a stable coordinate system for architecture.

For complex, changing, operational systems, the minimum stable basis is:

- Structure
- Dynamics
- Observation

And the practical method for communication is:

- View as projection, not separate truth.

This is not about inventing a new framework. It is about adopting a coordinate system that makes drift visible, change manageable, and evidence first-class.

If your documentation decays even when people work hard, treat that as a signal: the coordinate system is unstable. Fix the basis, then define Views on top of it.

---

The figure summarizes the three axes and a View as their projection.

```
      Observation (O)
            ^
            |
		    |
            |
            +--------> Structure (S)
           /
          /
         v
    Dynamics (D)

         \   |   /
          \  |  /
           \ | /
            \|/
          [View]
```

Observation produces and justifies evidence; a View selects and presents it for a specific audience and goal.

View = purpose- and constraint-defined projection of Structure, Dynamics, and Observation.
