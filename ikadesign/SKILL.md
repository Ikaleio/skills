---
name: ikadesign
description: Design and build distinctive, usable interfaces with task-appropriate density, readable typography, shared alignment rules, responsive layouts, audience-safe copy, and explicit visual verification. Adapt to the authorized project environment and its available tooling.
---

# ikadesign

## 1. Operating Contract

Apply these rules when designing, building, or revising an interface.

- Respect the user's task, supplied references, brand direction, and explicit source/inspection restrictions. Do not retrieve memories, inspect repositories, or seek outside examples when the user prohibits them.
- Treat the numeric values below as starting defaults for a balanced application UI, not universal limits. A clear user requirement or documented content need can override them. Security, truthful states, and accessible operation remain requirements.
- Optimize task clarity and legibility before decorative composition. Preserve character; do not turn every product into the same dense dashboard.
- Let content determine the size of ordinary panels. Do not manufacture height or stretch a few lines across a large surface to make a page look substantial.
- Define typography by semantic role and geometry by component family. Related components must share the appropriate dimensions and alignment tracks.
- Distinguish loading, empty, unavailable, error, and populated states. Their layouts do not automatically need the same height.
- Display product information for the current audience, not development commentary or raw implementation failures.
- Verify the rendered result when tools permit. Passing a build is not evidence of visual correctness. Never claim tests or visual inspection that did not occur.

## 2. Write a Task-and-Design Brief

Before substantive implementation, record a short brief in working notes or the delivery discussion, never inside the product UI. Include:

1. **Audience and task:** Who uses this screen? What must they understand or do first? Identify the primary action, or explicitly note that this is a read-only/unavailable state.
2. **Content and states:** Identify the real information hierarchy, data availability, and relevant loading/empty/error/permission variants. Do not invent data to improve a composition.
3. **Interface mode and density:** Choose a mode below and state the intended density.
4. **Layout contract:** Identify shared columns, component families, content-width behavior, and the main content that should begin in the reference desktop viewport.
5. **Visual direction:** Specify mood, a small palette of color roles, font roles with language coverage, and spacing/radius choices.
6. **Acceptance checks:** Select representative viewport sizes, long-content cases, and the states most likely to break the layout.

Choose density according to the task:

| Mode | Default approach |
| --- | --- |
| Dashboard, console, settings, billing | Balanced density; compact summaries; substantive controls or records appear early. Avoid promotional hero proportions. |
| Table, monitoring, professional workspace | Denser repetition with readable text and adequate interaction targets. Viewport-filling work areas can be appropriate. |
| Reading, documentation, article | Constrain text measure and support sustained reading. Side space is not inherently waste. |
| Marketing, editorial, portfolio | More expressive typography and whitespace when they support narrative, imagery, and action. |
| Focused flow, onboarding, authentication | Keep the task coherent and bounded. Do not fill the screen with unrelated information. |

For a new application screen without another direction, use balanced density. Mobile-first means adapting composition to available space, not keeping desktop typography small or preserving mobile stacking everywhere.

## 3. Content-Driven Layout and Density

### Give every large surface a reason

- Ordinary cards, summaries, notices, and empty sections use intrinsic height. Their height should follow content, line-height, padding, and gaps.
- Do not apply fixed heights, large `min-height`, viewport-height units, `aspect-ratio`, or `h-full` to ordinary information cards merely for visual impact.
- Explicit height is appropriate for justified workspaces, media, maps, charts, virtualized lists, and specific reference designs. State the content or interaction reason, not just a desire to fill space.
- Equal-height peer cards may stretch within a shared content-sized grid row. This does not justify stretching the grid to the viewport or giving all unrelated cards the same minimum height.
- Use `justify-between` to separate real groups, such as a toolbar's title and actions. Do not use it to distribute a label, value, and caption across an unnecessarily tall card.
- Anchoring account controls to the bottom of a sidebar or actions to the bottom of genuine peer cards is legitimate. It is not a reason to enlarge those containers.
- Leave unused space outside a compact completed section rather than inflating its internals. Do not add fake metrics, illustrations, tips, or extra cards to increase occupancy.

### Establish a spacing budget

For a balanced application UI, start with these values and adjust deliberately:

