# Chapter 7 · References

> Sources centrally compiled. Grouped by domain, within each group sorted by citation count descending; each question covers 2–4 sources, and the book's sources are dispersed and do not depend on a single material.
> Numeric sources (40% / 37% / 97% vs 99.5% / 2.5× etc.) are all industry-report caliber; the book already states them with the weak hedge "industry estimate."
> Note: the source file names below refer to the original Chinese-language material in the `资料/` folder. They are kept as-is for traceability; the English book renders their content faithfully without translating the underlying files.

---

## I. Source Domains (within each group sorted by citation count descending)

### Domain A · Primary Discourse / X Archives
| Abbrev | Source file | Main contribution |
|------|---------|---------|
| X-Steinberger | X_上的_Data_Science_Dojo (nine-word tweet) | Origin, 2.8M views, term-coining context |
| X-老金-假问题 | X_上的_老金《Loop 还是 Graph，其实是假问题》 | False problem, naming old habit, anchors, evolution axis |
| X-AlexPrompeter | X_上的_Alex_Prompeter《Graph Engineering 101》 | 6 upgrade signals (original), Chat Graph, org/employee analogy |
| X-ericosiu | X_上的_ericosiu | Rails / engine analogy, who decides the path |
| X-Shann³ | X_上的_Shann³ | Loop starts with a human, who decides the path |
| X-zostaff | X_上的_zostaff (Finance) | reducer / typed state / 60% state incidents / five design errors |
| X-老金-验证器 | X_上的_老金《如何给 Loop 造个验证器》 | Verifier, loops fighting |
| X-SydneyRunkle | X_上的_Sydney_Runkle (3 Years) | loop = simple graph, not DAG, dynamic dispatch |
| X-CarlosPerez | X_上的_Carlos_E._Perez | loop to graph evolution |
| X-AF智域 | X_上的_AF智域心识 (close read) | Four failures, anchor Chinese close read |
| X-Archive | X_上的_Archive (LOOP to GRAPH to HARNESS) | Evolution-chain node Harness |
| X-AlexMartin | X_上的_Alex_Martin | Prompt engineering is dead |
| X-FeicaiClub | X_上的_FeicaiClub | Chinese popular science, reader positioning |
| X-TowardsAI / X-AI超元域 | X_上的_Towards_AI / X_上的_AI超元域 | Term clarification, mainstream phrasing |
| X-MIKE | X_上的_MIKE《Stop Building Agents That Wait in Line》 | Single-agent long-run three failures (agentic laziness / self-preferential bias / goal drift), six topologies (fan-out / fan-in / diamond / routing / verification / converging-cycle), five anti-patterns (false edges / barrier by default / paying agent rent for mechanical work / non-converging loop / skipping verification), model layering (default inherits session model, must be set per node), Bun Zig to Rust migration sample |
| X-wandermist | X_上的_wandermist《Everyone Is Wrong About Graph Engineering》 | Loop/Graph comparison table, org-chart metaphor (loop = while, graph = org chart, loop a special case of graph), four-question self-check, three new capabilities a graph adds (dedicated parallel nodes / explicit auditable control flow / fan-out-fan-in), prior art (LangGraph StateGraph / AutoGen GraphFlow / Google ADK + A2A), real and over-marketed coexist |

### Domain B · Official and Authoritative Long-Form (WEB_)
| Abbrev | Source file | Main contribution |
|------|---------|---------|
| WEB-LangGraph3y | WEB_3-years-of-graph-engineering-langgraph | loop = simple graph, not DAG, node holds an Agent, when not to graph |
| WEB-Eigent | WEB_graph-engineering-ai-agents-eigent | Reality anchors, four single-loop failures, echo chamber |
| WEB-aibuilderclub | WEB_graph-vs-loop-which-should-your-agent-use | Decision checklist, 6 signals, hidden costs, whether to graph |
| WEB-Langfuse | WEB_comparing-agent-frameworks-langfuse | Framework comparison, checkpoint, time-travel, Temporal, observability |
| WEB-Anthropic-BEA | WEB_building-effective-agents-anthropic | workflow vs agent, deterministic + agentic |
| WEB-Anthropic-CWP | WEB_common-workflow-patterns-anthropic | Evaluation patterns, process metrics, false success |
| WEB-FrontierNews | WEB_graph-vs-loop-software-engineering-frontiernews | Old patterns renewed, Chase/Linear, knowledge-graph confusion |
| WEB-DigitalApplied | WEB_agent-architecture-patterns-taxonomy-digitalapplied | 8-pattern taxonomy, topology, upgrade guide |
| WEB-GitHub | WEB_multi-agent-workflows-fail-github | typed state / action schema / MCP, controlled boundary |

