# Reading Technical Bibles 08: Norman — Who Is This Design For

**Prologue**

When people ask what design is, the discussion quickly becomes abstract. We speak of elegance, usability, performance, robustness. None of these are wrong, but they are still one step removed from the pressure many engineers now feel in practice. The bottleneck is no longer where it used to be. For a long time, software work appeared to be constrained mainly by implementation: who could write the code, how fast it could be produced, how much detail could be carried from idea to artifact. But as LLMs lower the cost of implementation, the pressure shifts elsewhere. What matters more now is not only what can be written, but what can be read, what can be trusted, and where a system should allow us to proceed or force us to stop.

This is why Norman is useful here, not as a topic in itself, but as a lens. His vocabulary — signifier, feedback, conceptual model, constraint — helps us notice that design is not only about making things function, but about making the next step legible. Read this way, these are not just principles of usability. They are clues for thinking about boundary design: what should be visible, what should be hidden, and where interpretation should become stable enough for action.

This essay asks a narrower question: who is this design for, once the reader expands beyond the end user. Read this way, Norman becomes less a theory of usability alone than a lens for judgment surfaces: what a system makes visible, what it keeps internal, and where different readers are allowed to proceed or forced to stop.


**Section 1 — Where the bottleneck moved**

For a long time, the visible constraint in software work was implementation. Who could write the code, how quickly it could be produced, how reliably it could be turned from idea into artifact. Skill in writing was the apparent bottleneck, and much of our vocabulary for design grew around that constraint: abstraction, modularity, naming, coupling, performance. All of these matter. But the narrowest point in the system has been shifting.

LLMs now produce implementation at a speed and volume that would have seemed unreasonable a few years ago. Refactorings, wrappers, tests, even entire modules appear in minutes. The cost of writing has dropped. But the cost of reading has not dropped with it. If anything, reading has become harder, because the volume of output that must be reviewed, verified, and either accepted or rejected has increased while the capacity for human judgment has not.

This means the bottleneck is moving from implementation toward review, verification, and consent. The harder question is increasingly not "can we write this" but "can we read this," "where should we stop," "what counts as evidence that this is correct," and "who is responsible for the judgment that lets it proceed." These are design questions, but they appear earlier than the artifact and closer to the act of reading.


**Section 2 — Design happens before code becomes the artifact**

Code still looks like the main artifact of software work. But many of the most consequential design decisions are made before code becomes the center of attention, and they continue to matter long after the code is written. Before code becomes the artifact, design decides what will count as a readable surface. What is exposed as an interface. What is hidden behind it. Which states are observable. Which logs count as evidence. Which error messages help the next person locate the problem. Which view is meant for a user, which for an operator, which for a reviewer, and which for a future maintainer.

These are reading surfaces. An interface is a reading surface. So is an error message. So is a diff in code review. So is a dashboard. So is a log stream. So is a permission prompt. They are not secondary decorations added after the "real" design is done. They are part of the design itself, because they determine what can be seen, where action can be stopped, and what can later count as justification.

The distinction matters because it reframes what design is responsible for. If design is only about making a program work, then the artifact is the endpoint. But if design is also about making the program readable and operable by different people in different roles, then the reading surfaces are not additions to the design — they are the design's primary interface with judgment. The code is the visible result. The design is the prior decision about how judgment will be distributed.


**Section 3 — Norman as a lens for judgment surfaces**

By judgment surface I mean the part of a system that tells a reader what can be done next, what must be checked, and what counts as a result. The interest here is not to explain Norman's vocabulary one by one. It is to ask how a judgment surface is designed, and to use his concepts as tools for that question.

A signifier, in Norman's sense, is whatever tells someone what action is available. A door handle shaped for pulling signals "pull here." A flat plate signals "push." When the signifier is wrong — a pull handle on a door that must be pushed — the reader misreads the situation and acts incorrectly. This is Norman's most famous observation, and it transfers directly. In Between terms, a signifier is a judgment surface placed at a gate: it tells the reader what the next valid action is, and when the signifier is absent or misleading, the reader cannot stop at the right moment. The door with the wrong handle is a gate that fails to function. The reader passes through incorrectly, not because they lack skill, but because the surface did not carry the information needed for the next decision.

Feedback is what makes the consequence of an action observable. A light switch that clicks but produces no visible change in a distant room leaves the actor uncertain. Norman treats this as a design failure: the system acted, but the result was not returned to the person who needs it. In Between terms, feedback is evidence made available at the speed the next judgment requires. A CI pipeline that runs but returns only "pass" or "fail" without a legible reason is feedback without evidence. The action completed, but the reading surface does not support the next decision. Not every response counts as feedback in this sense. It becomes feedback only when it returns quickly and clearly enough to support the next judgment.

A conceptual model is the expectation of how a system works. When a user's model matches the designer's model, the system feels predictable. When they diverge, the user is surprised by correct behavior, or worse, unsurprised by incorrect behavior. In Between terms, this is a shared contract: an alignment of expectation across a boundary. The contract does not need to be explicit or formal. It needs to be stable enough that the reader's prediction and the system's behavior do not silently diverge.

Read this way, signifier, feedback, and conceptual model are not three separate principles. They are three aspects of a single design problem: how to make a boundary legible enough for the next person to act, stop, or verify.


**Section 4 — To hide is to protect attention**

Norman's fourth concept, constraint, is about making incorrect actions structurally impossible. A USB plug that only fits one way is a constraint. A form that grays out a submit button until required fields are filled is a constraint. The purpose is not to restrict the user but to close off transitions that would lead to states the system cannot recover from, or that the user cannot diagnose.

