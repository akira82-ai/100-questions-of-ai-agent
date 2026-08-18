# Chapter 2 - Get It Running in Three Commands

This chapter has one job: get DeepSeek Harness running today and make the first run meaningful. The commands below use the `0.1.0-rc.6` release context from 2026-08-17. DSH is still in developer preview and its README warns that compatibility-breaking changes are coming, so check the current documentation before relying on any command.

## 15. Can three commands really start a coding agent?

Yes, if Node.js is installed. Run `npx @deepseek-ai/dsh web`, then open `http://127.0.0.1:3080`. When the mode selector appears, the agent is running.

This is a real harness, not a chat demo: model adapters, tools, sandbox controls, and session logs run as plugins. Even Minimal mode includes a terminal tool and a file editor, so it can read and change files. The first workspace must be added and selected before the input box becomes active. That is an intentional safety boundary, not a broken UI.

The source route is also available: clone the repository, run `pnpm install` and `pnpm run build`, then start with `pnpm dsh web`. For a first run, `npx` is the shortest official path.

1) DeepSeek Harness repository https://github.com/deepseek-ai/deepseek-harness

2) Official quick start https://deepseek.com/harness/en/

3) Official user guide https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md

## 16. I do not even have Node installed. Can I run it?

Install the current Node.js LTS release from nodejs.org. If `node -v` prints a version, you have the hard dependency needed for the previous command.

The README does not pin a Node version. Community tutorials commonly say Node 18 or newer, but that is an experience-based guideline rather than a formal guarantee. Choose LTS over Current: the goal is a stable dsh run, not the newest Node feature.

The npm package has been moving quickly, with pre-release `0.1.0-rc` versions appearing close together. If a setup problem occurs, search Discussions before assuming your machine is uniquely broken.

1) Node.js https://nodejs.org

2) npm package https://www.npmjs.com/package/@deepseek-ai/dsh

## 17. `npx` keeps failing. How do I locate the failing layer?

Do not start by changing registries. Separate command parsing, network or package resolution, and version or runtime problems first.

```text
# Triage from the outside in
npx @deepseek-ai/dsh --version
# No version -> command or package resolution; on Windows try native PowerShell or CMD.

npx --yes @deepseek-ai/dsh@latest --profile web --dump-config
# Version works but startup fails -> capture the complete configuration and error.

node -v
# Confirm the local Node runtime.
```

`--dump-config` is useful beyond installation debugging: it shows the final effective configuration when a setting appears not to take effect. Locate the layer first; reinstalling or changing mirrors without evidence is just churn.

1) DeepSeek Harness Discussions https://github.com/deepseek-ai/deepseek-harness/discussions

## 18. Which of the four dsh modes should I choose?

Start with Standard. The four modes are different presets over the same plugin system.

| Mode | Official positioning | Best use |
|---|---|---|
| Standard | Full tools: editing, terminal, search, skills, planning, sub-agents, and workflows | Daily work |
| Code | Uses Code Mode SDK to expose tools as generated code for multi-step execution | Multi-step orchestration with fewer turns |
| Minimal | Keeps only bash and `str_replace_editor` | Model capability tests and a clean baseline |
| Creator | Builds custom agent presets with runtime inspection and plugin experiments | Plugin and runtime development |

The community label PTC is not the official mode name; the product calls it Code. Use Minimal for benchmarking, Standard for normal work, Code for many-step tool plans, and Creator when you are modifying the system.

1) Official mode overview https://deepseek.com/harness/en/

2) Official user guide https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md

## 19. Is Minimal mode really an "evil cultivation" mode, and who is it for?

That nickname is a meme. Minimal is the official benchmarking environment: only a terminal and a file editor, with fewer interventions and fewer sources of variance.

It suits two groups. Beginners get the smallest surface area. Experienced users get a baseline: run the same task in Minimal and Standard, then use the difference as diagnostic evidence. A task that improves sharply in Standard needed tools or orchestration. A task that stays poor may have a context or model problem instead.

Minimal is not automatically inefficient. The right tool matters more than the number of tools. Some Windows reports describe Minimal as unavailable in particular environments; treat that as an environment-specific compatibility report, not a universal rule.

1) Official mode page https://deepseek.com/harness/en/

2) GitHub Discussions https://github.com/deepseek-ai/deepseek-harness/discussions

## 20. What should I do first after starting an agent?

Give it a small real file that you already understand and ask it to summarize three points. This tests tool wiring, workspace permissions, and context injection in one step.

The official guide suggests a similar first request: summarize the repository and identify its main packages. "Hello" only proves that the model is online. Reading a known file proves that the complete system works. If it invents the file instead of reading it, stop there and fix the workspace or tool path before assigning a larger task.

Choose a file whose correct contents you can verify in seconds. When an operation requires approval, inspect what the agent is asking to do before allowing it. That prompt is the permission system doing its job and your first view into the agent's boundary.

1) Official user guide https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md

## 21. Can I connect Claude or GPT instead of a DeepSeek model?

Yes. DSH is designed not to lock you to one model family. Use the Providers settings: built-in providers can be configured directly, other services can be added as custom providers with a provider ID, base URL, API protocol, and at least one model.

Treat a custom provider ID as permanent. Requests, sessions, and credential references use it, so changing the name generally means creating a new provider and removing the old one.

