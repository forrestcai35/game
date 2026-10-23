# Nook agent instructions

## Start here

- Read `README.md` and `docs/architecture.md` before structural changes.
- Inspect Git status and the relevant code before editing. Preserve unrelated user changes.
- Read the nearest scoped `AGENTS.md` before editing that directory, even when your session starts at the repository root.
- Keep this file the shared source of policy for Codex and Claude. Claude entry points import it instead of duplicating rules.

## Repository boundaries

- `apps/mobile`: existing SwiftUI/RealityKit app, built with Xcode.
- `apps/web`: reserved browser workspace; no framework or implementation yet.
- `packages`: add shared packages only for concrete consumers. Swift cannot directly consume TypeScript libraries.
- Apps may import packages; apps must not import another app. Declare JavaScript workspace dependencies explicitly.
- Keep scope to mobile and browser until a feature requires more. Do not scaffold speculative services, frameworks, or generic utilities.

## Workflow

- Carry authorized work through implementation and relevant verification. Ask only when a missing decision materially blocks the work.
- Keep edits focused. Add meaningful behavior tests with new logic; do not invent passing tests for placeholders.
- Use the pinned pnpm version in `package.json` and the root lockfile. Do not introduce npm or Yarn lockfiles.
- Never commit secrets, local environment files, build output, Xcode user state, or agent session data.
- Update documentation when commands, architecture, or supported behavior changes.
- For coordinated work, define the objective, owned files, dependencies, and acceptance checks for each participant. Avoid overlapping edits; one integrator owns root manifests and the lockfile. See `docs/agent-workflow.md`.

## Verification

- Dependency/CI changes: `pnpm install --frozen-lockfile` and `pnpm exec turbo run build check --dry=json`.
- Native project changes on macOS: `pnpm check`. Native code or build changes: also `pnpm mobile:build`.
- `pnpm check` currently lists the Xcode project; it is not a test suite. The web workspace has no runnable tasks yet. Turbo dry runs validate configuration, not application behavior.
- Run `git diff --check` and inspect the staged diff before a commit. Report what actually ran and any checks blocked by the environment.

## Git and authorship

- Never identify Codex, Claude, an AI tool, or yourself as author or co-author. Never append AI attribution, generated-by signatures, or agent session links to commits or PR descriptions.
- Use the user's existing Git identity. Do not change `user.name`, `user.email`, or author/committer environment variables. If identity is missing, ask the user.
- Commit and push when the user requests it. Do not force-push, rewrite published history, or discard unrelated changes without explicit authorization.
- Stage only task-related files. Verify author, commit message, and remote before pushing. A push request does not require a second confirmation.
