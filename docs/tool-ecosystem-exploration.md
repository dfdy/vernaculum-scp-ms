# How Vernaculum could learn from the agent-tool ecosystem

**Vernaculum SCP:MS v1.2.0 — Accepted / Active / Stable.**

Vernaculum supplies a voluntary shared language for agents, durable knowledge and continuity. Adjacent tools could make collaboration easier without expanding the specification into a transport, runtime or security system. This exploration considers where each tool could help, what Vernaculum could learn from it, and where the boundary belongs.

This document is non-normative. The [complete canonical specification on main](https://github.com/dfdy/vernaculum-scp-ms/blob/main/PROTOCOL.md) governs. The integrations below are possibilities, not implemented features or interoperability claims. Linked project documentation describes the adjacent capabilities; applying them to Vernaculum is an assessment. A deployment would need to select and check the particular versions it uses.

The recommendation under the current contract is to begin with existing permitted communication, source retrieval and revisioned records. Add an adapter, scheduler or evaluation tool only when a concrete collaboration problem warrants it. The protocol's move away from scoped loading and required verification machinery reduces the case for building a dedicated Vernaculum platform; it strengthens the case for small, replaceable integrations around the shared language.

## What the protocol changes mean for this exploration

| Current contract | Consequence for tool selection |
| --- | --- |
| Complete specification in working context; no required loader or preflight | Tools can deliver the complete text and assist recovery. Selective retrieval and compression apply to supporting material. |
| Release agreement through `hello` / `ready` | Adapters preserve the offered and accepted versions and reply binding. A fingerprint or capability listing cannot substitute for agreement. |
| One inline YAML mapping with a restricted data model | Transport and generation experiments preserve the entire envelope and body, ordinary scalar types, and the exclusions in `SCP-MSG-002`. |
| Durable-record contracts independent of storage adapters; JSON recommended | Existing files or record stores are a reasonable starting point. A database, schema service or graph engine needs a separate operational justification. |
| Optional peer-agreed namespaced extensions | Try additional vocabulary outside the core when it preserves core meanings and permissions. Publication as an integration does not bind other peers. |
| Owner-approved core publication and explicit session agreement | Prompt optimisation, schema generation and deployment automation cannot adopt protocol revisions on the agents' behalf. |
| Efficiency measured by correctly completed work | Compare total collaboration cost, including the complete specification for each participant and reload, rather than advertised token savings. |

These consequences follow from the current [protocol](../PROTOCOL.md), especially Sections 3–7, 9 and 10. The linked [overview](../OVERVIEW.md) still contains release-candidate structures, including a fingerprint-based `hello`, scopes and schema-validation claims; those are not the current contract and should not be used to build an adapter.

## Start with the v1.2.0 contract

A participating agent reads the **whole canonical Markdown specification into working context** before claiming adherence. It reloads the whole text after recognised compaction, recovery, resumption, interruption or uncertainty. A summary, checkpoint, retrieved fragment or generated representation cannot replace it. An agent unable to read it discloses that limitation.

Minimum-sufficient constrains the **specification's own size and complexity**. Separate communication rules call for concise but sufficient task exchanges, and prefer reliable authorised non-inference operations when they meet the requirement at lower expected total cost. Reducing the governing context is not an integration objective.

Agents establish release agreement with `hello` / `ready` / `need`. `hello.body.supported_versions` lists supported releases; `ready` refers to the initiating message and states its accepted version. Agreement does not authenticate a sender or prove obedience. Every governed exchange carries its complete YAML envelope and body inline through an actually permitted channel.

Durable records preserve identity, interpretation version, revisions, sources, relationships and attribution. UTF-8 JSON is recommended for their content. Record acceptance, a successful check and an approval are distinct facts. Checkpoints preserve working claims that must be reconciled with current evidence on resumption.

Peers can agree on optional `x.<namespace>.<name>` vocabulary, fields, kinds, relationships and operations within their actual permissions. Such extensions bind only consenting peers and cannot alter core meanings, obligations, permissions or historical interpretations. Proposed core changes require explicit owner-approved publication to canonical main and agreement on the applicable contract.

There is no required bootstrap verifier, scoped context loader, generated normative YAML duplicate, hash manifest, amendment registry or installation gate. Optional software can assist agents or enforce host policy; it does not become part of the core by appearing in this exploration.

## 1. Communication and human interaction

### A2A: carry the semantic exchange across agent systems

[A2A](https://a2a-protocol.org/latest/definitions/) is relevant to communication between independently implemented agents. An adapter could carry a complete Vernaculum YAML message as text and present it intact to the receiving agent, correlating outer task identifiers with the inner conversation and reply identifiers.

The design lesson is explicit task lifecycle reporting: partial work, missing input, cancellation and completion need distinguishable meanings. An outer transport status does not replace a truthful Vernaculum response. Outer capability discovery also does not replace release agreement or establish permission. A file attachment or pointer alone cannot serve as the actionable YAML message.

### MCP: retrieve sources and use ordinary tools

[MCP resources](https://modelcontextprotocol.io/specification/latest/server/resources) and [tools](https://modelcontextprotocol.io/specification/latest/server/tools) could expose supporting records, source revisions and authorised deterministic operations. A resource could also make the entire canonical text available, provided the agent actually reads it and understands that the main-branch publication remains authoritative.

The useful separation is between finding information, describing an operation and permitting its execution. Discoverability grants no authority, and returned material can contain untrusted claims or instructions. MCP is an optional access mechanism; it is neither a context selector for the governing specification nor a prerequisite to participation.

### ACP: connect coding agents to an editor

[Agent Client Protocol](https://agentclientprotocol.com/get-started/introduction) concerns editor-to-agent communication. Its [tool-call interface](https://agentclientprotocol.com/protocol/v1/tool-calls) is relevant to displaying work and requesting permissions.

An editor integration could show a blocked task, clarification or approval request while keeping ordinary human communication readable. A separate bridge would still be needed for actual agent-to-agent YAML exchange. Vernaculum could learn from explicit progress and permission outcomes without treating an editor session or displayed approval label as permission for unrelated actions.

### ANP: external identity and discovery where needed

[Agent Network Protocol](https://github.com/agent-network-protocol/AgentNetworkProtocol) offers a reference point for agent identity and discovery across administrative boundaries. A deployment needing those functions could investigate a supported profile rather than adding identity machinery to Vernaculum.

The lesson is to make capability and identity claims explicit. A verified external identity can help attribute a sender, but cannot approve its requested task. A local owner-governed team may already have sufficient identity controls. Negotiation through another system cannot silently change Vernaculum's meanings or permissions.

### AG-UI: expose decisions and uncertainty to humans

[AG-UI](https://docs.ag-ui.com/introduction) could support a human interface showing proposed work, unanswered questions, partial results and supporting evidence. An approval view could identify the particular action and target under consideration.

Vernaculum could learn from making consequential state visible. A UI event remains evidence of that event, not proof that the requested work was authorised or completed. If an interface streams content, the recipient still needs a complete intelligible YAML message before treating it as a governed task. Humans need not write YAML to participate in oversight.

## 2. Representation, generation and supporting context

### JSON Schema: optional assistance with structure

[JSON Schema](https://json-schema.org/draft/2020-12) could express a deployment's record structures and agreed extension fields, or help construct message bodies. It can expose missing fields and inconsistent types without another model call.

Any schema would be an optional derivative aid, not a second normative specification or a required installation. It must follow the canonical contracts, including record-kind statuses and interpretation versions. For YAML messages, ordinary parsed-object validation is insufficient to detect duplicate keys or prohibited YAML features that a parser may discard or resolve; parsing would need to preserve or reject those features before schema checks. Parsing and schema success cannot establish truth, current approval, adequate task context or execution. Historical records must remain interpretable under their declared versions.

### XGrammar: reduce formatting errors where inference is useful

[XGrammar](https://github.com/mlc-ai/xgrammar) is relevant to constrained model output. A deployment could investigate generating an internal structured proposal and converting it into the actual inline YAML message. A custom YAML grammar would need deliberate agreement on the supported representation; Vernaculum v1.2.0 does not mandate a byte-exact serializer or a particular parser library.

The lesson is to avoid spending inference on repairable formatting errors. First compare ordinary templates and a reliable serializer with constrained generation: fixed envelopes and known values may need no model generation at all. A serializer must emit the restricted YAML data model, preserve strings such as version identifiers, and avoid anchors or tags. A constrained result can still contain a false assertion, inadequate instruction or unauthorised request. An internal JSON intermediate does not become an alternative wire format, and generated constraints do not replace the whole specification in the agent's context.

### TOON: compact repetitive supporting datasets

[TOON](https://github.com/toon-format/toon) is relevant to representing auxiliary structured data economically. Uniform collections could be compared with ordinary YAML, JSON or tables to see whether repetition can be reduced without losing needed meaning.

Such an experiment concerns supporting data, not the core message language. The actionable task stays in complete inline YAML; durable records retain their identity, interpretation and provenance, with JSON remaining the recommended representation. Any savings must exceed conversion, retrieval and correction costs. Another workload's token savings are not evidence of a benefit here.

### ISON: explicit references and economical structure

[ISON](https://github.com/ISON-format/ison) offers another reference point for structured supporting data and relationships. Vernaculum could learn from explicit references and compare representations for datasets where linked objects matter.

A deployment would need to preserve types, identities and resolvable sources when deriving another representation. ISON references cannot replace the protocol's record semantics or create authority. A format's canonical representation is also distinct from the authority of Vernaculum's canonical main-branch document.

### LLMLingua: compress background material, not governing text

[LLMLingua](https://www.microsoft.com/en-us/research/project/llmlingua/) is relevant to experiments with supporting-context compression. After removing irrelevant background, a deployment could compare compressed and uncompressed material for task quality and total cost.

The complete canonical specification remains in working context unchanged. Exact constraints and approval evidence must remain accessible and must not be replaced by a lossy summary presented as authoritative. If compression introduces uncertainty, retrieve the source or clarify. Useful measurements include omitted exceptions, changed meanings and recovery effort, not only token counts.

## 3. Scheduling, continuity and delivery

### LangGraph: separate saved workflow state from governing context

[LangGraph persistence](https://docs.langchain.com/oss/python/langgraph/persistence) could retain task progress, pending exchanges and unresolved questions. It offers a useful model for distinguishing stored workflow state from what an agent currently has in context.

Restoring a checkpoint does not satisfy Vernaculum recovery by itself. The agent reloads the whole specification and reconciles the checkpoint against current sources and record revisions. Storage durability and protection depend on the deployment. A saved adherence flag is not evidence that the resumed agent has read the specification.

### Google ADK: use ordinary control flow for known workflows

[Google ADK workflow agents](https://adk.dev/agents/workflow-agents/) are relevant to sequential, parallel and repeated work patterns. A deployment could schedule independent implementation and review work while reserving model judgement for interpretation and synthesis.

The lesson is to avoid repeatedly asking a model to decide a known next step. Shared-file edits still need coordination, and each participating agent needs the complete governing specification. Workflow completion cannot establish correctness or authorisation. Governed messages between agents remain complete inline YAML rather than informal routing summaries.

### Microsoft Agent Framework: make pending work and approvals explicit

[Microsoft Agent Framework checkpoints](https://learn.microsoft.com/en-us/agent-framework/workflows/checkpoints) and [human interaction](https://learn.microsoft.com/en-us/agent-framework/workflows/human-in-the-loop) suggest ways to retain outstanding work and correlate external decisions with requests.

A deployment could resume a paused task without reconstructing its entire conversation. It would still need to reload governing context and establish that the particular approval remains applicable. Framework labels do not redefine Vernaculum response statuses, record lifecycles or human authority; workflow state supplements the evidence rather than replacing it.

### Temporal: durable scheduling for long-running collaboration

[Temporal workflows](https://docs.temporal.io/workflow-execution) and [Activities](https://docs.temporal.io/activity-definition) are relevant where tasks need durable scheduling and retries across failures. Vernaculum could remain the semantic language while Temporal supplies operational continuity.

This is an infrastructure choice for a demonstrated need. A replayed workflow or retried activity does not establish that an external effect should happen again. Idempotency, transaction controls and current permissions belong to the host application. Restored execution history also does not replace the agent's complete-context recovery obligation.

### NATS JetStream: preserve messages across asynchronous delivery

[NATS JetStream](https://docs.nats.io/learn/jetstream) could retain complete YAML messages until another agent is available. An adapter would present the actual message text to the recipient and keep broker acknowledgements distinct from task outcomes.

Redelivery is relevant to `SCP-MSG-003`: distinct messages need distinct identifiers within their conversation, and agents should identify and avoid duplicate or stale requests. The core does not prescribe a replay database or guarantee exactly-once effects. A deployment needing stronger safeguards must supply them through its host. Renaming a retried request cannot make a repeated consequential operation safe or authorised.

## 4. Inference, observation and evaluation

### DSPy: improve task prompts around a fixed specification

[DSPy](https://dspy.ai/) could help compare task-prompt wording and examples against explicit objectives. Relevant outcomes include correct completion, useful clarification, faithful handoffs and truthful reporting.

Optimisation applies to supporting prompts and task presentation, not automatic amendments to canonical rules. It cannot omit governing context, weaken permissions or reward invented evidence. Correctly reporting a blocked task should count as a useful outcome when execution is not authorised. Compare on held-out tasks and total correction effort as well as nominal success.

### LiteLLM: route model work after considering non-inference options

[LiteLLM routing](https://docs.litellm.ai/docs/routing) could help a deployment choose models for tasks that still require inference. The protocol's own starting point is to prefer an available authorised non-inference operation where it reliably meets the requirement at lower expected total cost.

Model selection and fallback should preserve the whole governing context, task constraints and applicable information controls. A changed model does not automatically mean a new peer has accepted the release. Retries can produce alternative proposals; the host remains responsible for preventing unintended repeated effects.

### OpenTelemetry: find the actual sources of cost

[OpenTelemetry](https://opentelemetry.io/docs/) could help observe retrieval, model calls, peer waits, execution and recovery. Measurements could show whether delays come from excessive delegation or repeated reconstruction rather than message size.

Telemetry is optional deployment evidence, not a compliance certificate. Its collection needs appropriate permission and [sensitive-data handling](https://opentelemetry.io/docs/security/handling-sensitive-data/). Prefer minimal approved metadata over raw conversations or credentials. An observed call, receipt or status proves only what the instrumentation actually captured.

### Phoenix: evaluate meaning and outcomes

[Phoenix](https://arize.com/docs/phoenix) is relevant to experiments and evaluation around agent behaviour. A deployment could compare constraint retention, evidence accuracy, clarification quality and recovery with or without an integration.

Use deterministic checks for structural facts and reviewed human or model assessments where meaning requires judgement. A judge's score cannot establish approval or security. Evaluation data needs the same disclosure controls as its source material; self-hosting alone does not establish that every connected evaluator or telemetry destination is private.

## 5. Host policy and security review

### Open Policy Agent: enforce the host's decisions at its tool boundary

[OPA's agent tool-calling guidance](https://www.openpolicyagent.org/docs/agent-tool-calling) separates policy decisions from their enforcement by the surrounding application. A deployment could supply trusted facts about the actor, requested operation, target and approval to decide whether a tool call may proceed.

This complements Vernaculum's explicit limits: a message, record or claimed identity grants no permission. OPA is optional, and a smaller existing host policy may suffice. A model-generated approval reference is not trusted input merely because it appears in YAML. Policy enforcement remains external; it does not turn voluntary protocol adherence into mechanically guaranteed obedience.

### OWASP guidance: ask concrete deployment questions

The [OWASP AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html) offers questions about untrusted input, tool permissions and oversight. A deployment could use it to examine whether retrieved content redirects a task, a checkpoint contains misleading claims, or a request exceeds the user's actual approval.

The lesson is to connect each control to a particular operation and threat. Vernaculum explicitly cannot prevent prompt injection, fabricated evidence or unsafe execution by itself. A checklist is not evidence of effective protection, and applicable host controls need not become new core obligations.

## 6. Techniques that may be sufficient without another framework

Several useful improvements need no additional platform:

- **Source references:** use stable identifiers and exact revisions for supporting records, retain attribution and resolve necessary dependencies rather than guessing unseen content.
- **Ordinary retrieval:** select relevant supporting material while keeping the entire canonical specification in working context.
- **Caches:** retain derived supporting views with their source revisions, and reconcile freshness when resuming rather than trusting remembered claims.
- **Deltas:** follow `SCP-MSG-007` by identifying the exact base, deterministic operations and conflict preconditions. If reliable authorised application cannot be established, retrieve the complete record or escalate. The core specifies no universal delta language.
- **Direct computation:** use available authorised queries, comparisons and other reliable operations where they meet the task better than inference. Optional validators can assist without becoming an adoption gate.

The decision is whether a technique improves correctly completed work enough to justify its own complexity.

## 7. A possible collaboration

1. The owner supplies the objective and applicable permissions. Each participating agent reads the whole canonical specification.
2. Agents establish release agreement through `hello` and a reply-bound `ready`, or clarify missing information with `need`. Any optional namespaced contract is agreed by the peers it affects.
3. Agents retrieve relevant evidence through existing tools or, if useful, MCP. A simple scheduler or suitable orchestrator coordinates independent work.
4. Complete inline YAML requests travel through a permitted channel, potentially using an A2A or broker adapter. The recipient checks the contract, necessary sources and its actual authority before acting.
5. The recipient returns a correlated response with truthful status, evidence, limitations and unperformed checks. Durable records preserve substantive decisions and results with provenance.
6. After recognised interruption or context loss, the agent reloads the whole specification and reconciles current evidence before continuing. A workflow checkpoint can assist this step but cannot replace it.

This is an illustration, not a mandatory stack. Direct communication and existing project tools may already be sufficient.

## 8. Choosing what earns its place

The catalogue above describes possible roles, not an adoption sequence. For an owner-governed coding team, the following order offers a more proportionate starting point:

1. **Establish a baseline with existing tools.** Use the complete specification, a permitted channel, inline YAML, resolvable sources and revisioned records. Exercise a request, clarification, handoff and recovery before choosing infrastructure.
2. **Address an observed failure or cost.** Consider a small serializer or optional validator for malformed exchanges, MCP for difficult source access, or a scheduler for recurring coordination. Add A2A or a broker when communication actually crosses systems or availability windows.
3. **Add operational infrastructure for operational requirements.** Temporal, JetStream, external identity and policy engines become candidates when durability, delivery, identity or enforced tool policy requires them. Select the capability needed; these tools are not an implied combined stack.
4. **Run representation and model experiments after measuring the baseline.** TOON, ISON, LLMLingua, DSPy and model routing need evidence that their conversion, evaluation and recovery costs pay off. Small messages and modest supporting datasets may leave little to improve.

For the first trial, compare equivalent tasks with existing coordination and with Vernaculum using the same tools and permissions. Record task outcomes, omitted constraints, human corrections, model and tool costs, and recovery effort. Then change one integration at a time. This separates the value of the shared language from the value and overhead of its surrounding infrastructure. No such comparative results are reported here.

| Need | Possible capability | Useful evidence of value |
| --- | --- | --- |
| Access to sources or reliable computation | Existing tools; optionally MCP or JSON Schema | Less repeated interpretation without lost constraints or authority |
| Communication across agent systems | A2A or another permitted adapter | Complete instructions and reply bindings survive the boundary |
| Human interaction | ACP or AG-UI | People can understand the pending action, decision and outcome |
| Interrupted or asynchronous work | A suitable orchestrator, Temporal or JetStream | Less lost work and fewer unsafe repeated effects |
| Expensive inference or poor task prompts | DSPy, LiteLLM, direct computation | Lower total cost per correctly completed task |
| Unclear performance or quality | OpenTelemetry or Phoenix | Actionable observations with appropriate information protection |
| Large supporting datasets | TOON, ISON or selective LLMLingua experiments | Meaning survives conversion, retrieval and correction |
| External identity or tool permissions | Existing identity controls, possibly ANP or OPA | Appropriate identity evidence and enforced host decisions |

Compare task outcomes, retained constraints, truthful reporting, useful refusals, human correction effort, recovery cost and information exposure. The complete governing specification stays intact. A useful integration can remain replaceable infrastructure or a peer-agreed extension; it does not need to enlarge the canonical core.

Return to the [README](../README.md), consult the [overview](../OVERVIEW.md), or read the [protocol](../PROTOCOL.md).
