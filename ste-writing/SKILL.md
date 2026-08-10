---
name: ste-writing
description: >-
  Use whenever an Agent produces substantial technical prose, even when the
  user does not explicitly request STE. Trigger for architecture and design
  reports, technical documentation, READMEs, runbooks, plans, specifications,
  pull-request descriptions, release notes, error messages, prose comments,
  tool or skill descriptions, system prompts, and complex task instructions
  for other Agents. Also trigger when the user asks to write, rewrite,
  simplify, or review technical prose; remove AI-sounding language; enforce a
  controlled writing style; or apply STE in English, Chinese, or another
  language. Do not trigger when the requested output is primarily executable
  code, identifiers, command syntax, direct quotations, marketing copy,
  creative writing, or text that intentionally requires a distinct voice.
---

# Language-Agnostic STE Technical Writing

Write technical prose that is direct, consistent, and easy to understand or execute.

Apply controlled-language principles in the language that the user requests. Do not translate the output into English only to use this skill.

ASD-STE100 defines a controlled form of English. Only English text can follow its English-specific rules. For Chinese and other languages, apply the transferable principles as an STE-derived technical style.

Do not claim that non-English text complies with ASD-STE100. Do not claim formal ASD-STE100 certification for English text.

## Apply priorities

Apply these priorities in order:

1. Preserve technical correctness and safety.
2. Obey the user's explicit requirements.
3. Preserve all facts, conditions, limits, and scope.
4. Use the requested output language and format.
5. Apply the controlled technical style.

Do not simplify text when simplification changes its meaning.

Do not replace a precise domain term with a common word that has a different meaning.

Preserve normative distinctions such as `MUST`, `SHOULD`, and `MAY`.

## Select the output language

Use these rules:

1. Use the language that the user explicitly requests.
2. When rewriting text, preserve its language unless the user requests a translation.
3. For new text without an explicit language, use the language of the user's request.
4. Preserve identifiers, API names, commands, file paths, and established technical terms.
5. Keep a foreign technical term when its translation would reduce precision.
6. Define a necessary foreign term at its first use when the audience might not know it.
7. Use one language form for each concept after the definition.

Do not alternate between translated and untranslated names for the same concept without a technical reason.

## Select the operation

Use one of these operations.

### Write

Produce new technical prose in the controlled style.

### Rewrite

Convert existing prose into the controlled style.

Preserve every fact, number, condition, qualification, and uncertainty statement.

Change only the text that needs improvement.

### Review

Do not rewrite the complete text unless the user asks for a rewrite.

Report each material violation in a table with these columns:

`Rule | Original | Suggested text`

Translate the column names into the output language.

Use one row for each violation. After the table, identify text that you intentionally left unchanged and give the reason.

If the text already follows the applicable rules, return it unchanged and state that no material violation was found.

## Select the mode

### Strict mode

Use strict mode for:

- Procedures
- Runbooks
- Safety instructions
- Recovery instructions
- Error messages
- Operational checklists
- High-risk change plans
- Complex executable tasks for other Agents

Apply all transferable rules.

For English output, also apply the English-specific limits in this skill.

### Technical mode

Use technical mode for:

- Architecture reports
- Design documents
- Technical analysis
- General documentation
- READMEs
- Specifications
- Implementation plans
- Pull-request descriptions
- Release notes

Keep the vocabulary natural enough for the target language. Apply the rules for accuracy, terminology, sentence structure, active voice, and clear organization.

A document can use both modes. For example, use technical mode for an architecture explanation and strict mode for its deployment procedure.

## Preserve technical meaning

Preserve all of these elements:

- Facts
- Numbers
- Units
- Conditions
- Exceptions
- Limits
- Scope qualifiers
- Uncertainty
- Causal relationships
- Safety wording
- Acceptance criteria
- Required and optional behavior

Do not convert an observation into a conclusion.

Do not convert an assumption into a fact.

Do not convert a possibility into a certainty.

Separate observed facts, inferences, decisions, and recommendations when the distinction matters.

If the source contains an ambiguity, preserve it or identify it. Do not silently choose an interpretation.

## Use consistent terminology

Use one name for one thing.

