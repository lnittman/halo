# Rule: Apple Project Structure

All native Apple projects must follow a consistent, modular structure using a combination of an Xcode project and local Swift Packages. This mirrors the `packages` organization of the web monorepo and promotes code reuse and separation of concerns.

## 1. Root Directory Layout
The project must be organized with a main application target directory and a `Packages/` directory at the root.

-   `[project-name]-ios/`: The main iOS application target. This directory must contain all UI-related code (`Views/`), application logic (`ViewModels/`, `Managers/`, `Services/`), and app-level resources (`Assets.xcassets`, `Info.plist`).
-   `Packages/`: A directory containing all shared, modular code organized as local Swift Packages.

## 2. Swift Package Manager (SPM) for Modularity
-   **Local Packages**: All shared, reusable logic must be encapsulated in local Swift Packages located in the `Packages/` directory. The standard packages are:
    -   `Design/`: The SwiftUI Design System, including all reusable UI components, styles, colors, and typography.
    -   `Networking/`: The networking layer, responsible for all API communication.
    -   `Auth/`: The authentication module, responsible for wrapping the Clerk SDK and managing user sessions.
    -   `Analytics/`: The analytics module, responsible for event tracking.
-   **Package Independence**: Each package must be self-contained and define its own dependencies clearly in its `Package.swift` file.
-   **Application Target**: The main application target (e.g., `kumori-ios`) consumes these local packages as dependencies. It must primarily contain view composition and app-level lifecycle code, delegating all reusable business logic to the packages.

## 3. Feature-based Grouping
Within the main application target, files must be organized by feature, not by type. For example, all views and view models related to the user profile should be grouped under a `Profile/` directory.