| Relationship | Starting range |
| --- | --- |
| Icon to label; tightly related elements | `0.375–0.75rem` |
| Related rows or field groups | `0.5–1rem` |
| Panel padding | `1–1.5rem` |
| Sibling panels or major sections | `1–1.5rem` |
| Page gutter | `1rem` on narrow screens; `1.5–2rem` on desktop |

Use a small spacing scale. Make the distance within a group smaller than the distance between unrelated groups.

These are defaults, not commands to use the maximum everywhere. Audit stacked page padding, section padding, card padding, and child margins; individually reasonable values can create excessive cumulative space.

A utility panel with only a few short content rows but roughly `16rem` or more of height is a review trigger, not an automatic failure. Check whether media, a real interaction, or its peer content actually explains that height.

### Match width to content

- Reason about the width available inside the shell, after sidebars and gutters, rather than the viewport width alone.
- Use a shared page container and alignment edges. Avoid unrelated nested `max-width` wrappers that create progressively narrower content.
- Let tables, dashboards, and work areas use appropriate available width. Constrain reading passages and focused forms where that improves comprehension.
- Do not stretch a single short field or notice across a huge width without a compositional reason; group it with related content or bound that region.
- At the chosen reference desktop size, aim to reveal the main working section or its beginning beneath the summary. Do not force every record or every screen into one viewport.
- When supporting information pushes the primary task down, first reduce redundant copy, oversized containers, and repeated framing. Do not start by shrinking the text.

## 4. Layout Geometry and Alignment

Choose layout primitives by the relationship being represented, not by a blanket Flexbox-first rule.

- Use **Grid** for peer cards, aligned form columns, repeated metrics, and content whose column edges must line up. Even a simple two-column layout can benefit from Grid.
- Use **Flexbox** for one-dimensional relationships: icon-label pairs, toolbar groups, button contents, and linear navigation.
- Use normal document flow for prose and simple vertical sections. Use semantic tables for genuinely tabular data.
- Use absolute positioning for overlays, anchored decorations, and similar intentional layers, not as a substitute for normal page layout.

### Shared geometry contracts

For each component family, define the relevant shared properties before rendering variants: control height, padding, icon box, text style, header structure, column widths, and action alignment.

- Equal-rank sibling cards use shared tracks, such as `repeat(n, minmax(0, 1fr))`, when equal widths are intended. Do not approximate a grid with content-sized cards and `justify-between`.
- Use `min-w-0` on shrinkable grid/flex children and choose intentional wrapping or truncation. Do not let a long label silently widen one peer or overflow the page.
- Repeated headers align to the same inset; repeated values align to their intended baseline; matching control groups share height and padding.
- Align related label/control rows through shared columns or a shared layout component, not manual spaces or unrelated per-row offsets.
- If variable-length card content needs aligned footers, use a shared row structure or content-sized stretched peers with intentionally anchored footers. Do not clamp meaningful copy just to hide a mismatch.
- Equalize like with like: matching cards, buttons, fields, or tabs within a group. Unrelated panels and primary/secondary action variants do not need identical dimensions.

### Vertical centering versus baseline alignment

- Button and icon-label contents normally use `inline-flex`, `items-center`, a shared gap, and a predictable icon box.
- Make icons non-shrinking and block-level where appropriate. Check SVG viewBox whitespace when an icon appears off-center despite correct box alignment.
- Center single-line control content within its control. For multi-line titles with actions, choose top alignment or another intentional relationship rather than blindly centering everything.
- Align adjacent text and numeric values by baseline when their font sizes differ. Centering their boxes is not necessarily the intended alignment.
- Check actual font fallback, glyph appearance, line-height, and asymmetric padding before changing positions.
- Avoid item-specific `top`, negative margins, or `translateY` patches. A small optical correction is allowed only after those checks and should belong to a shared, documented component variant.

### Spacing responsibilities

- Padding controls a container's internal inset; gap controls separation among its children; margin controls its relationship to surrounding content. They may coexist.
- `grid gap-4 p-5` is a normal valid combination. Do not prohibit padding and gap on the same element.
- Prefer one owner for each inter-element relationship. Do not combine child margins and parent gaps to accidentally count the same space twice.
- Prefer gap for repeated children. Use margins intentionally for document flow or anchoring, not as an improvised layout grid.

## 5. Typography and Optical Scale

Define semantic type roles rather than choosing sizes independently in each component.

For balanced application interfaces, use the following starting scale. The pixel equivalents assume a browser root size of 16px; keep sizing relative and respect user scaling.

