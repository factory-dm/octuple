# React Best Practices for Octuple Users

## Introduction
Octuple is a React + TypeScript component library crafted for consistency across Eightfold web apps. Following a few proven practices will help you integrate components smoothly, keep bundles lean, and deliver accessible experiences.

---

## Component Usage Best Practices
- **Prefer composition over customization**  
  Combine foundational components (e.g., `Button`, `Card`, `Stack`) instead of overriding styles. Leverage props and slots first; reach for custom SCSS only when necessary.
- **Type-safe props**  
  Always import types exposed by each component (`ButtonProps`, `TabsProps`, etc.) to benefit from autocomplete and avoid runtime errors.
- **Theming via `ConfigProvider`**  
  Wrap feature roots with `ConfigProvider` to set size, shape, or brand theme once. Avoid inline overrides that bypass design tokens.
- **Keep styles local**  
  Create additional styles with BEM-compatible class names and colocate them in `.module.scss` files to prevent global leakage.

---

## Performance Considerations
- **Tree-shakeable imports**  
  Import directly from component entry points:  
  `import { Button } from '@eightfold/octuple';`  
  This guarantees Rollup/ESM can drop unused components.
- **Lazy-load heavy features**  
  Components like `Table`, `DateTimePicker`, or `Upload` include rich logic. Load them with `React.lazy` / dynamic `import()` inside route-level boundaries.
- **Memoize render-heavy lists**  
  When rendering large data sets, pair `VirtualList` with `React.memo` or `useMemo` to avoid unnecessary DOM work.
- **Use provided hooks**  
  Hooks such as `useDebounce`, `useOnClickOutside`, and `useBreakpoint` are battle-tested and optimized—reuse them instead of reinventing.

---

## Accessibility Tips
- **Keyboard navigation**  
  Octuple components support roving tabindex patterns. Ensure custom wrappers pass `ref` and prop spread (`...rest`) so focus isn’t lost.
- **Aria labelling**  
  Supply meaningful `aria-label`, `aria-labelledby`, or `title` props to interactive elements (e.g., `IconButton`, `Tooltip` triggers).
- **Color contrast**  
  Stick to tokenized colors (`var(--oc-color-… )`); avoid manual hex codes that may break contrast ratios in different themes.
- **Announce dynamic updates**  
  For status messages or async progress, use `Snackbar` or `Loader` which include polite live region attributes out of the box.

---

Happy building! Keeping these guidelines in mind will help you ship fast, performant, and accessible features with Octuple.
