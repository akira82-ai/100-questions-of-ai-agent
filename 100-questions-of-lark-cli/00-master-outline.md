# Master Outline · 100 Questions on the Feishu CLI

## I. Cognitive Disruption (16 questions)

1. Is the Feishu CLI made for humans or for AI?
2. Why did DingTalk, Feishu, and WeCom all open-source their CLIs within three days?
3. Feishu built AI its own keyboard, are you still clicking the interface by hand?
4. What does the shift from humans clicking the interface to AI calling the API mean?
5. Why does the Feishu CLI say humans only need to install and authorize?
6. If Feishu bots already exist, why do we still need the CLI?
7. How to explain the Feishu CLI to a non-technical person in one sentence
8. What exactly is the relationship between the Feishu CLI and the Open Platform API?
9. When should you use the CLI and when should you call the API directly?
10. Are the Feishu CLI and the MCP protocol competitors or complements?
11. If you already use n8n, is the Feishu CLI still necessary?
12. Who is each of the CLI's three command tiers suited for?
13. What is the real difference between the Feishu CLI and Feishu AILY?
14. Why is the Feishu CLI the lowest-cost entry point for Agents into the enterprise?
15. What trend does 15k stars in three months signal?
16. How is Agent-native office work different from old RPA automation?

## II. Killer Scenarios (26 questions)

17. The 5 killer scenarios most worth trying first with the Feishu CLI
18. How to tell AI in one sentence to send your weekly report to the group
19. How to avoid sending the weekly report to the wrong person or group
20. How to have AI auto-organize meeting notes and @ the relevant people
21. How to auto-sync to-dos from meeting notes into a task list
22. How to have AI check your calendar for free slots and create a meeting
23. How to batch-manage Feishu calendar events with the CLI
24. How to have AI push your day's schedule and to-dos every morning
25. How to auto-push CI/CD results into a Feishu group
26. How to have AI read an email and auto-fill a Base table
27. How to bulk-load CSV data into a Feishu Base
28. How to query Base data with natural language
29. How to auto-archive valuable group chat info into a knowledge base
30. How to have AI monitor a document for changes and auto-notify
31. How to do two-way data sync between Feishu and external systems
32. How to build a cross-app message bridge with the Feishu CLI
33. How to build a fully automated daily-report bot with Python plus the CLI
34. How to build a Feishu Q&A customer service bot that auto-replies in groups
35. What to do when a Minute transcript export stalls halfway
36. How to upload a local video via the CLI and convert it to a Feishu Minute
37. How to have AI read Feishu meeting notes and extract to-dos
38. Does a PDF exported via the Feishu CLI add an AI-generated watermark?
39. How to let Claude Code operate your Feishu directly
40. How much time can Feishu CLI automation actually save?
41. How to let AI perceive Base data changes in real time
42. Which office scenarios are best to automate with the CLI first?

## III. Three-Layer Architecture and Security (15 questions)

43. Why mixing user and bot identities is the biggest pitfall of the Feishu CLI
44. Why dry-run is the "regret medicine" for AI operating Feishu
45. How the preview-before-send mechanism for AI messages is built
46. What configuration problems can `lark-cli doctor` diagnose?
47. What can the user identity do that the bot identity cannot?
48. What can the bot identity do that the user identity cannot?
49. How to choose among the CLI's three command tiers without getting it wrong
50. How to handle token expiration without logging in manually every time
51. How much context quota does global Skills injection eat?
52. How to recover when the keychain master key is lost
53. What is the difference between the Feishu CLI's Skills and MCP tools?
54. How to check which permissions your CLI is currently authorized for
55. Why multiple Agents sharing one bot identity kick each other offline
56. What each of the three layers (OpenAPI → CLI → Skills) solves
57. How a Skill internally interacts with the Feishu API

## IV. Install, Configure, and Auth Pitfalls (23 questions)

58. Is it actually safe to let AI operate your Feishu?
59. Why 403 is the most common error Feishu CLI users hit
60. Bot installed but no reply in the group, how to troubleshoot
61. Why skipping config init makes everything collapse later
62. Why your chat-id is always filled in wrong
63. How to correctly extract the chat-id from a Feishu URL
64. config init refused by the system, how to troubleshoot
65. What if `--recommend` permissions are not enough
66. How to initialize if your company is not on the feishu.cn domain
67. What strange errors a wrong Node.js version causes
68. Why PowerShell JSON parameters error out on Windows
69. Authorization link expired or rejected, what to do
70. Bot not in the group, message send errors, how to fix
71. How to clean up stale cache when switching accounts
72. CLI-created document asks you to request permission, why?
73. Base attachment download returns 403, what went wrong
74. AI created select options on its own in a Base field, how to stop it
75. What Wiki knowledge base gaps to work around right now
76. Created document cannot be moved into the knowledge base, why?
77. Markdown import into Feishu docs adds a bunch of blank lines
78. Ordered list numbers become plain text in CLI-written docs
79. Why callout highlight blocks and mermaid diagrams won't read out
80. Things I wish I had known earlier after a month of Feishu CLI

## V. Automation Workflows and Advanced Practice (14 questions)

81. How to make Feishu CLI automation tasks run on a schedule
82. How to wire the Feishu CLI into a CI/CD pipeline
83. How event subscription lets AI respond to Feishu messages in real time
84. How to write a custom Skill to wrap repeated operations
85. How to handle Base cross-table relations with the Feishu CLI
86. How to batch-manage Feishu task lists with the CLI
87. How to package and distribute a custom Skill to the team
88. Can one Feishu CLI authorization be shared by a team?
89. How can an enterprise admin control who can create CLI apps?
90. How to choose between event subscription and polling without wasting quota
91. How to monitor whether an automation script is actually running
92. How to isolate identities across multiple Feishu apps
93. How to run the Feishu CLI as a resident service on a cloud server
94. Feishu message history is capped at 14 days, how to archive long-term

## VI. Cross-Platform Comparison and Boundary Reflection (6 questions)

95. Feishu vs DingTalk vs WeCom CLIs, who actually performs best in practice?
96. How long can Feishu CLI's lead hold?
97. When should you bypass the Feishu CLI and call the API directly?
98. Can the Feishu CLI access Lark (international) data?
99. Who is simply wasting time touching the Feishu CLI?
100. What will Agent-native office work ultimately look like?

---

**Chapter distribution:** I 16 / II 26 / III 15 / IV 23 / V 14 / VI 6 = 100

**Version note:** v3 final revised edition
- v1 → v2: based on real user Q&A review, removed 15 fabricated questions, added 15 real high-frequency questions
- v2 → v3: based on the user-insight report final review, filled in core taglines, first-tier must-write questions, virality formulas, and experience-type questions
- v3 added 7 high-virality questions: core tagline (Q4), design philosophy (Q5), top-5 scenario aggregation (Q17), Claude Code operating Feishu (Q39), efficiency quantification (Q40), overall security-fear solution (Q58), experience-style close (Q80)
