# Communication Protocol Overview, Not Authoritative

**Vernaculum SCP:MS — Semantic Communication Protocol, Minimum-Sufficient**

This document maps the communication structures and vocabulary defined by Vernaculum SCP:MS. It is a **non-authoritative orientation aid**, not a specification, validator or executable instruction. **[PROTOCOL.md](./PROTOCOL.md) alone is authoritative** and governs wherever this overview omits detail or differs.

## Reading the trees

The two trees separate **messages exchanged between agents** from **durable records maintained between exchanges**. They repeat shared protocol information, including identity, scopes and amendment classes, so that either tree can be read independently. The scope names denote rule-selection categories, not message or record fields or permissions.

Indentation indicates nesting. Ordinary text indicates the expected content; YAML flow lists and JSON arrays in these trees show *permitted alternatives* rather than values to send together. These are **illustrative structure maps**, not dispatchable messages or formal schemas. The `format` field describes the protocol document format, not the encoding of an individual message or record.

## Machine-to-machine messaging — YAML

Agents exchange a single inline YAML message with a common envelope and a `body` determined by the message `kind`. Negotiation, requests, responses, clarifications and message handoffs belong here. The presence of a field in the tree does not imply it is required for every message.

```yaml
VERNACULUM-SCP-MS:
  version: 1.0.0-rc.3
  format: 6
  authority: canonical_natural_language_only
  scopes: [kernel, baseline, negotiation, exchange, records, plan, implement, verify, handoff, amend, recovery, preflight]
  message_envelope:
    scp: VERNACULUM-SCP-MS
    version: Agreed protocol version
    kind: [hello, ready, need, offer, request, response, clarification, error, handoff, amendment_notice]
    id: Unique message identifier within the conversation
    sender: Sending agent identifier
    recipient: Receiving agent identifier
    conversation: Shared conversation identifier
    body: Content required by the selected message kind
    reply_to: Identifier of the message being answered
    refs: [Stable record or source reference]
  message_types:
    hello:
      body:
        fingerprint: SHA-256 fingerprint of the protocol document
    ready:
      body:
        accepted_version: Verified compatible protocol version
    need:
      body:
        reason: Reason a compatible verified protocol is needed
    offer:
      body:
        bundle_ref: Reference to the complete protocol bundle
    request:
      body:
        action: Requested task or operation
        target: Target of the requested action
    response:
      body:
        status: [completed, partial, failed, blocked]
    clarification:
      body:
        question: Clarification question about the preceding message
    error:
      body:
        code: Error or rejection code
        explanation: Explanation of the error or rejection
    handoff:
      body:
        objective: Objective of the transferred work
        next_action: Next action for the receiving agent
    amendment_notice:
      body:
        amendment_id: Identifier of the verified registered amendment
        version: Version associated with the amendment
  amendment_classes: [compatible, breaking, governance]
```

## Durable records — JSON

Durable records preserve requirements, proposals, decisions, implementation evidence, verification results, issues, handoffs and protocol changes. **Their actual encoding is JSON**, validated against the protocol’s JSON Schema contracts. The JSON below is a structural reference tree, not an individual record or an executable schema. Record `status` is a lifecycle state, not a message response status.

