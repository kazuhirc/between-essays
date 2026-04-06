# Design as Triage under Constraints

## 1. Accidents Make Design Visible

Steam power is often remembered through inventors and engines. But safe steam was not built by invention alone. It was also built by repeated accidents, by rules for design, fabrication, and inspection, and by the discipline of deciding when work must stop before damage scales. In the United States, a series of boiler explosions—including the 1905 Grover Shoe Factory disaster—drove the development of the first ASME Boiler Code in the 1910s. ASME’s own account presents the code as a response to repeated failures and as a formal set of rules for design, fabrication, and inspection.

That history matters here for one reason. It shows that engineering becomes visible not only in invention, but in failure, where local habit is no longer enough. A code is not merely a record of best practice after the fact. It is a way of deciding what may proceed, what must be checked, and what must stop. This essay starts from that observation.

## 2. What This Essay Adds

The previous essay named the operational distinctions that become necessary once explanation is no longer enough: execution, judgment, gate, evidence, and contract. It argued that work becomes governable only when comparability can be preserved, stopping can occur when assumptions fail, and decisions can cross boundaries without losing their basis. This essay asks a different question. Given those distinctions, what does design actually allocate under constraint?

My answer is that design allocates verification resources. It allocates attention, review time, computational budget, approval authority, and rerun cost. It decides where those resources must be concentrated, where they may be relaxed, where work may remain provisional, and where it must not proceed at all. In that sense, design is not only decision-making under constraints. It is triage under constraints.

## 3. Triage Means Allocation

Triage here is not emergency medicine. It is disciplined allocation under scarcity. In engineering work, scarcity is rarely the scarcity of possible actions. It is the scarcity of trustworthy comparison, replayable basis, available reviewers, and safe stopping points. That is why design begins before optimization. Before a team can choose the best solution, it must decide what is admissible on stable terms, what is still provisional, and what must remain outside the next step.

The first essay argued that 5W1H is useful for narration but weak as structure, and that a more stable basis requires Structure, Dynamics, and Observation, with View treated as projection rather than separate truth. Observation was not optional there. It was part of the minimum architecture because how we know is part of what the system is. The second essay then argued that once work must be rerun, checked, stopped, justified, and handed across boundaries, explanation is no longer enough. A richer operational vocabulary becomes necessary. This essay adds one more step. It asks how scarce verification resources are distributed across those operational distinctions so that they remain workable in practice.

## 4. Inspection Already Contains a Theory of Triage

A practical way to see this is inspection work. Inspection already contains a quiet theory of triage. Before a heavy process begins, someone checks the basis, the setup, the allowable conditions, and the point at which work must not continue. During the process, someone monitors motion, drift, abnormal fluctuation, or load behavior while the process is still reversible. After the process, someone reviews what happened, identifies where the basis failed or where comparison was illegitimate, and decides whether the standard itself must be revised. This is not a decorative wrapper around the real work. It is the work of allocating verification resources across time.

That allocation changes by phase. In pre-process, the scarce resource is not speed but admissibility. The question is whether expensive work should begin at all. Attention is spent on baseline confirmation, condition checking, and stopping authority before cost spreads. In in-process, the scarce resource is reversibility. Monitoring attention and abnormal-stop rights matter because correction is still cheaper than downstream repair. In post-process, the scarce resource is replayability. Review time, preserved records, and revision effort are allocated so that later judgment does not begin from memory alone.

The point is not that engineering is literally inspection. It is that inspection already makes visible how judgment and execution divide labor across time.

|Phase|Field image|Judging side|Executing side|Design question|
|---|---|---|---|---|
|Pre-process|Setup check|fixes the basis of comparison|checks whether execution may begin|should this work start at all|
|Pre-process|Large leak test|detects missing basis or unresolved prerequisites|detects missing authority environment or task fit|where should early stopping occur|
|In-process|Instrument watch|interprets whether drift is meaningful|monitors progress retries load and blockage|where should monitoring attention become denser|
|In-process|Abnormal stop|decides whether work must return to hold|aborts degrades or hands off|when is continuation no longer admissible|
|Post-process|Final inspection|checks whether comparison was legitimate|presents traces usage and execution history|what may now count as acceptable|
|Post-process|Standard revision|updates admissibility conditions|updates operational loops and safeguards|what must be changed before repetition|

