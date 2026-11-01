# Vernaculum SCP:MS v1.0.0 overview

**Status: Accepted / Active / Stable.** This is a non-authoritative orientation aid. The complete [canonical PROTOCOL.md on main](https://github.com/dfdy/vernaculum-scp-ms/blob/main/PROTOCOL.md) governs whenever this overview omits detail or differs.

## One specification, complete working context

Participating agents read the whole canonical Markdown before claiming adherence and reload it after recognised context loss or recovery. Minimum-sufficient governs the specification's own size; separate communication rules call for economical exchanges. It does not mean selecting only a subset of governing rules.

Vernaculum is voluntarily followed by agents. It supplies shared meanings and obligations, while user, owner, organisational and host authority remains separate. Neither structured content nor claimed conformance supplies tool permissions or proves execution.

## Messages and records are different

| Aspect | Agent messages | Durable records |
| --- | --- | --- |
| Purpose | Exchange a task, question, result, refusal or handoff | Preserve requirements, decisions, evidence and outstanding work |
| Representation | One complete inline UTF-8 YAML mapping | UTF-8 JSON is recommended; one logical object per stable identity |
| Identity | Message ID unique within a conversation | Persistent record ID and increasing revision |
| Version | Offered during establishment; agreed thereafter | Declared interpretation version retained in history |
| Status | A response reports completed, partial, failed or blocked | Lifecycle state depends on the record kind |
| Authority | A request or readiness claim grants none | Acceptance requires an independently applicable basis |

The shared message envelope contains `scp`, `version`, `kind`, `id`, `sender`, `recipient`, `conversation` and `body`, plus reply bindings and references where applicable. Establishment starts with `body.supported_versions` in a `hello`; `ready` states the accepted version and refers to its initiating hello. Other core kinds are `need`, `offer`, `request`, `response`, `clarification`, `error`, `handoff` and `amendment_notice`.

Durable kinds are requirement, proposal, decision, implementation evidence, verification result, issue, handoff and protocol change. Their precise fields, statuses and relationships are defined in the canonical tables. A message handoff and a durable handoff record serve related purposes but are not interchangeable contracts.

## Continuity and evolution

A checkpoint preserves working claims, not authority. On resumption, reload the whole specification and reconcile the checkpoint with current evidence and record revisions before consequential operations.

Peers may accept optional namespaced language extensions. Those extensions cannot change core meanings, permissions, obligations or historical interpretation. A proposed core edit takes effect only through explicit owner-approved publication to canonical main and agreement on the applicable version or compatibility profile.

Historical records remain readable under their declared versions. Their old fields or authorization conventions do not redefine the accepted v1.0.0 core.

See the [README](./README.md) for adoption and the [release notes](./RELEASE-NOTES.md) for migration considerations.
