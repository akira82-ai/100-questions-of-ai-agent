# Chapter 3 · Pitfalls and Anti-Patterns

When multi-agent systems fail, the blame rarely lands on model quality. Production post-mortems repeatedly surface another class of failure: the architecture looks elegant, but in operation the parts drag each other down, errors get laundered between nodes, and in the end no one can say where it broke. This chapter lays out those high-frequency failure modes. Each corresponds to a concrete mechanism, not a vague "be careful." Once you see these, you can tell which graphs are truly necessary and which merely swap a single agent's trouble for a more expensive container.

## 36. Why is a 40-agent graph harder to debug than a single loop?

The more nodes, the larger the single-point failure surface, and it is multiplicative, not additive. A single agent at 95 percent reliable per step drops to around 60 percent after ten steps in series; string five agents each running ten steps and the system-level failure rate climbs to something no operator will look at. A 40-node graph amplifies this multiplication to absurd levels, and so does the coordination overhead and deadlock probability.

Explicit control flow beats emergent coordination nine times out of ten. A 40-agent graph basically cannot draw who talks to whom. If you cannot draw it, do not ship it. A truly debuggable multi-agent system is either one supervisor with a few experts, or a fixed-step pipeline whose topology you can see through at a glance.

Ask first whether one agent with better tools solves it, before talking about adding nodes. The most reliable multi-agent system is often the one with the fewest agents.

## 37. What is over-orchestration, and how do I tell if I am graphing for graphing's sake?

Over-orchestration means the graph's structural complexity exceeds the problem's own complexity. The team is driven by "graphs sound advanced" rather than by a real data-flow dependency. A common signal is picking the framework before the problem; the topology grows to look good in a demo, and node count increases just to satisfy a craving for architectural completeness, not because the task needs it.

The practical test is one question: does this work actually need explicit state tracking and conditional branching, or can a bounded, retryable work unit do it? If a graph has no conditional edge, no loop, and state that does not outlive a single run from start to finish, then it is a plain function, and adding a graph only adds checkpoints, serialization, and a layer of abstraction, with zero benefit.

A graph's legitimate existence needs at least one of three conditions: steps branch on intermediate results, the flow needs to go back and redo, or state must persist across runs. To judge whether you overdid it, ask: if I flatten this graph into a sequential function, does functionality get lost? If not, do not graph yet. Another signal is when the graph's complexity grows with the team's org chart rather than the task. Stop then and go back to figure out what the data flow actually looks like.

More concretely, several fake graphs look like this: two steps are sequenced only because you greeted them in that order, not because the second truly reads the first's output, and the wait between them buys nothing; every stage gets a sync barrier first just because it feels tidier, when the next step does not actually need the whole group, and that wait is real wasted latency; and a job like deduplicating or flattening a list, which a few lines of deterministic code could finish, gets its own agent, which is paying agent rent for the plumbing. An agent should be reserved for judgment, not for wiring.

## 38. Why is the pit of losing information when passing context between sub-agents so common?

Context passing relies on serialization and truncation. Each agent has its own context window; at handoff only the compressed state can be passed, and the truly critical information is often dropped during compression. The downstream agent gets the upstream's summary, not its full reasoning, and has no way to know what was lost in the summary.

Worse, the loss does not error out. The downstream produces plausible output based on incomplete context, and the chain proceeds normally; the error only surfaces much later. The contamination pattern in production post-mortems, where "an upstream agent hallucinated a fact, a downstream agent treated it as truth, and a further downstream mixed it with real data," often roots in exactly this hand-to-hand context loss.

The mitigation is to put a semantic checkpoint between handoffs, where the receiver verifies key assertions against a trusted source before folding them into its own reasoning, rather than defaulting to the upstream being right.

## 39. How does a hidden loop make an agent look busy while making no real progress?

A loop does not necessarily error; it may just never stop. The classic case is "polite disagreement": the quality agent rejects, the production agent fixes, the quality agent rejects again on another ground, and after a few rounds every agent executes its instructions correctly while the system as a whole is deadlocked. Another is recursion with no exit, where sub-tasks keep splitting and never reach an executable granularity.

