# Stop Before It Spreads — Placing gates in legacy paper-Excel and 2D CAD

Outline with section titles and opening paragraphs (between-essays style)

---

**0 Prologue The floor that teaches the next move**

5S—sort, set in order, shine, standardize, sustain—often looks like housekeeping, but its effect is not cosmetic. It is a way to embed information into the environment so work can start without friction and errors become visible where they occur. Think of a tool shadow board: the outline on the wall tells anyone where each tool belongs, and the right return becomes obvious without asking or remembering. Cleaning is not for appearance; it is for noticing wear and anomalies early. In that sense, good 5S designs away hesitation. When hesitation disappears, flow appears. The environment itself teaches the next move.

I want to borrow the same attitude for paper-like Excel sheets and legacy 2D CAD: not to "digitize everything," but to decide where work should stop, what evidence should remain, and how the same conclusion can be replayed later.

**1 The field pain paper-like sheets and legacy drawings**

On many shop floors, "Excel documents" and "2D CAD drawings" behave like paper. They are printed, stamped, carried, and treated as the definitive instruction for the next step. The pain comes from a form that looks stable while the meaning is still in someone's head. Required numbers must be typed in by hand, often under time pressure, while each job quietly changes the assumptions behind those numbers.

That gap is where mistakes slip in. Copy-and-paste is not laziness here; it is a survival technique. But it also imports yesterday's context into today's work: a leftover unit, an outdated revision note, a reference that points to a previous order. The sheet still "looks right," so the error travels to inspection, purchasing, or the customer—until it is discovered late, when it is expensive to repair.

This essay treats that late discovery as a design failure. The goal is not to digitize everything or replace the tools. The goal is to decide where work must stop, what evidence must remain, and how a team can return to the same conclusion even after the context has faded.

**2 Three failure modes Missing Mismatch Non reproducible**

Most rework in this setting collapses into three shapes: missing, mismatch, and non reproducible. They look different on the surface, but they all have the same cost: they force a stop late, after the work has already moved on.

Missing means the work stops immediately because something required is absent. A required cell is blank, a title-block field is empty, or a drawing is missing a block that downstream steps assume exists. The fix is usually simple, but the interruption is not: someone must go back, reconstruct context, and fill what was never written down.

Mismatch means the work keeps moving while meaning drifts underneath. A revision ID differs between sheet and drawing, units are mixed, or a reference number points to the wrong part. Nothing "crashes," so the error travels. The team then spends time hunting for the first point where the story stopped matching.

Non reproducible means the same input does not lead to the same conclusion. A check passes on one machine but fails on another, a manual step depends on memory, or a file opens "fine" but yields a different result after re-export. Even in Excel, the same sheet can produce different numbers when the environment differs. At that point, the discussion returns to people—authority, habit, and "it worked last time"—because the process cannot explain itself. These modes share a common failure: the process cannot explain itself. That is why the later sections insist on a sidecar—so the stop comes with evidence, not with negotiation.

**3 Stop before it spreads Gates and evidence bundles**

Manufacturing has a familiar word for "don't let errors flow": poka-yoke. In documentation work, we cannot always prevent wrong input at the moment of entry. What we can do is decide where work must stop before a mistake spreads to the next person, the next file, or the next revision. That decision is design.

A gate is that designed stop point. It is a small, explicit check that runs before handoff, and it does not negotiate. When it fails, it must fail with an explanation, not just a red mark. The output is an evidence bundle: the minimum set of facts that lets someone repair the issue without guessing. It answers three questions: what is missing, where it should be, and what rule expected it—so a repair can be rehearsed before it is applied.

A gate is not a proof of perfection. It is the smallest fence that blocks embarrassing failures from leaking downstream. If the gate is reliable, it changes the tone of review. Review stops being a hunt for typos and becomes a check of intent. And when a shop can stop with a reason, it can resume with a clear repair path.  
  
**4 Excel first The smallest gate set for sheets**

In practice, the benefit can be much smaller—and that is enough. Before a cynical reviewer points out a careless mistake, you run one command and get a specific failure report. That alone reduces the wear of the night before submission, and lets tomorrow's self return to the same conclusion.

Start with Excel, because it is where assumptions are compressed into numbers. The goal is not to prove correctness but to stop early and point to the repair. A practical first gate set is three checks: required fields, revision ID consistency, and unit declaration (or unit mixing). Each check should produce an evidence bundle an operator can act on.

**5 CAD next The smallest gate set for drawings**

Then do the same in 2D CAD. In legacy 2D CAD, the failure is rarely "the geometry is wrong" in an abstract sense. It is that the drawing is missing a required block, a title attribute is blank, or the view you thought you were checking is not the view the next person will use. The work looks finished, but the handoff is not.

So the first gates in CAD should be boring and mechanical. They should not try to judge design intent. They should only stop the common ways drawings become unreviewable or unreplayable.

A practical smallest gate set is three checks.

First, required objects. Verify that the expected blocks exist (view anchors, title block, viewpoint markers), and that required attributes are present. Fail with a list: what block or attribute is missing, where it was expected, and which rule required it.

Second, revision identity. Ensure the revision ID is consistent across the places your shop treats as authoritative: the filename suffix, the title-block attribute, and any revision table text. The goal is not "one true source" on day one. The goal is to stop silent drift and force the mismatch to become visible.

Third, replayable extraction. Run the same extraction step your downstream tools rely on—block names, coordinates, attributes—and make it deterministic. If the extraction depends on window state, layer filters, or manual selection, treat that as a failure mode and record the conditions. A gate here is: "given this DWG, this extractor produces the same result set and the same log."

