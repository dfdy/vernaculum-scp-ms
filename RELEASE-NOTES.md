# Vernaculum SCP:MS v1.0.0

**Accepted / Active / Stable.**

The sole canonical specification is [repository-root PROTOCOL.md on main](https://github.com/dfdy/vernaculum-scp-ms/blob/main/PROTOCOL.md). Vernaculum is now a voluntary, agent-governed semantic communication standard, not a mechanically enforced protocol installation.

## Retained capabilities

- Canonical human-readable authority, release agreement and lightweight hello/ready/need negotiation.
- Complete inline YAML messages, registered meanings, reply bindings, clarifications and truthful outcomes.
- Minimum-sufficient communication and preference for reliable, authorised non-inference operations where appropriate.
- Durable record kinds, revisions, provenance, relationships and historical interpretation.
- Planning, implementation, verification, handoff, checkpointing and recovery responsibilities.
- Human authority and explicit limits on claimed compliance versus host-enforced security.
- Peer-agreed optional namespaced fields, kinds, relationships and operations that cannot alter core meanings or permissions.

## Simplified adoption

Agents read the whole canonical Markdown before governed work and reload it after recognised compaction, resumption, recovery, interruption or uncertainty. Minimum-sufficient constrains the complete specification's size without sacrificing precision or necessary obligations.

The former framing, section and bundle integrity manifests, byte-exact serializers, pinned PyYAML profile, generated normative YAML, bootstrap guides/fixtures, mandatory verifier suites, scoped loaders, maintenance pipeline and automated amendment registry/classification mechanisms are removed. They are not replaced by another installation or preflight gate.

## Migration considerations

Earlier protocol sessions and the rc.3 verification/installation model are not automatically compatible with this contract. Establish a new version agreement; `hello` now carries `supported_versions`, not a document fingerprint. Prior verification flags, generated packets and installation state do not establish v1.0.0 adherence.

Read the complete accepted specification. Core amendments always require explicit owner approval and canonical publication, including compatible changes. Peer-agreed namespaced extensions do not amend the core or bind unconsenting peers.

Historical records keep their original versions, identifiers and meanings. Host security, tool access and consequential execution approvals remain independent of protocol participation.

See the [README](./README.md), [overview](./OVERVIEW.md), and [agent instructions](./snippets/AGENTS.md).