```json
{
  "VERNACULUM-SCP-MS": {
    "version": "1.0.0-rc.3",
    "format": 6,
    "authority": "canonical_natural_language_only",
    "scopes": ["kernel", "baseline", "negotiation", "exchange", "records", "plan", "implement", "verify", "handoff", "amend", "recovery", "preflight"],
    "record_envelope": {
      "protocol_version": "Protocol version under which the record is interpreted",
      "record_version": "Monotonically increasing record revision number",
      "id": "Persistent record identifier",
      "kind": ["requirement", "proposal", "decision", "implementation_evidence", "verification_result", "issue", "handoff", "protocol_change"],
      "subject": "Subject or component addressed by the record",
      "summary": "Concise declarative summary",
      "status": "Lifecycle status permitted for the selected record kind",
      "authority": {
        "basis": ["agent_proposal", "user_directive", "approved_specification", "observed_implementation", "external_standard", "agent_report"]
      },
      "source_refs": [
        {
          "role": ["normative", "observed", "context", "approval", "external"]
        }
      ],
      "relations": [
        {
          "type": ["derived_from", "proposes_change_to", "implements", "verifies", "contradicts", "supersedes", "blocks", "affects", "resolves", "hands_off"]
        }
      ],
      "actor": "Actual person or agent responsible for the record",
      "created_on": "YYYY-MM-DD",
      "content": "Content required by the selected record kind",
      "extensions": "Registered namespaced extension content"
    },
    "record_types": {
      "requirement": {
        "statuses": ["proposed", "accepted", "rejected", "superseded"],
        "content": {
          "statement": "Normative requirement statement",
          "acceptance_criteria": "Criteria for accepting the requirement"
        }
      },
      "proposal": {
        "statuses": ["proposed", "accepted", "rejected", "superseded"],
        "content": {
          "change": "Proposed modification",
          "rationale": "Reason for the proposed change",
          "acceptance_criteria": "Criteria for accepting the proposed change",
          "open_questions": "Outstanding questions"
        }
      },
      "decision": {
        "statuses": ["accepted", "superseded"],
        "content": {
          "resolution": "Approved decision or resolution",
          "approved_by": "Identity of the approver",
          "approval_ref": "Reference to the approval evidence"
        }
      },
      "implementation_evidence": {
        "statuses": ["reported", "superseded"],
        "content": {
          "observations": "Observed implementation facts",
          "paths": "Exact file paths or revisions supporting the observations"
        }
      },
      "verification_result": {
        "statuses": ["reported", "superseded"],
        "content": {
          "target": "Artifact or assertion being verified",
          "outcome": ["pass", "fail", "partial", "not_run"],
          "method": "Verification method or command actually used",
          "evidence": "References to observed verification evidence"
        }
      },
      "issue": {
        "statuses": ["open", "blocked", "resolved", "superseded"],
        "content": {
          "problem": "Issue or contradiction",
          "impact": "Effect of the issue",
          "blocking": [true, false],
          "next_action": "Next action to address the issue"
        }
      },
      "handoff": {
        "statuses": ["open", "acknowledged", "completed"],
        "content": {
          "from_agent": "Identifier of the handing-off agent",
          "to_agent": "Identifier of the receiving agent",
          "objective": "Objective of the transferred work",
          "confirmed": "Confirmed facts and their sources",
          "next_actions": "Remaining actions for the recipient",
          "open_questions": "Outstanding questions"
        }
      },
      "protocol_change": {
        "statuses": ["proposed", "applied", "rejected", "reverted"],
        "content": {
          "change_class": ["compatible", "breaking", "governance"],
          "change_summary": "Summary of the protocol modification",
          "rationale": "Reason for the modification",
          "files_changed": "Files affected by the modification",
          "compatibility": "Compatibility assessment",
          "rollback": "Procedure for reverting the modification",
          "validation": "Validation results for the modification"
        }
      }
    },
    "relationships": ["derived_from", "proposes_change_to", "implements", "verifies", "contradicts", "supersedes", "blocks", "affects", "resolves", "hands_off"],
    "amendment_classes": ["compatible", "breaking", "governance"]
  }
}
```

## Authority and use

A message `handoff` and a record `handoff` are different contracts; both appear in their respective trees. The same applies to protocol amendments communicated by `amendment_notice` and changes captured as `protocol_change` records. Shared vocabulary does not make the two encodings interchangeable.

Use **[PROTOCOL.md](./PROTOCOL.md)** for mandatory and optional fields, exact types, validation, scope applicability, version compatibility, authorisation and security requirements. Structural validity alone does not establish identity, approval, execution or delivery.

Return to the [README](./README.md) for adoption guidance or explore [possible tool integrations](./docs/tool-ecosystem-exploration.md).
