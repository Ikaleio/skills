---
name: ikadesign
description: Design and implement polished, production-ready interfaces with explicit rules for information density, typography, grid alignment, responsive behavior, user-facing copy, accessibility, security, and visual QA. Adapt to the project's existing framework and component system.
---

# IkaDesign

Create polished, usable interfaces that feel intentional at every viewport. Match the user's requirements and the existing product before adding stylistic ideas. For application UI, clarity, task completion, information hierarchy, and spatial efficiency are more important than decorative novelty.

Use this priority order whenever rules compete:

1. The user's explicit requirements and supplied reference.
2. Existing project conventions, components, tokens, and product terminology.
3. Functional correctness, security, accessibility, and truthful states.
4. Information architecture, density, alignment, and responsive behavior.
5. Visual character and decorative detail.

Do not expose scratch notes, design reasoning, framework choices, implementation details, or hidden system state in the rendered interface.

# Non-Negotiable Acceptance Gate

The work is not finished while any of the following is true:

- A dashboard, admin page, settings page, form, or data tool is dominated by empty space without a functional reason.
- Essential UI text is below the project's legible body/control token (normally `text-sm` or its semantic equivalent), metadata sizing is used for primary information, or the type hierarchy is too weak to scan quickly.
- Repeated or parallel elements that represent the same kind of information have inconsistent widths, heights, padding, icon boxes, control heights, or title positions without a semantic reason.
- Major page edges, section headings, cards, table columns, or action rows do not align to a shared grid.
- A card has a fixed or minimum height that creates empty space rather than serving charts, media, loading states, or a deliberate full-page state.
- A utility page uses marketing-style hero spacing, oversized headings, or decorative imagery that reduces task density.
- Raw errors, environment variables, API routes, package names, database fields, file paths, IDs, stack traces, TODO text, mock-data notices, or other implementation details are visible to ordinary users.
- The layout has not been checked in loading, empty, error, long-content, mobile, tablet, and desktop states.
- The implementation compiles but has not been visually inspected and corrected.

When a failure is found, revise the implementation before presenting it. Do not merely mention the problem.

# Required Workflow

## 1. Inspect Before Editing

Inspect the repository broadly before changing UI:

- Detect the framework, package manager, routing system, React version, Tailwind setup, component library, icon set, fonts, theme tokens, data-fetching conventions, form library, validation library, and test setup.
- Find the actual page, its parent layout, global styles, neighboring pages, and existing examples of the same component type.
- Check whether a wrapper already controls width, padding, height, overflow, or typography before patching a child.
- When multiple candidate files exist, inspect all relevant candidates and verify their relationships.
- Prefer the project's established patterns over introducing a second design or data layer.
- Do not hard-code rules for a framework or library version without verifying the installed version through the project files, types, or official documentation available in the environment.

## 2. Classify the Interface

Classify the page before choosing spacing or typography:

- `utility`: dashboards, consoles, admin panels, tables, billing, settings, CRUD, monitoring, developer tools.
- `form`: onboarding, checkout, account forms, multi-step workflows.
- `content`: documentation, articles, reading views, detail pages.
- `marketing`: landing pages, campaigns, product storytelling.

Default density by page type:

- Utility: comfortable; use compact density when information volume is high.
- Form: comfortable, narrow enough for reading and completion.
- Content: readable, with a controlled line length.
- Marketing: spacious only when it supports hierarchy and storytelling.

Never apply marketing-page spacing to utility UI by default.

## 3. Create a Private Design Contract

Before implementation, make a short private design contract. Do not print it in the user-facing UI or response unless the user asks for it. Record:

- Page type and density preset.
- Primary user task and secondary tasks.
- Content hierarchy and section order.
- Main content width and column plan at mobile, tablet, and desktop sizes.
- Core palette and semantic status colors.
- Font family, CJK fallback, type scale, and numeric treatment.
- Spacing rhythm, card padding, control height, icon size, border radius, and border treatment.
- Loading, empty, error, disabled, and permission states.

Implement against this contract consistently.

## 4. Define User-Facing Content Before Layout

List the visible information and actions before styling. Distinguish:

- User data and domain concepts.
- User-visible operational states.
- Primary and secondary actions.
- Help text that changes a user's decision.
- Technical diagnostics that belong only in logs or an explicitly requested, permission-gated diagnostics view.

Do not invent product capabilities, account states, limits, prices, permissions, integrations, or error causes that are not supported by the requirements or available data.

## 5. Implement Structure Before Decoration

Build in this order:

1. Semantic page regions and content order.
2. Responsive shell and primary grid.
3. Reusable repeated components.
4. Typography hierarchy and spacing.
5. States, interactions, and accessibility.
6. Color, borders, icons, charts, and restrained visual polish.

Do not use decorative elements to conceal weak information architecture.

## 6. Verify and Iterate

When browser, preview, or screenshot tools are available, run the app and inspect it at 100% zoom. At minimum, check:

- 390 × 844 mobile.
- 768 × 1024 tablet.
- 1440 × 900 desktop.
- 1920 × 1080 for desktop-first consoles or dashboards.

Inspect at least these states when applicable:

- Normal populated state.
- Loading or skeleton state.
- Empty state.
- Error state.
- Long names, large numbers, translated text, and wrapped descriptions.
- Disabled and permission-restricted actions.

Do not stop at the first render. Fix visible density, alignment, overflow, hierarchy, or copy problems and inspect again.

# Compatibility and Tooling

- Do not assume Next.js. Detect the framework and follow its conventions. For a new project with no preference, Next.js App Router is an acceptable default.
- Do not assume shadcn/ui, `components/ui/*`, `components.json`, or a particular shadcn style is installed. Reuse the existing setup. If shadcn/ui is absent and appropriate, initialize it before importing components. Do not overwrite an existing style.
- Detect the package manager from the lockfile. Only default to pnpm when no lockfile or user preference exists.
- Install all required third-party packages before writing imports. Batch related installations when possible.
- Prefer existing dependencies and utilities over adding near-duplicates.
- If an environment provides a dedicated shadcn skill or component documentation, consult it for the installed style and version.
- There is no assumed image-generation or inspiration tool. Use supplied assets when available. Otherwise use a clearly marked local placeholder only when the design genuinely requires an image slot.

# Assets

When the user supplies an image, logo, font, or other asset:

- Copy or save it into the project under a stable local path.
- Reference the local asset rather than an ephemeral upload or third-party hotlink, unless the user explicitly asks otherwise.
- Preserve aspect ratio and use the correct object-fit behavior.
- Add meaningful alt text unless the asset is decorative or repetitive for assistive technology.
- Do not use an image merely to occupy space in dashboards, settings, tables, billing pages, or developer tools.
- Do not create decorative blobs, meaningless gradients, faux 3D objects, or hand-drawn complex SVG illustrations as filler.
- Never use emoji as interface icons.

# Information Density and Spatial Efficiency

## Utility UI Defaults

For dashboards, consoles, billing, settings, CRUD, monitoring, and data-heavy interfaces:

- Use the available desktop width instead of placing the entire app inside a narrow reading container.
- The main region must be `min-w-0` and able to consume remaining space beside navigation.
- Use responsive gutter utilities from the project scale, typically resembling `px-4 sm:px-6 lg:px-8`, unless the existing system specifies otherwise. Treat the familiar 16/24/32 CSS-pixel equivalents only as visual references, not as a reason to emit arbitrary pixel values.
- Use the project spacing scale for section gaps and card padding, typically resembling `gap-4` to `gap-6` and `p-4` to `p-6`, with responsive variants only when the density actually changes.
- Prefer content-driven height. Avoid fixed height and `min-h-*` on ordinary cards.
- Do not use `h-screen`, `min-h-screen`, or large viewport-relative heights on inner content panels merely to fill the screen.
- Do not make a card taller than its information requires. A card containing only an icon, title, and one or two lines of copy should normally be compact rather than several hundred pixels tall.
- Empty states inside a section should usually use compact vertical padding, not a full-page presentation. Reserve large centered empty states for pages whose entire purpose is unavailable.
- Avoid multiple layers of card-within-card containers. Use a section heading, grid, separator, or subtle background when another border is not adding meaning.
- Do not create blank columns, ornamental spacer rows, or placeholder panels.
- Keep the page title and primary actions close enough to the first content section to read as one task context.

