**Reading Technical Bibles 06: The Andon in Your CI**

**Section 0 Prologue Mismatch Turns Into Inventory**

The most troublesome thing in the field is not that something is broken, but that it keeps flowing as if nothing were wrong. A sense that something is off is pushed downstream, rework is pushed to another team, and the cause evaporates into "since when has it been like this?" By the time someone finally notices, it has already grown into a size that is hard to repair.

The excess inventory Taiichi Ohno fought was not simply a warehouse filled with parts. In this essay, "inventory" does not mean safety stock in general; it means feedback delay produced by overproduction and work-in-progress accumulation. Producing too much postpones inspection, and mismatch spreads.

What this essay wants to look at is not which production method is superior, but how "the ability to stop" became industrialized. To stop is not an act of courage or grit; it is to design a stopping point that triggers on the fact of abnormality. Once you can stop, the scope of repair becomes smaller, and improvement becomes repeatable.

This essay re-places the genealogy of stop rules on a 3×3 map, thickening Gate×Operation and Evidence×Operation, while connecting Pull as Contract×Integration.

**Section 1 The Problem Ohno Tried to Solve**

As noted in the Prologue, overproduction and accumulated WIP delay feedback, making it harder for mismatch to surface while it is still small. What is distinctive about Ohno's approach is that he did not send this situation back to "work harder" or "fix it locally." He built a language that makes problems visible as problems, and an operational form that keeps them visible. He redesigned how the field is seen, so that abnormalities do not become reasons to "deal with it later," but reasons to "stop and repair now."

The strength of TPS is not a bundle of techniques, but that it distributed vocabulary for flow, stopping, and responsibility to the field. The phrasing "the next process is the customer" is a minimal language for placing acceptance conditions at the boundary and transforming flow into agreement. When the language is shared, improvement can be repeated as an operation others can replay, rather than remaining as a particular person's intuition.

In this section, we read TPS not as a method for efficiency, but as a language for designing stops, detection, and repair unit size. In the next section, we look at Pull and Kanban as the boundary-level form of that language.

**Section 2 Pull Is a Contract, Kanban Is a Signal**

Pull is an agreement that defines acceptance conditions upstream, so that only what satisfies those conditions is allowed to flow. The point here is not controlling quantity or sequence, but fixing acceptance conditions at the process boundary. Once conditions are fixed at the boundary, what is "allowed through" and what is "not allowed through" becomes visible outside the individual worker's head.

Kanban is the signal that carries those acceptance conditions. It is not merely a tag; it functions as an interface that expresses the next process's acceptance state and demand. With Kanban, requests propagate in an observable form rather than as verbal requests or implicit expectations, and work proceeds along agreed boundary conditions rather than personal memory or goodwill.

This structure has one consequence. Once acceptance conditions are externalized, unmet conditions become detectable as a difference. Kanban makes the boundary between "accept" and "do not accept" visible on the shop floor. We do not stop here yet, but we create the grounds on which stopping can be justified. This is not limited to factories: API input constraints and schema compatibility checks are the same operation of fixing acceptance conditions at a boundary.

In this section, we covered defining acceptance conditions as a contract and propagating them as a signal. In the next section, we address how to stop when a difference appears, and how to keep the reason in a shared field of view.

**Section 3 Jidoka and the Stop Reason**

Jidoka is a designed stop that prevents abnormality from flowing onward as if it were normal. Stopping is not an act that depends on individual courage; it is an operational gate that makes continued work impossible at the moment abnormality appears as a fact. The key point is that the stop is executed by devices and procedures, not by negotiation.

Andon is the device that attaches a reason to that stop. It does not merely show "red," but presents, in short words, what happened at which process, in a shared field of view. For example, when a cord is pulled, the line stops, the board shows the process and the reason, and the defective workpiece or fixture state remains at the station, the next person can re-inspect the situation even if they were not the original operator. Here, Evidence is not "record-keeping," but "the stop's grounds remaining legible."

A stop does not complete itself; it is always paired with a recovery design. A gate is a point that stops, and at the same time a boundary that decides where to return. Evidence is the bundle of references that supports that decision. Whether stopping becomes sustainable as an operation depends on whether what happens after stopping has been designed.

The conclusion of this section is that the value of stopping is not "increasing the number of reds," but making stops legible with reasons. When reasons are shared, stopping is less likely to become the start of blame, and more likely to become the start of repair. In the next section, we address small batches and fast feedback as the conditions that make stopping a daily operation by shrinking the repair unit.

**Section 4 Small Batches and Fast Feedback**

Small batches are often described as a technique for speed, but their primary effect is to shrink the repair unit. Batch size is the amount you let flow as a lump, and the larger the lump, the longer the distance between "where it broke" and "where it becomes visible." As that distance grows, localization becomes harder, and repair turns from a local fix into a wider redo.

Small batches shorten that distance. When the unit that moves between processes is small, abnormality surfaces earlier and contaminates less. Stops may happen more often, but what you have to roll back is smaller, so stopping becomes a daily operation rather than a heavy decision.

In that sense, small batches increase the density of gates. This does not mean adding devices; it means cutting the boundary between detection and repair into finer increments. The finer the increments, the more often you can catch mismatch while it is still cheap to repair.

In the next section, the essay moves to the software side. The point is not a neat one-to-one correspondence, but the cost of migration: what becomes stronger, and what tends to become weaker, when "stop rules" are implemented as digital gates.

