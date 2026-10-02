# design.md Contract

`design.md` enters the model context when a model generates pages. Keep only the content that generation needs: rules, primitives, anti-patterns, and integration. Keep review records, measurement records, and discussions in the task record or the review directory.

Do not store secrets, private data, or assets without distribution rights in `design.md`.

## Content Boundary

`design.md` specifies how to present content. It does not specify which content the product contains. Product content comes from task requirements, product documents, and code. When you generate pages, read product content from these sources. Do not repeat it in `design.md`.

Put these items in `design.md`:

- Typography, color, spacing, grids, surfaces, icons, charts, and motion.
- The composition of each page type.
- The presentation and display format of each content type.
- The markers for content freshness, source, and demo status.
- The appearance, variants, and visual feedback of components.
- The tone of the copy.
- Style entry points, font loading, and theme switching.

Do not put these items in `design.md`:

- The page list, features, actions, flows, and supported languages of the product.
- The fields, columns, filters, and options of a page, table, or form.
- Business rules and product facts, for example billing methods, status thresholds, refresh rates, currencies, and product data volume.
- Data interfaces, state management, routes, URL parameters, algorithms, and mock data.
- Application entry points, internationalization setup, and build and deployment configuration.
- Business domain terms.

### Decision Method

Rewrite each candidate rule in terms of page types and content types. If the rewritten rule is still valid, write the rewritten rule. If you must name a specific page, business object, or field to state it, the content is a product requirement. Do not put it in `design.md`.

If only part of a rule is outside the boundary, remove that part. Keep the remaining part.

Write the result that the user sees. Do not write the implementation mechanism. For example, write "If a save fails, the interface shows the state from before the action." Do not write "Roll back the optimistic update."

Name page types by layout structure, for example dashboard, long list, master-detail editor, and multi-step form. Pages of one type share the layout of the first viewport, primary content, secondary content, and end position. Do not name page types by product feature, for example "top-up page" or "log page".

Name content types by data shape, for example amount, ratio, duration, count, status, time series, identifier, and long text. The product decides which content type each business field uses. The symbol position, thousands separator, and decimal places of an amount are display format.

One content type can have multiple format variants, for example the percentage form and the multiplier form of a ratio. Name variants by form, not by business field.

You can select a presentation by content volume. For example: "Use virtual scrolling for lists with more than 100 rows." Do not write the actual data volume of the product.

A domain component can be a primitive. Its primitive entry records its appearance, variants, real prop names, and usage conditions. Do not write which business data pages pass to the component.

Chart scale types, axis ranges, and reference lines are chart encoding. You can write them. If a visual rule depends on a business status, write only the mapping from status to visual. Task requirements or code define the status conditions and thresholds. If a reference line or color band shows a status threshold, write only its style. Task requirements or code also define its value.

## Length

The target length of `design.md` is no more than 400 lines. If it is longer, first remove content outside the content boundary. Then merge duplicate rules. Then remove rules without an implementation basis. Write each rule in one chapter only.

## File Header

Use YAML frontmatter:

```yaml
---
name: <brand>-design
description: <The product interfaces, page types, readers, and brand goals that this file applies to>
version: <Optional. A commit hash or a date.>
---
```

The `description` must state the trigger scope. Do not write vague text such as "Create beautiful web pages". Do not list pages or features.

`version` is optional. If a repository exists, use the commit hash. If no repository exists, use the date. Do not maintain semantic version numbers manually.

## Required Chapters

### 1. Scope and Priority

State the product interfaces, page types, components, and themes that `design.md` applies to. State the product interfaces that it does not apply to, for example marketing pages or documentation sites. List the priority order for conflicts. The usual order of protection is: facts and user requirements, accessibility and usability, reader tasks, project conventions, brand expression, and decorative details.

### 2. Brand and Readers

State the brand expression, the reader traits, and the tone of the copy. Write only reader traits that affect visual decisions, for example reading density, devices, and expertise. Do not write the business tasks of the readers.

Follow each abstract word with an observable behavior. The behavior must be visual or interactive. Do not write feature or data requirements. Do not write only "modern", "premium", or "simple".

### 3. Page Structure and Composition

Specify the composition of each page type. For each type, specify the layout of the first viewport, primary content, secondary content, and end position. For the definition of page types, read "Content Boundary".

Do not list product pages. Do not write what a specific page contains. Do not make all pages share one template, unless evidence or requirements explicitly ask for it.

### 4. Visual Rules

Specify each of these areas:

- Fonts, type roles, font weights, line heights, and number styling.
- Color semantics, themes, and contrast.
- Containers, grids, spacing, alignment, and responsive behavior.
- Borders, corner radii, shadows, and surface hierarchy.
- Images, icons, charts, and data display.
- Control appearance, and the visual feedback for hover, focus, loading, empty, error, and disabled states.
- Motion and reduced-motion settings.

Write each rule as "object + behavior + condition". For example: "A table fills its content area in desktop viewports. If the content is too wide, the table first uses horizontal scrolling inside its own area. The body text keeps its size."

### 5. Available Primitives

