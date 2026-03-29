---
title: "Between Mechanics and Software"
date: 2025-02-04
summary: "Design is projection—a disciplined reduction with a checkable contract. This essay explores what mechanical drawings and software specifications share: the discipline of choosing what to drop, and making the drop safe."
tags: [projection, contract, sidecar, design]
---

# Between Mechanics and Software

Much of my work has been in dimensional measurement, and the framework I keep coming back to is GD&T (GPS): not because it is “formal,” but because it makes the basis of comparison explicit. Datums, tolerances, and inspection rules do not add detail for its own sake; they tell us what counts as the same, what counts as different, and how we are allowed to check. This essay asks whether the same discipline can apply to a different kind of signal: design intent mediated through many artifacts.

Mechanical drawings and software specifications are often treated as different genres—one belongs to manufacturing, the other to computing. I think they are closer than they look. Both exist because the real thing is too rich, too contextual, and too expensive to move directly. We need an artifact that can travel across distance and time, and still lead to consistent action.

The lens I use here is projection: a deliberate reduction under an explicit convention, backed by a checkable contract. With that lens, a drawing, an API spec, and even source code become comparable artifacts: each preserves some structure, drops the rest, and must make the drop safe. 

---

## Design Documents Are Projections

A technical drawing is a projection of a 3D object into 2D views. Here I will treat a "View" (capital V) more broadly: any projection artifact with a reading convention—not only drawings. A View is not a picture; it is a machine for coordination. The drawing chooses a limited set of views, assigns dimensions, and attaches tolerances so that manufacturing and inspection can treat it as executable guidance. It creates a stable surface where many people can align their work without re-negotiating the full 3D reality each time.

An API specification plays a similar role. It projects a system's internal model and behavior into an interface surface that other systems can call. It is not the running software; it is the slice of the software that must be stable for someone else to depend on.

In both cases, the artifact is a designed reduction. What matters is not how complete the artifact is, but whether it is complete in the right places—complete enough that the receiver can act, and incomplete in ways that are explicitly compensated.

This is why "more detail" is not automatically "better." A drawing filled with implicit assumptions is dangerous even if it looks precise. An API document that hides operational constraints is dangerous even if it lists every field. The test is not density; the test is whether the projection is deliberate and whether its promises are checkable.

---

## Projection Always Loses Information

Projection is reduction, so loss is inevitable. In drawings, the 3D object has continuous surfaces, thickness, assembly context, material behavior, temperature sensitivity, and manufacturing fingerprints. None of that exists in a 2D view unless you force it into the projection. If you care about a hidden surface, you add a section. If you care about fit, you add a tolerance. If you care about orientation, you add datums. The information does not "come along for free."

Software projections lose different kinds of information, but the structure is the same. A JSON schema and an OpenAPI document do not automatically carry "why this field exists," "what sequence is safe," or "what the system assumes about the world." If you do not force those constraints into the projection, the receiver will invent them—usually incorrectly, and usually in a way that only fails in production.

Loss creates room for misreadings. These misreadings are not "careless mistakes." They are the natural result of a projection that dropped information without compensating for the drop. This suggests a useful definition of design quality: not perfection of description, but quality of omission. Good design chooses what to drop, and then makes the drop safe.

---

## Contracts Are How We Make Loss Safe

The way engineers survive projection is by writing contracts. In mechanical design, the contract is the admissible variation: tolerances, datums, geometric controls, surface finish, and the conventions that connect them to inspection. These exist to make drawings actionable under manufacturing reality, where variation is unavoidable.

A tolerance is a statement of identity under variation: within this range, two parts count as "the same part" for the function we care about. A datum system is a statement of basis: measurement must be performed in a specified frame, or the numbers are not comparable. GD&T, in that sense, is the grammar that turns a drawing into an executable agreement.

A canonical example is ISO 1: the reference temperature for dimensional measurement is 20°C. The point is comparability. Without a pinned basis, two measurements cannot be reliably compared, and design-manufacturing separation collapses into local convention. But pinning a basis alone is not enough: comparison becomes durable only when the instrument, conditions, and calibration lineage are recorded as traceable evidence—not as folklore, but as an explicit signal chain where drift becomes inspectable rather than arguable.

In software, the parallel contract is schema, validation, and explicit error surfaces. A schema is a statement of identity under variation: within these constraints, two messages count as "the same message" for the behavior we care about.

The important point is that contracts are not mere restrictions. They are boundaries that make freedom safe. Without a contract, any change becomes risky because the receiver cannot tell whether the meaning stayed the same. With a contract, you can change internal implementation while preserving external meaning—tooling and process in mechanical terms, internals and refactoring in software terms.

This also clarifies why "documentation" is not the core issue. The core issue is whether a receiver can reliably decide: "Is this still the same thing?" Contracts answer that question by defining admissibility, basis, and identity in a checkable form.

---

## Why Source Code Is Also a Projection

One might object that code is fundamentally different because it executes. But a drawing also "executes"—through manufacturing and inspection workflows. The difference is not in kind but in how directly the artifact drives its target process.

Projection is also a convention that determines what becomes visible and what stays implicit. In mechanical drawing, first-angle and third-angle projection can describe the same object while demanding different reading habits. The same object can be made legible or confusing depending on the assumed observer position. Confusion appears when the convention is not stated, or when teams silently switch conventions across documents. The views are still "correct," but the shared reading frame is broken.