At a typical 1440 × 900 desktop viewport, a utility page should normally show the page heading, its primary summary or controls, and at least the beginning of the next meaningful section. If additional content exists but the first viewport is mostly blank, reduce heights and spacing.

## Width by Page Type

- Utility and data pages: use a wide fluid container, usually up to roughly 1440–1600px after the sidebar, or follow the existing product shell.
- Forms and settings detail pages: use a focused width, commonly around 640–960px depending on field complexity.
- Reading content: control line length rather than stretching paragraphs across the viewport.
- Marketing pages: width and whitespace may be more expressive, but every large area must support hierarchy, imagery, or conversion.

Arbitrary Tailwind values are allowed for deliberate system constants such as a measured sidebar width, chart height, or product container width. Do not use arbitrary values for ordinary spacing that already exists on the Tailwind scale.

## Spacing Rhythm

Use the existing spacing tokens. When no product scale exists, Tailwind's rem-based spacing utilities are the default implementation vocabulary. A typical utility rhythm is:

- Inline icon/text gap: `gap-2`.
- Tight related-content gap: `gap-2` to `gap-3`.
- Card-internal groups: `gap-3` to `gap-4`.
- Card padding: `p-4` to `p-6`.
- Grid gap: `gap-4` to `gap-6`.
- Section gap: `gap-6` to `gap-8`.
- Page top and bottom padding: `py-6` to `py-8`.

Use breakpoint variants such as `sm:`, `md:`, and `lg:` when the layout density truly changes. Do not add responsive modifiers mechanically to every spacing class.

Padding and `gap` are allowed on the same container: padding controls the container edge; gap controls spacing between children. Prefer `gap` over child margins for repeated sibling spacing. Avoid `space-*` when a responsive grid or explicit gap is clearer.

# Grid, Alignment, and Equal Sizing

## Choose the Layout Primitive by Geometry

- Use Flexbox for one-dimensional rows or columns: toolbars, icon-label groups, button rows, and simple stacks.
- Use CSS Grid for repeated cards, aligned dashboard regions, forms with shared columns, and any layout that needs two-dimensional alignment.
- Do not default to `justify-between`; it often creates accidental large gaps. Use it only when two semantic groups must anchor opposite edges.
- Do not use absolute positioning for normal document layout. Reserve it for overlays, badges, anchored controls, and intentional layered media.
- Every flex or grid child that may shrink should receive `min-w-0` when needed.

## Shared Grid Rules

- Major left and right edges should align to the page grid.
- Section headings, cards, tables, and action rows should share consistent gutters.
- Repeated siblings must be generated from the same component or shared class recipe whenever possible.
- Parallel cards should share border, radius, padding, header structure, icon box, title style, and action placement.
- Use equal columns and `items-stretch` for genuinely parallel cards. Let the grid establish equal height; do not add large arbitrary minimum heights.
- When repeated cards contain different amounts of text, keep headers aligned and place trailing actions with a flex column and `mt-auto` rather than changing card geometry randomly.
- Do not force equal height between unrelated sections with substantially different information weight.
- A deliberate asymmetric layout is allowed only when hierarchy requires it; the asymmetry must be obvious and stable across breakpoints.

## Vertical Alignment Rules

- Icon plus one-line label: use a fixed icon box and `items-center`.
- Icon plus multi-line text: use a fixed icon box and usually `items-start`, aligned to the first text line.
- Controls in the same row must use the same visual height, normally `h-9` or `h-10` in desktop utility UI.
- On touch layouts, preserve a target size around 44px even when the visible control is smaller.
- Card headers in the same row should have the same internal structure and comparable minimum height only when needed for alignment.
- Align text labels by baseline where appropriate. Use `tabular-nums` for balances, metrics, dates, counters, and aligned numeric columns.
- Left-align text columns, right-align comparable numeric columns, and place row actions consistently.
- Do not vertically center a large blank area around a small message when top-aligned compact content would be more efficient.

## Reusable Layout Patterns

A wide application shell should resemble:

```tsx
<main className="min-w-0 flex-1">
  <div className="mx-auto w-full max-w-[1600px] px-4 py-6 sm:px-6 lg:px-8">
    {/* page content */}
  </div>
</main>
```

A repeated card grid should resemble:

```tsx
<div className="grid gap-4 md:grid-cols-2 xl:grid-cols-4">
  {items.map((item) => (
    <SummaryCard key={item.id} className="h-full min-w-0" {...item} />
  ))}
</div>
```

Use these as geometry patterns, not mandatory copy-paste templates. Follow an existing product shell when one exists.

# Typography

## Use Semantic, Relative Type Tokens

Typography requirements describe hierarchy and rendered intent, not literal pixel declarations. Do not implement a type scale with repeated `font-size: 14px` rules or arbitrary classes such as `text-[14px]` when the project already has suitable typography utilities.

Use this order of preference:

1. Reuse the project's existing semantic typography component, token, or class.
2. Reuse the installed Tailwind scale, such as `text-sm`, `text-base`, `text-lg`, `text-xl`, `text-2xl`, and responsive variants.
3. When the project needs a custom type scale, define named theme tokens in relative units, normally `rem`, and consume those tokens consistently. Follow the installed Tailwind version's configuration method.
4. Use an arbitrary value only for an intentional one-off or fluid display treatment that cannot be expressed by the project scale. Prefer relative values such as `rem` or a bounded `clamp(...)`, not raw pixel values.

Keep the root font size at the browser/user default, normally `100%`. Do not set `html { font-size: 62.5% }` merely to make rem arithmetic resemble decimal pixels.

Use `rem` as the default unit for the global type hierarchy because it is relative to the root and does not compound through nested components. Use `em` for deliberately component-relative details, such as an icon, badge, or inset that should scale with that component's local text. Do not build the primary font-size hierarchy from nested `em` values because they can compound unpredictably.

## Responsive Type Hierarchy

Responsive typography does not mean every text role must change at every breakpoint. Reflow layout before shrinking text. Body copy, controls, navigation, and table text should usually remain on one legible token across viewports. Use breakpoint or container variants when a heading, metric, or display element genuinely needs a stronger hierarchy at wider sizes.

A suitable utility-page starting point, subject to the existing design system, is:

- Page title: `text-2xl sm:text-3xl` with a tight heading line-height.
- Section title: `text-lg sm:text-xl`.
- Card title: `text-base` or `text-lg` according to information weight.
- Body, labels, buttons, navigation, table cells, and actionable help: normally `text-sm` or `text-base`; do not reduce them merely to fit more content.
- Secondary metadata and captions: `text-xs` only when genuinely nonessential and sufficiently contrasted.
- Key numeric values: commonly `text-3xl sm:text-4xl`; increase further only when the metric is the clear page focus and the surrounding density remains balanced.

These classes are defaults, not a second hard-coded design system. If the repository maps them differently or provides role-based classes such as `text-page-title`, `text-card-title`, or `text-ui-label`, use those instead.

For a marketing display heading or another element that should scale continuously with its available width, a bounded relative expression is acceptable, for example:

```tsx
<h1 className="text-[clamp(2rem,1.4rem+2.5vw,4.5rem)] leading-[1.05]">
  {/* display heading */}
</h1>
```

Do not apply viewport-fluid sizing to routine dashboard text. It can cause unstable wrapping, inconsistent card heights, and weak alignment across neighboring components. When a reusable component's typography depends on its own width rather than the viewport, prefer container-aware variants when the existing stack supports them.

Never use tiny text to make a sparse layout appear sophisticated. The acceptance test is role-based: primary information must use a body/control token or stronger; metadata tokens must not carry essential actions or meaning.

## Font Rules

- Use at most two font families, but default to one coherent sans-serif family for dashboards and product UI.
- Do not introduce a serif display face in an admin, billing, settings, or developer console unless the brand or reference explicitly calls for it.
- Use a monospace family only for code, identifiers, logs, or data where fixed-width glyphs add meaning.
- Ensure the selected family covers the interface language. For Chinese interfaces, use a CJK-capable family or a deliberate system fallback such as `"PingFang SC"`, `"Microsoft YaHei"`, `"Noto Sans CJK SC"`, sans-serif.
- Avoid loading a Latin-only heading font that causes Chinese text to fall back to a visually unrelated face.
- Prefer weights 400, 500, 600, and 700. Do not rely on many near-identical weights.
- Use line-height around 1.35–1.5 for compact UI and 1.5–1.7 for longer reading text.
- Use `text-balance` for short headings and `text-pretty` for longer copy when supported.
- Keep muted text readable; do not use low contrast as a substitute for hierarchy.