### Domain C · Anti-Patterns and Production Practice (WEB_)
| Abbrev | Source file | Main contribution |
|------|---------|---------|
| WEB-agentmarketcap | WEB_why-40-percent-multi-agent-pilots-fail | 40% failure, 37% coordination, 97%/99.5%, 5 failure modes |
| WEB-fallbrook | WEB_multi-agent-workflows-in-production-fallbrookresearch | 8 failure classes, 6 disciplines, ill-fitting scenarios, fail-closed, observability |
| WEB-devto | WEB_the-cascade-problem-devto | Cascade three modes, 5 survival, 3 pseudo-modes, cost gate |

### Domain D · Boundaries / Reflections / Manifesto
| Abbrev | Source file | Main contribution |
|------|---------|---------|
| manifesto-loop_is_over | the_loop_is_over | Chat Graph single-prompt, zero-code entry |
| manifesto-DSDojo | The_Frameworks_That_Were_Doing__Graph_Engineering__Before_It_Had_a_Name | Frameworks predate the name, time-travel |

---

## II. Per-Question Source Mapping (2–4 sources each)

### Chapter 1 · Foundations and Positioning
- Q1.1 What is Graph Engineering: WEB-LangGraph3y, X-Steinberger, WEB-FrontierNews
- Q1.2 Loop vs. Graph hierarchy: X-ericosiu, X-Shann³, WEB-LangGraph3y
- Q1.3 Not knowledge graph / GraphRAG: WEB-FrontierNews, manifesto-DSDojo, X-TowardsAI
- Q1.4 Cannot ask an agent if it is in a loop: WEB-Eigent, WEB-LangGraph3y
- Q1.5 Node / edge / state: WEB-LangGraph3y, WEB-GitHub, WEB-DigitalApplied
- Q1.6 loop is a simple graph: WEB-LangGraph3y, WEB-FrontierNews
- Q1.7 Goodhart's trap: WEB-Eigent, X-老金-假问题, X-AF智域
- Q1.8 Loops fighting: WEB-Eigent, X-老金-验证器
- Q1.9 Upward blind spot: WEB-Eigent, X-老金-假问题
- Q1.10 Broken measurement: WEB-Eigent, X-AF智域
- Q1.11 Evolution chain prompt to context to harness to loop to graph: WEB-LangGraph3y, X-Archive, X-SydneyRunkle
- Q1.12 Reality anchors matter more than the graph: WEB-Eigent, X-老金-假问题, X-zostaff
- Q1.13 A graph is not universal (when not to graph): WEB-LangGraph3y, WEB-Anthropic-BEA
- Q1.14 Who should learn Graph Engineering: X-老金-假问题, WEB-aibuilderclub, X-FeicaiClub
- Q1.15 Origin hook (2.8M views): X-Steinberger, WEB-FrontierNews, manifesto-DSDojo
- This round added (X-MIKE / X-wandermist): Q1.1 single-agent long-run three failures, Q1.2 org-chart metaphor and 'and then' diagnostic, Q1.3 a loop as a special case of a graph, Q1.4 anti-hype both poles overheated, Q1.5 and Q1.14 naming event not a technical event (prior art predates the name)