Here is a hard rule: you cannot ask an agent whether it is in a loop; you can only prove it mathematically. The concrete method is to put a counter and an upper bound on every loop, or detect repeated states at the orchestration layer, judging it a loop and escalating after the same state appears three times in a row. Without this mechanism, the loop keeps eating the budget until it runs out. Experience says each agent's iteration steps need a hard cap, say fifteen, and exceeding it triggers an escape sequence rather than more spinning.

Looking busy and actually advancing are two different things. Loop detection is the only thing that separates them.

## 40. What is false success, where the final result looks great but the process is already rotten?

False success means the final output passes acceptance, but intermediate steps already erred and were merely covered up by later polishing and summarization. Scoring only the final answer most easily lets such systems slip through, because the error gets polished in the middle hops into something that looks authoritative, and the end-to-end score is paradoxically high.

Mechanically there are two spots. One is binding the evaluation to the wrong object: only testing technical correctness, not business outcome, the system treats erroneous but fluent output as qualified, while most pilot evaluations measure single-agent accuracy, not pipeline-level success rate. The other is unreliable self-verification: the same node generates and then checks against its own criteria, and a producer is naturally lenient toward its own output. Research has quantified this: models recognize their own writing and score their own answers higher with markedly elevated probability (one study measured GPT-4 recognizing its own text about 73 percent of the time and scoring its own answers about 10 percent higher; another had Claude about 25 percent higher).

To distinguish false success, bind the evaluation to the real trace and look at each step's intermediate product, not just the last answer. Production also needs online sampling, where a human or judge model periodically reviews actual output. Offline test sets catch regressions; online sampling catches drift and emergent failure modes. Miss either face and false success keeps pretending.

## 41. Where does a retry storm come from? How does one flaky API burn through the whole budget?

Retry logic is often scattered across several independent layers. The HTTP client retries network errors, the tool-wrapper layer retries failed tool calls, and the agent-loop layer retries failed steps. Three layers each retrying three times turns one upstream failure into twenty-seven downstream calls. One network timeout becomes twenty-seven requests to the payment service.

Multi-agent systems are harder to defend than traditional distributed systems, because traditional systems have centralized retry strategy and multi-agent systems often do not. A payment agent's failure triggers a retry; an inventory agent seeing uncertain payment status retries its own allocation check; a notification agent finding inconsistent status triggers its own retry. Within seconds the retry count multiplies by ten and the downstream service is overwhelmed.

The response needs an agent-aware circuit breaker, which must have a "degrade" middle state and can recognize semantic failure, such as an agent returning 200 but the output is a hallucination. Duplicate detection is also necessary: if the same tool with the same parameters hits more than three times, open the circuit, keep state for debugging, and alert. Graceful degradation matters far more than mindless retry.

## 42. At which step does token explosion usually spiral out of control?

The loss of control almost always starts at the same place: recursion or tool chains with no hard cap. Unclean recursive decomposition produces call cascades and burns thousands of dollars in tokens before anyone notices. Unbounded tool chains are more direct: let the agent decide when to stop calling tools "until done," and it actually becomes two hundred LLM calls and forty dollars, with the agent lost in the dozens and stuck in a loop.

Parallel branches multiplied by iteration count is another bleed channel. One agent calling ten times easily becomes one hundred across five agents. Switching from a single agent to five commonly triples the token cost for the same workload, not counting the coordination overhead that eats the specialization gains.

The only defense is a hard budget, non-negotiable: max spend per task, max rounds per agent, max total rounds per task, tool-call budget. Without these, one bug can generate a bill over ten thousand dollars overnight; with them, the same bug gets stopped like hitting a rate limit.

## 43. Why does drawing agents along organizational lines almost always fail?

An org chart is a static reporting relationship, not a data-flow dependency. Drawing agents by department is like making the finance agent, risk agent, and operations agent collaborate by seating arrangement; whether they should talk is decided by title, not by data. Topology should be decided by data dependency: no data dependency between two nodes means parallel; the next must read the previous result means serial.

