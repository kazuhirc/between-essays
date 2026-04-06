
# Reading Technical Bibles - The Mythical Man-Month

**Stop the Merge Before Vibe Coding Breaks Comparability**

**Vibe Coding and the Friction of Integration**  
By “vibe coding,” I mean a mode of AI-assisted development where you let an agent produce something that runs quickly, and only later try to “clean it up.” In the short term, it is undeniably fast. Screens render, functions multiply, and a shape that resembles a product appears. Then a different pattern emerges: the same concept name starts to mean different things in different places, and each fix breaks something else. Output increases, yet the feeling of forward progress fades.

This is not primarily a problem of individual capability or effort. It is the friction of integration. Brooks’s Law is often quoted as “adding manpower to a late software project makes it later,” but the claim is structural: what increases is not only work, but boundaries, and boundaries show up as friction at the merge.

In Episode 01 terms, this resembles what happens when multiple measurement setups proliferate before a shared standard is fixed: the discrepancy you see is not random noise, but systematic disagreement across setups. Integration accuracy is not the prettiness of a single output; it is the ability to return to the same conclusion under the same declared conditions.

**Observation 1: The Surgical Team Keeps the Reference Singular**  
The Mythical Man-Month offers a famous metaphor: the surgical team. It describes a division of labor where one role concentrates design decisions and others support that role. The essential point is not hero worship. It is operational: keeping the reference singular, so parallel work does not diverge in meaning.

Many hands can work in parallel if they are all referring to one thing. If the reference splits, more output only accelerates divergence. Vibe coding feels fast because local generation moves forward, but if the reference is already fragmenting, integration will pull you back. The earliest protection is not speed. It is keeping the reference singular.

In the next section, I will name this “the master” (SSOT) and define it explicitly.

**Observation 2: Conceptual Integrity Provides the Master (SSOT) for Meaning**  
Here I will define “the master” (the Single Source of Truth, or SSOT). The master is the single reference for meaning: the unique place you point to when you say “this is what the concept is.” In measurement, the master carries correctness. In design, conceptual consistency carries correctness. Just as multiple instruments must refer to the same standard, multiple implementations must refer to the same concept.

Conceptual integrity plays the role of a datum: without it, “difference” is not a measurement but a dispute.

Brooks names this conceptual integrity. In this reading, conceptual integrity functions as the SSOT for integration. Style guides and naming conventions are downstream effects. The core is that terms, boundaries, inputs and outputs, and success conditions align under one concept.

When that alignment fails, the mismatch appears not as a small bug but as different specifications hiding under the same label. This is why projects slow down: not because “more people are bad,” but because meaning fractures and work becomes non-comparable. AI increases output, so it can increase the speed of fracture unless the master remains singular.

You can phrase the continuity with Episode 0 as a simple correspondence: instrument discrepancy corresponds to integration friction; the measurement master corresponds to the concept master; gauge repeatability corresponds to implementation consistency. This pattern—proliferating systems without a shared reference producing systematic rather than random error—was the central observation in Episode 0.

**The between Move: Turn Observations into a Procedure at the Integration Point**  
The surgical team and conceptual integrity describe a stance: keep the master singular. A stance is not enough. You need a procedure that can be executed at the integration point, repeatedly, by ordinary teams, under time pressure.

This is where the between framing offers a minimal ordering: Gate → Evidence → Contract. This gate is not about bureaucracy or approvals; it is a semantic alignment check against the master.

A Gate is where you stop. Evidence is what counts as proof to move forward. A Contract is the minimal declaration of prerequisites under which that evidence is valid. The order matters. If integration is where comparability breaks, you do not start by writing a complete contract. You start by deciding where you will stop. Once the stop point exists, you can define what proof is required to proceed. Once proof is defined, you can minimize the contract to exactly what that proof depends on.

This is not a story about making the AI “smarter.” It is a story about making merges comparable. When output grows faster than your ability to align meaning, expanding contracts can worsen fracture. A better move is to externalize the stop point and the proof, and keep the contract minimal.

**A Minimal Concrete Example: What to Stop, Right Before the Merge**  
A minimal fictional example works here. An agent generates an authentication module first, then a profile module, then an authorization module. Somewhere along the way, the concept `User` begins to drift. In auth, `User` is an ID and credentials. In profile, `User` is display name and bio. In authorization, `User` is a set of roles and permissions. Each module runs. Then, right before integration, the mismatch surfaces.

This is the moment to place a gate. Ask only three questions.

First, the master. What is `User`, exactly? Choose one master definition as the single reference, and make the others refer to it. The goal is not perfect design. The goal is one reference. If the master is singular, you can improve it later without chasing three competing definitions.

Second, the success condition. What does it mean that “user registration is complete”? State minimal inputs, outputs, and failure conditions in a form that can be compared. If this remains vague, each module will claim success in its own sense, and integration becomes a debate about words.

Third, the evidence. Record the diff and the reason for the decision. You do not need to store every generation trace. You do need to keep the evidence you used: a short decision note, a check result, and the diff that shows what changed. This is what lets you return to the same judgment later.

If the gate fails, do not add more agents. Fix the master first. If the gate passes, generation and implementation can proceed under a shared reference, and you preserve speed without sacrificing integration accuracy.

**Closing: Classics Name the Problem; Procedures Make It Repeatable**  
The Mythical Man-Month can be reread as a book about integration rather than a book about speed. The surgical team is a way to keep the master singular. Conceptual integrity is the SSOT for meaning. In the AI era, output increases first, so friction that resembles instrument discrepancy appears earlier. The response is to place a gate at the integration point, proceed by evidence, and minimize the contract.

If vibe coding is already happening in your environment, pick one integration point and run a small experiment: place a gate there. Classics can name the failure mode. Your procedure can make the remedy repeatable in daily work.

**Postscript**  
This essay does not summarize The Mythical Man-Month. It reads it as a lens for locating where integration breaks comparability, and for externalizing SSOT and procedure. The intended order is Gate → Evidence → Contract. First, place a gate at the integration point. Next, define what evidence allows you to move forward. Finally, minimize the contract to the prerequisites that make that evidence valid. This 3×3 is not a coverage grid; it is a way to choose what to thicken.

I will reuse this grid across the series, thickening only a few cells per episode. The goal is not coverage, but a repeatable way to locate where comparability breaks and what to externalize. In this reading, Brooks’s Law appears primarily as a Gate × Integration problem: when boundaries multiply, the stop criteria at the merge stops functioning, and comparability collapses.

Map as prose

- Axes (rows): Gate / Evidence / Contract
    
- Axes (columns): SSOT (master) / Integration (merge) / Operation (daily work)
    

Cells thickened in this episode

- Contract × SSOT: declare the concept master as the single reference for meaning, preventing name-equals-meaning fracture
    
- Gate × Integration: fix the stop criteria right before the merge, so you can halt before the master splits
    
- Evidence × Integration: keep proof to move forward (diff, short decision note, check result) so you can return to the same judgment
    

Cells left thin on purpose (examples)

- Evidence × SSOT: the history of why the master was defined that way
    
- Gate × Operation: day-to-day criteria for “do not proceed further”
    
- Contract × Operation: the procedure for sharing and updating terms while maintaining the master
    
