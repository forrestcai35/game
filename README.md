# nook

A consumer game app with separate native and browser clients.

```text
apps/
  mobile/        SwiftUI + RealityKit app and Xcode project
  web/           Reserved browser client workspace
packages/        Shared packages, added when they have real consumers
docs/           Architecture decisions
```

## Setup

Use Node.js 22 or newer and pnpm 10.34.7 (`npm install -g pnpm@10.34.7`).

```sh
pnpm install --frozen-lockfile
pnpm mobile:open
pnpm check
pnpm mobile:build
```

Native commands require macOS and full Xcode with SDKs compatible with the app's deployment targets. The wrapper uses `/Applications/Xcode.app` by default; set `DEVELOPER_DIR` for another installation. `mobile:build` performs an unsigned iOS Simulator build. For device builds, signing, and other Apple platforms, use Xcode.

`pnpm build` runs all implemented build tasks. `pnpm check` currently validates the Xcode project; it does not run a test suite. `pnpm dev` is reserved for future persistent development servers and currently has no tasks. The web workspace is a placeholder with no framework, server, or build yet.

Turborepo orchestrates package scripts; Xcode still compiles Swift. Native tasks bypass Turbo caching because their results depend on local Xcode and SDKs. JavaScript builds can use Turbo caching when implemented.

See [architecture](docs/architecture.md) for boundaries and the growth plan.

## Agent coding

Codex and Claude share [repository instructions](AGENTS.md), with scoped mobile and browser guidance. See [the agent workflow](docs/agent-workflow.md) for ownership, verification, and handoffs. Commits use the existing human Git identity without AI attribution.