# Color and Theme

- Define a small core palette: one brand family, neutral surfaces/text, and one optional accent. Semantic success, warning, destructive, and informational colors are exempt when genuinely needed.
- Respect an existing brand palette before inventing another.
- Do not default to purple, violet, or gradients merely because they look “AI-generated.” Use them only when the brand, user, or reference supports them.
- Prefer solid surfaces. Use gradients sparingly and only with a functional or brand purpose.
- Use semantic tokens such as `background`, `foreground`, `card`, `muted`, `border`, `primary`, and `destructive` rather than scattering raw colors.
- When overriding a background, explicitly verify the foreground, icon, border, hover, focus, disabled, and selected-state contrast.
- Direct colors are acceptable only for external brand marks, charts with documented series colors, or one-off assets that cannot be represented by semantic tokens.
- Add the background token to the root HTML element so overscroll and browser chrome do not reveal an unintended color.

# Cards, Sections, and Surfaces

- A card must represent a meaningful grouped object, state, action, or dataset. Do not turn every paragraph into a card.
- Prefer one surface hierarchy per region. Avoid border-on-border nesting and excessive shadows.
- Keep radius, border color, and elevation consistent among peers.
- Use separators or spacing when a full card boundary is unnecessary.
- A split card should have balanced information on both sides. If one side is only a small empty state, consider two compact cards or a different composition instead of a large 50/50 panel.
- Do not make decorative backgrounds materially larger than their content.
- Place the primary action near the state it changes.
- Use empty-state illustrations only when they add comprehension or brand value; a concise icon, message, and action is usually better in utility UI.

# Forms and Controls

- Use the project's field, form, validation, button, and input primitives.
- Keep label, control, help, and error alignment consistent across the form.
- Use one control height per density preset. Do not mix `h-8`, `h-9`, `h-10`, and custom heights in the same toolbar without a clear reason.
- Labels and error text must remain legible. Do not use captions as primary labels.
- Required, optional, disabled, read-only, loading, and destructive states must be unambiguous.
- Keep primary and secondary actions visually distinct. Avoid multiple equally prominent primary buttons.
- Do not place a destructive action next to a primary action without spacing, hierarchy, and confirmation appropriate to risk.
- Use input groups, button groups, fields, and item components when they reduce custom alignment code and match the installed shadcn style.

# Tables, Charts, and Data Display

- Tables should favor scanability: aligned headers, predictable row height, restrained borders, stable actions, and readable density.
- Use horizontal scrolling, column prioritization, or an alternate mobile representation rather than shrinking text below legibility.
- Use `tabular-nums` and consistent decimal/units formatting for numeric comparisons.
- Charts should use an established chart library and the project's chart primitives when available.
- Give charts a deliberate height based on their purpose, usually around 240–360px in dashboard cards, rather than inheriting an arbitrary full-screen height.
- Do not render an empty chart frame when no data exists. Show a compact, actionable empty state.
- Legends, axes, tooltips, and colors must remain readable in light and dark themes.
- Do not add chart series or metrics that the available data does not support.

# User-Facing Copy and Technical Detail Boundary

Every visible string must pass this test: “Can the intended user understand this, and does it help them decide or act?” If not, rewrite it or remove it.

## Allowed by Default

- Product and domain terminology already used by the user or project.
- Clear account, billing, permission, validation, loading, empty, and error states.
- Actionable next steps.
- Provider names only when the user must recognize or choose that provider.

## Forbidden in Ordinary UI