Credentials are stored locally. After saving, the UI receives a redacted descriptor rather than the plaintext key, and model changes apply on the next request without restarting the server. Run the known-file test after changing models; a new model name is not proof that the tool chain works.

1) Providers documentation https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.md

2) Community model coverage reference https://www.aixq.cc/62316.html

## 22. Can I connect an open-source local model?

The supported mechanism is a custom provider: point DSH at a compatible model service from the Providers page. Official documentation clearly supports custom providers; it does not make every community Ollama setup an official guarantee. Treat Ollama compatibility as version-dependent and verify it in your installation.

The safe sequence is simple: add the custom endpoint, connect one small model, run the known-file test, and only then use it for real work. Providers using native authentication, such as Bedrock, Vertex, or Azure, require their native credentials; one API key does not fit every provider.

1) Providers documentation https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.md

2) OpenAI agent-loop reference https://openai.com/index/unrolling-the-codex-agent-loop/

## 23. Why start with a Web UI instead of a desktop client or CLI?

The initial product shape is a local Web service: start it in a terminal and work in a browser. Web UI reduces cross-platform packaging cost and makes interface changes easier to ship, but it adds a startup step and currently has performance limits on very large contexts.

The "Web only" description is already becoming incomplete. The user guide exposes CLI and Python SDK paths, and the repository has CLI work. For now, learn the two-step habit: start the local service, then open the browser. If you need a pure CLI flow, follow the current repository and Discussions rather than an old tutorial.

1) Official quick start https://deepseek.com/harness/en/

2) Client and CLI discussion https://github.com/deepseek-ai/deepseek-harness/discussions/172

3) Official user guide https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md

## 24. What if the API key will not go into the UI?

Use an environment variable as the first fallback. UI failures often look identical when the actual causes are whitespace in the pasted key, a proxy blocking validation, or a provider's regional restriction. A direct API request separates a bad key from a missing `/models` endpoint.

| Report | Meaning and next action |
|---|---|
| `MISSING_CREDENTIAL` | Configure a credential in the model page or environment |
| `UNKNOWN_MODEL` | Select a configured model or add the model to the custom provider |
| `/models` returns 401 | The key or endpoint is wrong, or the provider does not expose model listing; enter the model manually |
| Image rejected before sending | The model does not declare image input; text-only DeepSeek routes cannot be changed into vision models by configuration |

```text
# API key triage
1. export YOUR_API_KEY=...   # Put it in your shell profile if appropriate.
2. Restart dsh and check whether the provider sees it.
3. Call the provider API directly to separate key errors from endpoint limitations.
```

1) Providers documentation https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.md

2) Community FAQ https://www.aixq.cc/62316.html

## 25. Why does it silently exit on Windows?

There are several distinct Windows failures. First classify them with `--version` and the exit code instead of treating every silent exit as one bug.

MSYS2 or CLANG64 may produce exit 127 because the process launcher cannot find the expected Windows binary. Native PowerShell or CMD with the official Node installer avoids that class. Some Windows 10 environments report a native `koffi` crash with exit code 3221225477. A directory-picker failure is a separate issue.

```text
# Windows starting point
1. Use PowerShell or CMD, not an MSYS2 or Git Bash compatibility layer.
2. Install Node from nodejs.org rather than a pacman package.
3. Run npx @deepseek-ai/dsh --version before troubleshooting startup.
   127? Try a native shell.
   3221225477? Check the current Discussions report.
   directory picker failed? Follow the corresponding issue.
```

1) Discussion of exit 127 https://github.com/deepseek-ai/deepseek-harness/discussions/1624

2) Community Windows handbook https://github.com/sandbaseai/deepseek-harness-handbook

## 26. What should my first real Agent task be?

Choose a small task with clear boundaries, an obvious acceptance test, and an easy rollback. A copy of a directory is safer than a decade-old working folder.

The first task is for trust calibration, not maximum time savings. Pick something you can verify in five minutes. The official capability set gives a useful menu: read or edit a workspace file, run one command, delegate a small piece of work, or maintain a plan. Test one capability at a time.

The launch directory is also a practical boundary: start dsh from the copy directory you want it to use. Do not let a first experiment touch important work.

1) Official user guide https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md

## 27. It runs, but the answer is stupid. Is that normal?

In Minimal mode, often yes. Minimal deliberately removes planning, search, and sub-agent support. Compare the same small task in Minimal and Standard before making a diagnosis.

If Standard is much better, the task needed those tools. If both are poor, inspect context and model choice. Separate missing-tool stupidity from missing-context stupidity: changing modes cannot fix a file the model never saw.

1) Official mode overview https://deepseek.com/harness/en/

2) New-user experience report https://www.zhihu.com/question/2071335529577239335

## 28. How do I know this is a real Agent rather than a wrapper?

Check evidence, not the chat copy. Use three tests: inspect the tool trajectory, confirm a real filesystem change, and rerun the same task to see whether the execution path changes.

```text
# Three tests for a new agent
1. Read a file   -> inspect the trajectory for tool calls.
2. Write a file  -> verify the file and contents outside the chat window.
3. Rerun         -> a changed path indicates actual tool-mediated decisions.
```

Agent self-reports are not acceptance tests. The filesystem diff and the recorded trajectory are. Anthropic's later browser-automation work makes the same point at a larger scale: exercising the result reveals problems that code inspection alone misses.

1) Session subsystem documentation https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/session.md

2) Anthropic on unreliable completion claims https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