This is where the verb "to hide" becomes interesting. In software design, hiding is often discussed as if it were about secrecy: implementation details are hidden so that external code does not depend on them. Ep04 read information hiding as containment of change propagation. Norman shifts the same verb toward the protection of attention. The boundary remains; the beneficiary changes. What is hidden is not hidden because it is secret, but because exposing it would overload the reader's capacity to act on what matters.

Both readings share a structural claim: a boundary is designed by what it does not let through. In Between terms, both are gate design — the decision about what crosses a boundary and what does not. The difference is which cost the gate is trying to contain: the cost of change propagation, or the cost of attention.

This means that hiding is not the absence of design. It is one of the most deliberate design acts available. Every interface, every abstraction, every dashboard that omits certain metrics, every log level that filters certain events — each of these is a decision about whose attention is being protected and at what cost. When the decision is made well, the reader sees what they need and is not distracted by what they do not. When the decision is made poorly, the reader either drowns in irrelevant detail or misses the signal that should have prompted a stop.


**Section 5 — Who is the design for**

Norman wrote primarily about end users. The person who opens a door, adjusts a thermostat, operates a stove. His central concern was that designers too often build for themselves or for the technology, rather than for the person who must actually use the result. This concern remains valid. But in software systems, the end user is only one of the readers the design must serve.

A reviewer reads diffs, pull request descriptions, and test results. Their judgment surface is not the running application but the change itself: what was modified, why, and whether the modification is safe to merge. An operator reads dashboards, alerts, and log streams. Their judgment surface is the system's current state: what is running, what has changed, what is approaching a threshold. A maintainer reads dependency graphs, module boundaries, and documentation. Their judgment surface is the system's structure: what can be changed safely, what is coupled, where a modification will propagate. A future maintainer — the person who must maintain a system they did not build — reads all of these, often without the context that made the original decisions legible.

Each of these readers needs a different judgment surface. The signifier that helps a user ("click here to proceed") is not the signifier that helps a reviewer ("this diff changes the authentication boundary"). The feedback that helps an operator ("response time exceeded threshold") is not the feedback that helps a maintainer ("this module has been modified by four teams in the last quarter"). The conceptual model that helps a user ("this app saves my work automatically") is not the conceptual model that helps a future maintainer ("this system assumes a single-region deployment").

Norman's question — who is this design for — does not have a single answer. Design quality depends not only on how well a system serves the end user, but on how well it distributes legible judgment surfaces to the readers who must act on it, stop it, verify it, or hand it forward.


**Section 6 — Design as the allocation of judgment, burden, and responsibility**

If design is read as the distribution of judgment surfaces, then its quality is not only about whether the artifact works. It is about whether the right people can see the right things at the right time, and whether dangerous steps can be stopped before they propagate.

This reframes design as an allocation problem. Three things are being allocated. First, judgment: what must be decided, by whom, and on the basis of what evidence. A well-designed system does not eliminate judgment; it places judgment where it can be exercised with adequate information. Second, burden: what must be read, how much must be held in attention, and what is filtered away. A well-designed system does not reduce burden to zero; it distributes burden so that each reader carries only what is relevant to their role. Third, responsibility: what happens when something is not stopped, who is accountable, and what evidence exists for retrospection. A well-designed system does not assign blame; it makes the path of decisions recoverable.

Norman showed that even a door can fail as a design if it does not tell the reader what to do next. The same logic scales. A software system that runs correctly but cannot be reviewed, cannot be stopped safely, cannot be understood by its next maintainer, and cannot be inspected after failure is not well-designed — regardless of how elegant its internals may be. Design is not complete when the artifact works. Design is complete when the boundaries have been drawn: who sees what, who stops what, who maintains what next, and what remains as evidence that the judgment was made.

What matters, then, is not only the artifact a system produces, but the boundaries that make it readable and operable. The artifact is what remains after these boundaries have been drawn.


**Postscript**

Through the 3×3 lens, this episode primarily thickens three cells.

Cells thickened in this episode

- Gate × Operation: signifier and constraint as designed stops in daily interaction. What the reader sees determines where they can stop and what transitions are closed.

- Evidence × Operation: feedback as observable consequence returned at the speed the next judgment requires. Evidence is not record-keeping; it is what makes the next decision possible.

- Contract × Integration: conceptual model as shared expectation across boundaries. When the model diverges silently, the boundary no longer carries its promise.

Cells left thin on purpose

- Evidence × SSOT: why the master reference was defined or revised that way. This cell remains available for a future episode.

- Gate × SSOT: when the master itself must be frozen or questioned. Norman does not address this directly; it belongs to a different kind of pressure.

- Contract × Operation: the daily procedure for sharing and updating terms. Norman's vocabulary assumes a single user; the multi-reader expansion in Section 5 points toward this cell but does not thicken it.


**Re-reading Kit**

Read Norman with one operational question: who is the reader of this surface, and what must that reader be able to do next.

Each time Norman describes a design failure — a confusing door, an unreadable stove, an opaque remote control — rewrite the failure in three steps. First, identify the judgment surface: what was the reader supposed to see. Second, identify the missing gate: where should the reader have been able to stop or choose. Third, identify the missing evidence: what feedback would have made the next decision possible.

Then extend the reader. Norman writes about the end user. Ask the same three questions for the reviewer, the operator, the maintainer, and the future maintainer. The failures change shape, but the structure — surface, gate, evidence — remains the same.
