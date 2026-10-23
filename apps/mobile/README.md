# @nook/mobile

The existing SwiftUI/RealityKit app lives here. Open `nook.xcodeproj` or run `pnpm mobile:open` from the repository root.

The folder is named mobile for product ownership; the existing Xcode target also supports macOS, tvOS, and visionOS. No platform support or deployment targets were changed during the monorepo move. The existing bundle identifier remains `game.game`.

Keep native UI, rendering, input, platform integrations, and Swift-specific state here. Organize new product features under `nook/Features/<Feature>` when needed. Extract Swift packages only when there is a real reuse boundary.
