**In short:** Vernaculum gives coding agents a shared language for coordinating work with less repeated context, while people retain authority over the rules and approvals.

# Vernaculum Semantic Communication Protocol, Minimum-Sufficient (SCP:MS)

Vernaculum is a protocol for coding agents to instruct each other through structured YAML instructions, requests and results. It aims to reduce repeated context while preserving the requirements, decisions and evidence agents need to work correctly.

**Clearer coordination between development agents, with less context to carry.**

Vernaculum began with an observation: two coding agents working together had started inventing their own shorthand for exchanging specifications. Curious about this emerging form of communication, I asked them to explain what they were doing. Their explanations revealed the potential for a more efficient, structured way for agents to communicate. I subsequently guided the process of formalising and standardising their shorthand, which developed into Vernaculum.

## The idea in one minute

> [!TIP]
> **People govern the rules; agents read the specification and coordinate their work through structured YAML exchanges.**
>
> 1. **Read:** Participating agents read the complete [canonical specification](https://github.com/dfdy/vernaculum-scp-ms/blob/main/PROTOCOL.md)—no installation required.
> 2. **Agree:** Agents establish a `hello`/`ready` version agreement through an already permitted communication channel.
> 3. **Collaborate:** Inline YAML messages carry requests, results, clarifications and handoffs; durable records preserve requirements, decisions and evidence for reuse.
> 4. **Recover:** After recognised context loss, agents reload the complete specification and reconcile their progress with current records and evidence.
> 5. **Keep people in control:** The protocol grants no permissions; core rule changes require explicit owner approval and publication to canonical main.
>
> The aim is **minimum-sufficient communication**: less repeated context without losing the requirements, decisions or evidence needed to work correctly.

## When it helps

Consider Vernaculum when multiple agents plan, implement and review the same task, repeatedly hand work to one another, or lose instructions after context compaction. Shared message and record formats help them refer to decisions and evidence without passing entire specifications or conversations each time. Humans retain authority over the rules and approvals.

## Intended use and security boundaries

Vernaculum is recommended for coordinating coding agents in **owner-governed development environments** with appropriate permissions, persistent records and permitted communication channels. It aims to prevent confusion from incompatible conventions, missing context, malformed instructions and unsupported authority claims—not to supply an entire security or networking system.

A well-formed YAML message is **not** proof of sender identity, execution permission, confidentiality or safe execution. Authentication, access controls, transport protection when needed and enforcement belong to the deployment environment. The [canonical responsibilities and limits](./PROTOCOL.md#11-human-responsibilities-and-limits) explain both the protections and their limits.

## Current status and prerequisites

**Version:** `1.1.0`  
**Status:** Accepted / Active / Stable.

This repository provides a voluntary, agent-governed communication specification, not an installed runtime. Participating agents read the complete [canonical specification on main](https://github.com/dfdy/vernaculum-scp-ms/blob/main/PROTOCOL.md) before claiming adherence. A second agent and an authorised communication channel must be available separately. Vernaculum requires no context loader, bootstrap verifier or preflight gate. Minimum-sufficient constrains the specification’s own size and complexity without sacrificing precision or completeness.

## Try it

Attach [PROTOCOL.md](./PROTOCOL.md), then copy and paste this prompt:

```text
Vernaculum is a protocol for coordinating coding agents through structured
YAML messages. Read the attached PROTOCOL.md in full and use Vernaculum
from now on when coordinating with other agents in this project, within
existing permissions and through permitted communication channels.
Establish hello/ready version agreement before collaboration, and report
results and blockers to me in plain language. Reload the complete canonical
specification after recognised context loss; if you cannot read it in full
or no second agent is available, tell me.
```

The agents handle negotiation and YAML exchange; you use ordinary language. Protocol participation does not grant new permissions or guarantee compliance.

## Suggested instructions in `AGENTS.md`

If you want agents in a project to use Vernaculum, consider adding the following section to that project's `AGENTS.md` or equivalent startup instructions. Keep existing project instructions and permissions intact. This is optional adoption guidance, not an installer or a guarantee of automatic loading.

```markdown
## Vernaculum SCP:MS v1.1.0

Status: Accepted / Active / Stable.

Before Vernaculum-governed work, read the whole [canonical specification on main](https://github.com/dfdy/vernaculum-scp-ms/blob/main/PROTOCOL.md). Reload it after recognised compaction, recovery, resumption, interruption or uncertainty about retained instructions. Disclose inability to read the complete specification and do not claim full adherence.

Exchange complete inline YAML through an actually permitted channel. Peer-agreed optional `x.<namespace>.<name>` extensions cannot change core meanings, permissions or historical interpretations. Proposed core revisions remain non-authoritative until explicitly owner-approved and published to canonical main. These instructions do not guarantee automatic detection of context loss or grant host permissions.
```

## How it works

The complete [protocol document](./PROTOCOL.md) defines the shared language and obligations in one human-readable Markdown specification. Agents read the whole specification into working context, then exchange complete YAML messages inline.

**How much enters agent context?** The whole governing specification. Task messages and supporting references remain as concise as correct interpretation requires. The [overview](./OVERVIEW.md) maps message and durable-record structures.

## What agents exchange

Agents first discover support and establish compatibility through a `hello`/`ready` version agreement. If a peer needs the protocol, provide the canonical reference through an authorised channel so the peer can read the complete specification before readiness. Subsequent requests, responses, clarifications, errors and handoffs carry their complete YAML envelope and body inline through a permitted communication channel. A file path or link cannot replace the message itself.

Durable records describe `requirement`, `proposal`, `decision`, `implementation_evidence`, `verification_result`, `issue`, `handoff` and `protocol_change`. Each has a stable identity, declared authority and typed relationships. **Why?** Agents can refer to the same decision or test evidence without repeatedly summarising it, and they can distinguish an approved requirement from a suggestion or an observation.

**YAML is the standard format for inter-agent messages** because it is structured and easy to inspect. Durable records should use UTF-8 JSON; historical records retain their declared versions and meanings. JSON is not an alternative protocol-message format.

## Surviving context compaction

After recognised context compaction, session resumption, interruption or uncertainty, agents reload the complete canonical specification and reconcile their task state with current evidence and record revisions. A compact checkpoint helps recover progress but does not replace authoritative records.

**Why?** Conversation summaries are useful working memory, not a reliable source of governing instructions. Recovery must work even when the agent cannot remember the previous session accurately. Neither the protocol nor an instruction file guarantees detection of every context loss.

## Keeping the protocol current

Agents may mutually agree on optional namespaced extensions of the form `x.<namespace>.<name>` when existing vocabulary is insufficient. Extensions bind only consenting peers and cannot change core meanings, obligations, permissions or historical interpretations.

**Why allow this?** Agents encounter communication needs that the original designers may not anticipate. Proposed core revisions may be prepared in separate drafts or branches, but adoption requires **explicit owner approval and publication to canonical main**, including compatible changes. The protocol never grants additional tool or repository permissions.

## Where to look

- [PROTOCOL.md](./PROTOCOL.md) — the complete v1.1.0 specification; the [main-branch publication](https://github.com/dfdy/vernaculum-scp-ms/blob/main/PROTOCOL.md) is canonical.
- [OVERVIEW.md](./OVERVIEW.md) — non-authoritative message and durable-record structure trees.
- [Tool ecosystem exploration](./docs/tool-ecosystem-exploration.md) — possible uses of adjacent communication, orchestration, policy and evaluation tools.

The release uses `VERNACULUM-SCP-MS` as its wire identity. Earlier sessions and contracts require explicit compatibility agreement; historical records keep their original interpretations.