### Chapter 2 · Core Architecture and Key Mechanisms
- Q2.1 Edge carries conditions: WEB-LangGraph3y, WEB-DigitalApplied
- Q2.2 Node holds a full Agent: WEB-LangGraph3y, WEB-DigitalApplied
- Q2.3 State flows between nodes: WEB-GitHub, WEB-LangGraph3y
- Q2.4 Production graphs often not DAG: WEB-LangGraph3y, WEB-FrontierNews
- Q2.5 Loop handling: WEB-LangGraph3y, WEB-FrontierNews
- Q2.6 Subgraph encapsulation: WEB-DigitalApplied, WEB-Langfuse
- Q2.7 Fan-out fan-in: WEB-DigitalApplied, WEB-Langfuse
- Q2.8 State externalized to persistence layer: WEB-GitHub, WEB-Langfuse, WEB-LangGraph3y
- Q2.9 Dynamic dispatch: WEB-LangGraph3y, WEB-DigitalApplied
- Q2.10 Human approval node: WEB-Langfuse, WEB-Anthropic-BEA
- Q2.11 Deterministic + agentic coexist: WEB-Anthropic-BEA, WEB-LangGraph3y
- Q2.12 Routing ownership (code vs. model): WEB-Anthropic-BEA, WEB-DigitalApplied
- Q2.13 Framework vs. paradigm: WEB-Langfuse, WEB-FrontierNews
- Q2.14 Framework lock-in cost: WEB-Langfuse, WEB-FrontierNews
- Q2.15 What recoverability recovers (principle): WEB-LangGraph3y, WEB-GitHub
- Q2.16 Shared state vs. messages: WEB-GitHub, WEB-Langfuse
- Q2.17 Who can stop it: WEB-Langfuse, WEB-Anthropic-BEA
- Q2.18 Graph's controlled boundary: WEB-GitHub, WEB-fallbrook
- Q2.19 Topologies supervisor-worker etc.: WEB-DigitalApplied, WEB-LangGraph3y, WEB-devto
- Q2.20 Loop-to-graph evolution signals: WEB-LangGraph3y, X-Archive, WEB-aibuilderclub
- This round added (X-MIKE): Q2.2 a linear chain is the most fragile graph (single path, no redundancy), Q2.13 six topologies and industry dynamic-workflow patterns (fan-out / fan-in / diamond / routing / verification / converging-cycle)

### Chapter 3 · Pitfalls and Anti-Patterns
- Q3.1 Compound-error multiplication: WEB-agentmarketcap, WEB-Eigent
- Q3.2 More nodes, larger failure surface: WEB-agentmarketcap, WEB-devto
- Q3.3 37% coordination failure: WEB-agentmarketcap
- Q3.4 Cross-boundary data contamination: WEB-agentmarketcap, WEB-GitHub
- Q3.5 False success / evaluation distortion: WEB-devto, WEB-Anthropic-CWP
- Q3.6 Retry storm: WEB-agentmarketcap, WEB-devto
- Q3.7 Performance drift: WEB-agentmarketcap, WEB-Eigent
- Q3.8 Over-orchestration: WEB-FrontierNews, WEB-aibuilderclub
- Q3.9 Reality anchors amplify errors: WEB-Eigent, X-老金-假问题
- Q3.10 Echo chamber: WEB-Eigent, X-老金-假问题
- Q3.11 State management 60% incidents: WEB-zostaff, WEB-fallbrook
- Q3.12 Tool-output poisoning: WEB-fallbrook, WEB-GitHub
- Q3.13 Multi-agent degradation: WEB-agentmarketcap, WEB-Anthropic-BEA
- Q3.14 Linear pipeline no parallel benefit: WEB-agentmarketcap, WEB-devto
- Q3.15 Cascade three modes: WEB-devto
- Q3.16 Five survival modes: WEB-devto, WEB-fallbrook
- Q3.17 Three pseudo-modes: WEB-devto
- Q3.18 Cost gate: WEB-devto, WEB-agentmarketcap
- Q3.19 Whether-to-graph decision tree: WEB-aibuilderclub, WEB-FrontierNews
- Q3.20 Tool-output injection to RCE: WEB-fallbrook, WEB-GitHub, WEB-devto
- This round added (X-MIKE): Q3.2 three fake graphs (false edges / barrier by default / paying agent rent for mechanical work), Q3.13 large-migration sample (one sub-agent per fix, independent workspace, adversarial review before merge)

### Chapter 4 · Verification, Quality, and Advanced Techniques
- Q4.1 Default stay in loop first: WEB-aibuilderclub, WEB-Anthropic-BEA
- Q4.2 Name signals before upgrading: WEB-aibuilderclub, X-AlexPrompeter
- Q4.3 One node per signal: WEB-aibuilderclub, WEB-LangGraph3y
- Q4.4 Reality anchors (dual-write / frozen): WEB-Eigent, X-老金-假问题, X-zostaff
- Q4.5 Fix the verifier first: WEB-aibuilderclub, X-老金-验证器
- Q4.6 Price the coordination: WEB-aibuilderclub, WEB-devto
- Q4.7 Collapsible graph: WEB-aibuilderclub, WEB-LangGraph3y
- Q4.8 Evaluation bound to real trace: WEB-Anthropic-CWP, WEB-devto
- Q4.9 False-success detection: WEB-Anthropic-CWP, WEB-devto
- Q4.10 Process metrics: WEB-Anthropic-CWP, WEB-Eigent
- Q4.11 Replayable audit: WEB-Langfuse, WEB-LangGraph3y
- Q4.12 Hidden costs (latency / coordination / debugging / state / failure surface / onboarding): WEB-aibuilderclub, WEB-Langfuse
- Q4.13 Graph slows delivery: WEB-LangGraph3y, WEB-aibuilderclub
- Q4.14 Prove graph is worth it: WEB-aibuilderclub, WEB-agentmarketcap
- Q4.15 Workflow enough, don't climb: WEB-Anthropic-BEA, WEB-Langfuse
- This round added (X-wandermist): Q4.1 four-question self-check (whether you truly changed paradigm), Q4.10 three new capabilities a graph adds (dedicated parallel nodes / explicit auditable control flow / fan-out-fan-in), Q4.12 a graph's maintenance account and new failure modes (multiple prompts / state schema / merge drops source / routing infinite loop / state leak)

