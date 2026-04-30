# CANONICAL.md — Agent-Native Skill Graph Routing Layer

> **Read first, every time.** Maps tasks to skills. Defines execution protocol.
> The agent doesn't guess what to load. It reads this file and follows the path.

---

## Architecture

This system has three layers, not one file:

| Layer | Location | Purpose |
|-------|----------|---------|
| **Skills** | `~/.hermes/skills/` | Domain methodologies — how to do specific work |
| **Context** | `$VAULT/memories/` | Identity and business knowledge — who I am and who you are |
| **Frameworks** | `~/.hermes/skills/software-development/` | Cross-cutting patterns — debugging, TDD, security, planning |

**Every file is one complete thought.** Skills are nodes. Context files are nodes. Frameworks are nodes. The edges between them are defined by manifests.

---

## Task → Skill Routing

### Code & Development
| Task | Skill | Category |
|------|-------|----------|
| Review a PR | `code-reviewer` | github |
| Create a PR | `github-pr-workflow` | github |
| Resolve merge conflicts | `github-merge-conflict-resolution` | github |
| Write a plan/spec | `writing-plans` | software-development |
| Implement from plan | `subagent-driven-development` | software-development |
| Debug systematically | `systematic-debugging` | software-development |
| Write tests (TDD) | `test-driven-development` | software-development |
| Pre-commit verification | `requesting-code-review` | software-development |
| Security review | `security-hardening` | software-development |
| Inspect a codebase | `codebase-inspection` | github |
| VS Code webview → standalone | `vscode-webview-standalone-bridge` | software-development |

### GitHub & Open Source
| Task | Skill | Category |
|------|-------|----------|
| Contribute to OSS | `oss-contributor` | github |
| Find repos to contribute to | `repo-scout` | github |
| Study merged PRs for patterns | `pr-analyst` | github |
| Post-mortem on closed PRs | `pr-postmortem` | github |
| Morning GitHub briefing | `morning-brief` | github |
| Manage GitHub repos | `github-repo-management` | github |
| Set up GitHub auth | `github-auth` | github |
| Fix profile README | `github-profile-readme` | github |
| Manage issues | `github-issues` | github |

### Meta & Self-Improvement
| Task | Skill | Category |
|------|-------|----------|
| Audit and improve skills | `self-improver` | software-development |
| Publish a skill | `skill-publisher` | software-development |
| Navigate the skill graph | `skill-graph` | meta |

### Research & Data
| Task | Skill | Category |
|------|-------|----------|
| Search academic papers | `arxiv` | research |
| Monitor blogs/RSS | `blogwatcher` | research |
| Query prediction markets | `polymarket` | research |
| Build LLM knowledge wiki | `llm-wiki` | research |

### Productivity
| Task | Skill | Category |
|------|-------|----------|
| Manage Linear issues | `linear` | productivity |
| Google Workspace ops | `google-workspace` | productivity |
| Create presentations | `powerpoint` | productivity |
| Notion operations | `notion` | productivity |
| OCR documents | `ocr-and-documents` | productivity |
| Edit PDFs | `nano-pdf` | productivity |
| Maps/location | `maps` | productivity |
| Obsidian notes | `obsidian` | note-taking |
| Task management | `pulse-todo` | productivity |

### ML & AI
| Task | Skill | Category |
|------|-------|----------|
| Fine-tune with Axolotl | `axolotl` | mlops/training |
| Fine-tune with Unsloth | `unsloth` | mlops/training |
| Fine-tune with TRL | `trl-fine-tuning` | mlops/training |
| Serve LLMs with vLLM | `vllm` | mlops/inference |
| Structured output (Outlines) | `outlines` | mlops/inference |
| Local inference (llama.cpp) | `llama-cpp` | mlops/inference |
| Build DSPy systems | `dspy` | mlops/research |
| Segment Anything model | `segment-anything` | mlops/models |
| Audio generation | `audiocraft` | mlops/models |
| HuggingFace Hub ops | `huggingface-hub` | mlops |
| Evaluate LLMs | `evaluating-llms-harness` | mlops/evaluation |
| Track experiments (W&B) | `weights-and-biases` | mlops/evaluation |
| Jailbreak testing | `godmode` | red-teaming |
| Remove refusals | `obliteratus` | mlops/inference |

### Automation & Workflows
| Task | Skill | Category |
|------|-------|----------|
| Multi-step workflows | `stepforge-workflow` | stepforge-workflow |
| Set up Python project | `uv-python-runner` | uv-python-runner |
| Morning routine | `wake-up` | wake-up |

---

## Execution Protocol

Every skill invocation follows this meta-workflow. Domain changes, execution pattern doesn't.

### The Five Steps

1. **Plan before executing.** State understanding, outline approach, identify context to load, note open questions. Wait for approval before doing work. *It's faster to course-correct a plan than rebuild finished work.*

2. **Clarify before starting.** Gather essential information. If answers are missing or ambiguous, ask directly. Don't assume. Don't proceed with incomplete information.

3. **Load relevant context.** Core context always loads (identity.md, user.md). Extended context loads based on skill domain. References load when the task needs depth. Read the manifest first.

4. **Execute domain-specific work.** The skill defines approaches, when to use each, how to execute, and what deliverables to create.

5. **Quality checks.** Validate that work meets standards before marking done. Binary pass/fail. If it doesn't pass, it's not done.

### Error Recovery

When quality checks fail:
1. Identify what specifically isn't working
2. Diagnose why — unclear requirements? Missing context? Wrong approach?
3. Apply fix — go back to clarification, load additional files, try different approach
4. Re-run quality checks
5. If 2–3 recovery attempts don't resolve: escalate, don't spin endlessly

---

## Four Governing Principles

All work is governed by these:

1. **Simplicity first.** Every solution should be as simple as possible. Is there a simpler way? Complexity must be justified. If you can cut it, cut it.

2. **Root cause focus.** Understand deeply before solving. Don't fix symptoms. Ask "why" until you reach the real problem. Correct diagnosis > fast solution.

3. **Demand elegance.** For non-trivial work, pause: is there a more elegant way? If a solution feels forced, explore alternatives. The right framing makes the solution obvious.

4. **Verification before done.** Never mark work complete without proving it works. "I think it's done" is not done. Test your output. Demonstrate correctness.

---

## Session Management

- **One major task per session.** Context quality degrades before it runs out.
- **Start fresh after milestones.** A new session with clear context outperforms a fatigued session.
- **Long, dense conversations lead to:** less precise output, forgotten decisions, repeated mistakes.

---

## Manifest Pattern

Every skill should declare what it needs. See skill YAML frontmatter for:
- `always_load` — skill file + core frameworks (loads every time)
- `context` — business-specific files the skill needs
- `references` — detailed materials loaded when task needs depth

The agent reads the manifest first, before reading content. It knows what exists, what matters, what to skip.

---

*Last updated: 24/04/2026*
*Inspired by: Baseline Core architecture (Trent Mitchell, baselinestudio.design)*
