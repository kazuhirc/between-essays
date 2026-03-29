# Industrial Quantities and Procedure Bundles

In mechanical design and dimensional measurement, a measurement is never just a number. It comes packaged with a method, a set of conditions, and a chain of calibration that makes the number meaningful. Remove any of those, and the number floats.

When reading software engineering literature—DRY, KISS, YAGNI, Conway's Law—something familiar appears. These principles read like compressed failure histories, much the way a hardness standard compresses decades of metrology into a short procedure. But somewhere in transmission, the procedure is stripped away, and what remains is a label. The label travels easily; the boundary conditions do not.

Starting from industrial measurement, where the link between value and method is explicit and non-negotiable, the transferable structure becomes visible. From there, the same question can be asked of software principles: what would make them operable rather than repeatable? The viewpoint here is the boundary—looking across it, and noting what appears to transfer.

---

## **1. Opening: Hardness as an Industrial Quantity**

Steel can be a raw material or a blade. A blade earns its function through heat treatment: the same alloy becomes a different tool once its microstructure is driven into a state that can hold an edge. In engineering practice, "hardness" is not treated as a free-standing intrinsic attribute that you read off the material. It is defined as an industrial quantity: a specified indenter geometry, a specified load, a specified dwell time, and a calculation from the resulting indentation. By contrast, Mohs hardness gives an ordering that is useful for identification, but it is not a calibrated quantity that lets distant labs land on the same number.

That definition is not decoration. It is the quantity. The number is inseparable from the procedure bundle that produced it. If you remove the bundle, the remaining value is ambiguous: it no longer tells you what was done to the object, under which assumptions, and under which sequence of operations.

Hardness is a representative industrial quantity. Like roughness or tensile strength, it is defined together with the procedure that produces it. The moment the bundle is fixed, comparability is born—not because the world became simpler, but because the method became shareable. Distant labs can land on the same number only because the procedure is constrained enough to be repeated and checked. Comparability, in short, is an engineered property—not a given.

Note (footnote or reference section): Vickers hardness — ISO 6507-1. Shore hardness — ISO 7619-1 (rubber), ISO 868 (plastics).

---

## **2. The Structure of an Industrial Quantity**

Comparing industrial quantities is not primarily about comparing numbers. It is about confirming that the procedure bundles match. If two measurements share a name but rely on different procedures, they are not the same quantity in the engineering sense—even if they produce values with similar-looking units.

The procedure bundle is not freely chosen. It is constrained by the object's regime. A method that works in one regime may fail to produce a stable, interpretable result in another. For ultra-hard materials, only some indentation methods are feasible because the indenter geometry, load range, and resulting indentation must remain within a measurable range. For elastomers, the response is dominated by viscoelasticity and recovery, so the measurement branches into dedicated scales that control dwell time, indentation depth, and readout conventions to maintain repeatability.

The key structure is therefore not "a value with a unit," but "a quantity with applicability conditions." Applicability is not a footnote; it is the boundary that makes comparison meaningful. Within that boundary, repeated application of the same procedure bundle produces results that can be compared across time, operators, and sites. Outside that boundary, the same label can become an illusion of comparability: you may still get a number, but you no longer know what it means relative to other numbers.

### Fixation block

Three elements that make an industrial quantity comparable:

- **Procedure bundle** — what to measure, how, with what, under which sequence
- **Applicability** — the material regime and conditions under which the bundle is valid
- **Comparability** — values are comparable only within the same bundle and applicability

---

## **3. Bridge: From Quantities to Software Principles**

### Correspondence table

| Industrial quantity | Software principle |
|---|---|
| Reference condition | Scope and invariants |
| Procedure bundle | Decision procedure and boundary design |
| Traceability | Evidence chain and provenance |
| Comparability | Comparable discussions and reviewable changes |

Software principles are also compressed from failure histories. Their original texts carried scope, but scope is often dropped in transmission. What remains is a label—repeatable, but hard to operate.

To treat a principle as engineering rather than slogan, expand it into a procedure bundle: fix applicability, fix observation, and fix a recovery path. This is the same structural move that makes industrial quantities comparable.

A procedure bundle is reproducible only when its provenance is recorded: which version of the method was applied, under which conditions, by whom. Without that chain, comparability is a claim without support. Standards provide shared reference conditions; hardness standards are an instance of this structure, fixing indenter geometry, load, and dwell so that distant labs can land on the same number.

Traceability is not a fourth element. It is not "recording for its own sake," but the discipline that keeps the three elements checkable by someone else, across distance and time.

---

## **4. The between Stance: Principles as Scoped Procedures**

A principle becomes engineering when it is operated as a scoped procedure: you declare where it applies, you declare what you observe, and you declare how you recover when it fails.

