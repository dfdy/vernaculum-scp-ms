# How Vernaculum could learn from the agent-tool ecosystem

**Protocol: Vernaculum SCP:MS v1.0.0 — Accepted / Active / Stable.**

The central opportunity is to reduce unnecessary interpretation while preserving the meaning, constraints, evidence and authority needed to complete a task. Smaller messages help only when the receiving agent still understands the task correctly. Better scheduling, reliable recovery and deterministic operations may save more work than a compact encoding.

This is a non-normative exploration of possible uses and design lessons. It does not claim that these integrations exist, amend the [canonical protocol](https://github.com/dfdy/vernaculum-scp-ms/blob/main/PROTOCOL.md), or make any named product a dependency. Tool capabilities below are supported by linked primary sources; their proposed application to Vernaculum is an assessment, not a vendor interoperability claim. Documentation and interfaces evolve, so an implementation would need an explicit supported version and capability profile.

## Keep the responsibilities distinct

| Responsibility | Vernaculum's contribution | Useful adjacent technologies |
| --- | --- | --- |
| Meaning and context | The complete governing specification, task constraints and typed relationships | JSON Schema, XGrammar, retrieval and immutable references |
| Connections and interaction | Complete messages, compatibility negotiation and truthful outcomes | A2A, MCP, ACP, AG-UI; ANP where cross-domain identity is needed |
| Scheduling and durability | Requirements for valid handoffs and recovery | LangGraph, Google ADK, Microsoft Agent Framework, Temporal, NATS JetStream |
| Decisions and execution | Separation of structural validity, authority and operational preconditions | OPA and ordinary deterministic software |
| Efficiency and observation | Correctness before brevity; total cost per correctly completed task | DSPy, LiteLLM, OpenTelemetry, Phoenix, selective compression |

These technologies are alternatives or complements at different layers. A small deployment need not adopt the entire list.

Four boundaries shape every proposed integration:

1. **Keep the complete YAML message inline.** An outer JSON transport can carry YAML as text, but a link, attachment or translated summary cannot replace the instruction delivered to the receiving agent.
2. **Preserve governing material.** Agents read the whole canonical specification on adoption and after recognised context loss. Retrieval may reduce supporting task material, but cannot replace governing text. A compressed summary cannot become approval or canonical policy.
3. **Separate agreement from permission.** A version agreement, schema pass, authenticated identity or workflow status establishes only its particular fact. Execution still needs applicable authority and operational safeguards.
4. **Reuse capabilities proportionately.** Prefer a small adapter or existing service when it satisfies a concrete need. A possible integration is not a reason to expand the normative protocol.

## 1. Communication and human interaction

### A2A: agent interoperability and task lifecycles

[A2A](https://a2a-protocol.org/latest/definitions/) defines agent communication, task state, messages and content parts, including text. It is a strong candidate for carrying Vernaculum between independently implemented agents.

Vernaculum could use an adapter that places one complete YAML envelope in a text part and presents that decoded text unchanged to the recipient. The adapter would map outer task and message identifiers to Vernaculum conversations and reply bindings, while preserving the distinction between transport acceptance, protocol readiness and task completion. Capability discovery could advertise a supported Vernaculum profile; the actual `hello`/`ready` exchange would still establish agreement on a supported release, without proving file identity or obedience.

The useful lesson is explicit lifecycle modelling. Cancellation, partial results, missing input and terminal outcomes should remain distinguishable. An A2A task status cannot automatically substitute for a truthful Vernaculum response, and a file part containing a YAML document would not satisfy the inline-message requirement.

### MCP: supporting context and deterministic tools

MCP exposes [resources](https://modelcontextprotocol.io/specification/latest/server/resources) and [tools](https://modelcontextprotocol.io/specification/latest/server/tools) through a common interface.

An owner-controlled MCP service could expose the complete canonical text, immutable supporting source revisions and approved records. Optional tools could check records, look up dependencies or perform an already-authorised operation; none is a prerequisite to reading or following the specification. That can eliminate repeated model interpretation of facts that software can establish directly.

A resource URI identifies supporting material; it does not replace a task's inline YAML instruction. Resource contents, tool descriptions and returned text remain untrusted until the appropriate checks succeed. A tool being discoverable does not authorise its invocation. Vernaculum could learn from the separation between resource discovery, tool schemas and execution, while leaving trust and enforcement with the host.

### ACP: coding-agent integration with editors

[Agent Client Protocol](https://agentclientprotocol.com/get-started/introduction) standardises communication between coding agents and editors. Its [tool-call protocol](https://agentclientprotocol.com/protocol/v1/tool-calls) includes progress reporting and permission requests.

ACP could support an editor-facing Vernaculum deployment: display pending operations, surface clarifications and approval requests, and associate tool results with the task that caused them. Its explicit permission outcomes offer a useful design reference for keeping cancellation, rejection and approval distinct.

ACP connects an editor and an agent; it is not automatically an agent-to-agent channel. A bridge would need to deliver complete YAML to the actual peer. An editor session, a remembered approval or a rendered permission label must not be treated as a universal execution grant. Remote capabilities should be assessed against the selected ACP version rather than assumed from the protocol's overall ambitions.

### ANP: identity and discovery across administrative boundaries

[Agent Network Protocol](https://github.com/agent-network-protocol/AgentNetworkProtocol) separates identity, authentication, discovery, messaging and other profiles. Its published specifications also distinguish released components from draft authorization and semantic-negotiation work.

This is relevant when Vernaculum crosses independently administered environments. An optional deployment could use an established identity/discovery layer to locate peers and bind a verified external identity to a claimed sender. Vernaculum could also learn from explicit profile descriptions and visible specification status.

The benefit is conditional: an owner-governed local team may already have adequate identity controls. Adopting decentralized identity solely to exchange local tasks would add complexity. ANP identity would not grant task authority, and dynamic negotiation must not silently alter Vernaculum's core grammar, meanings or agreed version contract. Draft capabilities should not be represented as available guarantees.

### AG-UI: meaningful human oversight

[AG-UI](https://docs.ag-ui.com/introduction) provides an event-based connection between agent backends and user-facing applications, including state updates and human interaction.

It could make Vernaculum's distinctions visible: proposed work, a blocked request, an approval awaiting a decision, a partial outcome, or evidence awaiting review. A UI could show the exact action and target before a consequential operation and correlate the owner's decision with that specific request.

The lesson is to expose actionable state rather than an undifferentiated conversation stream. UI events and displayed success indicators remain observations, not independent approval records. Editing or approving a request must preserve its binding to the operation actually executed. Streaming fragments should be assembled and validated before they are treated as a complete protocol instruction.

## 2. Representation, generation and compression

### JSON Schema: precise structural contracts

[JSON Schema Draft 2020-12](https://json-schema.org/draft/2020-12) can optionally support the JSON representation recommended for durable records. It can express required fields, types, enumerations and conditional structure.

Schemas could make record kinds, peer-agreed namespaced extensions and internal message-construction inputs easier to validate consistently. They can also identify missing structure before a model is asked to interpret a packet. Schema versions and supported validator features should be explicit; a schema dialect is not interchangeable with every constrained-generation engine's supported subset.

Structural success cannot establish that an approval is genuine, a source is current, or a task has sufficient context. Duplicate-key and restricted-YAML checks must occur before validating a parsed object. A deployment can restrict schema resolution to reviewed local definitions; the standard imposes no mandatory schema installation or registry. The useful combination is deterministic shape validation followed by separate authority and operational checks.

### XGrammar: fewer malformed model-generated proposals

[XGrammar](https://xgrammar.mlc.ai/docs/latest/defining_structures/json_generation.html) supports constrained generation from JSON Schema; its [EBNF support](https://xgrammar.mlc.ai/docs/latest/defining_structures/ebnf_grammar.html) can describe custom output languages.

Where inference is necessary, it could constrain an internal task proposal to a typed structure, after which ordinary software builds and validates the actual YAML message. A restricted YAML grammar is another possibility, but would require deliberate coverage of Vernaculum's quoting and scalar rules. This is not evidence of an off-the-shelf Vernaculum grammar.

The expected benefit is fewer formatting failures and corrective model calls. Grammar validity still cannot prove adequate instructions, truthful evidence, session validity or permission. A constrained JSON intermediate must remain internal rather than becoming an alternative wire format. Deterministic construction is preferable when no model judgement is needed, but there is no generated normative specification or mandatory byte-serialization gate.

### TOON: compact auxiliary structured data

[TOON](https://github.com/toon-format/toon) compactly represents the JSON data model, particularly uniform collections whose field names can be declared once. Its documentation also describes cases where compact JSON or CSV may be a better fit.

Vernaculum could learn from separating repeated structure from values. Possible uses include auxiliary tabular source material or an explicitly reviewed future representation experiment, with exact round-trip preservation of types, nulls, identifiers and ordering where meaningful. Comparisons should include ordinary YAML, compact JSON and simple tables rather than assuming a new format wins.

TOON is not an alternative to v1.0.0's core YAML message envelope. Auxiliary encodings must preserve record interpretations and peer-agreed contracts; JSON remains the recommended durable record representation. An encoded source attachment is supporting data, not the peer's task instruction. Any benefit must exceed parser, conversion and interpretation costs; published token savings on other workloads do not establish savings for Vernaculum.

### ISON: references and stable representations

[ISON](https://github.com/ISON-format/ison) offers typed tabular structures, references, a streaming form and a canonical form intended for deterministic representation.

Its clearest lessons for Vernaculum are economical references, explicit types and stable derivative representations for caching. It could be compared with TOON for suitable auxiliary datasets, especially where relationships between objects matter. Reference resolution, dangling identifiers, type preservation and reordering would need explicit treatment.

These are potential lessons, not a reason to add a second instruction language. ISON reference syntax cannot replace Vernaculum record identities or convey authority. Any derivative representation must retain a resolvable authoritative source, and canonicalization under ISON must not be confused with authority of the canonical main-branch document.

### LLMLingua: selective compression of supporting context

[LLMLingua](https://www.microsoft.com/en-us/research/project/llmlingua/) explores learned prompt compression, including query-aware and token-classification approaches.

It could reduce non-authoritative background text after irrelevant supporting material has already been removed. The interesting question is whether compression lowers total task cost without losing exceptions, dependencies or evidence needed by the receiving agent.

The complete governing specification, approval evidence and exact task constraints should remain available unchanged. Compression cannot itself certify semantic preservation, and compressed text must not replace an authoritative record. Source retrieval and expansion are necessary when interpretation becomes uncertain. The useful comparison is against simpler extraction and retrieval as well as an uncompressed baseline, with attention to changed meaning rather than token count alone.

## 3. Scheduling, state and durable delivery

### LangGraph: explicit state and recovery boundaries

[LangGraph persistence](https://docs.langchain.com/oss/python/langgraph/persistence) provides checkpointed thread state and stores for information shared across threads. Its [fault-tolerance model](https://docs.langchain.com/oss/python/langgraph/fault-tolerance) is relevant to interrupted workflows.

An optional integration could retain task progress, pending exchanges and unresolved questions, then resume at an explicit recovery boundary. The design lesson is to distinguish durable workflow state from the context currently visible to a model.

A restored checkpoint cannot establish current authority or replace reloading the whole specification and reconciling current sources. State storage, access protection and restart behaviour depend on the chosen backend; an in-memory checkpoint is not durable across process loss. Workflow routing must also preserve the complete governing context and check complete peer messages rather than passing informal state summaries as protocol exchanges.

### Google ADK: deterministic delegation patterns

[Google ADK workflow agents](https://adk.dev/agents/workflow-agents/) provide sequential, parallel and looping orchestration patterns.

These could schedule independent work, collect findings and invoke synthesis only where judgement is required. Vernaculum could supply the task, constraints and outcome contract at each genuine inter-agent boundary, while the orchestrator handles a known execution pattern without repeatedly asking models what to do next.

Parallel execution is useful only when tasks are actually independent. Shared-file mutations or competing amendments need appropriate serialization and conflict handling. Workflow completion does not confer authority or prove a correct result. The relevant lesson is to use ordinary control flow where it is sufficient, preserving complete validated YAML whenever agents exchange governed instructions.

### Microsoft Agent Framework: correlated handoffs and approval pauses

[Microsoft Agent Framework checkpoints](https://learn.microsoft.com/en-us/agent-framework/workflows/checkpoints) capture workflow state, including pending work. Its [human-in-the-loop model](https://learn.microsoft.com/en-us/agent-framework/workflows/human-in-the-loop) supports requests that pause execution for correlated external input.

Vernaculum could use these patterns to make handoff ownership, pending approvals and resumed work explicit. They also suggest a useful separation between a resumable workflow and the owner's decision about a particular operation.

Restoring an approval request must not restore permission automatically: the target, scope and applicable authorization still need checking. Checkpoint storage and serialization have their own protection and compatibility requirements. Framework state should supplement authoritative records rather than replace them, and proprietary workflow labels should not silently become protocol status meanings.

### Temporal: long-running coordination without repeated reasoning

[Temporal workflow execution](https://docs.temporal.io/workflow-execution) uses durable history and replay, while [Activities](https://docs.temporal.io/activity-definition) represent work that can execute and retry outside deterministic workflow logic.

For long-running collaboration, Temporal could retain scheduling and recovery state across failures, reducing repeated planning and manual reconstruction. Vernaculum would still define the meaning and constraints of exchanges and outcomes.

This is an infrastructure choice for deployments that need durable execution, not a baseline protocol requirement. Retried side effects need idempotency or equivalent application safeguards. Restored workflow state cannot refresh a revoked approval, and task execution should recheck relevant permissions before a consequential retry. Durable orchestration does not itself provide exactly-once external effects.

### NATS JetStream: asynchronous delivery with explicit redelivery

[NATS JetStream](https://docs.nats.io/learn/jetstream) provides persistent messaging. Its [delivery and acknowledgement rules](https://docs.nats.io/learn/jetstream/delivery-and-acknowledgment) explain redelivery when handling is not acknowledged.

It could carry complete YAML payloads between agents that are not simultaneously available, with an adapter delivering the actual message text to the recipient. Broker retention can also support transport-level recovery independently of model context.

Broker sequence numbers, acknowledgements and task completion are different facts. Redelivery must still encounter conversation-local replay checks; acknowledging delivery cannot authorise execution. A new message ID must not be used merely to bypass a rejected replay. Persistent session state, idempotent operations and reconciliation remain application responsibilities. Streaming or chunking must preserve a complete validated instruction before dispatch.

## 4. Optimising model use and measuring outcomes

### DSPy: improve prompts against explicit objectives

[DSPy optimization](https://dspy.ai/current/getting-started/gepa-optimization/) can improve program instructions and examples against supplied objectives and inputs.

It could explore task-prompt wording, relevant-context selection and demonstrations of truthful structured responses around the complete accepted specification. Useful objectives include successful task completion, retention of constraints, appropriate clarification and total cost. Held-out cases help distinguish improvement from memorization of examples.

An optimizer must not silently rewrite normative rules, omit governing rules or change approval gates to improve a score. Correct refusal needs to count as success where execution is not authorised. The lesson is to make the desired outcome measurable while preserving hard constraints that an optimizer is not allowed to trade away.

### LiteLLM: route inference after eliminating unnecessary inference

[LiteLLM routing](https://docs.litellm.ai/docs/routing) supports model routing, load balancing, retries and fallbacks.

An optional deployment could reserve more capable models for interpretation and synthesis, using lower-cost models for tasks that meet the same correctness requirements. Model access and budget controls can remain outside the semantic protocol.

First consider whether a validator, query or deterministic operation can do the work without a model. Where inference remains useful, a provider fallback must preserve message shape, context coverage, confidentiality requirements and approval boundaries. A model switch is not a new peer's agreement to the release. Repeated completion requests may generate alternative proposals; the surrounding runtime must prevent them from duplicating side effects.

### OpenTelemetry: observe where collaboration costs arise

[OpenTelemetry](https://opentelemetry.io/docs/) provides instrumentation for traces, metrics and logs. Its [sensitive-data guidance](https://opentelemetry.io/docs/security/handling-sensitive-data/) stresses careful collection and handling.

A deployment could observe time spent selecting context, verifying messages, waiting for peers, evaluating policy and executing work. Correlated stages can reveal that expensive delays come from repeated retrieval, needless handoffs or retries rather than message length.

Collect minimal approved metadata, redact at the source and avoid recording raw messages, identities, credentials or identifying paths by default. Trace context is not an authority reference. An observed event also cannot establish delivery, approval or semantic correctness unless the underlying system actually supplies that evidence.

### Phoenix: compare semantic outcomes, not just successful parsing

[Phoenix](https://arize.com/docs/phoenix) combines tracing with datasets, experiments and code-, model- or human-based evaluation.

It could help compare equivalent task sets for omitted constraints, invented evidence, clarification quality, handoff fidelity and recovery accuracy. Deterministic checks should establish structural facts; human assessment or carefully reviewed rubrics can address meaning that a schema cannot express. Model-judge agreement is useful evidence, not proof of security or permission.

Telemetry needs the same access and disclosure controls as its source material. Phoenix supports [attribute masking](https://arize.com/docs/phoenix/tracing/how-to-tracing/advanced/masking-span-attributes); its [self-hosting privacy documentation](https://arize.com/docs/phoenix/self-hosting/security/privacy) describes separate telemetry controls. Self-hosting alone does not settle whether instrumentation or external evaluators transmit data elsewhere.

## 5. Policy enforcement and security reasoning

### Open Policy Agent: explicit decisions enforced by the runtime

[OPA's agent tool-calling guidance](https://www.openpolicyagent.org/docs/agent-tool-calling) separates the policy decision point from the component that enforces the decision.

An owner-controlled runtime could supply trusted facts about actor, action, target, approval scope and current state to a policy engine. It could then permit or deny an operation deterministically after validating the message. This is a strong fit for Vernaculum's separation of structural, authoritative and operational validity.

The model must not manufacture the trusted inputs or treat its own `authority_ref` as proof. A policy result needs enforcement at the actual tool boundary, with policy protection and freshness appropriate to the operation. OPA is optional: a small fixed policy may be sufficient. [Decision-log masking](https://www.openpolicyagent.org/docs/management-decision-logs#masking-sensitive-data) is relevant when policy inputs contain sensitive information.

### OWASP guidance: concrete threat questions

The [OWASP AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html) provides guidance on tool permissions, untrusted inputs, oversight and agent trust boundaries.

Vernaculum could use it to ask concrete deployment questions: can a syntactically valid request bypass approval; can a stale approval be reused; can a recovered checkpoint smuggle instructions; can a tool result redirect execution or disclose protected information? Such questions connect broad security principles to the protocol's actual authority and recovery boundaries.

The entire checklist should not automatically become new protocol obligations. Applicable controls depend on the deployment and its threats. A review should identify the operation, trust boundary and demonstrated failure being addressed, and retain the distinction between a semantic convention and the environment enforcing it. Listing a control is not evidence that it exists or works.

## 6. Useful techniques that do not require another framework

Several opportunities in the original discussion are ordinary software techniques rather than products:

- **Immutable references and content addressing:** identify supporting material precisely, check its identity and relevance using appropriate tools or evidence and reuse it only while its revision and dependency validity remain established. Keep complete task instructions inline.
- **Relevant supporting context:** retain the whole governing specification and select the record contracts and sources needed for the task. Retrieval ranking or a vector similarity score cannot remove governing obligations or establish authority.
- **Dependency-aware caches:** cache derived views against exact source revisions. Missing dependency edges require expansion or refusal, and recovery must not trust a remembered adherence claim.
- **Incremental updates:** consider deltas only when an agreed grammar, immutable base and atomic authorised applicator already exist. Otherwise retrieve the complete authoritative object.
- **Queries and computation before inference:** use schema validators, repository queries, comparisons and explicit policy checks for mechanically decidable questions. Reserve inference for interpretation, generation and unresolved judgement.

These techniques can deliver value independently of the larger frameworks. They also provide useful baselines when deciding whether another dependency earns its cost.

## 7. How the pieces could work together

A possible deployment could follow this sequence without changing v1.0.0's wire language:

1. The owner supplies a task, constraints and the applicable execution permissions.
2. The agents read the whole canonical specification; MCP can expose supporting resources and optional deterministic lookup tools.
3. Ordinary workflow code, or a suitable orchestrator, schedules genuinely independent work. A model is used where the task needs judgement.
4. An adapter carries each complete validated YAML message through A2A or another permitted transport. Compatibility negotiation remains separate from an operation's authorization.
5. The recipient resolves relevant sources and checks structural, authoritative and operational validity. A policy engine may assist; the executor enforces the result.
6. The recipient returns a correlated YAML response with truthful status and applicable evidence. Delivery receipts and claimed success remain distinguishable from observed execution.
7. Minimal telemetry supports diagnosis and comparison without becoming a second store of sensitive conversations.

This sequence is an illustration of responsibility boundaries, not an implementation claim or mandatory architecture. ACP or AG-UI could provide the human interface; durable workflows or a broker are warranted only where interruption and delivery requirements justify them.

## 8. Priorities and decision criteria

| Priority | Opportunity | Decision criterion |
| --- | --- | --- |
| First | Deterministic validation, approved resource retrieval and explicit policy enforcement; JSON Schema and optionally MCP/OPA | Fewer repeated interpretations with unchanged authority and correctness |
| Next | A2A adapters; ACP or AG-UI where an editor or human interface is needed | Complete messages and correlated outcomes survive the boundary |
| As coordination grows | One suitable orchestrator, durable execution service or message broker | Measurable reduction in lost work, unnecessary handoffs or recovery effort |
| Where optimisation is needed | DSPy, LiteLLM and privacy-conscious OpenTelemetry/Phoenix | Lower total cost without weaker task, context or permission checks |
| Selectively | TOON, ISON and LLMLingua for suitable supporting data | Preservation of required meaning after accounting for conversion, retrieval and correction costs |
| Where external identity is needed | ANP or another established identity/discovery environment | A verified identity binding that remains distinct from task permission |

Across these choices, compare semantic fidelity, retained obligations and exceptions, correct task outcomes, correct refusals, human correction effort, inference expenditure, delivery/recovery overhead and information exposure. Assess them together: a smaller prompt that causes more retries or loses a constraint is not an efficiency gain.

The strongest direction is a small, stable semantic contract surrounded by replaceable, well-understood capabilities. Vernaculum can learn from this ecosystem without absorbing its transport, orchestration, identity and model-serving responsibilities into the protocol itself.

Return to the [README](../README.md) or read the [protocol](../PROTOCOL.md).
