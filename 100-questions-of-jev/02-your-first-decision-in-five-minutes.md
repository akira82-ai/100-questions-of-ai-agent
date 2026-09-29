# Chapter 2 Your First Decision in Five Minutes

## 15. Which path should you take to get your first Jev decision running in five minutes?

Four paths lead to the same endpoint: POST api.typesafe.ai/v1/systemone with the model field set to jev-latest. The only distinction is who consumes the result: a human looking at it in a browser takes the Playground, a program consuming it itself takes the API or the SDK, and a coding agent writing the integration on your behalf takes the Agent skill.

To try it in the browser first, three steps: sign up at console.typesafe.ai and create a key from the Keys page; open console.typesafe.ai/playground and sign in; paste any text as the state, add one Noul question such as "does this message express urgency", then mix Noul, Choice, and Score into a single call and see all the results. To send a raw HTTP request, POST to the endpoint with the key you just created. To put the judgment into application code, pip install typesafe-sdk (requires Python 3.10 or above); the client reads TYPESAFE_API_KEY from environment variables and calls jev-latest by default. To have a coding agent write the integration for you, run claude plugin marketplace add typesafe-ai/skills and then claude plugin install typesafe@typesafe-ai in Claude Code; other agents use npx skills add typesafe-ai/skills --skill typesafe-ai, which installs into the current project by default and globally with -g; once installed, just say "use the TypeSafe skill".

## 16. What do the request body and the response of an API call look like?

The request goes to POST https://api.typesafe.ai/v1/systemone, authenticated through the Authorization Bearer header. The request body has only three top-level fields. state is the content to evaluate, a plain text string or a structured object or array; model is set to jev-latest; questions is a typed question table named by the caller, with answers returned under the same keys, and key names are not sent to the underlying model and take no part in reasoning. instructions can be a string, or split into an object or array: put the context a long question needs into separate fields and reference them by field name with backticks.

The criteria differ across the three question types. Choice is a mapping from option names to descriptions, at most 255 options; Score is an array of level descriptions running from low to high, at least two levels, with the interface accepting at most 10; Noul takes only a single statement whose truth or falsehood can be judged, with optional criteria stating what true and false each mean. All three types can be mixed within one call, and all questions are evaluated in parallel against the same state.

The response returns by key: Choice carries the selected option, each option's probability, and confidence; Score carries the weighted score, the level legend, level probabilities, and confidence; Noul gives a truth probability from 0 to 1. Confidence is derived from the probability distribution, and Noul has no such field. The SDK client splits answers by question type into the three dictionaries nouls, choices, and scores, with values looked up by question name. Two more fields sit at the top level, model and usage: model reports the version number that actually answered (for example jev-1.13.0), and usage gives the input and output token counts. The quick-start example response counts 392 input tokens and 65 output tokens.

Table T4: Elements of one API request

| Element | Description |
| --- | --- |
| Endpoint | POST https://api.typesafe.ai/v1/systemone |
| Input | state plus the questions table, each question declaring its type |
| Return | Returned in three groups: nouls, choices, scores |
| Billing | Input billed, output free |
| Limits | Choice at most 255 options, Score at most 10 levels |

## 17. How do you choose between the two official SDKs, Python and JS?

Both SDKs are maintained by TypeSafe, both read TYPESAFE_API_KEY from environment variables, and both default to the jev-latest model, yet their progress is not in sync. The Python package typesafe-sdk iterated from its first public release v0.5.7 on September 14 to v0.7.2 on September 26, with synchronous and asynchronous clients both in place (TypeSafeClient and AsyncTypeSafeClient), requiring Python 3.10 or above; from v0.7.0 the serialization library changed from msgspec to pydantic, and system_one gained a response_model parameter that binds the response to a custom pydantic model for shape validation. The JS package @typesafe-ai/sdk requires Node.js 20 or above, released v0.5.7 first on September 11 and reached v0.6.0 on September 15 before standing still, one minor version behind Python; it asks questions through the three constructors choice, noul, and score, infers answer types from the questions automatically, and ships ESM, CommonJS, and TypeScript declarations inside the package.