**Section 5 From Factory Signals to CI/CD Gates**

Migration changes one thing that matters: stopping can become stronger, while the reason for stopping becomes harder to read. If this stays vague, the mapping looks clean but does not reach the pain of the field.

Consider a familiar scene. A customer says, "it crashes sometimes," and you cannot reproduce it. Logs exist, but the crucial line is missing, or buried under noise. There is no handover, the assumptions behind the behavior are not shared, and you are told to "investigate." The suffering is often not the bug itself, but the prolonged state where no one can re-inspect the issue under the same premises.

Factory stops were designed to reduce that state. When Andon turns red, it does not only announce that something stopped; it places a short reason in a shared field of view. Red and the reason live in the same place, so even a non-participant can form the next step. Stopping is less likely to become the start of blame, and more likely to become the start of repair.

Software has a minimal model of "stop and return a reason." HTTP status codes such as 404 or 503 do not end failure as a binary; they return a short identifier for the type of failure. The code does not repair anything by itself, but it narrows where to look next and reduces pointless search. In that sense, it is close to a reason tag.

CI/CD red often fails to reach even this minimal model. The stop is shared, but the reason does not become a short tag like "which acceptance condition failed." It is buried in logs. Automation makes stopping easier, but it does not automatically make stop reasons legible. This asymmetry makes red carry only the fact of stopping, while increasing the cost for others to excavate the reason.

What is needed is not more gates. What is needed is that a stop returns a short reason. Concretely, the failure should surface as a readable tag of which acceptance condition failed, while the grounds are bundled as references you can dig into. This two-layer split mirrors what Andon achieved by separating red, a reason tag, and the physical trace at the station.

Legible stops protect people. They reduce nights spent on non-reproducible failures, reduce the burden of inheriting opaque behavior, and reduce situations where someone is blamed under thin evidence. The point of migrating stop rules from factory to CI/CD is not stopping itself, but keeping stop reasons shareable.

**Postscript Thick Cells and Thin Cells**

With the landing confirmed, this postscript fixes which cells were thickened and which were left thin. The thick cells in this episode are Gate×Operation, Evidence×Operation, and Contract×Integration. Contract×SSOT, the primary definition of acceptance conditions themselves, is left thin on purpose: Ohno's original text carries that role, while this episode prioritizes the diachronic structure of the genealogy.

Re-reading kit: when you scan the tables, read "What it stops" as the Gate×Operation question (which mismatch is prevented from spreading), and read "What it keeps as evidence" as the Evidence×Operation question (what remains legible enough to support re-inspection).

The work that keeps a constrained field running is creative, but it often stays unnamed. Naming it—gates, evidence bundles, sidecars—is already a step toward making it shareable, checkable, and worth improving.

A pipeline, then, is not a device you install once. It is something you cultivate: adjusting where to stop, what to name as a reason, and which evidence to keep. In that sense, it is closer to Kaizen than to automation.


**Appendix Genealogy of Stops as Devices**

The Appendix table is not a summary of the five sections. It is a guide line: a time-ordered placement that helps you see how similar pressures can converge toward similar stop rules, without claiming strict one-way causality. Core rows are limited to devices directly discussed in the main text; extended rows supply surrounding context as swap candidates.

**Appendix A Core timeline**

| Era or year | Added idea | What it stops from spreading | What it keeps as evidence |
|--:|---|---|---|
| early 1900s– | Jidoka and Andon | Abnormal work continuing "as if normal" | The stop itself, plus the trigger condition (why we stopped) |
| 1978 (JP) / 1988 (EN) | TPS as a teachable system (book form) | Local fixes that do not change the system | Shared vocabulary for flow, stop, and responsibility (so improvement can be replayed) |
| 1999 | Continuous Integration as an XP practice | Large-batch integration surprises | A repeatable integration check that runs frequently enough to keep failures small |
| 2010 | Continuous Delivery (pipeline model) | Release as a rare, fragile event | The conditions for "releasable now," and the recorded results over time |

**Appendix B Extended timeline (swap candidates)**

| Era or year | Added idea | What it stops from spreading | What it keeps as evidence |
|--:|---|---|---|
| mid-1950s–1960s | Pull and Kanban as a signal | Acceptance conditions drifting by local interpretation | Acceptance conditions carried as a visible signal (what can be accepted, by whom) |
| 1960s–1980s | Poka-yoke (mistake-proofing) | "Human attention as the last line of defense" failures | Constraints/devices that make correct action obvious and mistakes harder |
| 1996 | Lean Thinking (value / waste) | "Busy work" masking delay and rework | A named frame for waste vs value, to point to friction without blaming people |
| 2018 | Accelerate (research-backed measures) | "Speed vs stability" as a trade-off excuse | Comparable metrics that make improvement measurable |
| 2021 | The DevOps Handbook (2nd ed.) | Improvement collapsing into culture talk only | A pattern vocabulary (flow, feedback, continual learning) that stays auditable |

**Mini glossary JP–EN**

| JP | EN |
|---|---|
| 不整合 | mismatch |
| 契約 | contract |
| 受入条件 | acceptance conditions |
| 停止点 | gate |
| 証拠 | evidence |
| 停止理由 | reason for stop |
| 自働化 | jidoka |
| 行灯 | andon |
| 引き取り | pull |
| 看板 | kanban |
| 小ロット | small batch |
| 継続的インテグレーション | continuous integration |
| 継続的デリバリー | continuous delivery |
