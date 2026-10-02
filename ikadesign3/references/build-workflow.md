# Build Workflow

## Objective and Scope

Use `design.md` to build real pages that support the reader tasks. A consistent brand does not require a consistent layout. Different pages can use different structures. But they must share the applicable visual rules and primitives.

Do not create an additional theme system. Do not install components that the current task does not need.

This workflow is the Build mode of the `ikadesign3` skill. [Review and Rule Update](review-loop.md) defines the review record, mechanical checks, issue classes, and stop rule.

## 1. Read design.md and the Task

1. Read the `design.md` that the user specifies.
2. If the user does not specify one, use the existing `design.md` of the project.
3. Check whether `design.md` covers the current page types and themes.
4. List the target readers, main tasks, real content, and necessary actions.
5. Separate user requirements, `design.md` constraints, and the implementation decisions of this task.

The features, fields, and data of a page come from the task requirements and code. They do not come from `design.md`. `design.md` decides only how to present them.

If no `design.md` exists, do not claim that you build from one. Return to Extract or Create in the [skill entry](../SKILL.md).

If `design.md` covers only part of the task, use the confirmed parts. Make minimal implementation decisions for the missing parts. List these decisions in the delivery. If the missing information changes the brand direction, business meaning, or license scope, ask the questions together. Do not return to Create because of a local gap.

Keep the facts, formulas, units, qualifiers, and assets that the user gives. Do not invent customer reviews, statistics, product capabilities, prices, or recommendations.

## 2. Examine the Host Project

Examine the actual framework, routes, style entry points, fonts, themes, component APIs, and start command. Keep the existing structure and unrelated changes.

Select the implementation approach that matches the project and the content of `design.md`:

### The Project Has an Implementation

Reuse the existing tokens, components, layouts, and theme entry points. Read the real props and usage examples of the related components. Do not guess an API from a component name.

### design.md Refers to a Stylesheet

Check that the asset URL is accessible and returns CSS. Load the stylesheet once, as `design.md` specifies. Use the public primitives and the extension namespace from Chapter 5. Do not guess unlisted names. Do not override internal selectors.

If the public primitives are sufficient, you do not have to read the full CSS into the context. If a loading, specificity, theme, or state problem occurs, you can read the related implementation to find the cause.

If network, privacy, or project policy blocks a remote asset, use an approved local copy or an explicit alternative implementation. Record the differences. Do not use broken links or assets without usage rights.

### design.md Contains Only Design Values

Add the necessary tokens and component variants to the existing style entry point of the project. If no entry point exists, select the smallest shared style file.

Separate base values, semantic roles, and component uses. Implement only the rules that the current page needs. Do not copy color, font size, and spacing declarations into each page.

Write the real names and paths of new tokens into `design.md`. If you have no permission to change `design.md`, give specific change proposals in the delivery.

## 3. Decide the Page Structure

List the content and actions first. Then select the layout.

Decide these items internally:

- The page type and its applicable rules.
- The answers, actions, or evidence that the first viewport must show.
- The order and width relations of the main areas.
- The reflow method of the mobile layout.
- The necessary interaction states and data states.

If the content supports clearly different structures, compare two compositions. Select the structure that best supports the reader tasks. You do not have to make alternatives for an explicit existing layout.

Do not change every task into a centered title with a card grid. Do not apply the Vercel brand choices as general requirements. These choices include black and white color, the Vercel fonts, no gradients, and a hidden theme switch.

Do not show design reasoning, rule numbers, or review records in the user interface.

## 4. Implement the Page

Implement in this order:

1. Semantic structure and content order.
2. Shared layout and responsive behavior.
3. Real components and their variants.
4. Fonts, colors, spacing, and media.
5. Necessary interactions, states, and accessibility.

Use the public primitives of `design.md`. A new layout can combine primitives. But page-level overrides must not silently change their meaning.

If a layout method is missing, add minimal page layout styles in the extension namespace that `design.md` declares. If a reuse mechanism is missing, extend the component or style entry point that owns the rule. Do not create a parallel naming system.

If the task requires a backend or real data, connect the actual behavior. A visual example can use fixed sample data. In that case, state in the task scope that the data is sample data. Do not claim that inactive buttons, false success states, or static demos are complete features.

Use native semantics, visible focus, accessible names, and sufficient contrast. Do not hide overflow to conceal layout errors.

## 5. Run and Review

Start the real page with the existing project command. Open the target route with the existing browser or preview tool.

Keep the content, viewport, theme, and `design.md` version constant for this review. Review the desktop layout first. Then review the narrow layout. If the project has breakpoints, use them. Otherwise, you can use 1440 × 900 and 390 × 844 as initial review viewports. These viewports are not design rules.

First, do the mechanical checks in [Review and Rule Update](review-loop.md). Then review the first viewport and the full page in its manual review order. As necessary, review the supported themes, long text, large numbers, loading, empty, error, and disabled states, and keyboard operation. Create only the states that apply to the page.

Use screenshots to review appearance. Use the DOM, computed styles, and real interactions to review structure and behavior. Model self-assessment can only help the review. It cannot replace rendering. It also cannot represent user approval.

If you cannot run the page or use a browser tool, do the code and reference review that you can run. Report "no rendered review" or "interactions not reviewed". Do not call a code review a visual pass.

## 6. Fix and Update Rules

Record each finding with the issue classes in [Review and Rule Update](review-loop.md). Use its stop rule to decide the fix scope and the recheck method.

Fix the current page first. Then write the reusable missing rules into `design.md`. A page fix does not replace a rule update. A rule update does not replace a page fix.

Keep user feedback separate from model suggestions. If a directional change needs a user choice, propose it. Do not claim that the user approved it.

Write the review record in the existing task record, in the format of [Review and Rule Update](review-loop.md). If you changed a `design.md` that has a `version` field, update that field. Do not keep conflicting copies of values in documents and code.

## Completion Criteria and Delivery

- You implemented the requested content and behavior.
- Each component, token, and asset that the page uses resolves.
- You fixed the violations in the scope of the stop rule.
- You wrote the reusable missing rules into `design.md`, or you gave explicit change proposals that the user did not approve yet.
- The review record matches the checks that you actually did.

Deliver the page path, the start or access method, the `design.md` changes, and the review limits. Report a successful run only after an actual run. If tools or permissions block more review, state the blocker and the completed work. In that case, do not claim that the review cycle is complete.