These three checks do not guarantee a correct drawing. They guarantee a drawing that can be checked. Once a drawing is checkable, later gates—difference checks, cross-reference validation—can be added without changing the contract.

**6 The submission package Ship something replayable**

In these paper-centered workflows, "delivery" is not deployment. It is a submission package: a result you can hand off, review, file, and replay later. The point is not speed for its own sake. The point is that, when something is questioned a week later—or a year later—you can return to the same conclusion without reconstructing the whole context from memory.

A submission package has three parts.

First, the finalized drawing: the DWG as the working source and a PDF as the paper-like view that travels well. The PDF is not "more correct," but it freezes a view boundary: what was meant to be read.

Second, the finalized inspection instruction: the Excel sheet exported to PDF. Again, the PDF is a snapshot, not a replacement. It is the form that downstream work can trust without inheriting your workbook's hidden dependencies.

Third, the sidecar. This is the part that makes the package replayable. The sidecar records the gate results and the evidence bundles: what was checked, under which conditions, what failed, and what action was taken. It also records the small identifiers that connect artifacts—revision ID, drawing number, sheet ID—and, if present, any anchor mapping.

The sidecar is intentionally plain. It is not an execution system or an automation layer—it is a contract and a trace: enough structure that the next person who opens the package can understand why it is considered deliverable.

With this three-piece package, you can stay in a paper-centered culture and still gain a modern property: the ability to replay a decision. You only need to decide what must stop and what evidence must remain—and later, how the pieces will be tied together. The sidecar is where “we think it is fine” becomes checkable: it reduces negotiation by keeping the reasons for stops and the evidence for restarts.

**7 Integration later Anchors as the minimal bridge**

Do not start by integrating Excel and CAD. Start by letting each side become replayable on its own. Once you can stop with a reason and keep evidence inside each tool, the remaining gap is smaller than it looks. At that point, integration is no longer "make them talk." It is "make them refer to the same thing."

An anchor is that smallest shared reference. It is a stable ID that both artifacts can point to: a line item in the sheet and the corresponding element in the drawing. The anchor does not need to describe geometry, dependencies, or intent. It only needs to survive copy, export, and handoff, so later you can say, "this number and this callout were meant to match."

Keep the first anchor mapping deliberately narrow. For example, pair a sheet item ID with a drawing placement ID—the balloon number or callout that marks where a part appears: the row that defines a requirement, and the block instance that realizes it. Store the mapping in the sidecar, not in a complex database. The goal is not automation; it is alignment. When the same anchor appears in both the sheet package and the drawing package, a reviewer can compare without guessing, and a repair can target the right place without reopening the whole context.

Anchors are how "paper-like" artifacts become comparable without becoming one system. They make it possible to ship a package where the sheet and the drawing are separate, yet still belong to the same story.

**8 First step Make one gate real**

The first step is deliberately small: decide where the required-fields list lives, decide what counts as a revision ID (a filename suffix, a title-block attribute, or a header cell in the Excel sheet), and make one gate that always produces an evidence bundle. When a shop can stop with a reason, it can restart without argument—and that is the beginning of a loop.

---

**Appendix A Timeline Stop the line as a transferable pattern**

This appendix is a reading guide, not a claim of a single origin. It lists moments when "stop the line," "mistake-proof," and "keep deliverability" became teachable and transferable across domains. The purpose is practical: once you see the lineage, you can reuse patterns without importing entire toolchains.

| Era or year | Added idea | What it stops | What it keeps as evidence |
|---:|---|---|---|
| early 1900s | Jidoka (automation with stop) | Abnormal work from continuing "as if normal" | A visible stop and its trigger condition (the "why we stopped"). ([Lean Enterprise Institute](https://www.lean.org/lexicon-terms/jidoka/)) |
| 1960s–1980s | Poka-yoke (mistake-proofing) | Human attention as the last line of defense | A device or constraint that makes the correct action obvious (and the wrong action harder). ([ASQ](https://asq.org/quality-resources/articles/apply-poka-yoke-devices-now-to-eliminate-defects)) |
| 1978 (JP) / 1988 (EN) | TPS as a teachable system (book form) | Local fixes that don't change the system | A shared language for flow, stop, and responsibility, so improvement can be replayed across teams. ([Routledge](https://www.routledge.com/Toyota-Production-System-Beyond-Large-Scale-Production/Ohno/p/book/9780915299140)) |
| 1996 | Lean Thinking (value / waste) | "Busy work" that hides delays and rework | A named frame for waste and value, so you can point to friction instead of blaming people. ([Amazon](https://www.amazon.com/Lean-Thinking-Banish-Create-Corporation/dp/0684810352)) |
| 1999 | Continuous Integration as an XP practice | Large-batch integration surprises | A repeatable integration check that runs frequently enough to keep failures small. ([ACM Digital Library](https://dl.acm.org/doi/abs/10.5555/318762)) |
| 2010 | Continuous Delivery (book form) | Release as a rare, fragile event | A pipeline model that records whether the current state is releasable, and the conditions that make it so. ([Amazon](https://www.amazon.co.jp/-/en/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912)) |
| 2018 | Accelerate (research-backed measures) | "Speed vs stability" as a trade-off excuse | Four key metrics that make delivery improvement measurable and comparable. ([IT Revolution](https://myresources.itrevolution.com/id006657092/Accelerate)) |
| 2021 | The DevOps Handbook (2nd ed.) | DevOps as "culture talk" only | A pattern vocabulary (flow, feedback, continual learning) that makes improvement auditable across teams. ([IT Revolution](https://myresources.itrevolution.com/id006657007/DevOps-Handbook-The)) |

---
