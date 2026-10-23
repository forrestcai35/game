# Shared packages

Add one workspace per concrete reusable concern, directly under this directory. Each JavaScript workspace needs a private `@nook/<name>` package manifest and explicit `workspace:*` dependencies.

Potential boundaries are contracts (API/event schemas), game-content (versioned data), design-tokens (platform-neutral values), and configuration. These are planned boundaries, not implemented packages. Swift cannot directly import TypeScript packages: cross-platform sharing needs schemas/data and explicit code generation or native adapters.

Avoid a generic shared or utils package. Keep code local until another consumer needs it.