Each changelog contains one breaking change with identical content: from v0.6.0 the criteria of Score changed from an integer-keyed dictionary to an ordered sequence. The choice follows the project's language, and the two sides draw type safety from different sources: the Python side relies on explicit binding through response_model, the JS side on automatic inference from constructors. The interfaces share the same shape and answers return under the same key names; migration changes only how questions are constructed.

Table T5: The two official SDKs compared

| Dimension | Python | JavaScript |
| --- | --- | --- |
| Package | typesafe-sdk | @typesafe-ai/sdk |
| Version | 0.7.2 | 0.6.0 |
| Construction style | Classes and dictionaries | Functional, choice and the like |
| Environment | 3.10 or above | Node 20 or above |
| Distinctions | pydantic, response_model | Documentation pinned to v0.6.0 |

## 18. What scenarios does each of the five integration channels fit?

The integration map in Awesome Jev lists five paths and notes that these are documented integration routes, not equivalent SDKs, and that they carry no claims about price, latency, or reliability. Direct TypeSafe connection uses its JavaScript or Python SDK with a TypeSafe key; the state is sent to TypeSafe and the interface is the documented systemOne contract. Cloudflare Workers AI runs typesafe/jev, called through Workers AI bindings or the Cloudflare API, using Cloudflare's request structure and credentials; the model page marks Jev as a third-party model with a 32K-token context window. Netlify AI Gateway uses TypeSafe's JavaScript SDK inside a Netlify Function or Edge Function, provides environment configuration once the gateway is enabled, and is a server-side path, not a browser key. Vercel AI Gateway goes through the AI SDK's experimental evaluate with typesafe-ai/jev, mapping boolean questions to Noul, an interface different from systemOne. OpenRouter uses the decisions API with the model name typesafe/jev-1.13 or the latest routing, an OpenRouter key, and the decisions request structure; questions of this kind are not to be sent to the chat-completions endpoint.

The order for picking a channel is to follow the platform already in place: applications running on Cloudflare, Netlify, or Vercel take the corresponding gateway and save one key management setup; those already using OpenRouter for multi-model routing only swap the model ID to typesafe/jev-1.13; those not going through a gateway connect to TypeSafe directly. jev-1.13 was listed on OpenRouter on September 18, 2026, at $0.042 per million input tokens with output free. For trying the interface shape locally there are aggregators such as Ollaya: open-source decision models run locally with an interface shaped like Jev's, so the code is not bound to either side. The LangChain ecosystem has an additional langchain-typesafe package, and three classes of integration, basic classification, model routing, and tool-call gating, can plug into the channels above.

Table T6: The five integration channels

| Channel | Model identifier | Scenario |
| --- | --- | --- |
| Direct TypeSafe | jev-latest / jev-1.13.0 | Production main path |
| Cloudflare Workers AI | @cf/typesafe/jev | Calls close to the edge |
| OpenRouter | typesafe/jev-1.13 | Unified multi-model routing |
| Vercel AI Gateway | typesafe-ai/jev | AI SDK ecosystem |
| Local aggregators such as Ollaya | Local open-source models | Trying the interface shape locally |

## 19. What is the least-effort way to reach Jev from a mainland China network?

There are two billing routes: TYPESAFE_API_KEY goes through the TypeSafe endpoint with the bill recorded on the TypeSafe account; OPENROUTER_API_KEY goes through the OpenRouter Decisions endpoint with the bill recorded on the OpenRouter account. When both keys exist, TYPESAFE_API_KEY takes precedence, and a leftover OpenRouter key does not silently move the bill.

Both routes connect directly overseas, and when access to both is inconvenient the alternatives come in two layers. At the process layer, validate the pipeline locally first with a compatible open-source decision model and decide whether to adopt the cloud service once it runs through; on the model side, use a multi-model inference platform directly accessible from mainland China, such as the API access service from Qiniu Cloud, which is compatible with mainstream SDK formats. The trial layer has entrances of its own: the Playground is directly usable after signing in, and the third-party gateway OpenCode Zen lists jev-1.13 and the free jev-1.13-free.