Do not rotate synonyms only to make the prose appear varied.

For example, do not use `check`, `verify`, `validate`, and `confirm` for the same action. Select one term and reuse it.

Keep different terms when they identify different technical operations.

Use the conventional term that practitioners of the target language use.

Define an abbreviation at its first use when the audience might not know it. Use the abbreviation consistently after the definition.

Give each word or term one meaning within the same document.

## Use direct words

Prefer short, common, and concrete words when they preserve the meaning.

Avoid:

- Marketing adjectives
- Empty intensifiers
- Metaphors
- Idioms
- Fashionable jargon
- Ceremonial introductions
- Unnecessary hedging
- Vague references
- Filler transitions

Do not use words such as these without measurable support:

- Seamless
- Robust
- Powerful
- Effortless
- Cutting-edge
- World-class
- Next-generation
- Revolutionary

Remove empty phrases such as:

- It is important to note that
- It is worth mentioning that
- As everyone knows
- In order to
- With that being said
- At the end of the day

State the information directly.

## Use direct verbs

Use a verb to identify an action.

Write `analyze the log`, not `perform an analysis of the log`.

Write `configure the service`, not `perform the service configuration`.

Use active voice when the actor is known and relevant.

Write `The parser reads the file`, not `The file is read by the parser`.

Permit passive voice when the actor is unknown, irrelevant, or intentionally omitted.

Use imperative verbs for procedures and task instructions.

Use simple tense and aspect when the target language supports that choice.

Avoid stacked auxiliary verbs and modal chains.

Do not hide the responsible actor when the actor affects execution or ownership.

## Control sentences

Give each instruction one main action.

Give each descriptive sentence one main proposition.

Split independent actions into separate sentences.

Put a condition before the action that it controls.

Use punctuation between the condition and the action.

Example:

`If the test fails, read the log.`

Keep related sentences connected with plain logical connectors.

Use connectors such as:

- Then
- But
- Because
- Thus
- As a result

Do not make sentences short by deleting necessary articles, subjects, objects, or qualifiers.

Do not turn a required sentence into a fragment. Labels, headings, changelog entries, and flow-list items can remain short phrases.

## Control sentence length

For strict English:

- Use no more than 20 words in an instruction.
- Use no more than 25 words in a descriptive sentence.

Split a longer sentence when the split preserves its meaning.

Do not delete facts or conditions to meet a length limit.

For languages that do not use spaces to separate words, do not apply an artificial word or character limit. Instead:

- Use one action per instruction.
- Use one proposition per descriptive sentence.
- Split independent clauses.
- Split separate condition-result chains.
- Keep the complete technical meaning.

If a sentence cannot be split safely, keep it and identify the reason during review.

## Control noun groups and modifiers

Avoid long stacks of nouns or modifiers.

For English, use no more than three words in a multi-word noun when practical.

Unpack a longer noun group with a preposition, a relative clause, or a defined term.

For other languages, split long modifier chains when the reader must retain too many qualifiers before reaching the main noun.

Keep established technical names unchanged.

## Organize paragraphs and lists

Use one topic per paragraph.

Use no more than six sentences in a paragraph when practical.

Use a numbered vertical list for a procedure.

Give each numbered step one main action.

Place a condition before the action that it controls.

Use parallel grammatical forms for related list items.

Keep rationale separate from an executable instruction when combining them could cause ambiguity.

Do not expand a short label into a complete sentence only to satisfy a grammar rule.

Use headings that identify the content of their sections.

## Use punctuation deliberately

Prefer a period when two clauses can be separate sentences.

Do not use a semicolon to join independent instructions.

Do not use an em dash as a substitute for clear sentence structure.

Use a colon to introduce a list or an explanation when the target language permits it.

Use parentheses only for secondary information.

Preserve punctuation inside code, commands, identifiers, error strings, and direct quotations.

## Write safety information

Use these labels consistently:

- `WARNING`: Risk of injury
- `CAUTION`: Risk of equipment, system, or data damage
- `NOTE`: Supporting information only

Do not put an instruction inside a `NOTE`.

Put a safety statement directly before the step that it protects.

Start with the condition or required action. Then state the risk.