The table is not only a process map. It is a map of allocation: where attention must thicken, where stopping authority must sit, and where later return must remain possible.

## 5. Judging and Executing Protect Different Things

Seen this way, the boundary between judging and executing is not a theoretical nicety. The executing side protects flow. The judging side protects meaning. The previous essay already made that distinction explicit: changing execution order is not the same as changing the criteria by which comparability, sufficiency, or completion are judged. The first changes flow. The second changes meaning. When the two are blurred, work may continue while comparability quietly fails.

The present point is that design allocates the scarce resources by which that boundary remains real. It decides where stop authority must sit, where preserved basis is required, how much review must occur before acceptance, and how much cost may be risked before rerun becomes mandatory.

## 6. Partial Admissibility

Because verification resources are scarce, not everything can be fully reviewed immediately. This is why partial admissibility matters. Much work is neither simply accepted nor simply rejected. Some results are visible but not yet comparable. Some are informative but not yet promotable. Some are excluded for now, but indexed so that judgment can later return. The second essay named the operational distinctions at the boundary: gate, evidence, and contract. At that boundary, gate protects what is not yet admissible, evidence preserves what is not yet settled, and contract limits what may count as a legitimate crossing. Triage is the allocation that decides how much of each is required, where, and at whose cost.

## 7. False Continuity

A common failure mode now becomes easier to describe. A process can appear to be running on the same inspection sheet while its basis has already changed. The metrics may look continuous. The workflow may look cleaner. The team may feel that the new state is an improvement. But if the basis of comparison has shifted, the appearance of continuity is false. The work is no longer running on the same sheet in any meaningful sense.

What failed in such cases is not only technical discipline. What failed is triage. False continuity is a triage failure. Basis changed, but stopping authority was not exercised. Replayability was not strengthened. The burden of later repair was pushed forward invisibly. A successful comparison, even when it looks tidy, does not by itself imply correctness, adoption, or legitimacy. When prerequisites change, continuity must not be assumed silently. The cost of not reallocating verification effort appears later, and usually elsewhere.

## 8. Standard Revision Reallocates Responsibility

This is also where standard revision should be understood more sharply. A revised standard is not merely a better description. It is a revised boundary for admissible comparison. Standard revision reallocates what must be checked, where work must pause, and what conditions must now be met before work may count as comparable again. That was one of the deep lessons of boiler code. Rules for design, fabrication, and inspection were not created simply to honor best practice. They were created because repeated failures showed that local memory and scattered expertise were not enough to protect safety at scale.

## 9. AI Sharpens Scarcity

AI makes this sharper, not weaker. The previous essay argued that agent design is better read as boundary design than as a mystery of anthropomorphic action. An agent bundles some combination of execution, judgment, gate handling, evidence preservation, and contractual handoff. The additional point here is about scarcity. AI increases throughput faster than verification capacity scales. Review attention, approval authority, and replay effort do not grow at the same rate as generation, summarization, or automated execution. Weak premises no longer produce occasional local mistakes. They produce fast, distributed mistakes whose repair cost arrives later and elsewhere. The next question is therefore not only what may be automated, but where verification must become denser as speed increases.

This is why design should not be reduced to choosing what to automate. The harder question is where verification resources must thicken as capability rises. Which results may remain at the level of view. Which require human review before comparison. Which may move toward formal adoption. Which should remain excluded but visibly indexed for return. Those are design questions because they determine whether later judgment will still be possible on a shared basis.

## 10. Where the Trilogy Arrives

The trilogy therefore arrives in three steps. The first essay stabilized explanation by giving it firmer coordinates: Structure, Dynamics, Observation, and View. The second named the operational distinctions that make work governable across boundaries: execution, judgment, gate, evidence, and contract. This essay has argued that design sits one level above both. It allocates the scarce resources by which those distinctions remain workable in practice.

Design under constraints is therefore not only the search for a solution. It is the disciplined allocation of what makes later judgment still possible. That is why the lesson visible in boiler code history still matters. Repeated failures did not merely demand stronger machines. They demanded stronger boundaries: boundaries for stopping, inspecting, comparing, and revising before damage scaled further.

The same lesson returns whenever systems become faster, more opaque, and more powerful. Work does not become safer merely because it becomes more capable. It becomes safer when design decides what may proceed, what must stop, what must remain provisional, and what must stay visible so that judgment can later return on the same basis. In that sense, design is triage under constraints.