| Role | Starting size |
| --- | --- |
| Page title | `1.75–2rem` / 28–32px |
| Section or card heading | `1.125–1.25rem` / 18–20px |
| Main body, explanatory text, form entry | `1rem` / 16px |
| Navigation and control labels | `0.875–1rem` / 14–16px; favor the upper end for Chinese UI |
| Secondary metadata and supporting labels | `0.875rem` / 14px |
| Important summary number | `2–2.75rem` / 32–44px, only when its importance warrants it |

- Do not make 14px the default size for the whole application. Secondary metadata must remain secondary in both role and frequency.
- Do not use text below `0.875rem` in ordinary application UI. Exceptions require a deliberate specialist/dense requirement and a legibility check; never use them to rescue an oversized layout.
- Do not enlarge every heading and value to compensate for oversized containers. Fix the container and the hierarchy together.
- Use body line-height around 1.45–1.65, favoring roughly 1.5–1.7 for multi-line Chinese text. Headings and short controls can be tighter, but must not clip glyphs.
- Do not set the root font size below the user's normal setting to make rem-based UI smaller. Do not disable browser zoom or scale the entire page to fit.

### Font roles and language coverage

- Default to one intentional UI text family. Add at most one intentional display or monospace family when the product benefits. Language fallbacks are not extra decorative font choices.
- For Chinese interfaces, use a coherent CJK-capable sans-serif stack unless the brief explicitly calls for a different style. A Latin font choice alone does not specify Chinese typography.
- Do not apply serif headings by habit to a utility console. Use them only when they fit the actual visual direction and their CJK rendering has been checked.
- Inspect representative Chinese, English, numerals, and punctuation with the fonts actually loaded. Check fallback and loading behavior when custom fonts are used.
- Use tabular numerals for comparable amounts, counts, and changing metrics when supported by the chosen font. Keep units and currency labels legible.
- Apply font roles through project-compatible tokens. Avoid self-referential font variables or assuming that a CSS variable alone loads or applies a font.
- Use balanced wrapping for display headings when helpful. Do not force balancing, no-wrap, or truncation on every short application label.

## 6. State-Aware Composition

Design the relevant states explicitly instead of dropping different text into an unchanged large card.

- **Loading:** Use a restrained indicator or skeleton that approximates the expected structure when useful for stability. Reserve space for content that is actually expected, not for speculative widgets.
- **Empty:** Explain what is absent and provide one relevant next action when available. Embedded empty states should normally collapse to a compact row or content-sized panel.
- **Unavailable or unconfigured:** State the capability's status and an appropriate next step. Do not retain a large dormant form or purchase panel solely to fill the layout.
- **Error:** Preserve useful context and safe existing data, explain the impact, and offer a real retry or recovery path when supported.
- **Populated:** Prioritize real content and controls. Pagination, scrolling, and dense repetition should serve the task.
- **Permission-limited:** Show only information and actions appropriate to the verified role. Client-side hiding does not replace server authorization.

A page-level empty state can be more spacious than an inline one. A meaningful stable workspace may keep its structure between states. Apply compactness to the context, not mechanically to every blank area.

Never replace unknown or failed data with misleading values such as zero, an unlimited allowance, a paid status, or fabricated records.

## 7. UI Copy and Information Boundaries

For each visible string, ask: **Does this audience need this information here to understand a state, make a decision, complete a task, or recover from a problem?** If not, omit it or move it to an appropriate authorized diagnostics/documentation surface.

### Separate product copy from implementation notes

- Product UI contains real labels, useful instructions, relevant status, and actionable feedback.
- Source comments, development notes, tool explanations, and delivery caveats belong in their appropriate development channels, not in ordinary product panels.
- Do not render framework names, component names, database schema, server environment variables, file paths, stack traces, or implementation TODOs unless they are intentionally relevant to that product screen and authorized audience.
- Do not expose raw exception messages, serialized error objects, request dumps, or backend responses as user-facing copy. Map expected errors to reviewed messages; use a safe fallback for unknown failures.
- Keep secrets and sensitive operational data out of public UI and client-visible debug output. Redact diagnostics and minimize logged personal data.
- A safe support reference can be shown when it helps resolution. Detailed diagnostics require an intentional audience, suitable authorization, and redaction.

