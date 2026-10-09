# Running cross-model reviews

Use the [skill](../skills/agent-arena/SKILL.md) for intent, authorization and completion rules, and the [runtime reference](../skills/agent-arena/references/runtime.md) for actual CLI calls. This guide illustrates packet construction; it does not impose extra rounds or budgets.

## Prepare the packet

For a new design discussion, give each participant the same user request, relevant original wording and corrections, success criteria, raw facts and approved evidence paths. Save all independent first answers before exchanging them. Keep the primary's preferred design out of a peer's first pass.

For review of an existing artifact, share that artifact directly. Supply exact files or raw excerpts with paths, omissions and access to necessary context. Include relevant test commands and results as evidence; omit persuasive commentary such as “already safe” or “just confirm.” A reviewer must be able to disagree.

```text
User request and current decisions: ...
Superseded decisions: ...
Success criteria: ...
Evidence root and actual files/version: ...
Known facts, assumptions and omissions: ...
Authorized recipient, tools, content and actions: ...
Question: identify supported defects, alternatives and uncertainty.
For each finding: location, evidence, affected requirement, severity.
```

The primary compiles this from available context; the user need not fill out a form. An inventory and named snapshot keep materials understandable. They do not introduce a hash, stat or UUID gate. Missing essential evidence limits only the affected review coverage.

## Send and collect

Write the packet to a file, send it through the locally supported stdin mechanism, and capture raw output/stderr to files. This avoids shell quoting and argv-size problems; it does not diagnose every slow call as an argv failure. Verify model availability/authentication and supported tools before the real call. Keep credentials out of prompts, packets and diagnostics.

Use the [Claude examples](../skills/agent-arena/references/runtime.md#claude-code) or the chosen harness's current help. For another harness, verify its noninteractive and resume syntax rather than copying Claude flags.

Collect completed results before reporting; preserve raw text if a digest parser fails. The [optional local parser](../skills/agent-arena/references/state-and-results.md#optional-claude-parser) can index Claude results but cannot judge whether they substantively answer the question. A wrapper success with `is_error=true`, pending queue entry and useful partial answer are distinct states.

## Scope and recovery

An initial bounded review can use a closed set of raw evidence. Splitting questions is useful when they are independent and their dependencies remain visible. Do not silently turn a failed open review into selected excerpts, disable discovery, or drop parts of the question to force an answer. Keep the original scope during lossless recovery or obtain authorization for the concrete change.

Separate queue wait, model runtime, host observation windows and actual failures. One owner should launch each topic/round; adding subagents to a serialized provider does not create more concurrent model requests. Preserve all failed attempts and recovery evidence.

## Review and finish

Discussion requires actual exchange after independent proposals. Existing-artifact reviews may finish with one sufficient substantive result. Changes require focused rechecks of the delta, unresolved findings, necessary context and affected downstream results. Optional suggestions do not hold delivery automatically.

When the user requests convergence, both sides must explicitly accept the same final revision with no material unresolved blocker. If a required participant is pending, keep it pending. Otherwise ordinary discussions can end with useful evidence and preserved dissent. Companion and supervision retain their separate lifecycles.

Report mode, actual model identities and verification limits, successes, failed/recovered attempts with causes, unfinished coverage and the conclusion. Distinguish design, source, outputs and measured behavior. State what another retry would change, or that recovery succeeded and no retry is needed.