Source code behaves similarly. Here, "View" does not mean MVC or a database view; it means a projection artifact with a reading convention. Code expresses structure and behavior strongly, but it expresses observation and intent weakly unless you explicitly externalize them.

When teams treat code as the only source of truth, two failures become common. First, everything that is not naturally expressed in code—operational assumptions, expected ranges, basis choices, recovery policies—becomes tribal knowledge. Second, when reality violates an implicit assumption, the failure appears far away from the decision that created the assumption. The system breaks, but the artifact that could have explained the break is missing. Timeouts, retry caps, rounding policies, evidence thresholds, recovery playbooks: these are the hidden surfaces of a software system that code alone does not carry.

Code should be treated as one View among multiple Views that together define a system. Tests express admissibility, telemetry expresses observation, runbooks express operational reality, and schemas express interface meaning. If code is made to carry everything, it will carry the wrong things badly and drop the right things silently.

Seeing code as a View also makes design discipline transferable. Once you recognize that every View is a projection with loss, you start asking the same questions everywhere: What did we drop? Where is it compensated? What is checkable, and by whom?

---

## Sidecar Makes Preconditions and Rationale Diffable

Once you accept that every View is incomplete by design, the next question is where the missing information should live. Pushing all context into the primary artifact usually fails. Primary artifacts have their own constraints: drawings are optimized for manufacturing workflows, source code for execution and local reasoning, API specs for interface stability. When you overload them with context, you make them worse at their primary job—while still failing to preserve what you actually needed.

A sidecar is a structured, diffable container that carries the reading conditions, evidence, and rationale without forcing them into the primary View. It is where you put the pieces that must survive projection but do not naturally fit inside the projection artifact. In mechanical terms, you already do this: inspection instructions, process sheets, and quality records are external to the drawing, but they are part of what makes the drawing actionable. In software, ADRs, schema registries, and data contracts play the same role.

The key property is diffability. A sidecar can be designed to be append-only and structured, so it produces small, readable diffs that capture what changed and why. When diffs are readable, review becomes reliable, agreement becomes durable, and replay becomes practical.

The goal is not to store everything. The goal is to store the minimum that makes a decision replayable: what basis was assumed, what contract was applied, what evidence was accepted, and what change was made to restore admissibility when reality drifted. When that minimum is captured in a diffable form, replay stops being a heroic effort and becomes a routine operation.

---

## Accountability Is Replay, Not Memory

Engineering explanation becomes easy when you can reproduce the path that led to the current shape. Version history matters not as a diary, but as a method to re-run reasoning under the same constraints. When you can replay a decision, you can answer the hard questions without relying on personal credibility: What did we assume? What changed? Was the change within the contract? If not, what was the recovery plan?

A replayable system is one where artifacts cooperate. Code expresses behavior, tests express admissibility, telemetry expresses observation, and sidecars express basis and rationale. Together, they turn accidents into analyzable events and reduce the cost of renegotiation.

This framing also makes "governance" less emotional. Accountability becomes an engineering property: the system is designed so that reasons can be reconstructed. A postmortem that links an outage to a specific contract change and its recorded rationale is easier to trust than one that relies on recollection. Trust is not a personality trait. Checkability is what makes trust practical.

---

## What Remains Beyond Description

Even with strong contracts and perfect history, some parts of design refuse to compress. Craft includes judgment under uncertainty, and judgment includes values: what you optimize, what you tolerate, and what you refuse to ship. Automation can reduce effort, but it does not erase the need to choose conventions and define admissibility. In fact, faster execution makes conventions more important, because misunderstanding spreads faster too.

A clean CAD model is not the end; it is the beginning of projection. The hard work is deciding what must survive projection, and then designing contracts and evidence so that others can act safely. That work is social, temporal, and contextual. It does not disappear just because a tool can generate artifacts quickly.

The point, then, is not to replace humans with artifacts, but to build artifacts that preserve what humans decided. A good projection makes action possible. A good contract makes action safe. A good history makes action explainable. This is the shared discipline I recognize across mechanical drawings, API specifications, and code—that is why “between” matters to me: not as a tool, but as a design stance—one that keeps comparisons possible when many views must coexist.

---

## References

This essay is Episode 00 of the _Reading Technical Bibles_ series: it introduces the lens—projection—that the later episodes will use. The references below are not authorities for the argument; they are optional lenses. ISO 1 is included as a minimal example of pinning a basis (20°C) to make comparison possible; Brooks frames design as deliberate choice under constraints; Evans explains why meaning boundaries demand contracts; Kleppmann maps how comparability breaks when Views multiply in data systems.

- ISO 1101:2017, *Geometrical product specifications (GPS) — Geometrical tolerancing — Tolerances of form, orientation, location and run-out*
- ASME Y14.5-2018, *Dimensioning and Tolerancing*
- ISO 1:2016, *Geometrical product specifications (GPS) — Standard reference temperature for the specification of geometrical and dimensional properties*
- Fred Brooks, *The Design of Design*
- Eric Evans, *Domain-Driven Design*
- Martin Kleppmann, *Designing Data-Intensive Applications*

