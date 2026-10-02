# Review and Rule Update

Use the existing preview tools, browsers, screenshot tools, or project commands. The goal is to make the rules in `design.md` produce visible results on real pages.

This file is the only definition of the review record format, stop rule, mechanical checks, and issue classes. Other files refer to this file. They do not repeat these definitions.

## Review Record

Record these fields for each review. Write the record in the task record, a temporary Markdown file, or the review directory. Do not write it in `design.md`.

```md
Scenario: <page name>
Input: <fixed data, content, and assets>
Viewport: <width × height>
Theme: <light / dark / not supported>
design.md version: <commit hash or date>
Generation context: <new context / current context that saw the source material>
Review method: <browser, screenshots, existing command, or manual review>
Result: <pass / fail / not done>
Violations:
- <a fact that breaks a [MUST] rule or a universal invariant>
Deviations:
- <a fact that differs from a [SHOULD] rule, and whether the difference is intentional>
Open questions:
- <a finding that maps to no rule>
Limits:
- <the scope that you did not review>
```

Do not write "verified" without the review method. Do not use screenshot differences to judge brand quality automatically.

## One Review Cycle

1. Select one representative page and a fixed input.
2. Generate or review the page with the current `design.md`.
3. Do the mechanical checks.
4. Review the first viewport at desktop and narrow widths in the manual review order. If the page has themes, review each supported theme.
5. Record each finding with an issue class.
6. Fix the implementation errors.
7. Write the transferable missing rules into `design.md`.
8. Recheck once with the same input.
9. Record the recheck result. Then stop.

### Stop Rule

In one review cycle, fix only two kinds of findings. The first kind breaks a `[MUST]` rule or a universal invariant. The second kind blocks the main reader task. Record other findings as deviations or open questions. Do not fix them. Do not iterate.

During the recheck, keep the first output from before the change. Do not present the best attempt as the first result. If a rule affects other page types, recheck one affected existing page. Do not generate a full page set only to increase the count.

Stop after one recheck. Do not do a second round unless the user asks for it. Do not claim that generation is stable.

If no rendering environment is available, do the document and code review. Mark the visual result "not done". Do not use the existence of code as visual evidence.

## Mechanical Checks

Mechanical checks use the DOM, computed styles, or artifact text. They do not use visual impressions.

### Universal Invariants

These items do not involve design choices. If a page breaks one, record a violation:

1. The page has exactly one `h1`.
2. `document.scrollWidth` is not more than the viewport width.
3. The `th` and `td` cells of one column use the same text alignment.
4. Each class, token, font, and asset that the page refers to resolves to an implementation.
5. Each focusable element shows a visible style when it has focus.

### Checks from design.md

Make checks from the `[MUST]` rules in `design.md`. Change a rule into a check if it meets both of these conditions:

- You can locate the object in the DOM or in the artifact text.
- You can evaluate the condition as true or false.

For example, "Pages use only the tokens in Chapter 5" can become a check. "Tables express a sense of evidence" cannot become a check.

Do not make checks from `[SHOULD]` or `[UNCONFIRMED]` rules. Each brand has its own check list. This file does not supply a default list.

### Result Levels

- **Violation**: The page breaks a `[MUST]` rule or a universal invariant. You must fix it.
- **Deviation**: The page differs from a `[SHOULD]` rule. Decide whether the difference is intentional. If it is intentional, write a one-sentence reason. The item then passes. If it is not intentional, fix it.

The checks do not make design decisions.

## Manual Review Order

### Reader Tasks

- Does the first viewport show the reader task that the page serves?
- Do the main answers, actions, or evidence come before secondary information?
- Does the page state the same conclusion more than once?

### Structure

- Does the page type match the content density?
- Do the main edges, titles, content areas, and action areas align to one grid?
- Are there empty columns, empty cards, or large empty areas without a task reason?

### Visuals

- Do elements of the same kind use the same type role, spacing, size, and states?
- Does each color express a clear meaning?
- Do tables, charts, and numbers keep their units, ranges, precision, and comparison baselines?
- Do components use the primitives that `design.md` lists?

### Responsive Behavior and States

- Does the narrow layout reflow instead of compressing the content until it is unreadable?
- Did you review long text, large numbers, and the empty, error, loading, and disabled states?
- Is there horizontal overflow, a hidden focus indicator, or an inaccessible action?

### Copy and Security

- Is each visible text useful to the reader?
- Does the page expose paths, internal fields, exceptions, secrets, debug text, or implementation details?
- Does the page state inferences as facts?

## Issue Classes

Give each issue one primary class:

- **Implementation error**: The rule is clear, but the page does not obey it. Fix the page.
- **Requirement issue**: The features, fields, data, or business behavior of the page do not match the task requirements. Fix the page to match the task requirements. Do not write the issue into `design.md`.
- **Missing rule**: `design.md` does not cover a decision, and evidence shows that the decision is a system pattern. In an Extract review, the source page is the evidence. In other reviews, the same issue must occur in multiple scenarios. Add the rule to `design.md`.
- **Missing primitive**: The rule is clear, but the existing tokens, components, or assets cannot express it. Record a minimal implementation proposal. Do not invent a parallel system.
- **Environment issue**: The preview, data, fonts, or tools fail. Fix the environment, or record the check as not done.
- **One-off model error**: The issue occurs only once, and the rule is clear. Do not change `design.md`.

## Rule Update Format

Before you add a rule, answer these questions:

1. Which page, input, and check showed the problem?
2. Is it a judgment problem, a mechanical style problem, or an environment problem?
3. Is the rule inside the "Content Boundary" of the [design.md Contract](design-contract.md)? If it is not, classify it as a requirement issue. Do not add it to `design.md`.
4. Which page types does the rule apply to? Which page types does it not apply to?
5. Can you check the change with the same scenario?
6. Does the rule conflict with existing rules?

Write the answers in the review record. Do not write them in `design.md`.

Acceptable rule update:

```md
[SHOULD] An evidence table fills the available width of the desktop content area. If the columns are wider than the content area, the table scrolls horizontally inside its own area. The body text keeps its size.
Applies to: evidence tables, comparison tables.
Does not apply to: short two-column forms.
```

Unacceptable rule update:

```md
Make the table more comfortable.
```

After you change a rule, recheck the original scenario once. If you did not recheck it, report only "Rule changed, not rechecked".
