# Hexabot Workflow Writer Skill

This repository packages a Codex skill that helps AI coding agents generate, review, and improve Hexabot v3 workflow YAML, action contracts, bindings, memory requirements, and agentic automation designs.

The agent-facing instructions live in [`skills/hexabot-workflow-writer/SKILL.md`](skills/hexabot-workflow-writer/SKILL.md). This README is human-facing GitHub documentation for the skill repository.

## What Hexabot Is

Hexabot v3 is a self-hostable AI workflow automation platform for building workflows that talk, act, and remember. It combines conversational channels, YAML-based workflow definitions, reusable actions, model/tool bindings, memory and RAG capabilities, MCP integration points, and human handoff patterns in one runtime.

Teams can use Hexabot to build customer-facing assistants, internal service automations, scheduled workflows, and operational agents while keeping the platform and production data under their own control.

## What This Skill Provides

- Workflow authoring guidance for `conversational`, `manual`, and `scheduled` Hexabot workflows.
- Review checklists for YAML parsing, schema shape, flow references, action availability, bindings, memory, and prompt safety.
- Action design guidance for custom Hexabot actions and integration wrappers.
- Output templates for polished workflow generation, workflow review, action design, and demo-use-case responses.
- Example workflow YAML files that demonstrate common workflow structures and advanced agent loops.

## Repository Layout

```text
skills/hexabot-workflow-writer/
├── SKILL.md
├── examples/
│   ├── contact-calendar-agent.workflow.yaml
│   └── customer-support-triage.workflow.yaml
└── references/
    ├── action-design-guide.md
    ├── output-templates.md
    ├── workflow-authoring-guide.md
    └── workflow-review-checklist.md
```

## How To Use

Ask the agent to use this skill when you need to:

- Convert a business use case into Hexabot workflow YAML.
- Review or debug a Hexabot workflow definition.
- Design a custom workflow action, action package, or integration wrapper.
- Plan bindings for models, tools, memory, MCP servers, or external systems.
- Turn a sales demo, documentation example, or product showcase into a runnable Hexabot workflow.

For the most accurate output, provide the workflow type, available actions, configured bindings, memory definitions, external systems, and whether a live Hexabot MCP server or checked-out Hexabot repository is available.

## Validation Notes

The skill is designed to prefer live source-of-truth checks before final YAML is presented. When available, the agent should inspect a checked-out Hexabot repository or a configured Hexabot MCP server for action schemas, workflow schemas, binding kinds, memory definitions, and existing workflows.

If only this packaged skill is available, the included references and examples can guide drafting, but runtime verification still requires Hexabot source files, a running Hexabot API, or a Hexabot MCP server.

## Useful Hexabot Links

- Website: <https://hexabot.ai/>
- Documentation: <https://docs.hexabot.ai/>
- GitHub repository: <https://github.com/hexabot-ai/Hexabot>
- GitHub issues: <https://github.com/hexabot-ai/Hexabot/issues>
- GitHub pull requests: <https://github.com/hexabot-ai/Hexabot/pulls>
- CLI package: <https://www.npmjs.com/package/@hexabot-ai/cli>
- CLI source docs: <https://github.com/hexabot-ai/Hexabot/tree/main/packages/cli>
- Extensions marketplace: <https://hexabot.ai/extensions>
- Discord community: <https://discord.gg/hexabot>

## Local Development Pointers

When authoring workflows against a local Hexabot project, the default development endpoints are:

- Admin UI: <http://localhost:3000>
- API: <http://localhost:3000/api>
- API docs, when enabled in non-production environments: <http://localhost:3000/docs>

Common project bootstrap commands:

```bash
npm install -g @hexabot-ai/cli
hexabot create my-project
cd my-project
hexabot dev
```

## License And Attribution

This skill is documentation and guidance for working with Hexabot workflows. Refer to the official Hexabot repository for current Hexabot license terms, attribution requirements, and contribution guidelines.
