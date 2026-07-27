# Appendix · References

This book is compiled and written based on the following sources. The body no longer carries per-question citations; all origins are consolidated here, grouped by source domain, with entries within a group ordered from most to least referenced.

---

## I. Official Documentation and Code Repositories

| # | Source | Description | Coverage |
|---|--------|-------------|----------|
| 1 | lark-cli official README (GitHub: larksuite/cli) | Overall CLI introduction, three-tier command system, auth system, Skills list, security notes | Whole book |
| 2 | lark-cli CHANGELOG (69 version logs) | Version evolution, feature additions, bug-fix records | Ch. 1, 3, 4, 5 |
| 3 | lark-cli AGENTS.md | Contributor guide, local build flow, PR checklist | Ch. 5 |
| 4 | lark-cli Skills directory (26 SKILL.md) | Trigger words, parameters, execution logic per business-domain Skill | Ch. 2, 3, 4, 5 |
| 5 | Feishu Open Platform official docs | OAuth flow, permission scope definitions, API endpoints, error codes | Ch. 3, 4 |

## II. GitHub Issues and Community Feedback

| # | Source | Description | Coverage |
|---|--------|-------------|----------|
| 6 | Issue #442: auth login no permission | Authorization login no-permission problem | Ch. 4 |
| 7 | Issue #416: auth scope diagnostics | Permission-diagnosis enhancement request | Ch. 3 |
| 8 | Issue #394: permission denied 230027 | 403 error root-cause analysis | Ch. 4 |
| 9 | Issue #337: config init refused | config init refused (Windows proxy problem) | Ch. 4 |
| 10 | Issue #181: auth consent auto-submits drafts | Authorization flow auto-submits drafts | Ch. 3 |
| 11 | Issue #913: app profile mismatch low-signal errors | Profile mismatch causing low-signal errors | Ch. 4, 5 |
| 12 | Issue #1405: hermes home context leak | Context-leak problem | Ch. 3 |
| 13 | Issue #1122: base attachment download 403 | Base attachment download 403 | Ch. 4 |
| 14 | Issue #1846: auth 403 scope combination | Permission combination causing 403 | Ch. 4 |
| 15 | Issue #248: keychain master key missing | Keychain master-key loss recovery | Ch. 3, 4 |
| 16 | Issue #76: auth login custom scopes | Custom scope authorization | Ch. 3, 4 |
| 17 | Issue #58: wiki capabilities gap | Wiki capability gap | Ch. 4 |
| 18 | Issue #51: drive folder file listing gap | Cloud-drive file-listing gap | Ch. 4 |
| 19 | Issue #64: windows params json parsing | Windows JSON-parameter parsing problem | Ch. 4 |
| 20 | Issue #390: recommend default readonly | Suggest default read-only permission | Ch. 3, 4 |
| 21 | Issue #1651: launcher addons broad permissions | Launcher over-broad permission scope | Ch. 4 |
| 22 | Issue #1649: im message read status | Message read-status query | Ch. 2 |
| 23 | Issue #1746: task inline image unreachable | Task inline image unreachable | Ch. 2 |
| 24 | Issue #1805: bot follow created threads | Bot follows created threads | Ch. 2 |
| 25 | Issue #590: page all silent truncation | Pagination silent truncation | Ch. 2 |
| 26 | Issue #1167: openapi quota clarification | OpenAPI quota clarification | Ch. 5 |
| 27 | Issue #914: doctor auth status user bot split | doctor command distinguishing user/bot status | Ch. 3 |
| 28 | Issue #780: approval user identity deprecated scopes | Approval user-identity scope change | Ch. 3 |
| 29 | Issue #766: auth login exclude scopes | auth login excluding certain scopes | Ch. 3 |
| 30 | Issue #804: unified skill organization | Skill unified-organization suggestion (umbrella skill) | Ch. 3, 5 |
| 31 | Issue #1115: im messages export | Message bulk export | Ch. 5 |
| 32 | Issue #1430: cardkit completion renotification | Card completion re-notification | Ch. 2 |
| 33 | Issue #813: sub page list stripped | sub-page-list block discarded | Ch. 4 |
| 34 | Issue #814: mention doc token type rewrite | mention doc token type rewritten | Ch. 4 |
| 35 | Issue #818: mention doc label overwritten | mention doc label overwritten | Ch. 4 |
| 36 | Issue #816: list blockquote reshape | List-nested-quote-block reshape | Ch. 4 |
| 37 | Issue #817: adjacent blockquotes fused | Adjacent quote blocks fused | Ch. 4 |
| 38 | Issue #819: overwrite title stacking | Overwrite-write title stacking | Ch. 4 |
| 39 | Issue #829: v2 update legacy quote fails | v2 update legacy quote-block fails | Ch. 4 |
| 40 | Issue #643: block level lossless preservation | Block-level lossless-preservation need | Ch. 4 |
| 41 | Issue #842: search filter ignored | Search filter ignored | Ch. 2 |
| 42 | Issue #772: selective skill install | Selective Skill install mode | Ch. 3, 5 |
| 43 | Issue #1848: skill global injection context cost | Skill global-injection context cost | Ch. 3 |
| 44 | Issue #813-842 series: markdown conversion problems | Markdown-to-Feishu-doc conversion loss | Ch. 4 |