Do not use a safety label only to add emphasis.

Translate a label when the target language has an established equivalent. Preserve a required regulated label when exact wording is mandatory.

## Write architecture and design reports

State the system boundary.

Identify the current state before the proposed state.

Separate facts from assumptions.

Identify constraints and dependencies.

State each decision directly.

Give the reason for each important decision.

Describe rejected alternatives when they affect the decision.

State tradeoffs without promotional language.

Identify risks, owners, and validation methods when that information is available.

Do not describe a proposal as implemented behavior.

Do not hide uncertainty behind confident language.

## Write documentation and runbooks

Identify the intended audience when it affects the instructions.

State prerequisites before procedures.

Use exact names for commands, files, services, and configuration fields.

Give steps in execution order.

State the expected result of an important step.

State the failure path when the reader needs it.

Keep examples separate from mandatory instructions.

Do not modify executable examples only to make their prose comply with this skill.

## Write plans

State the objective and the completion condition.

Define the included scope.

Define important exclusions.

Identify dependencies and unresolved decisions.

Use numbered actions in execution order.

Assign an owner when ownership matters.

State the validation method for each high-risk result.

Define acceptance criteria that another person or Agent can test.

Separate required work from optional improvements.

Do not use vague actions such as `handle`, `improve`, `look into`, or `take care of` without a measurable result.

## Write complex tasks for other Agents

Use strict mode for complex Agent instructions.

Include all applicable information:

1. The objective
2. The owned files, modules, systems, or responsibility
3. The work that is outside the task
4. Whether the task is read-only or permits changes
5. The relevant context and evidence
6. The required constraints
7. The unresolved decisions that the Agent must not assume
8. The required implementation or analysis
9. The validation commands or checks
10. The exact deliverables
11. The success criteria

Use direct action verbs such as:

- Inspect
- Compare
- Change
- Add
- Remove
- Run
- Verify
- Report

Make each instruction testable.

State file or subsystem ownership when multiple Agents work in parallel.

Prevent overlapping work unless coordination is intentional.

Tell an Agent to preserve unrelated changes when it shares a workspace with other Agents.

State whether the Agent can make external changes, deploy, commit, push, or send messages.

Do not give authority that the user did not grant.

Do not ask an Agent to make an unresolved product decision unless the task explicitly assigns that decision.

Do not hide an important constraint in background text. Put the constraint next to the action that it controls.

## Apply English-specific rules

Apply this section only to English output.

Use American spelling unless the user requests another spelling standard.

Do not use contractions.

Use simple tenses:

- Infinitive
- Imperative
- Simple present
- Simple past
- Simple future

Avoid the present perfect when a simple past form gives the same meaning.

Avoid phrasal verbs when a direct verb is available.

Prefer:

- `start` to `begin`, `commence`, or `initiate`
- `use` to `utilize` or `leverage`
- `help` to `facilitate`
- `do` to `perform` or `conduct`
- `give` or `supply` to `provide`
- `before` to `prior to`
- `after` to `subsequent to`
- `about` to `regarding` or `concerning`
- `get` to `obtain` or `acquire`
- `show` to `demonstrate`
- `also` to `additionally`, `furthermore`, or `moreover`

Use these replacements only when they preserve the technical meaning.

Use an article or demonstrative adjective before a specific countable noun when English grammar requires it.

Do not add an article to a general statement or an abstract concept only to satisfy a mechanical pattern.

A past participle used as an adjective is not necessarily passive voice. For example, `The field is required` can be correct.

In strict English, prefer:

- `but` to `however`
- `because` to `since` when stating a cause
- `must` to `should` or `shall` when the action is mandatory
- `can` for ability
- `may` for permission
- `use` or `with` to an unclear `using` phrase
- `obey` to `follow` when referring to mandatory instructions
- `push` to `press` for a physical control when that term is correct

Do not replace normative keywords when the replacement changes their defined meaning.

## Apply Chinese-specific adaptation

Apply this section only to Chinese output.

Use standard modern technical Chinese.

Use the technical terms that the intended Chinese-speaking audience commonly uses.

Keep the actor explicit when multiple components, services, users, or Agents can perform the action.

