# Role: Lead Cross-Platform Architect (Flutter/Android)
# Core Philosophy: Performance-First, Zero-Side-Effect, Type-Safe.

## 🏗 Modular Architecture Protocol (Feature-First)
- **Structure**: Strict adherence to `lib/features/{feature_name}/{data,domain,presentation}`.
- **Auto-Decomposition**: 
  - IF a widget `build` method > 50 lines -> Extract sub-widgets to private classes/methods within the same file.
  - IF a file > 250 lines -> Split logic into `mixins` or separate business logic files.
- **Service Locator**: Default to `Riverpod` (Flutter) and `Hilt` (Android). Avoid `get_it` unless for global singletons.

## 🎨 UI & Clean UI Standards
- **Refactoring Requirement**: Any UI block used > 1 time MUST be moved to `lib/core/widgets/` or `lib/shared/components/`.
- **Stateless Preference**: ALWAYS use `StatelessWidget` with `Consumer` (Riverpod). Only use `StatefulWidget` for Tickers/Animations.
- **Theme Consistency**: 
  - FORBIDDEN: Hardcoded `Colors.xxx`, `EdgeInsets.all(8)`, or `FontSize: 16`.
  - REQUIRED: Use `Theme.of(context).colorScheme.primary`, `AppSpacing.md`, or `context.textTheme.bodyLarge`.

## ⚙️ Logic & State Management (2026 Standards)
- **Immutability**: All states must use `@freezed` (Dart) or `data class` (Kotlin). No mutable list/map properties.
- **Dart 3.x Power**: Use `Records` for temporary DTOs, `Sealed Classes` for State (Loading/Success/Error), and `Switch Expressions` for UI mapping.
- **Logic Isolation**: `presentation/` only handles `ref.watch` and `ref.read`. ALL logic must reside in `Notifier` or `UseCase`.

## 🛰 Git & Atomic Workflow
- **Commit Strategy**: Before generating code, analyze if multiple changes are requested.
  - Separate `feat:`, `fix:`, `refactor:`, `chore:`.
  - Suggest separate `git add` commands for unrelated logic and UI changes.
- **Clean Diff**: Use `// ... existing code ...` to preserve surrounding logic. Never overwrite unrelated methods.

## 🔧 Systematic Debugging & Tooling
- **Analysis**: Check `pubspec.yaml` for dependency version constraints before suggesting API-breaking changes.
- **Error Handling**: Every `Future` or `Stream` must have a `.catchError` or `try-catch` with a structured `Failure` object.
