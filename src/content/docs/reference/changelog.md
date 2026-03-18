---
title: Changelog
description: History of changes in the Synapse project.
---

v0.1.1
Initial release
---
v0.1.2
# 🚀 Release v0.1.2

Welcome to **v0.1.2**! This release brings a more streamlined profile experience, layout improvements, and a crucial fix for chat avatars.

Here is the detailed breakdown of what's new:

## ✨ New Features

* **Profile Navigation:** Combined the "Followers" and "Following" lists into a single, easy-to-navigate tabbed screen. 👥 (#37)

## 🐛 Bug Fixes

* **Chat Screen Avatars:** Fixed an issue where profile pictures would appear in the Inbox but fail to show in the Chat Screen if they weren't fully loaded immediately. The `participantAvatar` is now passed directly into `AppDestination.Chat` to serve as a seamless fallback for the top Appbar. 🖼️ (#36)

## 🎨 UI/UX Improvements & Chores

* **Profile Layout:** Reordered the Profile Screen layout by moving the "About" and "Following" sections above the `ContentFilterBar` for better visibility and a smoother user experience. 📱 (#38)

---
*Thank you to all contributors who helped make this release possible! 🙌*
---
v0.1.3
# 📦 Changelog - v0.1.3

Welcome to version **0.1.3**! This release brings significant UI/UX enhancements, including the adoption of Material 3 Expressive design, a new Telegram-style file picker, and a fully automated Android release pipeline.

Here is the detailed breakdown of what's new, improved, and fixed.

## ✨ New Features

*   **Telegram-Style File Picker:** Implemented a sleek, new bottom sheet for file selection, inspired by Telegram's intuitive design. (#40)
*   **Persistent Create Post Sheet:** Replaced the previous modal combination with a `BottomSheetScaffold` on the Create Post screen. Action icons now remain persistently visible in a peek bar and can be expanded to reveal the full content list. (#41)

## 🎨 UI & UX Polish

*   **Material 3 Expressive Design & Motion:** Completely overhauled the app's motion and button aesthetics to align with Material 3 Expressive guidelines. (#42)
    *   Updated `SynapseTheme` to utilize `MaterialExpressiveTheme` and `MotionScheme.expressive()` globally.
    *   Introduced `ExpressiveButton` and `ExpressiveIconToggleButton` with shape-morphing transitions (`animatedShape()`).
    *   Refactored `ProfileHeader` to use the new expressive buttons (including `AnimatedFollowButton`) for a more fluid user experience.
*   **X-Style PostCard Refinements:** Polished the `PostCard` component to fix UI inconsistencies and improve readability. (#39)
    *   Reduced reply indicator spacing to a minimal 2dp padding in `PostHeader`.
    *   Adjusted `PostContent` padding to remove excess space above the text.
    *   Cleaned up the `PostInteractionBar` by conditionally hiding the Views count row on comments.

## 🐛 Bug Fixes

*   **Poll Business Logic:** Restored missing poll business logic and resolved design token violations to ensure strict adherence to MaterialTheme guidelines. (#41)
*   **Profile Screen Stability:** Fixed an issue in `ProfileScreen` by explicitly passing `parentAuthorUsername = null` to the `PostUiMapper` for more graceful state handling. (#39)
*   **CI Compilation Fixes:** Resolved an `Unresolved reference 'iconToggleButtonShapes'` error that caused the `:app:compileReleaseKotlin` CI task to fail by properly mocking experimental Material 3 APIs. (#42)

## ⚙️ CI/CD & Build

*   **Automated Android Releases:** Introduced a robust GitHub Actions workflow (`release.yml`) for end-to-end Android release automation. (#43)
    *   Added manual triggers with semantic version bump options (patch, minor, major).
    *   Automated `projectVersion` and `versionCode` incrementing.
    *   Configured secure release APK builds and signing using GitHub Secrets.
    *   Automated the creation of GitHub Releases and APK asset uploads.
*   **Version Bump:** Synchronized and bumped project versions across the repository to `v0.1.3` (Android `versionCode` 2, `docsWeb` updated). (#44)

---
*Thank you to all contributors who helped make this release possible!* 🚀
---
v0.1.4
# 📋 Changelog: v0.1.4

We are excited to announce the release of **v0.1.4**! This update brings a significant visual overhaul to user profiles, streamlines the interface by unifying bottom sheets, and introduces critical performance optimizations for a smoother scrolling experience.

---

## 🚀 Features
- **Comment View Counts:** Extended the view count system to comments. Users can now see engagement metrics for individual comments via the new `viewsCount` mapping. 📊
- **Inline Profile Stats:** Replaced the bulky stats row with a sleek, compact `InlineStatsRow` displaying "Followers · Following · Posts" in a single line. 🔢

## 🎨 UI/UX Improvements
- **Profile Header Redesign:**
    - Transitioned to a layered `Box` layout for a more modern, depth-oriented feel. 🖼️
    - Added a **Surface card** with 28dp rounded corners that overlaps the cover photo by 40dp.
    - Repositioned the **Avatar** to sit on the card boundary with a 4dp surface-colored border for better contrast.
    - Realigned user metadata (Name/Followers) to the right of the avatar.
    - Repositioned the **Bio** section to prevent text overlap and improve readability.
- **Unified Bottom Sheets:** Standardized the user experience by consolidating `CommentOptionsBottomSheet` and `PostMenuBottomSheet` into a single, consistent UI pattern. 🛠️
- **Layout Polishing:**
    - Removed unnecessary vertical gaps between post captions and user display names.
    - Eliminated spacing inconsistencies between "replying to" indicators and captions. ✨

## ⚡ Performance
- **Feed Optimization:** Significant under-the-hood improvements to feed scrolling performance to ensure a fluid user experience. 🏎️
- **FPS Stability:** Addressed specific frame-rate (FPS) drops identified during PR reviews to eliminate stuttering during rapid scrolling. 📉

## 🛠️ Bug Fixes
- **Display Logic:** Fixed issues with display names and usernames by simplifying the `showHandle` logic. 🆔
- **Data Mapping:** Corrected `CommentWithUser` mapping to ensure views and user data are reflected accurately. 🔄

## 🧹 Maintenance
- **Code Health:** Extracted "magic numbers" into named variables within the Profile Header for better maintainability and easier theming. 📝

---

### 🤝 Contributors
Special thanks to **TheRealAshik** and **google-labs-jules[bot]** for their contributions to this release!

---
V0.1.5

# 📋 Changelog - v0.1.5

We are excited to announce the release of **v0.1.5**! This update introduces robust offline capabilities, significant architectural refactors for better cross-platform compatibility, and automated documentation deployment.

---

## ✨ New Features

### 🔄 Background Sync & Offline Resilience
Implemented a comprehensive **Background Sync & Retry Queue** system to ensure a seamless user experience regardless of network connectivity.
*   **Persistent Action Queue:** Added `PendingAction.sq` for reliable, disk-based storage of offline actions.
*   **Optimistic UI Updates:** Refactored `PostRepository` and `SupabaseChatRepository` to reflect user actions immediately while syncing in the background.
*   **Smart Retry Logic:** Enhanced `SyncWorker` to automatically process the pending queue with intelligent retry mechanisms upon network restoration.
*   **Expanded Action Types:** Moved and expanded the `PendingAction` domain model to the shared module to support a wider variety of synchronizable events.

---

## ♻️ Refactors & Improvements

### 🎨 UI & Theming
*   **Theme Token Integration:** Replaced hardcoded UI values with standardized theme tokens to ensure design consistency across the application.
*   **Screen Enhancements:** Refactored various UI components and updated the **Settings** screens for improved usability.

### 🏗️ Architecture & DI
*   **Dependency Injection:** Updated both **Hilt** and **Koin** modules to support the new `OfflineActionRepository` and `PendingActionDao`.
*   **KMP Compatibility:** Improved Kotlin Multiplatform (KMP) support by implementing a shared `TimeProvider` and resolving cross-module compilation issues.
*   **Code Cleanup:** Squashed 12 development commits to streamline the codebase, fixing minor bugs and improving DI wiring.

---

## 🚀 CI/CD & Documentation

### 📖 Automated Docs Deployment
*   **GitHub Pages Integration:** Introduced a new workflow (`deploy_docs.yml`) to automatically build and deploy documentation for `docsWeb` on every push to the main branch.
*   **Astro Configuration:** Updated `astro.config.mjs` and `playwright.config.ts` to support the new GitHub Pages subpath and base URL structure.

---

## 🐛 Bug Fixes
*   Resolved compilation errors in `ActionQueue` and `SupabaseChatRepository` following model migrations.
*   Fixed various minor UI bugs identified during the refactoring phase.

---

### 📦 Dependency Updates
*   Updated internal repository structures to support the new offline-first architecture.
*   Synchronized shared module models for better consistency between Android and iOS targets.

**Full Changelog:** [v0.1.4...v0.1.5](https://github.com/your-repo/compare/v0.1.4...v0.1.5)
