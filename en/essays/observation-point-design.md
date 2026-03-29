# Designing Observation Points: Starting from sin(30) to Build Comparability

---

## Introduction: Establishing Comparison Before Producing Values

When driving, you sometimes notice that you don't react to danger by thinking first. The moment you see a pedestrian's movement, oncoming traffic speed, or road surface condition, your hands move to the brake or steering wheel before explanation catches up. There is a prediction that works ahead of reasoning, and "this won't hold as-is" is visible as a bodily sense. Something similar happens in design review. A veteran will glance at a drawing and say "this doesn't hold" before tracing every tolerance. It isn't sharp eyesight—they are placing undrawn premises: fixtures, assembly order, adjustment margins, shop-floor habits. In software, the undrawn premises are implicit environment variables, deploy order, or configuration defaults. Once you place those, the points of failure become literally visible.

Generative AI can produce plausible output fast, yet it sometimes shapes results to look valid even when preconditions are missing. The faster generation gets, the more the bottleneck shifts to review and approval, and the more you need observation points that stop with a reason when something fails to hold.

This article explains how to establish conditions for valid comparison first, and stop with a reason when they are not met. Stopping isn't defensive—it is observation designed to identify the cause and enable learning.

An observation point is "a location where, when comparison cannot be established, the system stops and returns a reason rather than a value." Later sections make this stopping behavior reproducible by fixing a small, structured record of what must be returned when we stop.

---

## 1. Why Excel's sin(30) Is Fragile

When you enter `SIN(30)` in Excel, it silently returns a value. But if it's unclear whether 30 means 30° or 30 radians, that calculation isn't actually valid. Scientific calculators display [D]/[R] precisely to avoid leaving preconditions implicit.

The problem isn't mathematical—it's that computation proceeds while preconditions remain hidden.

What's undefined isn't sine itself, but "30 lacks an angular unit precondition."

---

## 2. Observation Design We Already Do Unconsciously

Most people, seeing `SIN(30)`, instantly expect sin(30°) = 0.5. They detect "something's wrong" by checking if the result is near 0.5. This is unconscious observation design.

For example, detecting via ratio makes anomalies visible even when scale changes.

$$
r=\frac{\lvert y-0.5\rvert}{0.5}
$$

If $r$ stays small, it's fine. If $r$ suddenly grows large, suspicion shifts not to "sine operation is broken" but to "the precondition (deg/rad) is broken."

What matters is deciding "how to detect anomaly" before looking at results.

---

## 3. "Stopping by Design" Helps Locate Causes, Not Just Defense

An observation point is a location where you can stop processing and check "the state up to here." You design places where you can see what's present and what's missing when stopped.

If preconditions are undefined but a value is returned anyway, it mixes into downstream processing and the cause becomes invisible. Without observation points, errors either cancel out and disappear, or amplify and take different forms.

So instead of returning a value, allow "stopping with a reason." Where it stops becomes an observation point. With observation points, the cause is always contained "just before or just after the stop."

---

## 4. Making Implicit Knowledge Explicit as "Sticky Notes" Enables Consistent Stopping

To avoid `SIN(30)` accidents, people mentally do roughly three things:

- Precondition: Is 30 in degrees or radians?
- Ordering: First check preconditions, then verify function specification
- Evidence: Which document, spec, setting, or run record supports this decision?

Writing these as external "sticky notes" means the same input stops for the same reason. The more judgment varies by person, the more value in externalizing.

(Note: These three are external annotations for establishing comparison—precondition, ordering, and evidence.)

---

## 5. Similar to Computer Types, But Different

Computers declare types to limit permitted operations and catch breakage before execution. The "align preconditions, stop if misaligned" approach described here feels similar.

The difference: real data and evidence are semi-formal (including natural language), and external dependencies are unavoidable. So the focus isn't just "types"—it's handling preconditions, external factors, and evidence as a set.

---

## 6. Five Questions for Establishing Comparison

Generalizing so far, establishing comparison requires deciding five things in advance:

1. What to compare?
2. Under which preconditions? (units, time windows, ordering, etc.)
3. What external factors can change results?
4. What to preserve for later tracing?
5. What does the system promise to preserve?

No need to memorize "terminology." What matters is: leaving these five ambiguous breaks comparison.

(Note: For educational purposes, these map to SSOT / basis / effect / evidence / contract)

Here, SSOT does not mean "the only truth." It means the reference master you compare against—the "correct up to here" anchor you can return to.

These five questions serve as lenses for identifying what is missing when comparison fails to hold. An observation point returns the result as gate (approve / hold / reject), reason (why it stopped), ssot (which authoritative source was referenced), and evidence (what trace was preserved)—so a stop becomes inspectable rather than a dead end.

