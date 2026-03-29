**Reading Technical Bibles 07: Site Reliability Engineering**

**Prologue**

In Episode 06, I argued that the real cost of "porting a pipeline" is not automation. It is readability: being able to stop with a reason that others can inspect later.
When I opened _Site Reliability Engineering_ (Beyer, Jones, Petoff, Murphy; O'Reilly, 2016), I found the same problem formalized under a different name—reliability. Not as heroics, but as an engineering property: where to stop, what to measure, what to keep, and how to recover.
This episode reads the SRE book as a map of those habits, then asks what it would mean to demand the same properties in paper-and-CAD workflows.
This episode thickens three cells: Gate×Operation, Evidence×Operation, and Contract×SSOT (as "acceptable" in SLI/SLO terms).


**1 Reading the problem SRE was trying to solve**

_Site Reliability Engineering_ is not merely a book about “keeping servers alive.” It is a book about a failure mode that appears when software becomes infrastructure: the system is always on, always changing, and already depended upon. In that world, reliability cannot be a personal virtue. If reliability depends on heroics, the system's success depends on exhaustion.

The book's first move is to shift the unit of discussion. The question is not "How do we avoid all failures?" The question is "How do we keep delivering value while failures remain possible?" That is why the book treats reliability as an engineering property, not a moral standard. The practical consequence is clear: you need explicit stop points for risky change, explicit signals for health, and explicit ways to recover.

A second move is to name what used to be invisible. Operational work is not dismissed, but it is classified. Some work is necessary and meaningful; some is repetitive, reactive, and does not create lasting value. By naming the latter as toil, the book makes it improvable. Once a cost is named, it can be designed out of the system. This is not a Google-sized trick. It is a stance toward work: distinguish what should be automated, what should be standardized, and what must remain judgment.

A third move is to insist on evidence over negotiation. When reliability is debated without shared signals, teams fall back to authority, habit, and fear. The book pushes in the opposite direction: define what "good" looks like in measurable terms, and use those measures to govern both change and recovery. The point is not measurement for its own sake, but checkability: the ability to say why a decision was made, and to revisit it later without reconstructing the whole context from memory.

Read this way, the SRE book is a map of disciplined habits under pressure: stop in the right places, keep signals that others can inspect, and make recovery repeatable. In the next section, we translate those habits into Between vocabulary, so we can ask a blunt question: what would it mean to demand the same properties in paper-and-CAD workflows?


**2 Translating SRE into Between vocabulary**

This section does not summarize SRE. It translates it. The goal is to make SRE's engineering attitude portable across domains by expressing it in a small set of terms.

To make SRE's attitude portable, I restate it as five minimal conditions: Stop (where work must halt), Observe (what signals count), Evidence (what must remain), Replay (whether others can re-inspect later), and Repair (how to restart without negotiation). In Between terms, these map to Gate, Contract, and Evidence as the smallest stable core, with observation, replay, and repair treated as operational consequences that must remain inspectable.

| SRE term (book) | What it means in practice | Between reading | Paper/CAD analogue |
|---|---|---|---|
| SLI / SLO | Define "good" in measurable signals | Observe + Contract | A fixed checklist of observable conditions (revision ID, required fields, required blocks) |
| Error budget | A limit that governs how much risk to take | Gate condition | A "stop rule" that blocks shipment when evidence is missing or drift is detected |
| Incident | A failure that requires coordinated response | Gate trip + scope | A submission failure that halts handoff and triggers a repair loop |
| Postmortem | Learn from failure with evidence | Evidence bundle + replay | Sidecar logs: what failed, why it failed, what changed, and what to prevent next time |
| Toil | Repetitive work that does not compound | Repair cost signal | A category for "manual hunting" work that gates aim to eliminate |
| Automation | Reduce toil, keep humans for judgment | Boundary of responsibility | Scripts that run gates; humans decide intent and trade-offs |
| Change management | Control risky change with signals | Change rehearsal | Before editing, know what must stop and what evidence will be required |

In this reading, an SLI is a projection that makes system state comparable, so the contract is not a slogan but a checkable view.

The translation is deliberately asymmetric. SRE assumes systems that emit signals continuously, while paper-and-CAD workflows emit signals only at handoff. But the structure is the same: stop points prevent silent spread, evidence reduces negotiation, and replayability makes decisions inspectable later.

From this angle, "reliability" is not a property of cloud infrastructure alone. It is a property of any workflow that must survive handoffs, exceptions, and time. The next sections test that claim against two very different environments: a factory lineage that solved parts of it early, and a paper-and-CAD workflow that still lacks a shared contract for stops and evidence.


**3 A factory already had it: TPS as a prior solution**

I see the same failure mode on shop floors. We often have rich measurement data—drift, wear, correction signals—yet decisions still depend on the few people who know when to stop and how to restart. "Industry 4.0" is frequently sold as connectivity and dashboards, but the harder part is making those decisions replayable without heroics. In that sense, the SRE problem is not software-specific.

Toyota Production System is often introduced as a way to make manufacturing efficient. Read through the SRE lens, it looks like something more basic: an early answer to reliability under constraints. The system treats flow as fragile, assumes abnormalities will occur, and designs the line so those abnormalities are seen and contained where they happen.

On the "stop" axis, TPS is explicit. Andon and stop-the-line practices are not about blame; they are about preventing silent spread. A defect that travels becomes a story problem: nobody knows where it entered, and repair turns into negotiation. In TPS, the stop itself is a signal. It forces a local repair loop instead of a late, expensive discovery.

On the "observe" and "evidence" axes, TPS also has a clear bias: make conditions visible and shared. Visual management, standardized work, and 5S are not decorations. They embed information into the environment so that deviations stand out without requiring heroics. Evidence here is not a report; it is a change in the workspace that makes the next move obvious and repeatable.

Where TPS is less explicit—at least in its popular retellings—is replay across time and across boundaries that are not physical. Factories preserve knowledge through layout, fixtures, and routines, but paperwork and design intent can still drift when a job is copied, revised, and handed off. That is where the next section matters: a paper-and-CAD workflow needs the same attitude, but it must encode stops and evidence into artifacts that travel, not only into the shop floor that stays in place.


**4 A paper-and-CAD case: the smallest workable loop**

A paper-and-CAD workflow looks far from cloud systems, but it fails in familiar ways. Context lives in people's heads, artifacts travel without their reasons, and errors spread quietly until they become expensive. The goal here is not integration and not automation. Connectivity is no longer the hard part; the hard part is making evidence and contracts explicit across boundaries. The goal is to make one loop that can stop early, explain itself, and be replayed later.

Start with the sheet. Treat the Excel workbook as a working surface, but require a small gate set before handoff. The first gates are deliberately cheap: required fields, revision ID consistency, and unit declaration or unit mixing. Each gate must fail with an evidence bundle that points to repair without guessing—what is missing, where it should be, and what rule expected it. This is already a poka-yoke move: the sheet is allowed to be messy while you think, but it must become checkable before it travels.

Then do the same for the drawing. Don't argue about geometry first; argue about extractability and reference. A minimal CAD gate set is: required blocks present, title-block revision attributes consistent, and stable extraction from the same DWG. The third gate matters because comparison depends on replay: if extraction drifts, you cannot reliably stop, explain, or repair. Without a stable basis, you end up debating people instead of repairing the artifact. When these gates fail, the evidence bundle must include the extraction conditions, not only the result. In other words, the sidecar should carry not only numbers, but the extraction conditions and steps that produced them—so others can replay the judgment.

Once each side can stop with evidence, you can ship a submission package. Freeze a paper-like view of each artifact (DWG + PDF for the drawing; Excel exported to PDF for the instruction), and attach a sidecar that records gate results and evidence bundles. The sidecar is intentionally plain: it is not an execution system, but a contract and a trace. It reduces negotiation by making "we think it is fine" inspectable later.

Finally, connect the sheet and the drawing without turning them into one system. Add an anchor mapping in the sidecar: the sheet item ID and the drawing placement ID—the balloon number or callout that marks where a part appears. Keep it narrow. The point is not to automate; it is to make the two artifacts refer to the same thing so mismatches can be found and repaired without reconstructing context from memory.

Seen through the same lens, the failure modes here have familiar names in SRE. A mismatch that crosses a boundary often shows up as an incident: the system and its expectations no longer agree. A postmortem is one way to turn "we can't replay why this happened" into evidence that others can inspect.

This is the smallest workable loop: a few gates, a three-piece package, and a minimal anchor. It fits on a desktop and survives paper-centered handoffs. If that feedback loop becomes runnable at the shop-floor level, what used to live in a master's eyes can become a replayable capability of the workflow—and reliability becomes a property of the workflow rather than a heroics of the people.


**Postscript**

This loop is not a device you install once. It is a discipline you keep small enough to run daily.

Thick cells: Gate×Operation, Evidence×Operation, Contract×SSOT.

Thin cells: Gate×Integration (rollout protocols beyond one desk), Evidence×SSOT (full audit-trail design). This episode stays at the single-loop level; scaling across boundaries is a later question.

Re-reading kit: Where does work stop? What makes the stop checkable? What makes the restart replayable?


**Appendix A Pattern map**

This table is a travel guide across domains, not a lecture on any single one.

| Name (domain label) | Core habit (pattern) | Stop point | Evidence that makes it replayable |
|---|---|---|---|
| 5S (manufacturing) | remove friction, make deviations visible | before work starts | layout, shadow boards, standard locations |
| Andon (TPS) | stop-the-line as a shared signal | at the point of abnormality | visible call, local context |
| Poka-yoke | make the right move obvious | before the wrong move spreads | constraint in form or fixture |
| CI (software) | frequent checks keep failures small | before merge/release | build/test logs, conditions |
| CD (software) | keep deliverable state | before shipment | pipeline evidence, artifact snapshots |
| SRE (software) | reliability as engineering | before error budget is exceeded | SLI/SLO, incident records, postmortems |

Each row names a habit that makes "stop / evidence / replay" teachable in its home domain. The point is practical: once you can name the pattern, you can reuse it without importing an entire toolchain or organization model.
