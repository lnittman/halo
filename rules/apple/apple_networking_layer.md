# Rule: Apple Networking Layer

The networking layer for Apple projects must be implemented in a dedicated `Networking` Swift package. It must be built using modern Swift concurrency features for safety, performance, and reliability.

## 1. NetworkManager Architecture
-   **Actor-based**: A central `NetworkManager` must be implemented as a Swift `actor`. This is required to ensure thread-safe access to all network resources and state.

## 2. Core Features
The `NetworkManager` implementation must include the following features:

1.  **Type-Safe Endpoints**: All API endpoints must be defined as a strongly-typed `enum` or `struct` that specifies the path, method, headers, and body. This prevents runtime errors and ensures correctness.
2.  **Request Coalescing**: The manager must maintain a dictionary of active requests to prevent duplicate in-flight network calls. If a request is made for an endpoint that is already being fetched, the existing `Task` must be returned.
3.  **Response Caching**: A `NetworkCache` actor must be integrated to cache responses based on a defined `CachePolicy` (e.g., `.default`, `.noCache`).
4.  **Interceptor Chain**: The networking client must support a chain of `RequestInterceptor` protocols. This is the required pattern for handling cross-cutting concerns such as injecting authentication tokens, logging requests/responses, and implementing automatic retry logic.