"Five agents of different roles figuring it out themselves" keeps spinning, passing work to each other, producing garbage, or quietly collapsing into one agent doing everything. Explicit control flow beats emergent coordination nine times out of ten. A rule of thumb: if you cannot draw who talks to whom in a graph, do not ship it.

People who draw by org chart often assign roles before figuring out what the task's data flow looks like. Role assignment is a result, not a starting point.

## 44. Why does a graph loop into self-deception, treating mutual confirmation as truth? And how does a graph without reality anchors efficiently amplify errors?

Multiple agents that never question each other easily treat each other's output as truth. One agent's conclusion is cited by another, then summarized by a third, and the error is solidified in "consensus" because every link looks checked. A graph without reality anchors can pass every internal check while the whole graph has drifted from reality, becoming a self-consistent echo chamber.

The error-amplifying mechanism is concrete: an upstream agent hallucinates a fact, a downstream agent consumes it as truth and mixes it with real data to pass further downstream, and by the time of output the hallucination is indistinguishable from legitimate information. One hand-to-hand contamination gets laundered clean after a few hops.

An anchor is an external fixed node the graph's internal optimization machine has no right to rewrite, such as revenue that actually arrived, tests that actually ran, customers who actually stayed, counts that actually match physical goods. They pass values into the graph but are not dynamically affected by it. Without anchors, however exquisite the topology, it only organizes nonsense more politely.

## 45. Why is the God agent an anti-pattern? What happens if you cram 50 tools into it?

The God agent is one node taking on planning, execution, verification, and all tool calls, stuffing every responsibility into the same prompt. It violates the bottom line of "one node, one operation." Once a node wears many hats, when it fails you cannot tell which part broke; on recovery from a checkpoint, several operations rerun together, including the ones that already succeeded.

Too many tools brings three concrete consequences. One, tool selection starts erring, often silently, with the orchestrator picking the wrong tool or passing wrong parameters undetected. Two, the single node becomes the system's single point of failure; when it goes down, everything stops. Three, self-verification fails again, because the same node both produces and checks, making the check meaningless.

The split is straightforward: put planning, execution, and adjudication in different nodes. The adjudication node uses a different model and a different prompt, reads only the result, not the producer's reasoning. This separation is structural and far more reliable than writing "please check yourself objectively" in the prompt.

## 46. How does silent failure let an agent swallow an exception and pretend nothing happened?

Silent failure means the exception is swallowed and the agent returns a null or partial result, with the upstream continuing none the wiser. For example, an expert node fails and the supervisor treats it as "this item has no result"; the aggregated answer looks complete but is actually missing a piece. The production case of "three experts succeeded, two failed, and the system silently returned an incomplete result that looked like a complete answer" comes from exactly this.

The root cause is often the exception being eaten, or missing data being treated as a legitimate null. Missing is not the same as erroneous, but the two behave identically downstream and pollute every subsequent step.

The correct approach reverses this: the supervisor has an explicit policy for partial failure, rather than silently returning an incomplete result as a complete answer. Specifically, the supervisor reads from the marker which branch dropped and what dropped, and decides whether to retry or escalate to a human. Failure should be explicit and scope-limited, not quietly dragging the whole pipeline off course.

## 47. What is context poisoning? How does dirty data from upstream hit downstream?

Context poisoning means erroneous or adversarial content generated upstream enters the shared context, and downstream consumes it as trusted fact. In an agent chain it gets laundered hop by hop: a research agent establishes a wrong fact, a writing agent expands on it as basis, an editing agent polishes it into an authoritative-looking conclusion, and by the terminal the error is mixed with legitimate information, indistinguishable.

It is more dangerous than a single agent erring, because every downstream agent may be operating normally within its own accuracy threshold, yet the contamination spreads along the chain to every consumer. One source hallucination can cascade into a business decision based on fabricated information.

The detection architecture puts a semantic verification checkpoint between handoffs. The receiver does not trust the upstream to be right, but verifies key assertions against a trusted source before folding them into its own reasoning. Tearing down the assumption that "upstream output is trustworthy by default" is the first gate against poisoning.

