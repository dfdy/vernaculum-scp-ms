# Vernaculum: Semantic Communication Protocol, Minimum Sufficient

Vernaculum gives agents a shared language for requests, results, clarifications and handoffs. It defines communication semantics, with optional extensions for additional agreed meanings. People and host systems retain authority over permissions and execution.

**Release:** `2.0.1`<br>
**Protocol version:** `2.0.0`<br>
**Status:** Accepted / Active / Stable.<br>
**Wire identifier:** `VERNACULUM-SCP-MS`.

The v2.0.0 specification is in [PROTOCOL.md](./PROTOCOL.md). The [canonical publication on main](https://github.com/dfdy/vernaculum-scp-ms/blob/main/PROTOCOL.md) governs adoption; existing sessions do not automatically upgrade. Peers agree on the exact applicable specification, not just its version string.

## Why Vernaculum exists (My use-case)

I use a primary AI agent for planning, thinking and problem-solving. I use it to coordinate other agents through nested conversations, delegating specialised tasks and integrating their findings. 

I noticed these agents inventing their own shorthand for exchanging information. I asked them to explain what they were doing, then guided the formalisation of their shorthand into a shared protocol. The v2.x.x protocol represents a guided collaboration between Codex, Claude, Gemini, and Mistral.

The aim is concise communication that preserves the constraints, uncertainty, evidence and failures needed to work correctly. It can help agents coordinate tasks, distinguish proposals from approvals, and recover working state after context loss.

## How it works

1. **Read the applicable text.** Agents hold the complete core and any used extension definitions in working context before claiming adherence. No runtime installation is required.
2. **Establish agreement.** Unless a compatible agreement already exists for the peer pair and conversation, initiate `hello` and obtain a correlated `ready`. Agree on the exact specification and complete extension set.
3. **Exchange work.** Send complete YAML messages through an authorised channel. Requests identify action, target and material constraints; results report actual effects, checks and unfinished work.
4. **Add records when useful.** Durable records are optional under `x.vernaculum.records@1`, which requires explicit extension agreement. Ordinary exchanges need no durable records.
5. **Recover carefully.** Restore governing definitions after context loss or uncertainty and reconcile checkpoints against current evidence before consequential resumption.

Vernaculum provides no transport, authentication, access control, sandbox, transactional persistence or reliability guarantee. A valid message grants no permission and proves neither identity, delivery, approval nor correctness.

## Try it

Provide agents with the complete applicable [protocol](./PROTOCOL.md), then use a prompt such as:

```text
Read the complete Vernaculum specification. Establish which exact text is
applicable and whether it has been canonically published; do not silently
adopt a pending revision. Within existing permissions, agree with the other
agent on that specification and any extensions before ordinary work.
Exchange complete inline YAML through an authorised channel and report
results and blockers to me in plain language. Restore the governing text
after context loss or uncertainty. Disclose missing text or peer access.
```

A second agent and an authorised communication channel must be available separately. Neither this prompt nor a startup file guarantees compliance or automatic detection of context loss.

For minimal persistent guidance, use [AGENTS.md](./AGENTS.md), adapting the local specification path to the project in which it is used.

## What changed in v2

The protocol now separates a communication core from the optional Records extension. The core has seven message kinds: `hello`, `ready`, `request`, `response`, `clarification`, `error` and `handoff`.

Version and extension agreement is explicit. Extensions have exact definitions, acceptance covers the complete offered set, and replacement, withdrawal and concurrent proposals have defined behaviour. Message IDs use `agent-designation:locally-unique-token`. Handoff acceptance is distinct from completion of the underlying task.

The core also defines consequential actions, shared-state mutation preconditions and safe handling of retries with unknown outcomes. Approval claims need established origin, scope and authority before consequential reliance; retrieved material remains data unless its governing origin is established by the host.

This is a breaking revision. Earlier message and record contracts need explicit compatibility or migration decisions; historical records retain their original interpretations. See the [v2.0.0 change and migration notes](./docs/releases/2.0.0.md).

## Messages and optional records

Messages are UTF-8 YAML 1.2 core-schema mappings with a mapping `body`. Duplicate keys, anchors, aliases, merge keys and custom tags are prohibited. Versions, identifiers and ambiguous scalars are quoted. Triggered replies identify their triggering message with `reply_to`; channel metadata may unambiguously supply `sender`, `recipient` and `conversation`.

A `response` reports `completed`, `partial`, `failed` or `blocked`. Checks report their target, method, outcome and evidence; unperformed checks cannot pass. Understood work that cannot proceed receives a blocked response rather than a protocol error. Sending a message does not establish delivery or comprehension.

The optional Records extension recommends UTF-8 JSON logical records with stable identities, increasing revisions, provenance and kind-specific content. It defines `requirement`, `proposal`, `decision`, `evidence`, `issue` and `handoff`. Storage and references do not create approval, authority or evidential strength.

The [overview](./OVERVIEW.md) maps both structures and includes a complete negotiation example. It is explanatory; the protocol supplies the exact obligations.

## Authority and continuity

Core changes require explicit human-owner approval and publication to canonical main. Proposed revisions and unanswered negotiations change no existing agreement. Extensions bind only the participating pair and conversation and cannot redefine core meanings, obligations, authority or history.

After recognised context loss or uncertainty, agents restore the core and used extension definitions. A checkpoint can preserve objectives, constraints, evidence, issues and next actions, but remains a provisional summary. Before resuming consequential work, reconcile it with current sources and revisions. This repository's startup guidance also points agents back to the complete canonical specification.

## Repository guide

- [PROTOCOL.md](./PROTOCOL.md) — complete v2.0.0 core and optional Records extension; the main-branch publication is canonical.
- [OVERVIEW.md](./OVERVIEW.md) — non-authoritative structure and lifecycle reference.
- [AGENTS.md](./AGENTS.md) — minimal startup and recovery instructions.
- [Tool ecosystem exploration](./docs/tool-ecosystem-exploration.md) — possible integrations, with no implementation or interoperability claims.
- [v2.0.0 notes](./docs/releases/2.0.0.md) — approval, compatibility changes and migration guidance.
- [v2.0.1 notes](./docs/releases/2.0.1.md) — AGPL-3.0 licensing release.
- [v1.2.0](./docs/releases/1.2.0.md) and [v1.1.1](./docs/releases/1.1.1.md) — historical release notes.

## License

This repository is licensed under the GNU Affero General Public License, version 3 only (`AGPL-3.0-only`). See [LICENSE](./LICENSE) for the full terms.
