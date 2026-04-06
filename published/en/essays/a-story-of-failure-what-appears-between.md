# A Story of Failure: What Appears Between

## 1. Prologue: Forgetting to Update a Dimension

This happened during a reuse design in 2D CAD.

I only needed to extend the overall length by 10 mm. I selected the outer profile as a rectangle, applied a stretch, and the geometry changed correctly.

But when the drawing reached manufacturing, I got a message: "The dimensions don't match."

The outline layer had been updated, yet the dimension layer was frozen, so the numeric value stayed old. This is easy to miss when you are tired or rushing, when the final verification pass gets thinner.

Was this merely a checking mistake — or a structural issue in a tool where geometry and dimensions live on separate layers and can drift independently?

It felt less like a single slip and more like a failure born at that interface: my attention on one layer, the drawing's truth split across two layers that had drifted apart.

---

## 2. Failures Happen at Boundaries

In the news, you often see phrases like "operator error" or "design error."

But when you look closely, many failures are not caused by a single element. They occur at boundaries.

* across the interface between humans and machines
* along the fault line between design intent and shop-floor interpretation
* in the gap between words and actions

The same structure appears in CAD drawings.

### 2D CAD boundaries

A 2D CAD drawing has multiple layers.

* outline layer: geometry
* dimension layer: dimension values
* text layer: notes
* title block layer: part number and material

Each layer can be edited independently. Changing one does not automatically update the others.

Failure emerges at the boundary between geometry and dimensions.

### Common inconsistencies

Geometry–dimension drift

* the outline moved, but the dimension value did not

Title-block copy-paste errors

* the geometry is for a new part, but the part number remains old

Assembly–detail drawing mismatch

* I updated the assembly drawing but forgot to propagate the change to the detail drawing

These are all consequences of alignment breaking at the boundary.

### 3D CAD can hide a different boundary

3D CAD seems to eliminate some inconsistencies by coupling geometry and dimensions.

But it can also relocate failure to a later boundary — often the one at the interface between design intent and manufacturing reality.

I will unpack that migration in Section 4.

---

## 3. When Alignment Slips

A system works when the right thing is in the right place at the right time.

Failure is what you observe when one of those slips.

### Three axes

Spatial alignment

* not in the right place
* example: hole position, part placement

Temporal alignment

* not at the right time
* example: revision control, forgetting to propagate an update

Semantic alignment

* not the right thing
* example: unit misinterpretation, mismatch across title block and geometry

In my 10 mm stretch mistake, geometry reflected the latest state while the dimensions remained anchored to an older one.

Different times coexisted inside a single drawing — and that split is where the failure became visible.

The next question is practical: when alignment slips, what exactly broke and what does the repair look like?

---

## 4. Learning From Failure as Structure

To learn from failure as structure, it helps to name how transformations break in practice.

I use three tactile modes because they lead to different repairs:

**Missing** — an update or carry-over never happened.

**Mismatch** — two states coexist but disagree across a boundary.

**Non-reproducible** — after the fact, you cannot reconstruct which state or assumption was in effect.

| Mode              | Tactile example                                    | Minimum repair                                                                                      |
| ----------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Missing           | A dimension value did not carry to the new revision | Complete: add the missing value, then pin the revision you consider authoritative                    |
| Mismatch          | Outline says 110, dimension says 100                | Compare on a pinned basis: freeze both states, diff, resolve, then republish as one consistent revision |
| Non-reproducible  | Which revision did we send to the shop floor        | Trace: attach evidence (timestamp, file hash, approval note) so the artifact's identity points to one reconstructable state |

Non-reproducible is often an identity failure: you cannot point to which state the artifact is.

The mode shapes the repair. But detection timing shapes the cost.

This shift is what I call a *night-before structure*: a pattern in which detection is deferred to the last possible boundary, where it collides with the moment when human attention is thinnest — deadlines, fatigue, and compressed review cycles.

Detection drifts later just as human attention decays: fatigue rises, review time compresses, and the cost of a miss spikes.

Fail-fast is simply the opposite time geometry — pull detection earlier so repair stays cheap and local.

In that sense, 5S can operate on the time axis: sort revisions, remove stale intermediate states, and keep one "current" state easy to pin.

### Failure reports are not enough

Failure reports often end with "prevention measures."

* make a checklist
* enforce double-checking
* record changes

These are necessary, but not sufficient.

If you read failures as records of structure, the design of the tool itself becomes visible.

### Parametric design as a partial solution

Modern 3D CAD can couple geometry and dimensions.

If you change geometry, dimensions update automatically. This is a design that automates alignment across layers.

The "forgotten dimension update" that happens in 2D CAD becomes harder to trigger in 3D CAD.

### But the failure only moved

3D CAD can therefore look feasible long before it is buildable.

On screen, the assembly closes and interference checks pass.