## 48. Why are multi-agent setups in a linear writing pipeline often less controllable and more troublesome than a single agent, only earning their keep when multi-perspective verification is needed?

A linear writing pipeline gets no real parallel benefit but pays the full price of contamination and cost. On the same task, a single agent achieves 99.5 percent success, while an equivalent multi-agent implementation drops to 97 percent, and the gap widens with pipeline complexity. Once one step in the pipeline errs, every later step inherits it: a researcher hallucinates a source, a writer amplifies it, an editor polishes it into misinformation.

The extra failure modes a multi-agent setup introduces in a linear pipeline bring unclear benefit, because the chain could be done serially by a single agent within the same step, with better controllability. Multi-perspective verification is another matter: have several agents analyze the same problem independently, then a judge adjudicates conflicts. This debate pattern pushes cost above 2.5 times a single model, but in tasks like legal classification, financial verification, and medical diagnosis where one error is extremely costly, the error-rate drop earns it back.

So the judgment is simple: if the task decomposes linearly and wants controllability and cheapness, prefer a single agent; if the task needs cross-validation and cannot afford errors, then go multi-agent.

A sample done right is a large migration: break the work into units a single agent can hold steadily, one call site, one failing test, one module, and spin up a sub-agent in its own workspace for each, while another agent adversarially reviews every change before merging. No one wrote dozens of sequential prompts to run that migration; a script coordinated the crew, and review was written into the topology itself rather than bolted on after.

## 49. How do I decide whether to add an agent now or first fix the single agent's prompt?

First ask three questions. Does the single agent fail because of insufficient context or tools, or because it truly needs another independent reasoning body? Can the task be decomposed serially, and after decomposition are the steps truly independent? Can the reliability budget tolerate the multiplication of compound errors?

If you cannot answer even one of the three, do not add an agent yet. In most cases, fixing the prompt, adding tools, and adding an evaluation set works better than adding an agent. A single agent with better tools often beats a hastily assembled multi-agent system on reliability, cost, and time to ship.

There is a harder criterion: if you cannot draw who talks to whom in a graph, do not ship it. A drawable multi-agent system is usually one supervisor with a few experts, or a fixed-step pipeline. Adding agents should be the action taken only after proving the bottleneck is truly in multi-agent, not an architectural aesthetic preference. The most powerful multi-agent optimization is often reducing the agent count to one.

## 50. If you treat the graph as a silver bullet, what are the three most common costs?

First, complexity and debugging cost exceed the problem itself. The graph's abstraction layer, checkpoints, and serialization are pure net liability on simple tasks. A problem a function solves gets burdened with the whole orchestration mental load.

Second, coordination overhead eats the specialization gains. Multi-agent systems theoretically get stronger through division of labor, but the time and quality eaten by coordination, handoffs, and conflict resolution often make the whole worse than a well-tuned single agent. On the same workload, switching from single agent to five commonly triples the token cost.

Third, the silver-bullet mindset itself. The most reliable systems often have the fewest agents, yet the silver-bullet mindset makes people ignore this fact, treating "adopting a graph" as progress itself, graphing where graphs are not needed. On the same workload, single-to-five triples token cost and coordination overhead eats the division-of-labor gains; the bill is paid by later maintainers.

## 51. Why do some teams spend months building multi-agent systems when fixing the prompt would have been enough?

They got the order backwards. They drew a multi-agent architecture first, then crammed the problem in, instead of first verifying whether the single agent had truly hit a ceiling. The result is huge effort spent on distributed collaboration, deadlocks, and state sharing, troubles a single agent with good tools would never have.

The correct order is reversed: first get a single agent with mature tools running, with evaluation in place, and confirm the bottleneck truly lies in "needing multiple independent reasoning bodies in parallel or cross-validation" before adding agents. A single agent with good tools often beats a hastily assembled multi-agent system on reliability, cost, and time to ship.