List the tokens, components, layout classes, chart methods, and visual assets that pages can use. For each item, state the name, purpose, scope, and prohibited uses. If the project has real style and component APIs, refer to them. Give primitives without a code implementation the status "to be implemented".

Do not list hooks that read or write product data, API clients, business functions, or routes. Theme and interface preference entry points are part of theme switching. You can list them.

This chapter must declare the extension boundary. The brand decides how open the boundary is. But the chapter must state these three items:

- Which names are public primitives. Pages use only the listed names. Pages do not guess unlisted names.
- Which namespace page-specific styles use, for example `<brand>-custom-*`. If there is no limit, write "no limit".
- Whether page-specific styles can change the layout, typography, borders, and surfaces of published primitives. If they can, state the conditions.

### 6. Copy and Number Formats

Specify how to write titles, buttons, help text, and error messages. Specify the display format of units, precision, time ranges, sources, and uncertainty. Do not specify which data a page shows. Do not specify business calculation methods. Do not invent facts, capabilities, data, sources, or conclusions.

### 7. Anti-Patterns

List the patterns that you observed, that the brand explicitly prohibits, or that the brand clearly does not need. Write each item as a recognizable behavior. For example: "Do not use pill labels for ordinary metadata." Do not use "looks cheap" as a check item.

For Extract and Create, start from these brand-neutral generator habits. Tag all of them `[SHOULD]`:

- A centered hero with a card grid as the default page structure.
- Cards inside cards.
- Decorative icon tiles or colored icon backgrounds.
- Font sizes, font weights, or color literals outside the primitives.
- Small low-contrast text for primary information.
- Pill labels for ordinary metadata.

If samples or requirements conflict with an item, remove the item or change it into a scoped condition. If the same item occurs again in the review records of different tasks, recommend a change to `[MUST]`. Make the change after the user confirms it.

### 8. Implementation and Integration

State the style entry points, font loading, theme switching, and component sources. Do not write application entry points, data layers, routes, internationalization, or build configuration. Do not record review results in this chapter.

## Rule Tags

Tag each rule with one of these tags:

- `[MUST]`: A user, platform, security, accessibility, or confirmed brand constraint.
- `[SHOULD]`: A default behavior that repeated observations or explicit design decisions support.
- `[UNCONFIRMED]`: A reasonable inference without sufficient evidence.

Map evidence states to rule tags:

| Evidence state | Rule tag |
|---|---|
| Requirement | `[MUST]` |
| Observation | `[SHOULD]` |
| Inference | `[UNCONFIRMED]` |
| Decision | `[SHOULD]`, with the note "Decision" |

Give a source only for `[UNCONFIRMED]` rules and rules with the "Decision" note. A source can be a project path, a page URL, a user requirement, or a one-sentence basis. Do not give sources for other rules.

Do not change an `[UNCONFIRMED]` rule into a fact only to complete the document. If the item affects the current implementation, keep the basis of the inference. Then give a temporary implementation choice with the "Decision" note. If the item does not affect the current implementation, move it to the open items.

## Glossary

Make a table of concepts and names for the design concepts and primitives in `design.md`. Include domain components as primitives. Do not include other business domain terms. Use one name for each concept. Keep the real token names, component names, class names, and prop names from the code. Do not create translated names, aliases, or new abbreviations for the same object.

## Rule Quality

A rule is acceptable if a reader can use it to make an implementation choice. A rule is also acceptable if a reader can use it to decide whether an implementation breaks it.

These rules are not acceptable:

- "Keep a premium feel."
- "Use appropriate white space."
- "Make the colors harmonious."
- "Make the components consistent."

Change them into rules with an object, relation, condition, or scope. If you cannot change a rule this way, remove it.

## Implementation Binding Format

Use this table in the "Available Primitives" chapter. Fill it with the actual project values. Do not keep placeholders.

| Role | Implementation name or value | Source or path | Usage condition | Status |
|---|---|---|---|---|
| Body text | A real token, or an exact font size, line height, and weight | Style entry point | Regular reading text | Implemented or to be implemented |
| Primary action | A real component and its variant prop | Component path | The primary action of the current task | Implemented or to be implemented |
| Page container | A real layout component, or width and margin rules | Layout path | The matching page type and breakpoint | Implemented or to be implemented |

Give each color as a usable color value or an existing token. Give font sizes, spacing, and layout as usable values or real component bindings. Text such as "use the brand blue" or "keep a wide container" does not satisfy this contract.

If you use breakpoints, give exact thresholds and the reflow behavior. If you have only screenshots, do not record a screenshot width as a confirmed breakpoint. You can give an implementation decision and record its basis.

If code exists, the code is the source of truth for values. Refer to names and paths in `design.md`. Do not copy values that then need synchronization. If no implementation exists, the values in `design.md` are the implementation basis. After implementation, update the binding paths. Then remove obsolete proposals.

Give a minimal usage example for each primitive that needs exact nesting or props. Each example must match the real API. Use literal values in place of copy and data sources. Do not mark an unchecked example as runnable.

A written `design.md` and a page that passed review are two different states. Record the review status in the review record. For its format, read [Review and Rule Update](review-loop.md).