Do not implement a blanket ban on technical vocabulary. Model names, endpoints, rate limits, API keys, and request identifiers may be core product information in a developer console. Distinguish user-owned configuration from unrelated server internals.

### Write for the actual state and role

- Prefer a specific status and next step over repeated descriptions of what the page already obviously does.
- Do not show setup instructions for administrators to ordinary users. Offer an administrator a configuration action only when that role and destination actually exist.
- Do not invent working buttons, support channels, links, or recovery capabilities. A clear informational state is better than a dead action.
- Do not silently remove meaningful limitations to make a screenshot cleaner.
- Never misrepresent a prototype, placeholder, payment flow, authentication flow, or demo data as production functionality. Use an intentional demo disclosure when needed and describe unresolved integration work in the delivery report.
- Keep UI language consistent with the user's request; retain technical identifiers in their appropriate form.

## 8. Color, Surfaces, Assets, and Character

- Use a small set of color roles: usually one primary, a neutral surface/text system, and limited accents. Define concrete token values in the brief or theme.
- Treat a 3–5-color target as palette discipline, not an exact count of every rendered shade. Semantic success, warning, error, focus, disabled, and chart colors may require additional tokens.
- Choose colors from the brief and brand, not a universal favorite or prohibition. Prefer solid surfaces by default; use gradients only when they have an intentional role in the requested direction.
- Define semantic background/foreground pairs. When changing a surface, check its text, icons, borders, focus state, and disabled treatment together.
- Do not achieve quiet styling by making essential text too faint. Check contrast against the actual rendered background.
- Use a small radius and elevation system. Do not put every heading, sentence, and row inside its own bordered card.
- Keep purposeful whitespace and distinctive typography where appropriate. Avoid decorative blobs, fake charts, arbitrary illustrations, or oversized icon circles as filler.
- Use the project's coherent icon family when available. Define shared icon sizes and stroke treatment; do not substitute emojis for interface icons.

### Assets and fonts

- Use provided or otherwise authorized assets. Save provided assets locally and reference local paths when appropriate to the project and user request.
- Do not invent asset URLs or assume image-generation, asset-search, or platform-specific tools exist. Use only capabilities actually available and authorized.
- Missing imagery does not automatically require a placeholder. Omit nonessential decoration; use an explicitly provisional local placeholder only when the design requires that slot.
- Provide meaningful alt text for informative images and empty alt text for decorative images. Alt text is user-facing content, not a place for developer TODOs.
- Use established libraries and real data for maps or complex geographic visuals. Do not fabricate geographic paths or data. Reuse the project's charting approach; do not install chart libraries for a screen without charts.
- Prefer existing/self-hosted font support when practical. Do not assume Latin-only assets cover the UI's language or that a remote font will always load.

## 9. Environment-Aware Implementation

This skill does not imply any particular tool, framework, component library, or dependency is installed.

### Respect scope and compatibility

- When inspection is allowed, read the minimum relevant manifests, framework versions, theme definitions, components, and parent layouts. Expand only to resolve a concrete dependency or uncertainty; do not read every search match indiscriminately.
- When inspection is prohibited, work from the authorized materials and explicit contract. Do not infer unseen implementations or claim repository compatibility was verified.
- Reuse the established framework and design system unless changing them is part of the task. Do not migrate a project just to follow this skill.
- For a brand-new React project with no specified preference or constraints, Next.js App Router is a default, not a requirement for every interface.
- Follow the installed versions of React, Next.js, Tailwind, and other packages. Do not assume version-specific hooks, directives, caching APIs, configuration files, or migration rules from this skill.
- If API behavior is uncertain, consult version-matched official documentation when external research is permitted. Do not guess or silently upgrade dependencies.

### Components and packages

- Do not assume `components/ui`, shadcn/ui, or a specific shadcn style is present. Use existing components when available; add missing ones only when needed and authorized.
- If choosing shadcn/ui for a new project without another style direction, `new-york` is a starting option, not an instruction to overwrite an established theme.
- Use the repository's package manager and lockfile; otherwise default to pnpm. Install necessary new dependencies before adding imports, batching related installations where appropriate.
- If installation or execution is unavailable, report the limitation. Do not pretend imports were resolved or packages were installed.
- Split meaningful component responsibilities, especially repeated geometry and state variants. Avoid both a monolithic page and needless abstraction for every text node.