### Chapter 5 · Engineering in Practice and Real Scenarios
- Q5.1 typed state / reducer: WEB-zostaff, WEB-GitHub
- Q5.2 Narrow state prevents loss: WEB-zostaff, WEB-GitHub
- Q5.3 State recovery (idempotency key): WEB-zostaff, WEB-Langfuse
- Q5.4 Checkpoint selection: WEB-zostaff, WEB-Langfuse, WEB-LangGraph3y
- Q5.5 Checkpoint is not fault tolerance: WEB-zostaff, WEB-GitHub
- Q5.6 Human interrupt resume: WEB-Langfuse, WEB-zostaff
- Q5.7 Agent-level observability: WEB-fallbrook, WEB-Langfuse
- Q5.8 Tracing OpenTelemetry: WEB-fallbrook, WEB-Langfuse
- Q5.9 Time-travel debugging: WEB-Langfuse, manifesto-DSDojo, WEB-zostaff
- Q5.10 Retry / circuit break / timeout: WEB-fallbrook, WEB-GitHub
- Q5.11 Test graph structure: WEB-DigitalApplied, WEB-LangGraph3y
- Q5.12 Judge not maker, different model: WEB-zostaff, WEB-Langfuse
- Q5.13 Finance approval must stop: WEB-zostaff, WEB-fallbrook
- Q5.14 Framework selection: WEB-Langfuse, WEB-FrontierNews
- Q5.15 When to introduce outer graph: WEB-Langfuse, WEB-aibuilderclub
- This round added (X-MIKE / X-wandermist): Q5.9 model layering, default inherits session model and must be set per node, Q5.13 naming event not a technical event (prior art predates the name)

### Chapter 6 · Boundaries, Alternatives, and Reflections
- Q6.1 True/false judgment + rebranding stakes: WEB-FrontierNews, X-老金-假问题
- Q6.2 No single optimal framework: WEB-Langfuse, WEB-FrontierNews
- Q6.3 Framework comparison dimensions: WEB-Langfuse, WEB-fallbrook
- Q6.4 Frameworks predate the name: manifesto-DSDojo, WEB-FrontierNews
- Q6.5 Old patterns renewed (David K / Chase / Linear): WEB-FrontierNews
- Q6.6 Knowledge graph vs. orchestration graph confusion: WEB-FrontierNews, manifesto-DSDojo
- Q6.7 Paradigm differences (graph-style vs. lightweight vs. workflow): WEB-Langfuse, WEB-DigitalApplied
- Q6.8 Temporal underneath: WEB-Langfuse, WEB-zostaff, WEB-devto
- Q6.9 CrewAI role crew vs. LangGraph graph: WEB-Langfuse, WEB-DigitalApplied
- Q6.10 Non-code entry Chat Graph: manifesto-loop_is_over, X-AlexPrompeter
- Q6.11 Naming old habit: X-老金-假问题, WEB-FrontierNews
- Q6.12 Anti-pattern caution (big graph not direction): WEB-agentmarketcap, WEB-devto
- Q6.13 Those who bet on underlying syntax benefit from word changes: WEB-FrontierNews, X-老金-假问题
- Q6.14 Three marketing-noise phrases: WEB-FrontierNews, X-AlexMartin, WEB-agentmarketcap
- Q6.15 Cross-node authorization fail-closed: WEB-fallbrook, WEB-GitHub
- This round added (X-wandermist): Q6.1 naming event not a technical event (prior art predates the name), Q6.13 real and over-marketed coexist (lasting value in dedicated parallel nodes / auditable control flow / fan-out-fan-in)