Prefer a direct actor-action-object structure when it improves clarity.

Use direct verbs instead of constructions that turn an action into an abstract operation.

Use one sentence for one main action or proposition.

Split a sentence that contains multiple independent actions.

Split multiple condition-result chains into separate sentences.

Put a condition before the action that it controls when execution order matters.

Avoid idioms, literary parallelism, ceremonial wording, and empty meta-introductions.

Do not alternate between an English term and its Chinese translation for the same concept. Define the relationship once, then select one form.

Keep an established English technical term when a forced translation would be uncommon or inaccurate.

Do not copy English article, tense, contraction, or word-count rules into Chinese.

Use Chinese grammar and punctuation naturally.

Do not omit a subject when the omission makes ownership or execution unclear.

Do not add a subject to every sentence when the context already makes the actor unambiguous.

## Adapt to other languages

Apply the universal rules through the grammar of the target language.

Do not mechanically copy English rules about articles, tense, contractions, noun order, or word counts.

Use the target language's standard technical register.

Use an explicit actor when the language normally permits omission but the omission creates ambiguity.

Avoid idiomatic, literary, promotional, or ceremonial wording when direct technical wording is available.

Preserve conventional loanwords and untranslated technical names when they improve precision.

Use native punctuation and sentence boundaries.

Optimize for a competent technical reader of that language, not for literal similarity to English.

## Preserve protected text

Do not change:

- Executable code
- Identifiers
- Commands
- Command options
- File paths
- URLs
- Part numbers
- Units
- Protocol tokens
- Schema names
- API field names
- Required legal wording
- Required safety wording
- Existing error strings when they are quoted as evidence
- Direct quotations

When the user asks you to create or edit an error message, apply this skill to the message. When the user cites an existing error message as evidence, preserve it exactly.

Rewrite only the prose around protected text.

## Guard against information loss

Never remove a fact, number, condition, exception, or scope qualifier to make a sentence shorter.

Never change a narrow statement into a broader claim.

Never remove uncertainty that is present in the source.

Never invent evidence, rationale, ownership, or validation results.

Never make a plan appear complete when required work remains.

When rewriting, change the smallest span that fixes the problem.

If a required technical term is long or uncommon, keep it.

If the source already complies, return it unchanged.

## Verify the result

Before producing the final text, check these items:

1. Does the output use the requested language?
2. Does it preserve every fact, number, condition, and qualifier?
3. Does one name identify each concept?
4. Does each instruction contain one main action?
5. Does each descriptive sentence contain one main proposition?
6. Does each condition clearly control an action or result?
7. Is the responsible actor clear where ownership matters?
8. Did you replace nominalizations with direct verbs where possible?
9. Did you remove filler, hype, idioms, and vague language?
10. Did you split long modifier or noun groups?
11. Did you preserve all code, identifiers, commands, and quotations?
12. Did you preserve normative keywords and technical distinctions?
13. Are procedures ordered and testable?
14. Do plans include scope, validation, and completion criteria?
15. Do complex Agent tasks include ownership, constraints, deliverables, and success criteria?
16. For strict English, do instructions stay within 20 words?
17. For strict English, do descriptive sentences stay within 25 words?
18. For non-English text, did you use native grammar instead of copying English mechanics?

Perform no more than two self-review passes unless the user asks for formal editing.

Do not report a lint score unless a real lint tool produced it.

Do not claim formal compliance based only on this checklist.

## Produce the output

Write only the requested artifact when the user asks for a document, plan, report, prompt, or task description.

Do not add a preamble, summary, or closing statement unless it helps the requested artifact or the user asks for it.

Preserve the requested format.

Use Markdown only when the requested format permits it.

## Scope and attribution

Use this skill to control the form of technical prose. Do not use it to make unsupported content appear authoritative.

This skill cannot make an incorrect statement true.

The strict English guidance derives from ASD-STE100 principles. The complete standard is available at https://asd-ste100.org.

Do not reproduce the complete standard. It is copyrighted.

This skill is unofficial and is not affiliated with the ASD Simplified Technical English Maintenance Group.

ASD-STE100 is a registered trademark.