Without scope, a principle travels as a name; with scope, it travels as a method. The same three-part structure reappears here: procedure bundle, applicability, and comparability—now phrased as what we declare, what we check, and what we can review.

Before applying a principle, ask:

- What cost does this procedure aim to reduce?
- Which failure mode does it guard against?
- At which layer does it take effect (code, protocol, operations, organization)?

Apply only within the declared scope. Leave evidence—before state and after state—so the application is reviewable by someone who was not present when the decision was made. If the scope cannot be declared, hold: gather more observation before proceeding.

I treat principles as procedures: ask first, apply within scope, leave evidence. I call this framing "between": a minimal way to make assumptions, checks, and evidence explicit.

---

## **5. Concrete Example: DRY as a Procedure Bundle**

The three-part structure (bundle, applicability, comparability) describes when comparison is valid. To make a principle operable, expand it into a five-part card: cost, basis, contract, gate, and evidence.

DRY is often repeated as a slogan: "eliminate duplication." Read as a procedure bundle, it becomes something stricter and more practical. It asks you to define what counts as the same knowledge, to justify why it should change in sync, and to prepare an observation-and-recovery path so the refactoring remains reviewable over time.

The key move is to stop treating DRY as moral advice ("duplication is bad") and start treating it as an operational definition ("this identity must be preserved across changes"). In industrial measurement, comparability is not a property of the number; it is a property of the procedure bundle. DRY works the same way: the outcome is only comparable when the procedure is explicit.

Gate is the decision point; contract checks are its criteria. When DRY is applied without a gate, it becomes a gradual slide into over-abstraction. When DRY is applied without evidence, it becomes an unreviewable refactor story.

### DRY Procedure Bundle Card

| # | Element | Question |
|---|---|---|
| 1 | Cost | What breaks if the bundle is absent (e.g., missed change propagation)? |
| 2 | Basis | What counts as "the same knowledge" (definition of identity)? |
| 3 | Contract | What must stay aligned when the knowledge changes? |
| 4 | Gate | Decision point. Criteria are contract checks. Includes rollback path. |
| 5 | Evidence | Before/after artifacts that make the application reviewable. |

Cost here means failure cost: what breaks when the bundle does not exist. This is distinct from verification cost: what it costs to operate the bundle (reviews, tests, audits). The card starts from failure cost because that is the natural reasoning order, while remaining compatible with the Gate → Evidence → Contract reading order used elsewhere in the series. Verification has a cost, so scope the bundle.

Just as hardness has standard forms (e.g., ISO 6507-1 for Vickers, ISO 868 for Shore), software principles can be given explicit procedure definitions. The card above is one such standard form.

---

## **6. Other Principles as Questions**

The same card structure applies beyond DRY. Below are seed questions—not answers—for a few widely repeated principles. The goal is not to settle debates, but to make applicability explicit before the name travels.

These questions live at different layers (code, protocol, operations, organization). That is exactly why they are easy to apply without checking: a slogan can move across layers without carrying its boundary conditions.

- **KISS** — Which failure mode does this complexity guard against? Which complexity does it introduce in return? Where is the gate that stops simplification from erasing necessary structure?
- **YAGNI** — Who will use it, when, and what is the maintenance cost until then? What evidence would justify building it now rather than later?
- **Leaky Abstractions** — Where does the abstraction leak, and who absorbs the leak (callers, operators, users)? What evidence would show that the leak is now the dominant cost?
- **Conway's Law** — Do responsibility boundaries and design boundaries coincide? If they do not, what failure mode appears first: coordination delays, inconsistent interfaces, or broken ownership?
- **CAP** — Under partition, what do we protect and what do we sacrifice? What is the gate that detects we are in the partitioned regime, and what evidence is required to justify the trade-off?

Each principle can be expanded into its own procedure bundle card: cost, basis, contract, gate, evidence. The point is not to fill every card now, but to establish the habit of asking before applying.

In each case, the question is only useful if it leads to a gate (when to stop) and evidence (what to compare). Otherwise, the principle remains a label that cannot be operated.

---

## **7. Closing: Designing Comparability**

The center of engineering is not choosing the right word, but designing comparability.

Industrial quantities become comparable when the procedure bundle is fixed. Software principles become comparable when applicability, checks, and evidence are fixed—so that two people can review the same change and still land on a shared judgment.

Verification has a cost, so scope it. Review is expensive, testing is expensive, audit is expensive. That is exactly why principles should come with gates and evidence: not as universal laws, but as scoped procedures that can be repeated, checked, and recovered when they fail.

Why premises become invisible once they are fixed is a separate question. (→ "The Cost of the Obvious")

---

## **Related**

This essay treats standards as comparability devices: shared reference conditions plus traceable procedures.

- Reading Technical Bibles 04: Parnas — Information Hiding as a Stop Rule
  (change-likelihood decomposition and DRY identity share the same structure)