The registration hurdle was removed at the end of September 2026: the TypeSafe account pinned the announcement "Jev is back. Capacity has increased, and registration is now open". Before that it was early access plus a waitlist, with new registrations suspended while demand surged; for the current status, typesafe.ai is the authority.

## 20. What does Jev's input-token-only billing mean for how you use it?

The pricing on the model page is a single line: $42 per billion input tokens, or $0.042 per million, with output tokens free. All cost lands on the input side; the length of an answer produces no expense at all, and however large the state and however many the questions, that is the entire cost of one call. For comparison: traditional LLM input prices run about $0.20 to $10 per million, with output prices usually 5 times the input. One real reranking run left a ledger sample: 1,200 calls, 1,536,002 input tokens and 25,200 output tokens, $0.0645 in total.

The output-free billing structure is what makes the Speculative Fan-Out pattern viable: one call carries many questions, including speculative ones, and the code decides afterwards which are relevant; all questions are evaluated in parallel, adding more barely affects response time, and the price is that every question counts against input tokens. Stuffing in more speculative questions barely raises cost: output is free, so the extra answers carry no expense, and input-only billing means each added question pays only for its own tokens; the need to split judgments into serial calls to save a round trip is gone.

The cheap bill also changes how experiments are run: the cost of running hundreds to thousands of test prompts is negligible, and structured experiments on Jev are more worthwhile than on ordinary large models. Three qualifiers are kept on pricing sustainability: there is no way to prove the price carries no early subsidy, whether it can hold long term is a question for time, and the expected long-term direction is down, never up.

## 21. With Jev rate-limited at 250,000 tokens per second, how do you use it to the full without hitting the wall?

The rate limit has two lines: 250,000 tokens per second and 1,200 requests per minute, and exceeding either returns 429 Too Many Requests. The SDK retries with backoff by default and honors the retry-after header in the response; on a 429 or 529, back off exponentially and do not resend immediately: 429 means the rate limit is exceeded, retry after backoff with a short delay, and 529 means TypeSafe is temporarily overloaded, retry after a short delay. On the Python side a RetryPolicy can be configured on the client or on a single call, with the parameters max_retries, backoff_max, and timeout, and exceeding the limit raises TypeSafeRateLimitError.

Using the limit to the full without hitting the wall means reading the two lines together. The token budget is wide and the request budget is tight: with one question per request, the 1,200-per-minute line is reached first and the token line is never filled; pack multiple questions into one request and send the same state only once, and the extra questions consume only the token budget, which presses down the request-count line. Under high concurrency, add HTTP/2 so multiple requests multiplex over a single connection; the http2 extra of typesafe-sdk supplies the required dependencies.

The two numbers themselves are not stable: the model page notes that rate limits are being adjusted dynamically as a very large volume of demand is absorbed; as large GPU shipments arrive and more users are admitted, the caps may change without notice, and more stable limits can be offered only once the situation settles; custom and enterprise editions offer higher limits.

Table T7: Rate limits and fault tolerance

| Parameter | Value | Description |
| --- | --- | --- |
| Rate limit | 250,000 tokens per second | Official spec, subject to change at any time |
| Rate limit | 1,200 requests per minute | Same as above |
| Status code | 429 | Rate limited, back off and retry |
| Status code | 529 | Overloaded, non-standard code |
| Retry | max_retries 3, backoff_max 0.2, timeout 1.0 | SDK example parameters |

## 22. How do you get Claude Code to put Jev to work directly?

Three paths, ordered from the lowest configuration cost to the highest: MCP server, Agent Skill, and SDK; the first two are one command each, and the SDK requires writing code. The three stack, and the usual combination is to install MCP first to open the call path, add the Skill as needed, then fix the settled judgment logic into code with the SDK.

For MCP, use the community-maintained typesafe-mcp, a single-file binary written in Go with no dependency on a Node or Python runtime. One command, TYPESAFE_API_KEY=<key> evaluate setup mcp, completes registration; the script probes for codex on the PATH and registers into both Claude Code and Claude Desktop; at registration the environment variables starting with TYPESAFE_ are copied into the client configuration, because MCP clients do not inherit the shell environment when starting the server, so the command must be rerun after changing the key.

