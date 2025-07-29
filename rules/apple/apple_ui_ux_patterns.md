# Rule: Apple UI/UX Technical Patterns

All Apple projects must implement consistent technical patterns for UI organization and interaction handling.

## 1. Design System Organization
-   **Package Structure**: All reusable UI components must be defined in the `Packages/Design` Swift Package for consistency and reusability across targets.
-   **Component Architecture**: Design components should follow a consistent API pattern with clear initialization, configuration, and styling hooks.

## 2. Haptic Feedback Architecture
-   **Centralized Manager**: A singleton `HapticManager` must be used to provide all haptic feedback to ensure consistency and prevent redundant generator instances.
-   **Semantic API**: The manager must define semantic actions (e.g., `PrimaryAction.selection`, `SystemFeedback.error`) that map to specific `UIFeedbackGenerator` patterns.

## 3. Navigation Architecture
-   **Navigation Manager**: Navigation state and transitions must be managed through a central `NavigationManager` to maintain consistency and enable deep linking.
-   **Gesture Handling**: Gesture recognizers must be properly coordinated to prevent conflicts, using the navigation manager as the central coordinator.

## 4. Animation Patterns
-   **Consistent Timing**: Animations should use consistent timing curves and durations defined in a central location.
-   **Interruptible**: All animations must be interruptible and reversible to ensure smooth user interactions.