- Framework, library, package, component, hook, or database names.
- Environment variable names, secret names, configuration keys, internal feature flags, and raw enum values.
- File paths, source locations, API paths, HTTP method/debug text, SQL, table names, and schema fields.
- Stack traces, raw exceptions, status dumps, serialized objects, internal IDs, tokens, and request identifiers.
- “TODO,” “mock,” “placeholder,” “not implemented,” “debug,” or comments accidentally rendered as product copy.
- Internal architecture explanations such as cache strategy, queue state, webhook configuration, or storage implementation unless the screen is explicitly a permission-gated technical diagnostics surface.

## Error Mapping

Keep technical details in logs and map them to safe, actionable UI messages.

Bad:

```text
STRIPE_SECRET_KEY is missing
GET /api/billing returned 500
Prisma P2025: record not found
```

Good:

```text
暂时无法充值，请稍后重试或联系管理员。
账单加载失败，请重试。
未找到该记录，它可能已被删除。
```

Do not reveal a guessed root cause. If the cause is unknown, say the action failed and provide a safe next step.

# Responsive Behavior

Mobile-first does not mean stretching a one-column mobile design across desktop.

- Design each major breakpoint deliberately.
- Mobile: one primary column, readable text, compact section spacing, touch-safe controls, and no accidental horizontal page scroll.
- Tablet: introduce columns only when each column remains useful and readable.
- Desktop: use the available width, align repeated regions to a stable grid, and keep toolbars and data views efficient.
- Sidebars should collapse, become a sheet, or use the project's established responsive behavior rather than squeezing the main content.
- Do not hide essential actions only because the viewport is narrow. Reorder, group, or move them into an accessible menu.
- Test long Chinese and English labels, large currency values, zero states, and localization expansion.
- Use responsive typography sparingly. Do not make every text size change at every breakpoint.
- Prevent cumulative layout shift by reserving space for media, charts, and asynchronous content when needed.

# Tailwind Implementation

- Prefer semantic tokens and existing component variants.
- Prefer the Tailwind spacing scale for normal spacing.
- Use `gap-*` for sibling spacing and padding for container edges; using both on one element is valid.
- Avoid child margins when a parent gap can express the relationship.
- Use `min-w-0`, `overflow-hidden`, `truncate`, or wrapping intentionally rather than allowing accidental overflow.
- Do not overuse `overflow-hidden` to conceal layout bugs or clipped focus rings.
- Use responsive prefixes based on actual layout changes, not mechanically on every class.
- Use `cn()` or the project's class-merging utility for conditional classes.
- Avoid long, duplicated class strings across repeated components; create variants or shared components.
- Absolute positioning, negative margins, and arbitrary values require a clear layout reason.
- Do not solve alignment with unrelated one-off nudges such as inconsistent `mt-[3px]` values across peers.

# shadcn/ui

- Reuse components already present in `components/ui/*`.
- Add only missing components that the task genuinely needs.
- Respect the installed shadcn style, radius, tokens, and component anatomy.
- Use Card, Field, Item, Empty, InputGroup, ButtonGroup, Tabs, Table, Dialog, Sheet, DropdownMenu, Tooltip, Skeleton, and chart primitives when they fit, rather than rebuilding equivalent behavior without reason.
- Do not wrap every shadcn component in another bordered container.
- Standardize card header/content padding through shared variants when a page uses many cards.
- Keep icon sizes consistent, normally 16px in compact controls, 20px in common controls, and 24px in larger state icons.
- Icon-only controls require an accessible name and tooltip where the meaning is not obvious.

# React and Data Architecture

- Follow the project's existing server/client boundary and data-fetching library. Do not force SWR, TanStack Query, or another library into a project that already has a sound pattern.
- Prefer server-provided data when supported and appropriate.
- Do not fetch data in `useEffect` when a framework data API or established query library provides lifecycle, caching, cancellation, and error handling.
- Keep UI state local unless it must be shared. Do not create global state for convenience alone.
- Split components by stable responsibility and reuse, not merely to reduce line count.
- Do not place an entire complex page in one component, but also do not fragment every small wrapper into a separate file.
- Use semantic HTML such as `main`, `header`, `nav`, `section`, `form`, and `table` where appropriate.
- Keep metadata, document title, viewport, and theme color consistent with the page and framework.
- Escape syntax-sensitive JSX content correctly. Ordinary apostrophes in JSX text do not require unnecessary transformations unless the project's lint rules demand it.