The Skill teaches Claude Code when to hand a judgment to Jev: run claude plugin marketplace add typesafe-ai/skills and then claude plugin install typesafe@typesafe-ai in order; other agents use npx skills add typesafe-ai/skills --skill typesafe-ai; once installed, just say "use the TypeSafe skill". Two accompanying principles: put the questions and threshold constants in the same file so they are easy to review; agents are bad at writing questions, so expect to co-edit with them, and what a human should review most is exactly the questions and the threshold constants. At the framework layer, DSPy 3.4.0 additionally provides native support for Jev and System One models, working through compatible signatures, and its bundled optimizer ReAnchor is designed specifically for calibrating outputs that carry confidence.

## 23. How many hurdles stand between signing up and holding a key?

The early launch went through a waitlist, and approvals moved fast: fast applications cleared the same day, slow ones within a day or two. On September 20, 2026, TypeSafe opened registration to everyone; on September 22 new registrations were suspended as demand surged, with existing accounts unaffected.

The end-of-September announcement removed that hurdle: the TypeSafe account pinned "Jev is back. Capacity has increased, and registration is now open". Once the key is in hand, every entrance lives in the console: the Keys page creates keys, the Usage page shows token consumption, and the Playground is directly usable after signing in.

If registration is blocked again, there are two fallback entrances: for the current status, typesafe.ai is the authority; jev-1.13 and the free jev-1.13-free listed on OpenCode Zen serve as trial entrances.

## 24. Are Jev's registration-free one-click package and the mirror sites safe to touch?

The one-click package comes from a V2EX post whose author describes themself as an open-source replication enthusiast with no connection to TypeSafe. It packs an open-source replica of the Jev model from HuggingFace into a Windows x64 one-click bundle: no registration, no invite code, no activation code, ready to use after unzipping at about 1.66GB, with python-embed 3.10 bundled; it runs on a CPU with no graphics card needed and is entirely free. The author tested three machines and all of them ran, one an old laptop with integrated graphics only, doing CPU inference at about 2 to 3 tokens per second.

Mirror sites are another category. The Chinese site jevtypesafeai.com is operated by CODEFASHION TECH LTD., offers a free playground and a trial API, and its price board lists input at $0.25 to $0.42 per million, while the model page's input price is $0.042 per million. Another, jev-ai.pro, put up an llms.txt that was posted to V2EX, where a reply read: "I looked for ages and there is not even a way to switch to Chinese".

Both sources state their standing in the open: the one-click package is a packaging of a community-replicated model, not Jev itself; a gap from the original in results is normal, and routing, filtering, and scoring are what it suits. The mirror sites state in their footers that they have no affiliation with and no endorsement from TypeSafe AI, and their price boards run 6 to 10 times the model page's input price.

## 25. What version strategy sits behind the default model name jev-latest?

The alias table on the model page holds two names. jev-latest points to the most recent stable official release; it is the client SDK default and the name used in documentation examples. jev-preview points to the most recent release, official or not, and runs ahead of jev-latest whenever a preview build exists. As of the snapshot of September 28, 2026, both point to jev-1.13.0, and the model page notes that jev-preview currently resolves to the same model as jev-latest, with no preview build at present.

Aliases move as new versions ship, and the answer behind one can change with nothing changed on your side; the model field in the response reports the version number that actually answered, so every result can be traced back to the version that produced it. GET /v1/models lists the aliases your account can send, and version-number IDs such as jev-1.13.0 can be written straight into the model field whether or not they appear in the list.

For usage, the alias table's rules reduce to one line: if your confidence thresholds are already tuned against a particular version, pin that version's ID rather than the alias and migrate on your own schedule. The Python SDK shipped five versions in twelve days, and aliases move more often than ordinary dependency upgrades; once the version number is pinned, the timetable for migrating to a new version sits in your own hands.

## 26. What does the SDK shipping five versions in twelve days tell you?

