# Repository architecture

## Decision: apps by delivery surface, packages by responsibility

Use a pnpm workspace with Turborepo for task orchestration. `apps/mobile` owns the current native Apple app; `apps/web` reserves the browser client. Both evolve and ship independently. The initial move preserves the existing SwiftUI and RealityKit implementation.

Keep workspace globs shallow (`apps/*`, `packages/*`) following [Turborepo's repository guidance](https://turborepo.dev/docs/crafting-your-repository/structuring-a-repository). Apps may depend on packages, packages may depend on other packages, and apps must not import other apps. Declare dependencies in manifests so Turbo can compute the task graph.

## Sharing across native and browser

Share API contracts, event definitions, game content, and design tokens through platform-neutral schemas and data when needed. Generate or validate Swift and TypeScript representations from the same source. Rendering, platform input, navigation, and UI remain client-specific. Do not assume Swift and TypeScript can share executable game logic.

If deterministic simulation becomes a product requirement, first define its ownership and consistency model, then evaluate a portable engine or server-authoritative implementation. Avoid selecting an engine solely to maximize code sharing.

## Growth path

1. Build one end-to-end gameplay feature and identify which experiences actually need browser parity.
2. Add `packages/contracts` when an API or cross-client event model exists, with schema validation and compatibility checks. Mobile releases can lag behind web/backend releases, so contracts must support older clients.
3. Add `apps/api` when server-owned identity, persistence, progression, or social features are implemented. Keep one modular service initially, with feature boundaries such as accounts, sessions, progression, and social. Durable rewards, inventory, and competitive results should be validated server-side.
4. Introduce `apps/worker` only when asynchronous work needs independent execution. Split realtime services only when latency or scaling requirements justify it.
5. Extract game content and design tokens once both clients consume them. Keep secrets, persistence code, and privileged backend logic out of client packages.

Organize substantial client code by product feature (for example onboarding, play, profile, friends), with platform infrastructure kept separate. Avoid empty feature directories before requirements exist.

## Tooling and delivery

Use the root pnpm lockfile for reproducible JavaScript dependency installation. Keep native dependencies under Xcode/Swift Package Manager, committing their resolution files when introduced. Native compilation uses Xcode rather than a JavaScript compiler.

Turbo caches implemented JavaScript build outputs. Native tasks are uncached to avoid reuse across incompatible SDKs or signing environments. Add real lint, typecheck, and test scripts with each implementation; missing tasks must not be presented as passing coverage.

The initial CI checks frozen dependency installation and workspace graph discovery on Linux. Native project checks and builds currently run locally on macOS. Add a macOS CI job with a compatible pinned Xcode image when the app's SDK requirements are available on the runner. Add web build/check jobs when web implementation lands. Deploy each app independently and add backend migrations, observability, and release controls with the corresponding systems.

## Open product decisions

- Browser parity: full gameplay, companion experience, or discovery/onboarding?
- Apple-native only initially, or Android support requiring a broader mobile strategy?
- Solo, asynchronous social, or realtime multiplayer gameplay?
- Which outcomes must be authoritative and durable on the server?

These decisions affect engine and backend choices; the repository layout allows them without committing to infrastructure prematurely.