---

## 7. Same Accidents in Different Domains: SQL Preprocessing

The angle story seems small, but SQL preprocessing sees identical structural accidents:

- JOIN duplicates inflate row counts, inflating totals
- Missing value handling changes aggregation results
- Time interpretation or timezone shifts observation windows
- Reference table updates change results

These aren't "SQL is hard"—they're "preconditions and external dependencies were implicit." So the remedy is the same: declare preconditions and external dependencies upfront, preserve evidence, and stop with reason when misaligned.

As generative AI writes more code and queries, these accidents will increase. The more generated artifacts, the more precondition and dependency differences surface, and the more review and approval become the bottleneck. Later sections revisit observation points as "a way of stopping that advances review."

---

## 8. Positioning Relative to Existing Approaches

Data quality tools write assertions against expected values. Contract testing verifies boundary compatibility. These "define what's correct upfront" and validate against it.

What's described here is the preceding layer. Align conditions for comparison (preconditions, external dependencies, evidence) first, and stop with reason if misaligned. Before writing assertions, fix the conditions where assertions hold meaning.

| Layer | Question | Example |
|----|------|-----|
| Establishment | Is comparison even possible? | Are units, reference points, time windows aligned? |
| Validation | Does it match expectations? | Is value within threshold, does schema match? |

The validation layer alone doesn't explain "why mismatch." With the establishment layer, you can distinguish whether mismatch is "missing precondition" or "wrong value."

---

## 9. Aggregation Is Compression—And Irreversible

Another important reality: most processing reduces information. Aggregation is typical—collapsing 100 rows into 1. Irreversibility itself isn't the problem, but if you can't go back, you need a "specification."

The specification requires only four points:

1. What transforms into what
2. What must be preserved (identity, ordering, units, etc.)
3. What may be discarded (acceptable loss)
4. Where to compare (go back to original, or compare after transformation?)

Example: when a SQL query groups sales rows by date to produce daily totals, if you accidentally include sales from November in a monthly rollup or mix different currencies, the total is still computed—but it is no longer comparable to the budget. Violating the "time window" boundary breaks the meaning of the number.

If these four are vague, when difference appears after compression, you can't decide what should differ and what shouldn't.

(Note: corresponds to domain / codomain, invariants, loss budget, compare rule)

---

## 10. "Correct Up to Here" Becomes the Return Path

When people have a correct reference point, observation becomes even stronger. Like holding the expectation 0.5 for `SIN(30)`, "correct up to here" becomes the return path.

Even if stopped at undefined, rather than restoring via inverse operation, you return to the last valid point and distinguish whether precondition, external factor, or compression broke it, then move forward.

Observation points make this round-trip mechanical.

---

## 11. Summary: Undefined Is the Starting Point for Specification and Learning

Two typical ways comparison breaks: external factors leaking across boundaries, and compression (information loss) breaking identity.

Given these, externalize preconditions and evidence, prepare specifications, and stop with reason when misaligned. Undefined isn't exceptional—it's an observation point and improvement starting point.

Three immediately effective practices:

1. Place expected values for critical calculations; detection methods follow domain expertise
2. Preserve conditions (units, time windows, references) in output
3. For irreversible processing, document what to preserve, what to discard, and where to compare before execution

---

## 12. AI and Comparability

Now that AI accelerates generation, the bottleneck has shifted to review and approval. The design described so far—establish conditions for comparison, stop with a reason when they are not met—directly addresses that bottleneck. This isn’t because AI is immature. As generated artifacts multiply, differences in information "boundaries"—preconditions (units, references, ordering), external dependencies (dictionaries, databases, tool versions), irreversible compression (aggregation, normalization)—surface, making comparison and approval difficult for humans.

In other words, the problem's center isn't code volume, but the interface between machine-readable generation and human-readable explanation/accountability.

So rather than automating judgment, mechanize validity checks and explanation to preserve human judgment capacity. Stop at observation points with an explicit "undefined" plus a reason, isolating where the precondition broke.

Machines detect gaps; humans judge meaning. Designing comparability means fixing that boundary as specification. When boundaries are clear, review transforms from "wandering work" to "progressing work."

For me, observation points are not just error checks. They are small, reliable markers that keep a return path visible when many views and assumptions coexist.

---

## Appendix: Terminology (Minimal)

| Concept | Components | Formal Names |
|------|----------|----------|
| Three sticky notes | What condition? / What order? / What evidence? | Precondition / Ordering / Evidence |
| Five questions | What to compare / Preconditions / External factors / What to preserve / Promise | SSOT / basis / effect / evidence / contract |
| Specification 4 points | From what to what / Preserve / Discard / Where to compare | domain/codomain / invariants / loss budget / compare rule |

---
