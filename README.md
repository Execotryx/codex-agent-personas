# Codex Custom Agents

This repository contains standalone TOML definitions for Codex custom agents. It is intended to be used as a personal custom-agent directory, matching the placement model documented by Codex.

The agents in this repository were migrated from GitHub Copilot `.agent.md` profiles. Each TOML file preserves the original role, source invocation metadata, source tool intent, and any source handoff mapping inside `developer_instructions`.

## Documentation basis

This README was written after consulting the current official Codex manual, fetched on 2026-06-27:

- [Codex subagents](https://developers.openai.com/codex/subagents): custom agents are standalone TOML files placed in the documented personal or project-scoped custom-agent directories.
- [Custom instructions with AGENTS.md](https://developers.openai.com/codex/guides/agents-md): Codex reads `AGENTS.md` guidance at global and project scopes before work begins.

Relevant Codex manual points used here:

- A custom agent file must define `name`, `description`, and `developer_instructions`.
- Optional settings such as `model`, `model_reasoning_effort`, and `sandbox_mode` can be included in a custom agent file; omitted optional settings inherit from the parent session.
- Codex identifies a custom agent by the `name` field, not by the filename, although matching them is the simplest convention.
- Codex only spawns subagents when explicitly asked; subagent work uses its own model/tool budget.
- Subagents inherit the current sandbox policy, but a custom agent file can set defaults such as `sandbox_mode`.

## Repository layout

```text
.
|-- agent-optimizer.toml
|-- claude-code-porter.toml
|-- domain-knowledge-verifier.toml
|-- implementation-planner.toml
|-- model-adaptation-advisor.toml
|-- model-selection-advisor.toml
|-- object-detection-kaggle-gpu-stabilizer.toml
|-- optimize.toml
|-- performance-optimizer.toml
|-- performance-profiler.toml
|-- pipeline-optimizer.toml
|-- progressive-refactor-tech-lead.toml
|-- pytorch-multi-hardware-scaffold.toml
|-- root-cause-investigator.toml
`-- tt-forge-pipeline-architect.toml
```

The repository does not contain application source code, tests, package manifests, or build configuration. It is a catalog of agent definitions.

## TOML schema used by these files

Every file starts with:

```toml
# Generated from a GitHub Copilot .agent.md file.
name = "..."
description = "..."
model = "..."                  # optional in Codex; omitted by some files here
model_reasoning_effort = "..."
sandbox_mode = "..."
developer_instructions = "..."
```

Two files intentionally omit `model`:

- `object-detection-kaggle-gpu-stabilizer.toml`
- `performance-optimizer.toml`

Per the Codex manual, omitted optional fields inherit from the parent session.

The `developer_instructions` strings include a common migration wrapper:

- Original Copilot source tools.
- Intended capability profile.
- Source user-invocable flag when declared.
- Argument hint when declared.
- Source callable-agent and handoff mappings.
- Original agent instructions and output contracts.

The migrated files explicitly note that Codex custom-agent TOML does not provide a Copilot-style `tools:` allowlist. The preserved source tools should therefore be treated as behavioral constraints, not as an enforced Codex tool schema.

## Agent catalog

| File | Agent name | Model | Effort | Sandbox | Purpose |
|---|---|---:|---|---|---|
| `agent-optimizer.toml` | `agent_optimizer` | `gpt-5.4` | high | workspace-write | Optimize a single GitHub Copilot `.agent.md` profile for token use, model fit, staging, tool alignment, and documentation-backed identifier checks. |
| `claude-code-porter.toml` | `claude_code_porter` | `gpt-5.4` | high | workspace-write | Port GitHub Copilot custom agents to functionally equivalent Claude Code artifacts. |
| `domain-knowledge-verifier.toml` | `domain_knowledge_verifier` | `gpt-5.4` | medium | read-only | Verify domain-specific claims, exact identifiers, and version-sensitive terminology against authoritative current sources. |
| `implementation-planner.toml` | `implementation_planner` | `gpt-5.4` | medium | read-only | Convert validated investigation or review findings into a staged implementation plan for a follow-on executor. |
| `model-adaptation-advisor.toml` | `model_adaptation_advisor` | `gpt-5.4` | medium | read-only | Research a target LLM and produce prompt-engineering directives for adapting an agent to that model. |
| `model-selection-advisor.toml` | `model_selection_advisor` | `gpt-5.4` | high | read-only | Recommend a best-fit model for an agent from current official model, pricing, capability, and availability sources. |
| `object-detection-kaggle-gpu-stabilizer.toml` | `object_detection_kaggle_gpu_stabilizer` | inherits | high | workspace-write | Generate, repair, or stabilize PyTorch object-detection workflows for constrained Kaggle or Colab GPU runtimes. |
| `optimize.toml` | `optimize` | `gpt-5.4` | medium | read-only | Produce a read-only performance optimization plan for changed files after profiling confirmed bottlenecks. |
| `performance-optimizer.toml` | `performance_optimizer` | inherits | high | workspace-write | Apply strict memory, speed, dependency, bundle-size, and startup-time optimization to provided code. |
| `performance-profiler.toml` | `performance_profiler` | `gpt-5.3-codex` | medium | read-only | Perform static performance profiling, with deepest heuristics for JS, TS, and React, without editing files. |
| `pipeline-optimizer.toml` | `pipeline_optimizer` | `gpt-5.4` | high | workspace-write | Audit and optimize a fleet or pipeline of GitHub Copilot custom agents, focusing on handoff and capability consistency. |
| `progressive-refactor-tech-lead.toml` | `progressive_refactor_tech_lead` | `gpt-5.4-mini` | medium | workspace-write | Apply a three-stage correctness, structure, and performance refactor while preserving behavior. |
| `pytorch-multi-hardware-scaffold.toml` | `pytorch_multi_hardware_scaffold` | `gpt-5.4` | high | workspace-write | Scaffold typed PyTorch projects for GPU, TPU, TT-Forge/Tenstorrent, and CPU runtimes. |
| `root-cause-investigator.toml` | `root_cause_investigator` | `gpt-5.4` | high | read-only | Investigate bugs read-only, rank hypotheses, identify root cause, and produce a safe fix strategy. |
| `tt-forge-pipeline-architect.toml` | `tt_forge_pipeline_architect` | `gpt-5.4` | high | workspace-write | Generate or repair TT-Forge / TT-XLA phase pipelines from inspected PyTorch model, dataset, and checkpoint artifacts. |

## Agent groups

### Agent migration and porting

- `agent_optimizer`: optimizes one `.agent.md` while preserving behavior, handoff prompts, output contracts, tool intent, model pins, and domain payload.
- `pipeline_optimizer`: audits a directory of source agent files as one pipeline and fixes cross-agent contradictions.
- `claude_code_porter`: converts Copilot custom agents into Claude Code agents, skills, MCP configuration, or chain artifacts.
- `model_selection_advisor`: supports the Claude Code porter by selecting models from current official documentation.
- `model_adaptation_advisor`: supports the optimizer by adapting prompt structure to a specified model.
- `domain_knowledge_verifier`: supports agents that must verify exact identifiers or domain facts before changing them.

### Planning, debugging, and refactoring

- `root_cause_investigator`: starts with evidence, traces symptoms backward, ranks hypotheses, and produces a fix strategy.
- `implementation_planner`: converts validated findings into implementation stages and validation steps.
- `progressive_refactor_tech_lead`: performs small behavior-preserving edits in correctness, structure, and performance stages.

### Performance

- `performance_profiler`: read-only profiling and evidence collection.
- `optimize`: read-only optimization planning, scoped to changed files.
- `performance_optimizer`: direct optimization agent with workspace-write access.

### ML and hardware workflows

- `pytorch_multi_hardware_scaffold`: creates typed PyTorch scaffolds across CUDA, TPU/XLA, TT-Forge/Tenstorrent, and CPU.
- `object_detection_kaggle_gpu_stabilizer`: focuses on object detection under Kaggle/Colab GPU limits, checkpoint survivability, loss calibration, and artifact export.
- `tt_forge_pipeline_architect`: builds TT-Forge / TT-XLA phase pipelines with explicit contracts, confirmation gates, artifact history, and device-ordering safeguards.

## Declared collaboration graph

The following relationships are declared inside the migrated metadata and original instructions.

| Caller | Declared callees or handoff targets |
|---|---|
| `agent_optimizer` | `domain_knowledge_verifier`, `model_adaptation_advisor` |
| `claude_code_porter` | `model_selection_advisor` |
| `implementation_planner` | `root_cause_investigator`, `progressive_refactor_tech_lead` |
| `object_detection_kaggle_gpu_stabilizer` | `progressive_refactor_tech_lead`, `optimize`, `domain_knowledge_verifier` |
| `optimize` | `performance_profiler`, `implementation_planner` |
| `pipeline_optimizer` | `agent_optimizer` |
| `pytorch_multi_hardware_scaffold` | `progressive_refactor_tech_lead`, `optimize`, `domain_knowledge_verifier` |
| `root_cause_investigator` | `implementation_planner` |
| `tt_forge_pipeline_architect` | `progressive_refactor_tech_lead`, `domain_knowledge_verifier` |

Agents not listed as callers either declare no callable agents or do not have a declared source handoff in the inspected metadata.

## Sandbox defaults

Read-only agents:

- `domain_knowledge_verifier`
- `implementation_planner`
- `model_adaptation_advisor`
- `model_selection_advisor`
- `optimize`
- `performance_profiler`
- `root_cause_investigator`

Workspace-write agents:

- `agent_optimizer`
- `claude_code_porter`
- `object_detection_kaggle_gpu_stabilizer`
- `performance_optimizer`
- `pipeline_optimizer`
- `progressive_refactor_tech_lead`
- `pytorch_multi_hardware_scaffold`
- `tt_forge_pipeline_architect`

The Codex manual states that subagents inherit the current sandbox policy and live runtime overrides, while custom agent files can set their own defaults. Treat the values above as declared defaults, not a guarantee that a given session will permit every action.

## Maintenance guidance

When editing an agent file:

1. Keep the `name`, `description`, and `developer_instructions` fields present.
2. Preserve the source migration metadata unless you intentionally update the migration contract.
3. Do not treat preserved Copilot source tools as an enforced Codex allowlist.
4. If changing a model pin or version-sensitive identifier, use the appropriate verifier/advisor workflow documented inside the relevant agent.
5. Keep filenames aligned with agent names where practical, but remember that Codex uses the `name` field as the source of truth.
6. Update this README when adding, removing, renaming, or materially changing an agent.

## Validation

There is no build or test command in this repository because it contains only TOML agent definitions and Markdown documentation.

For documentation-only changes, validate by:

```powershell
rg -n "TODO|TBD|invent" README.md docs
git diff -- README.md docs
```

For agent-definition changes, additionally inspect the changed TOML directly and verify that each changed file still contains `name`, `description`, and `developer_instructions`.
