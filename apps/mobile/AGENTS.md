# Mobile app

- Keep SwiftUI UI and RealityKit rendering/input in this app. Preserve the existing Apple-platform conditionals.
- Open `nook.xcodeproj` in this directory; source files live in `nook/`.
- Do not change bundle identity, signing team, deployment targets, or supported platforms unless the task calls for it.
- Run `pnpm check` from the root for project changes and `pnpm mobile:build` for Swift or build configuration changes. The latter is an unsigned iOS Simulator build, not device or all-platform verification.
- Native tasks require macOS and full Xcode. Respect `DEVELOPER_DIR` when supplied. Do not enable Turbo caching for native builds without accounting for SDK, toolchain, and signing inputs.
- Organize substantial new functionality by feature. Extract Swift packages only at demonstrated reuse boundaries.
