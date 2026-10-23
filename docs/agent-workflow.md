# Agent coding workflow

## Shared instructions

`AGENTS.md` holds repository-wide policy. `apps/mobile/AGENTS.md` and `apps/web/AGENTS.md` add local constraints. Each `CLAUDE.md` imports its neighboring `AGENTS.md`, keeping both tools aligned without duplicate policies. `.claude/settings.json` disables commit and PR attribution; the shared Git rules apply to every agent.

This follows the useful structure of Sophic's local agent setup: shared policy, small provider entry points, explicit ownership, and verifiable handoffs. Sophic's marketing roles and automated routines are not part of Nook.

## Task handoff

For substantial work, describe:

- Outcome and acceptance criteria.
- Owned paths and files that must remain untouched.
- Relevant architecture and existing implementation.
- Dependencies on other work and required checks.

When parallel agent work is requested, assign disjoint ownership. Mobile owns `apps/mobile`; browser owns `apps/web`; the integrator owns root configuration, CI, and the lockfile. Assign a shared package to one owner at a time. Reviewers report actionable findings with file locations and evidence. Do not create idle specialist agents for a small change.

The integrator collects completed work, reviews the combined diff, and runs checks for the resulting code. A dispatched task or successful dry run is not evidence that implementation works. Do not push while required workers are still editing.

## Completion report

State what changed, what was verified, any remaining limitations, and the commit/branch if published. Keep reports concise. Never add an AI author, co-author, generated-by signature, or session link.

## References

- [Codex repository instructions](https://developers.openai.com/codex/guides/agents-md/)
- [Claude instruction files and imports](https://code.claude.com/docs/en/memory)