The Python package's changelog reads entry by entry: v0.5.7 (September 14), first public release; v0.6.0 (September 15), breaking change, Score's criteria switched from an integer-keyed dictionary to an ordered sequence; v0.7.0 (September 18), breaking change, the serialization library swapped from msgspec to pydantic, fixing along the way str subclasses being serialized into lists of characters, and adding the response_model parameter; v0.7.1 (September 21), the API key validated up front, with the key value excluded from logged exceptions; v0.7.2 (September 26), a new http2 extra plus HTTP/2 documentation.

Two breaking changes say the interface contract is not yet frozen: both the shape of question construction and the underlying serialization library were swapped within half a month, and code that upgrades without reading the changelog runs straight into them. The remaining three releases are convergence on defects and performance: v0.7.0 fixed str subclasses being serialized into lists of characters, v0.7.1 validated the API key up front and kept the key value out of logged exceptions, and v0.7.2 added HTTP/2 support.

The JS package is the contrasting line: first release v0.5.7 on September 11, v0.6.0 on September 15, then updates stopped, one minor version behind Python, and the v0.6.0 breaking change is the same one on both sides. The ecosystem is under two weeks old and updates frequently, so for exact commands the latest instructions in each repository govern.

Table T8: SDK version timeline

| Version | Date | Notes |
| --- | --- | --- |
| Python 0.5.7 | 09-14 | First release |
| JS 0.5.7 | 09-11 | JS first release |
| 0.6.0 | 09-15 | Score.criteria switched to ordered sequence (breaking) |
| Python 0.7.0 | 09-18 | msgspec to pydantic, response_model added |
| Python 0.7.1 | 09-21 | Fixed key leaking into exception logs |
| Python 0.7.2 | 09-26 | Current version |
| JS 0.6.0 | 09-15 | One minor version behind Python |

## 27. Once the first requests go out, which numbers should you record first?

The validation steps give a closed loop: define the Schema with historical samples and confirm that the true case cannot be stuffed into the wrong option; record prediction, probability, ground-truth label, and human action for every field; compute accuracy, confidence bucketing, calibration error, false positives, and false negatives separately; set thresholds for automatic execution, human review, and fallback; run in shadow mode first, without directly changing production actions; then watch latency, tokens, retries, human takeovers, and long-term price.

For what the first two steps record, the response body has matching fields. Choice carries the selected option, each option's probability, and confidence; Score carries the score, the level legend, level probabilities, and confidence; Noul carries a truth probability from 0 to 1 and has no confidence field; usage's input_tokens and output_tokens record the input and output token counts; model reports the version number that actually answered. The comparison of predictions against ground-truth labels splits into two recorded categories: false positives and false negatives.

The starting point is historical samples, not a dry run: define the Schema and confirm the true case cannot land in the wrong option before talking about recording and computing. For magnitude, take the quick-start example: one support ticket plus three questions, with the response counting 392 input tokens and 65 output tokens.

## 28. Is packing three question types into one call marketing or a real saving?

The controlled experiment ran on the 53,777-character (about 54,000) GDPR Wikipedia entry, with 13 questions (8 Noul, 2 Choice, 3 Score), one packed call against splitting into 13. Asking everything in one pass: 1 call, $0.000497, 0.27 seconds. Asking 13 times, one question each: 13 calls, $0.006090, 2.71 seconds. Packing is 12.2 times cheaper and 10.0 times faster.

Unchanged answers are the premise of these numbers. Each question scores the document independently, and answers do not depend on the other questions in the same request; both packing modes ran 5 times each, most answers were identical across runs with a standard deviation of exactly 0.0, and the run-to-run sampling noise that exists on the two Noul questions is the same size under both modes: packing neither moves the mean nor adds variance.

Where the saving lies depends on reading the measurement correctly. On cost, 13 single-question calls resend the article 13 times while packing sends it once, and this saving holds no matter how you parallelize; on time, the 2.71 seconds sums 13 single-call latencies assuming serial execution, and issuing them concurrently narrows the gap, but the 13-times token cost stands. The matching usage is Speculative Fan-Out: put every question the system might need into one request and let the code decide afterwards which are relevant; send every possibly useful question in one go and have the code read only the answers it needs, at the price of all questions counting against input tokens.
