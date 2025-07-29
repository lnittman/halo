# Rule: Apple Architecture Patterns

All Apple projects must adhere to a consistent set of architectural patterns to ensure scalability, testability, and maintainability.

## 1. Primary Architecture: MVVM
-   **Pattern**: The Model-View-ViewModel (MVVM) pattern is the required architecture for all UI-related features.
-   **View**: SwiftUI views must be lightweight and primarily responsible for layout and presentation. They should contain minimal business logic.
-   **ViewModel**: Each major view or feature must have a corresponding ViewModel, which is an `ObservableObject`. The ViewModel is responsible for managing the view's state, handling user input, and executing business logic by calling services.
-   **Model**: Data models must be simple structs conforming to `Codable` and `Identifiable`.

## 2. Dependency Injection
-   **Pattern**: A centralized dependency container (e.g., `AppDependencies`) must be used to manage and provide access to all shared services.
-   **Implementation**: This container must be implemented as a singleton (`shared`) and injected into the SwiftUI environment at the root of the application, making services available to all child views and view models.

## 3. Service Layer
-   **Responsibility**: All business logic, such as API calls, data processing, and local storage management, must be encapsulated within service classes (e.g., `ImageGenerationService`, `FilterService`).
-   **Protocols**: All services must conform to a protocol (e.g., `ImageGenerationServiceProtocol`). ViewModels must depend on the protocol, not the concrete implementation, to facilitate testing and dependency injection.

## 4. Data Flow
-   **Pattern**: Data flow must be unidirectional and reactive, using `Combine` and `@Published` properties.
-   **Implementation**: Services and ViewModels expose data through `AnyPublisher`. Views subscribe to these publishers to reactively update the UI. Direct modification of state from a View is forbidden; all changes must be initiated through ViewModel actions.