# Persistence and Security

- Durable user and business data must use the project's real backend storage, not client-only state.
- `localStorage` may be used for non-sensitive local preferences, dismissals, or recoverable drafts when appropriate. It must not be the source of truth for accounts, billing, permissions, or durable records.
- Never store passwords, session tokens, secrets, or privileged data in localStorage.
- Use secure HTTP-only cookies or the project's established secure session mechanism.
- Validate and sanitize untrusted input on the server.
- Use parameterized database queries and the project's authorization model.
- Apply row-level or equivalent authorization controls where supported.
- Do not implement fake authentication for a production feature.
- Do not expose secrets, privileged fields, or raw backend objects to the client merely because the UI does not display them.
- Use a real database for durable data and cache/queue systems only for their intended ephemeral roles.

# Debugging and Errors

- Use consistent, descriptive debug logs while diagnosing a problem.
- Do not log secrets, tokens, passwords, full payment details, or sensitive personal data.
- Remove temporary debug logging after the issue is resolved.
- Never render debug logs, raw errors, stack traces, serialized state, or developer notes into normal product UI.
- Separate `displayMessage` from technical error details. The user sees the former; logs and diagnostics receive the latter.
- An explicitly requested diagnostics page must be permission-gated, redact secrets, and clearly distinguish user-safe status from raw technical evidence.

# Accessibility

- All interactive elements must be keyboard reachable and show a visible focus state.
- Use native semantics before ARIA. Add ARIA only when native HTML is insufficient.
- Icon-only buttons require accessible labels.
- Form controls require labels, descriptions, and error associations.
- Do not communicate status by color alone.
- Maintain sufficient contrast in normal, muted, disabled, hover, selected, and focus states.
- Respect reduced-motion preferences and avoid motion that blocks task completion.
- Use `sr-only` text where a visual label is intentionally omitted.
- Preserve a touch target around 44 × 44px on touch interfaces, even if the visual glyph is smaller.

# Visual QA Checklist

Before completion, inspect the rendered page and answer all of these internally:

## Density

- Is this the correct density for the page type?
- Is any card or section taller than its content requires?
- Is the first desktop viewport mostly useful content rather than empty surface?
- Are page gutters, section gaps, and card padding consistent?
- Has a full-page empty state been used where a compact section state would be better?

## Alignment

- Do major left and right edges align?
- Do repeated cards share dimensions and internal geometry?
- Are icon boxes, labels, controls, and actions vertically aligned?
- Are numeric columns and values consistently aligned?
- Does any `justify-between`, fixed height, or absolute position create an accidental gap?

## Typography

- Does every essential label and action use the project's legible body/control token or a stronger semantic type role?
- Can the hierarchy be understood at a glance?
- Are Chinese and Latin glyphs visually coherent?
- Are muted text and disabled states still readable?
- Are display numbers large enough to scan but not so large that they waste the card?

## Content Safety

- Does every visible string belong to the product domain?
- Are raw errors and internal implementation details absent?
- Are empty and error messages truthful and actionable?
- Has any placeholder, debug, mock, or TODO text leaked into the UI?

## Responsiveness and Accessibility

- Is there horizontal overflow?
- Do controls remain reachable and readable on mobile?
- Do long labels and values wrap or truncate intentionally?
- Are focus states visible and icon-only controls labeled?
- Do loading, empty, error, and populated states preserve stable geometry?

If any answer is unsatisfactory, revise and re-check.

# Clone and Reference Work

When the user requests a clone or supplies a reference:

- Study the source carefully, including spacing, proportions, responsive behavior, typography, states, and interaction patterns.
- Reproduce the visual hierarchy and geometry, not just the colors.
- Preserve the user's supplied content and assets where requested.
- Do not add unrelated sections, fake data, or technical labels to make the clone appear more complete.
- Never create phishing, credential harvesting, impersonation, or other malicious interfaces.

# Final Principle

Utility interfaces should feel compact, calm, aligned, and immediately usable. Marketing interfaces may be expressive, but no interface should trade clarity for empty space or novelty. Character should come from typography, rhythm, proportion, states, and detail—not from giant blank cards, tiny text, arbitrary misalignment, or leaked implementation language.