Yet fabrication exposes a different class of constraints: the tool cannot reach, there is no space to tighten screws, or the assembly sequence has no valid path.

The failure did not disappear; it moved — and when it moves later, it becomes more expensive and more likely to surface "the night before."

### Failure migration

| Tool          | Boundary where failure emerges        | Typical detection timing |
| ------------- | ------------------------------------- | ------------------------ |
| Hand drafting | geometry–dimension inconsistency      | drawing review           |
| 2D CAD        | inter-layer inconsistency             | drawing review           |
| 3D CAD        | design–manufacturing drift            | fabrication / assembly   |

Even as tools evolve, failures born at boundaries remain, changing form.

### Both 2D and 3D are necessary

This is not a debate about which tool is superior.

2D CAD strength: analytic understanding.
When designing a complex shaft-like part, you draw many cross-sections, like CT slices. Readers can examine each section independently and organize shape changes logically. In 3D CAD you can grasp the whole, but internal structure can be harder to understand. Cutting by sections is an analytic method.

3D CAD strength: feasibility checking.
Feasibility verification is where 3D CAD becomes central. Interference, assembly sequence, overall geometry: these are hard to verify in 2D CAD.

In practice, you use both depending on purpose.

* 2D: structural analysis, manufacturing drawings
* 3D: feasibility verification, assembly drawings

No single tool solves everything. The designer's work is to bridge the gaps across tools.

### Reading as structure

For my drawing mistake:

* slipped axes: space (geometry–dimension position), time (revision drift across layers)
* detection gate: automatic cross-check of dimensions against geometry
* repair: parametric coupling

If you understand this structure, you can evolve the same failure into a system that can observe it.

Failure is not for blame. It is a clue for redesign.

---

## 5. Closing: Toward a Culture of Observing the Between

A failure is not someone's personal fault. It is a fault line where system inconsistency becomes visible.

Across drawings and the shop floor. Across design and manufacturing. Along the seam between one layer and another.

By observing these boundaries, we learn the outline of the system.

Instead of pursuing blame, we look at structure. That is the beginning of a culture of reading what happens between.

---

A senior designer I deeply respected had a rule.

"CAD forbidden. Erasers forbidden. If you make a mistake, start over."

It sounds extreme, but the intent was clear.

When you are wrong, do not delete. Redraw on a new sheet.

The clogged drawing remains as-is.

On the desk, the trial-and-error process accumulates physically. Each attempt is a "failure," but when you place them side by side, the process of exploration becomes visible.

Slightly different approaches to the same problem. Slightly different combinations of parts.

In hindsight, it resembles branching in software development with Git.

By lining up multiple attempts, structures you could not see in a single attempt emerge.

The accumulation of failure produces new ideas.

When I am exploring from zero, or when a design gets stuck, I also close CAD and sketch on a fresh page.

A pale blue 5 mm grid does not insist on anything. It quietly catches ideas.

CAD can erase failures. But if you leave traces on purpose, design becomes an exploration log.

3D CAD can guarantee geometric consistency. But it does not guarantee the process of exploration.

Choosing a tool is a question of what you want to protect.

Failure is a fault line where system inconsistency becomes visible.

And choosing not to erase it — placing multiple trials side by side — returning to blank paper to catch ideas again.

That, too, is part of a culture of observing what happens between.

---

## Figures

### Figure A: Inter-layer inconsistency

```
[Outline layer]
  ●─────●  (geometry: new position)

[Dimension layer]
  ├─ 10 ──┤  (dimension: old value)

↓ inconsistency

Shop floor:
  geometry and dimensions contradict

Caption:
Failure emerges at the boundary called a layer
```

### Figure B: Three axes of alignment

```
Space  ──◯────× (geometry–dimension position drift)
Time   ──◯────× (revision drift across layers)
Meaning──◯────× (title block vs geometry mismatch)

Caption:
The axis where alignment breaks shapes the failure
```

### Figure C: Failure migration

```
[Hand drafting]
  failure: geometry–dimension inconsistency
  detection: drawing review ●

    ↓ to CAD

[2D CAD]
  failure: inter-layer inconsistency
  detection: drawing review ●

    ↓ to 3D

[3D CAD]
  failure: design–manufacturing drift
  detection: fabrication / assembly ●●● (moves later)

Caption:
Even as tools evolve, failures remain by changing form
Detection timing can move later
```

### Figure D: A drawing as an exploration log

```
[Try 1]       [Try 2]       [Try 3]
 ●─●          ●─●          ●─●─●
   └× stuck     └× stuck     └○ done

Keep attempts side by side physically
  ↓
Similar but slightly different shapes become visible
  ↓
A source of new ideas

Caption:
By not erasing failures, the exploration process becomes visible
This resembles Git branches
```

---

## References

* Yotaro Hatamura, *Shippai-gaku no Susume* (An Introduction to Learning From Failure), Kodansha, 2000.