### Styling and application behavior

- Use semantic tokens for typography, spacing, colors, radii, and relevant dimensions. Prefer the project's spacing utilities over arbitrary repeated values.
- Use rem/em and flexible tracks for text-oriented geometry. Fixed icon/control dimensions can be intentional; fixed large information-panel heights require a reason.
- Implement tokens using the installed Tailwind/CSS setup rather than assuming a particular configuration generation. Make the root document background agree with the app surface where controllable.
- Use responsive changes where content needs them. Reflow peer columns and actions before they collide; do not simply shrink the whole interface.
- Use semantic HTML, appropriate native controls, accessible names, visible focus, keyboard operation, and properly associated labels/errors. Prefer native semantics over unnecessary ARIA.
- Size interaction targets deliberately: typically 36–44px high for desktop controls and about 44px or larger for touch-oriented controls. These are design defaults, not a claim of accessibility conformance.
- Preserve zoom, readable reflow, and reduced-motion preferences. For inherently two-dimensional content, use deliberate local scrolling rather than accidental page-wide overflow.
- Escape JSX text where syntax requires it. Do not inject untrusted HTML. Keep document titles and metadata appropriate to the application.
- Follow the framework's established data-loading and state-management approach. Prefer its loader/server mechanisms or an existing query library; do not force SWR into every project.
- Do not add a backend, database, authentication system, ORM, or unrelated infrastructure just to perform a visual redesign.
- When real persistence or authentication is in scope, use the actual backend contract and server-enforced authorization. Do not substitute fake authentication or browser storage for production account data.
- Keep session credentials out of localStorage. Preserve applicable safeguards such as secure session cookies, server validation, parameterized queries, and database access policies. Do not implement custom password cryptography.
- Avoid logging whole user objects, credentials, or request bodies. Remove temporary debug instrumentation and development-only UI before delivery.

## 10. Verification and Release Gate

Implement the real information hierarchy and relevant states before polishing decoration. Then inspect, identify specific defects, correct them, and inspect the affected result again.

### Visual inspection

When browser/rendering tools are available:

1. Choose a representative desktop viewport, such as 1440×900, and a narrow viewport, such as 390×844. Add a mid-width or wider workspace view when the layout calls for it. These are test fixtures, not required product dimensions.
2. Inspect the actual rendered page with its fonts loaded. Check at normal scale rather than relying only on a reduced thumbnail. Inspect fallback behavior when fonts are external.
3. Exercise the relevant populated, empty, unavailable, loading, error, and long-content states. Use real data or explicitly isolated test fixtures; do not leak fixtures into production.
4. Compare related controls and panels. Check shared edges, equal intended dimensions, text baselines, icon centering, wrapping, and action alignment.
5. Inspect vertical allocation: does each large region earn its height? Are summaries or empty panels delaying the primary content without benefit?
6. Check keyboard focus, readable zoom/reflow, and overflow. Treat 200% zoom as a useful test condition, not proof of complete accessibility compliance.
7. Read every visible string as the intended user. Review raw-error paths, placeholder text, internal notes, misleading defaults, and role-inappropriate instructions.

When DOM measurements are available, turn intended equalities into checks. Compare the relevant border boxes or shared edges within about 1 CSS pixel of rounding tolerance. Equal size is a check only for components intended to match; optical glyph alignment still needs visual inspection.

When rendering is unavailable, review the layout rules, tokens, responsive behavior, and state branches statically. Explicitly report that visual verification was not performed. Do not claim that the UI is centered, pixel-perfect, or fully responsive based only on code inspection.

### Block release or explicitly report the unresolved defect when

- Essential content is unreadable, clipped, or lost through unintentional overflow.
- Like-for-like peers have unexplained size, inset, baseline, or control-height mismatches.
- Utility panels have large unexplained blank regions or empty states retain unjustified populated-state dimensions.
- Internal details, raw errors, secrets, developer notes, or misleading data appear in ordinary product UI.
- A visible action is broken, invented, or presented as working without its required integration.
- The claimed verification did not happen.

Do not fix these problems by blindly reducing all spacing, enlarging all text, hiding essential information, or adding filler. Correct the underlying relationship: content, state, type role, shared geometry, or audience boundary.

Finish with a brief delivery summary of the substantive changes, checks actually performed, and unresolved limitations. Keep implementation commentary out of the product itself.