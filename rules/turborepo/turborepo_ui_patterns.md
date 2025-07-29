# Rule: Turborepo UI Patterns

Common UI patterns and libraries used across turborepo web applications.

## 1. Theme Provider (Required - 100% adoption)
All projects must implement theming using `next-themes` with the following standard configuration:
- **Provider**: `ThemeProvider` from next-themes
- **Default Theme**: `defaultTheme="system"` to respect user OS preferences
- **Attributes**: `attribute="class"` for Tailwind CSS integration
- **System Detection**: `enableSystem={true}` to enable automatic theme switching
- **Storage**: Theme preference stored in localStorage
- **Implementation**: Wrapped in DesignSystemProvider from packages/design

## 2. Form Handling (85% adoption)
The recommended pattern for form handling combines:
- **React Hook Form**: For form state management and validation
- **Zod**: For schema validation and type inference
- **Pattern**: Define Zod schema → Infer TypeScript types → Use with useForm hook
- **Alternative**: Native form handling with FormData API is acceptable for simple forms

## 3. Toast Notifications
Projects typically use `sonner` for toast notifications:
- **Provider**: `<Toaster />` component at app root
- **Usage**: `toast.success()`, `toast.error()`, `toast.promise()`
- **Position**: Bottom-right by default
- **Duration**: 4000ms standard, with longer durations for errors

## 4. Loading States
Consistent patterns for handling loading states:
- **Skeleton Components**: Use skeleton loaders from shadcn/ui for content placeholders
- **Suspense Boundaries**: Leverage React Suspense for async components
- **Loading Indicators**: Subtle animations, avoid full-page spinners
- **Progressive Enhancement**: Show partial content as it loads

## 5. Error Boundaries
Error handling follows these patterns:
- **Page-level Boundaries**: Each route group has an error.tsx file
- **Component Boundaries**: Critical components wrapped in error boundaries
- **User Feedback**: Clear error messages with recovery actions
- **Logging**: Errors sent to monitoring service (Sentry)

## 6. Data Tables
For complex data display:
- **Library**: `@tanstack/react-table` for advanced table features
- **Features**: Sorting, filtering, pagination, column visibility
- **Styling**: Consistent with shadcn/ui table components
- **Performance**: Virtualization for large datasets

## 7. Modal and Dialog Patterns
- **Library**: Radix UI Dialog primitives via shadcn/ui
- **State Management**: Controlled by URL params or Jotai atoms
- **Accessibility**: Proper focus management and keyboard navigation
- **Animations**: Smooth enter/exit transitions with Framer Motion or CSS