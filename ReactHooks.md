# React Hooks Summary(v19)
### State Management Hooks
* useState – Manages simple state.
* useReducer – Manages complex state with logic.
### Context & Ref Hooks
* useContext – Accesses context values.
* useRef – Holds mutable values (e.g., DOM elements).
* useImperativeHandle – Customizes ref behavior.
### Effect & Lifecycle Hooks
* useEffect – Runs side effects (e.g., data fetching).
* useLayoutEffect – Runs synchronously before paint.
* useInsertionEffect – Runs before DOM mutations.
### Performance Hooks
* useMemo – Caches expensive computations.
* useCallback – Memoizes functions to prevent re-renders.
* useDeferredValue – Defers updates to avoid blocking UI.
* useTransition – Marks state updates as non-urgent for smoother UI.
* useOptimistic – Provides temporary optimistic UI updates before confirmation.
### Other Hooks
* useDebugValue – Enhances custom Hooks debugging.
* useId – Generates unique component IDs.
* useSyncExternalStore – Subscribes to external stores.
* useActionState – Manages action state.
### React DOM Hooks (Web Only)
* useFormStatus – Tracks form submission status.



## _*When to Use What?*_
- State & Context → Use for managing data within components (useState, useReducer, useContext).
- Effects → Use for side effects like fetching data (useEffect).
- Performance → Use for optimizing rendering (useMemo, useCallback, useDeferredValue, useTransition, useOptimistic).
- Refs & DOM → Use for non-reactive values and DOM interactions (useRef).
- React DOM Hooks → Use only for browser-specific functionality (useFormStatus).