Those "fixing the prompt would have been enough" cases almost all root in premature distribution: prompting, tooling, and evaluation problems that should have been solved at the single-agent layer were wrongly escalated to an architecture problem, and the cost lands on failure rate and unit economics.

## 52. How do you prevent side effects like double charges and duplicate messages in a graph?

A graph reruns, and reruns re-trigger side effects. Recovering from a checkpoint after a crash, if what is recovered is the message history rather than state with a deduplication marker, replaying the node may resend email or double-charge.

The prevention is to make side effects idempotent. Each external action carries an idempotency key, such as task identifier plus action type; the same key retrying does not execute again. Confine actions like sending messages and charging to controlled nodes, so the graph cannot err just by rerunning. On checkpoint recovery, pair with the idempotency key so what is recovered is the state object, not the bare message history, and a rerun does not trigger twice.

The underlying logic: side effects must fall within the graph's controlled boundary; outside the graph only put pure queries and harmless operations. Any action that, once it errors, has consequences on the outside world must never sit on a path that can be executed repeatedly without deduplication protection. The idempotency key is usually composed of task identifier plus action type; on retry the system first checks whether this key has executed, skips if so, cutting off double charges and duplicate notifications at the root.

## 53. How do you avoid the pit of binding too tightly to a framework, where switching one means throwing everything away?

Topology design should be framework-agnostic. First draw the state machine and boundaries clearly; treat the framework only as an execution engine, so switching vendors does not mean starting over. The problem is writing framework-specific semantics into the business logic: how reducers merge, how interrupts suspend, how checkpoints store, if these mix with business rules, migration throws everything away.

Teams with heavy engineering preference increasingly lean toward defining agent graphs in pure code, wanting full control over graph structure without a framework abstraction in the way. An open-source stack plus a portable runtime resists risk better than being locked to a single proprietary runner.

The concrete method is decoupling orchestration logic from the runtime, expressing business rules in a framework-neutral way, with framework-specific mechanisms only in a thin adapter layer. That way, when a framework becomes unsuitable, the cost of switching is rewriting the adapter, not the whole graph. Draw the topology as a state machine by data dependency first; the framework only decides how nodes are scheduled and how state is persisted, and this layer's replacement should not drag the business rules.

## 54. Why can't you take the "85% cost reduction" that marketing accounts tout at face value? What should you look at?

Numbers like 85 percent mostly come from vendor or analyst reports, not neutral conclusions, and are often pulled out of context as slogans. There is a more honest observation in the industry: the cost of operating multi-agent systems is indeed falling, but not as fast as marketing claims, and very unevenly across use cases.

On the same workload, switching from a single agent to five commonly triples the token cost, which is a real account. What to look at first is the benchmark caliber: is it the same task, same workload, same quality bar being compared? Many cost-reduction claims omit the big line item of operations labor, and omit the observability and circuit-breaking infrastructure added for reliability.

Second, look at unit economics rather than percentage slogans: for the same money spent, what quality, what latency, what failure rate did you get? The plain criterion: anything that gives only a flashy percentage without comparison conditions and caliber, treat as marketing first. The truth is the number your own task produces when run, not someone else's launch event.

## 55. How does tool-output prompt injection hijack an agent and turn a graph into an RCE entry point?

The content a tool returns, such as a fetched web page, a read file, or an API response, may hide adversarial instructions. If the agent executes that content as instructions, it oversteps to do things it should not, and the graph's boundary becomes void at that moment, exactly the seam the title calls turning a graph into an RCE entry point.

Indirect injection enters through several surfaces. The web page, file, or API response a tool returns are themselves carriers of adversarial content; memory stores and RAG-stored historical documents, if from untrusted sources, carry injections that get pulled into context at retrieval. The cunning of indirect prompt injection is that the malicious content never appears in your initial prompt; it hides in the data the agent goes to fetch itself.

Defense has several layers: constrain tool output with a structured schema to avoid instructions slipping into free-form text; sanitize the output; treat tool output as data, not instructions; make cross-node authorization fail-closed, rejecting external actions when the authorization context is unclear. Only together do these turn the "graph" from a hijacked entry point back into a controlled execution structure.
