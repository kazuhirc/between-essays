# **Reading Technical Bibles 05: DDIA — Data Engineering as Comparative Observation**

**0. Data Is Not a Number, but an Observation**
Data engineering is not the art of collecting numbers. It is the craft of making observations comparable. The same failure shows up in spreadsheets, in warehouses, and in distributed systems: results circulate while the assumptions that produced them disappear. Between is a small vocabulary for treating that failure as a design problem. This essay is not a critique of _Designing Data-Intensive Applications_ (DDIA). I use it as a shared reference because it makes "many Views in production" concrete—the setting where comparability becomes a design problem. DDIA has a substantially revised second edition (Kleppmann & Riccomini; O'Reilly, February 2026). That revision only strengthens the premise here: production systems accumulate more Views over time. This essay is edition-agnostic in how it cites the book—I refer to topics rather than chapter numbers.
One sentence: Keeping results comparable is a design problem, not a data problem.

**1. Comparative Measurement: Differences Are Often Conditions**
A kitchen scale has a tare button. You place a container, zero it out, and the display now speaks only about the contents. Nothing about the world changed; you just pinned the basis of comparison. Without that pin, two readings that look comparable may include different hidden offsets, and the discrepancy becomes impossible to attribute—object, method, or assumptions. This is what “basis must be inspectable” means in practice: the offset is not a private detail of the instrument, but a visible part of the reading convention.  A difference is not always an error; it can be a difference in conditions. When context stays invisible, we end up arguing about numbers that were never comparable in the first place.

**2. What "Comparability" Means: An Inspectable Basis**
Comparability is not "we used the same metric." It is "we evaluated on the same footing," in a way others can inspect. When the basis is implicit—or collapsed into a scalar score—outsiders cannot tell whether two results share the same assumptions. Then a performance gap cannot be decomposed into differences in the target, the method, or the basis. The goal is not to dismiss collected data, but to design the basis to be exposed so that comparisons remain meaningful and disputes become diagnosable.

**3. Many Views in Production: DDIA as a Book About Projection**
DDIA can be read as a book about operating with many projections of the same reality. Databases, indexes, caches, streams, materialized views, and derived datasets are all Views: each preserves some properties and drops others. As Views multiply, mismatches in identity, time, ordering, missingness, and retry behavior become unavoidable sources of divergence. The most damaging failures are not "the data is wrong" but "we cannot tell under which assumptions this result was produced." This is my reading of DDIA, not the book's own framing. The next question is: where do these mismatches arise, and what must be designed so that comparability survives?

**4. Why a 3×3 Map Helps: Locating Where Comparability Breaks**
When Views multiply, the breaking points of comparability become hard to locate. In practice, failures cluster in three stages: Observe (intake), Transform (derivation), and Publish (consumption). And at each stage, three things must be made explicit: contract (what is admissible and promised at the boundary), basis (the footing under which interpretation is stable), and evidence (what allows re-inspection later). Putting these together yields a 3×3 map that turns "it doesn't match" into a diagnosable location. It also lets you place DDIA's topics as answers to specific cells rather than as a grab bag of techniques. In the series grid, Basis usually remains implicit inside Contract and Evidence; here it is promoted to its own row because data engineering failures most often trace to invisible footing — time semantics, ordering, identity keys, and related reading conditions — which must be diagnosed separately from what was promised and what was recorded.

_Figure 1. The 3×3 map (topic-level, edition-agnostic)_

|           | Observe (intake)   | Transform (derivation)    | Publish (consumption)   |
|-----------|--------------------|---------------------------|-------------------------|
| Contract  | schema intake      | transactions / quality    | APIs / SLOs             |
| Basis     | encoding / time    | ordering / clocks         | aggregation / time zone |
| Evidence  | raw / provenance   | job defs / reprocessing   | audit / lineage         |

Each cell lists representative topics, not an exhaustive mapping. See Appendix A for a working checklist.

**5. Contract: Boundaries Make Comparisons Possible**
Most breakdowns look like a technical dispute, but start as a boundary dispute: what was accepted, what was allowed, and what was promised. Without an explicit contract, data moves between Views with hidden interpretations, and the first mismatch becomes a debate of "it should be correct." A contract defines admissibility and comparability at the boundary—schema expectations, compatibility rules, error surfaces, and operational promises. Evans' bounded contexts are one concrete instance of this idea, but the point here is broader: every View boundary needs a contract if we want comparisons to be stable rather than rhetorical.

**6. Basis: Fix the Footing, and Make It Inspectable**
Even with a contract, comparisons fail when the footing is invisible. Basis names the reading conditions that make an observation interpretable: time semantics, ordering, identity keys, units, rounding, and retry behavior. These are often treated as implementation details, but they are the comparison itself. If basis stays implicit, you cannot tell whether a difference comes from the object, the method, or the assumptions. Basis must therefore be exposed in an inspectable way, rather than being buried inside a single output number or dashboard. The same basis shows up differently across the pipeline. At Observe, it is time semantics and encoding: what this timestamp means, what this string denotes. At Transform, it is ordering and consistency: which history we treat as real when we merge, retry, and replay. At Publish, it becomes consumer-facing time and freshness: windows, cutoffs, and what “up to date” is allowed to mean. In distributed systems, consistency models—read-your-writes, causal consistency, and their relatives—are part of the basis. They pin what counts as a comparable read by defining which histories, offsets, and reorderings are allowed to disappear from the reading. When those guarantees differ across Views, results computed from “the same metric” are no longer observations on the same footing.

**7. Evidence: Keep a Chain for Re-Inspection**
When something diverges, the real question is not "who is right," but "can we re-inspect what happened." Evidence is the minimal record that makes later inspection possible: inputs, execution conditions, dependency versions, applied normalizations, and the thresholds used for decisions. This is not an argument for hoarding logs; it is an argument for keeping the comparability-relevant facts diffable. Evidence turns disagreements into diagnoses—and diagnoses into inputs for replay.

**8. Sidecar: Externalize Assumptions Without Breaking the View**
("Sidecar" here does not mean the Kubernetes sidecar container pattern; it means a separable, diffable artifact that externalizes basis, contract, and evidence without polluting the primary View.)
A View is optimized for use, not for explanation. If you stuff basis and rationale into the primary dataset or API payload, you often break what the View is for. A sidecar externalizes basis, contract, and evidence as an attached but separable artifact: appendable, structured, and diffable. In data systems, schema registries, data contracts, job metadata, quality rules, ADRs, and incident records are all sidecar-like. The point is not documentation for its own sake; it is keeping comparability auditable without contaminating the View.

**9. Minimal Implementation: Place a Gauge (Go/No-Go for Data)**
A contract becomes real only when it can say “admit or reject.” That decision point is a gate. A gate is the decision; a gauge is the instrument. You cannot stop a pipeline based on a feeling; you stop it based on a measurable signal. A gauge is not a proof of correctness; it is a stable go/no-go signal—more like a pilot lamp than a theorem—good enough to justify a gate.

Comparative measurement in the field ends with a practical need: stable OK/NG decisions under local conditions. That is why shops place go/no-go gauges—known references tested under controlled assumptions—to answer "passes or fails" reliably. Concretely, run a paired "golden dataset + golden query" on the production schedule, in the production environment, and alert on drift. Add a canary pipeline run that exercises the real dependencies, and contract tests that fail fast on incompatibilities.

**10. Replay: Accountability Is Reproducibility**
Accountability is not a claim; it is replayability. Replayability means you can regenerate the result under the same basis and contract, and re-judge it with the same gauge. Logs, backfills, and reprocessing are valuable because they make failure recovery and explanation possible, not because they guarantee correctness. The minimal practice is to bundle reference inputs (golden/canary) with execution conditions (versions, configs, time semantics), version the transformation, and append the reason for reprocessing in the sidecar. Then "it changed" becomes "we can show why."

**11. Closing: The Same Pathology From Excel to Distributed Systems**
What breaks in Excel is not childish; it is the same pathology at smaller scale: invisible footing, drifting versions, evaporating rationale, and diffs that cannot be diagnosed. Between generalizes the intuition of comparative measurement into a discipline for keeping comparability alive when Views multiply. A practical way to start is to place a gauge and run it continuously; once it runs, missing basis, missing contracts, and missing evidence surface as concrete engineering tasks. At that point, the vocabulary stops being theory and becomes a shared language for design conversations.

---

**Postscript**

This episode uses a local 3×3 — Contract / Basis / Evidence × Observe / Transform / Publish — because in data engineering the pipeline stage is the most legible column axis. The series 3×3 — Gate / Evidence / Contract × SSOT / Integration / Operation — remains the shared coordinate. The local map is a nested diagnostic view, not a replacement.

Mapped back to the series grid, the thick cells are Gate × Operation, Evidence × Operation, and Contract × SSOT. Gate × Operation appears in the gauge: a daily go or no go decision that stops drift before it spreads. Evidence × Operation appears in replay, lineage, reprocessing, and the sidecar like chain that lets others re inspect what happened. Contract × SSOT appears at the Observe boundary, where admissibility and schema expectations define what may enter as a comparable observation.

Basis is the internal content that makes those cells inspectable. It is not a separate axis in the series grid, but the declared footing carried through Observe, Transform, and Publish. Thinner here are Gate × Integration and Contract × Integration. They are visible at the edges of the essay, but the main weight is elsewhere, and the boundary question is left for the next move toward bounded contexts.

---

**Appendix A: Re-reading Kit (the 3×3 checklist)**
Use this as a quick way to locate where comparability is breaking.

- **Observe (intake)**
    - **contract:** admissibility rules, missingness policy, schema expectations
    - **basis:** units, time semantics, identity keys
    - **evidence:** raw inputs, acquisition context, timestamps / hashes

- **Transform (derivation)**
    - **contract:** transformation spec, compatibility policy, quality requirements
    - **basis:** rounding, join rules, ordering assumptions, retry / idempotency behavior
    - **evidence:** job definition, dependency versions, applied normalizations, reason for reprocessing

- **Publish (consumption)**
    - **contract:** SLO/SLA, compatibility promises, error surface
    - **basis:** aggregation grain, time zone, visualization conventions
    - **evidence:** release notes, data dictionary, audit logs

**Appendix B. Reading DDIA with the 3×3 Map**
Read each topic as an answer to a specific cell, not as a standalone technique. As you read, ask two questions: (1) where does comparability break—Observe, Transform, or Publish? (2) what is missing—contract, basis, or evidence? Keep a short note mapping topics to cells; the point is not perfect classification, but making "it doesn't match" actionable.

Some examples to seed the habit:

- **Replication lag → [Transform × basis].**
  If replicas return stale reads, the implicit time semantics becomes part of the basis. Without naming it, two "correct" reads are not comparable.

- **Schema evolution (Avro / Protobuf) → [Observe × contract].**
  Intake compatibility rules are a contract. If they are not explicit, data under old and new schemas gets compared as if it were the same observation.

- **Change Data Capture (CDC) → [Publish × evidence].**
  Downstream Views need evidence of "which upstream state" they reflect. Without that, replay and incident diagnosis degrade into guesswork.

- **Consistency models (Linearizability / Serializability / Eventual) → [Transform × basis].**  
  Consistency is an agreement about which history counts. If one View assumes linearizability while another only eventual consistency, they operate on a different basis of time and ordering. Comparing their outputs directly produces phantom discrepancies.

- **Backwards compatibility of published interfaces (API versioning / schema-compat rules / SLOs) → [Publish × contract].**  
  Once a View is consumed by others, compatibility becomes a promise: what changes are allowed, what errors mean, and what latency or freshness is guaranteed. Without that contract, consumers silently shift interpretations, and discrepancies look like “data bugs” rather than broken promises.

- **Data freshness / data SLA (cutoff, completeness) → [Publish × contract].**  
  “Up to date” is not a feeling; it is a contract. If freshness and cutoff rules are implicit, consumers compare values produced under different publishing promises as if they shared the same footing.

---

**References**

- Martin Kleppmann. _Designing Data-Intensive Applications_. O'Reilly Media, 2017. — A substantially revised second edition, co-authored with Chris Riccomini, appeared in 2026.
- Eric Evans. _Domain-Driven Design_. Addison-Wesley, 2003.
- W3C. _PROV-DM: The PROV Data Model_. — For provenance as an inspectable evidence chain.

A companion essay, "Between Mechanics and Software," develops the projection / contract / sidecar vocabulary in the context of mechanical engineering and source code.

Next, I want to apply the same 3×3 to bounded contexts: where “translation” becomes a published promise and starts to drift.  
The practical question is the same: what gauge can we install so a gate can act before replay becomes the only option?