# Improvement Suggestions for Cover letter agent A

## Overall assessment

The current agent document has a workable intent, but it is still partly in template form and leaves too much room for interpretation. The biggest risks are:

1. vague metadata that makes the agent hard to discover and invoke correctly
2. a broken source-file reference
3. contradictory fallback rules
4. an output contract that is not strict enough for reliable table-filling

## Priority improvements

### 1. Replace the placeholder frontmatter

The current frontmatter still says:

- description: Describe what this custom agent does and when to use it.
- argument-hint: The inputs this agent expects, e.g., "a task to implement" or "a question to answer".

This should be replaced with metadata that makes the agent immediately usable.

Suggested direction:

- name: Cover letter agent A
- description: Fill Column B of a cover-letter planning table using the job description, the template instructions in Column C, and the candidate profile in the skill list document.
- argument-hint: Provide a job description and the cover-letter planning template to complete.

### 2. Fix the skill-list file reference

The document instructs the agent to read complete_skill_list.md, but the workspace currently contains complete_skill_list_26032026.md.

This matters because the agent may fail or hallucinate the source if the filename does not exist.

Recommended fix:

- either reference complete_skill_list_26032026.md directly
- or instruct the agent to locate the latest file matching complete_skill_list*.md before answering

The second option is more robust if you expect dated versions in the future.

### 3. Make the output contract explicit

Right now the agent says to fill Column B and generate Output.md, but it does not clearly define what must stay unchanged.

Recommended clarification:

- preserve the table structure exactly
- only write to Column B
- do not rewrite Column A or Column C
- keep unanswered cells blank unless the instructions explicitly say otherwise
- do not convert the table into prose

This reduces the chance that the agent will produce a narrative answer instead of an editable planning table.

### 4. Remove contradictory fallback behavior

The document currently contains both of these ideas:

- if information cannot be found, leave Column B blank
- if no satisfactory answer is found, write "AI cannot answer this because I have skill issue [Crying emoji]"

These rules conflict.

For a professional drafting workflow, the second rule should be removed. It lowers output quality and creates noisy content inside the table.

Recommended fallback policy:

- if a field cannot be answered confidently from the JD, the source file, or web search, leave Column B blank

If you want visibility into gaps, use a neutral marker such as Needs manual input, but only if that fits your workflow.

### 5. Tighten the decision rules for Column C

The keyword system is a good idea, but it would be more reliable if expressed as a strict policy rather than loose explanation.

Suggested rule set:

| Column C instruction | Required behavior |
| --- | --- |
| Infer from JD | Use only the job description |
| Refer to source | Use only the skill-list document |
| Google search | Use web search only when the answer is not already available in the provided files |
| Leave blank | Leave Column B empty if the required evidence is missing |
| Emotion-type question | Write a grounded answer based only on the candidate profile and personal-summary content in the skill-list document |

Also add one rule above the table:

- Never invent employers, achievements, metrics, tools, dates, or personal preferences that are not supported by the JD or the source document.

### 6. Define answer quality standards

The document tells the agent to answer "as if you were the job seeker," which is useful stylistically, but it also creates a risk of fabricated details.

Add explicit quality constraints such as:

- prefer evidence-backed claims
- quantify outcomes only when the source document provides them
- do not state years of experience unless the source supports them
- keep tone professional and natural, not exaggerated
- tailor answers to the JD, but do not invent domain experience

### 7. Clarify selection behavior for partial completion

The agent currently says it does not need to answer every question and should choose only a couple of relevant ones. That may be valid for some cover-letter sections, but it is ambiguous when the output is a table.

Recommended clarification:

- fill all factual cells that can be answered confidently
- for open-ended persuasive sections, prioritize the strongest and most relevant points instead of forcing weak content

This keeps the table complete where possible while preserving quality in narrative sections.

### 8. Reduce prompt bulk and move examples out of the agent file

The long embedded example JD and template increase noise without adding much operational value once the rules are clear.

Recommended structure:

- keep the agent file focused on behavior, inputs, and output rules
- move large examples into a separate reference document if you still want them available

This will make the agent easier to maintain and easier for the model to follow.

### 9. Clean up wording and typos

There are several language issues that reduce clarity, for example:

- describtion
- independtly
- oppourtunity
- skillsets and experience possessed by the job seeker

These are minor individually, but they add friction. Tighter wording will make the instructions easier for the model to parse.

### 10. Consider narrowing tool access

If you want this agent to be more predictable, you can limit it to the tools it actually needs.

Likely enough for this workflow:

- read
- search
- web
- edit

You probably do not need broad execution capability for a document-filling agent.

## Suggested structure for a revised version

If you revise the agent later, a cleaner structure would be:

1. Purpose
2. Inputs
3. Source priority order
4. Column C decision rules
5. Output rules
6. Quality constraints
7. Failure behavior

## Suggested rewrite skeleton

You do not need to use this verbatim, but this is the level of specificity the file should aim for.

---
name: Cover letter agent A
description: Fill Column B of a cover-letter planning table using the job description, Column C instructions, and the candidate skill profile.
argument-hint: Provide a job description and a markdown cover-letter template with Columns A, B, and C.
---

Purpose:

Complete Column B of the provided cover-letter planning table.

Inputs:

- a job description
- a markdown template containing Columns A, B, and C
- the candidate profile document, preferably the latest file matching complete_skill_list*.md

Source priority:

1. the job description
2. the skill-list document
3. web search, only when Column C explicitly requires it or the answer is missing from the provided files

Rules:

- preserve the table structure
- only fill Column B
- do not rewrite Column A or Column C
- do not invent facts
- leave cells blank when the answer cannot be supported confidently
- for persuasive sections, choose the strongest relevant evidence instead of filling every possible talking point

Column C policy:

- Infer from JD: answer only from the job description
- Refer to source: answer only from the skill-list document
- Google search: use web search if needed
- Leave blank: leave the cell empty if evidence is insufficient
- Emotion-type question: write a grounded answer based on the candidate profile and personal-summary content

Output:

Return the completed table as markdown in Output.md, with only Column B updated.

## Final recommendation

If you only make three changes, make these:

1. replace the placeholder metadata
2. fix the skill-list filename logic
3. remove the conflicting fallback instruction and enforce one clear output policy

Those three changes alone will make the agent materially more reliable.