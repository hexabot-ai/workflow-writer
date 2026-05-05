---
name: hexabot-workflow-writer
description: Use when generating, reviewing, or improving Hexabot v3 workflow YAML, workflow actions, bindings, memory definitions, or agentic automation use cases, including conversational, manual, scheduled, event-driven, system, sales-demo, documentation, and product-showcase workflows.
---

# hexabot-workflow-writer

Use this skill for Hexabot v3 workflow authoring and review. Hexabot workflow YAML is strict; inspect the current repository before producing final YAML.

## When to use

- Generate a Hexabot workflow from a business use case.
- Review, debug, or improve Hexabot workflow YAML.
- Design a Hexabot agentic automation, including conversational, manual, scheduled, event-driven, or system workflows.
- Design workflow actions, bindings, memory requirements, LLM steps, or tool usage.
- Convert a sales, documentation, or product showcase demo into a Hexabot workflow.

## When not to use

- Generic chatbot marketing copy without Hexabot workflow implementation.
- Generic AI strategy or automation advice not tied to Hexabot.
- Non-Hexabot automation platforms.
- General NestJS or React work unless directly related to Hexabot workflow/action/binding development.

## Source of truth

Before final workflow YAML or action contracts, inspect the relevant current repo files:

- DSL and examples: `packages/agentic/DSL.md`, `packages/agentic/src/dsl.types.ts`, `packages/agentic/examples/*/workflow.yml`.
- Runtime validation and execution: `packages/agentic/src/workflow.ts`, `packages/agentic/src/workflow-compiler.ts`, tests under `packages/agentic/src/__tests__/`.
- API workflow integration: `packages/api/src/workflow/**`, especially DTOs, entities, input schemas, trigger wrappers, and `lib/workflow-definition.ts`.
- Actions and bindings: `packages/api/src/actions/**`, `packages/api/src/extensions/actions/**`, `packages/api/src/bindings/**`.
- Shared workflow types: `packages/types/src/workflow/**`.

Built-in API actions are not exhaustive. End users can install action packages from npm or create project-local custom actions in a Hexabot CLI-bootstrapped project. Do not invent unsupported YAML fields. If the repo does not expose a needed schema or action, state whether it is assumed to be installed/custom and present the YAML as requiring runtime verification.

## Workflow YAML rules

- Workflow definition YAML supports these root fields: `inputs`, `context`, `defaults`, `defs`, `flow`, `outputs`.
- Workflow metadata such as name, description, `WorkflowType` (`conversational`, `manual`, `scheduled`), schedule cron, publish state, layout, and version message lives in API workflow records outside the YAML definition.
- `defs` is the root registry. Task defs use `kind: task` and declare `action`; non-task defs use a binding kind and must declare `settings`.
- Supported flow primitives are `do`, `parallel`, `conditional`, and `loop`. Loop blocks require `type: for_each` or `type: while`.
- Any string beginning with `=` is evaluated as JSONata. Literal strings must not begin with `=`. Final `outputs` values must be expression strings.
- Expressions can use `$input`, `$context`, `$output.<task>`, `$iteration`, and `$accumulator`.
- Task output mapping is not supported; the raw action result is stored under `$output.<task>`.
- Binding references must point to existing defs with matching `kind`. Current built-in binding kinds include `model` as a single reference and `tools`, `memory`, and `mcp` as arrays.

## Authoring process

1. Identify the workflow type and trigger outside YAML: conversational inbound message, manual API/UI run, or scheduled cron run.
2. Inspect available action schemas and workflow-type compatibility before selecting actions.
3. Define the minimal `inputs.schema` for values the workflow needs.
4. List required actions and external integrations, then map each to existing action names or note a custom action design.
5. Add bindings only when required by an action, especially AI model, tools, MCP, or memory bindings.
6. Keep memory explicit: use existing memory definition IDs/slugs where available, or document needed memory definitions separately.
7. Build a small flow first, then add branching, parallelism, loops, retries, and human handoff only when the use case requires them.
8. Validate expressions, task references, binding cardinality, and final outputs before presenting final YAML.

## Review process

1. Parse the YAML shape against `WorkflowDefinitionSchema`.
2. Check every `flow` task reference against `defs`.
3. Check action names against the runtime action registry or source files.
4. Check each binding kind, cardinality, def reference, nested binding, and supported-binding allowlist.
5. Check workflow type fit: conversational actions should not be used in manual or scheduled workflows unless source code says they support it.
6. Check LLM prompts for prompt-injection exposure, secret leakage, vague outputs, and missing structured-output schemas.
7. Check error handling through `defaults.settings`, task settings, retries, fallback branches, and human escalation.
8. Report findings by severity with concrete YAML paths and repo references where possible.

## Output formats

- New workflow generation: provide a short assumptions section, workflow metadata to configure outside YAML, final YAML in a fenced `yaml` block, and validation notes.
- Workflow review: lead with findings ordered by severity, then include open questions, suggested patch snippets, and validation steps.
- Action design: provide action name, workflow types, input schema, output schema, settings schema, supported bindings, idempotency notes, errors, observability, and test expectations.
- Demo use-case design: provide audience, demo narrative, workflow type, trigger, actions, bindings/memory, happy path, failure path, and what to show in the UI.

## References

- Read `references/workflow-authoring-guide.md` when converting a use case into workflow YAML.
- Read `references/action-design-guide.md` when designing or reviewing custom actions.
- Read `references/workflow-review-checklist.md` when reviewing an existing workflow.
- Read `references/output-templates.md` when the user wants a polished response format.
- See `examples/customer-support-triage.workflow.yaml` for an illustrative workflow skeleton.
- See `examples/contact-calendar-agent.workflow.yaml` for an advanced illustrative agent loop with memory, MCP, and a custom action.