## III. Community Q&A and User Discussions

| # | Source | Description | Coverage |
|---|--------|-------------|----------|
| 45 | Feishu CLI discussion-group Q&A compilation (June 1 group, 71KB) | June community high-frequency Q&A | Whole book |
| 46 | Feishu CLI discussion-group Q&A compilation (July 1 group, 8KB) | Early July community questions | Whole book |
| 47 | Feishu CLI discussion-group Q&A compilation (July 1-6) | Early-July community questions | Whole book |
| 48 | Feishu CLI discussion-group Q&A compilation (basic version, 13KB) | Early community accumulated high-frequency questions | Whole book |
| 49 | Q&A collection (June 1-14, 99KB) | Mid-early-June detailed Q&A | Whole book |
| 50 | Q&A collection (June 15-21, 36KB) | Mid-June detailed Q&A | Whole book |
| 51 | Q&A collection (June 22-30, 37KB) | Late-June detailed Q&A | Whole book |

## IV. Official-Account Articles and Industry Analysis

| # | Source | Description | Coverage |
|---|--------|-------------|----------|
| 52 | WeChat official account "AI 时代漫游指南" 《飞书 CLI AI 实战》 | Scenario-based Feishu CLI interpretation | Ch. 1, 2 |
| 53 | ai-bot.cn 《飞书、企业微信、钉钉 CLI 深度实测对比》 | Three CLIs measured comparison | Ch. 6 |
| 54 | WeChat official account "工程师的第二大脑" 《飞书 CLI 正式开源》 | Technical-perspective CLI interpretation | Ch. 1 |
| 55 | WeChat official account "发狂的书生" 《飞书开源、钉钉建广场、企微沉默》 | Industry commentary on the three open-sourcing events | Ch. 1, 6 |
| 56 | Zhihu 《协同工具终局之战：飞书如何打破"叫好难叫座"的增长魔咒》 | Feishu business analysis, Feishu scale data | Ch. 1, 6 |
| 57 | Sohu 《飞书 2025 年加速全球化布局》 | Feishu globalization strategy, Lark version info | Ch. 6 |

## V. User-Insight Report

| # | Source | Description | Coverage |
|---|--------|-------------|----------|
| 58 | 《关于飞书 CLI 的 100 个问题》用户洞察报告 (2026-07-10) | Customer-tier segmentation, need pool, pain pool, itch pool, content strategy, topic priority | Whole-book topic selection and narrative caliber |

---

## Version and Data Cutoff Notes

- This book is based on public information of lark-cli v1.0.68 (2026-07-09) and earlier versions
- GitHub data cutoff 2026-07-10: 15.4k stars, 69 releases, 159 open issues
- Three-CLI comparison data cutoff 2026-07-10
- The Feishu CLI iterates very frequently (averaging 2-3 version updates per week); some command parameters, Skill lists, and error codes may change in new versions. The official latest documentation prevails.

## How to Give Feedback

- Book content errors or outdated: file an Issue in the GitHub repository
- Feishu CLI's own bugs: file an Issue in the larksuite/cli repository
- Feishu Open Platform API problems: consult the Feishu Open Platform official docs or submit a ticket

---

> Every judgment and experience in this book comes from cross-validation of the above sources. The body leaves no source traces, but all hard facts (command parameters, error codes, version numbers, capability boundaries) can be traced back to their origin in this appendix. Soft judgments and experiential content come from community discussions and real user feedback, governed by group consensus.
