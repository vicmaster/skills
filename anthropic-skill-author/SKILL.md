---
name: anthropic-skill-author
description: Create concise, reusable Anthropic-compatible skills centered on a valid SKILL.md file for Claude Code, the Claude API, or cross-platform agent workflows. Use when asked to turn a user request into a discoverable skill with proper naming, frontmatter, and practical execution instructions.
---

1. Purpose

Create an Anthropic-compatible skill that converts a user's request into a clean, reusable `SKILL.md` file for Claude Code, the Claude API, or a cross-platform agent setup.

2. When to Use

Use this skill when:
- The user wants a new skill for Claude Code, the Claude API, or another Anthropic-compatible agent workflow.
- The user asks for a reusable agent instruction set, playbook, or capability packaged as a skill.
- The output should follow Anthropic-style skill conventions with YAML frontmatter and concise numbered sections.

Do not use this skill when:
- The user only wants a one-off answer, not a reusable skill.
- The user wants general prompt writing that is not meant to be packaged as a `SKILL.md`.

3. Inputs

Collect or infer:
1. The user's goal
2. The target platform:
   - Claude Code
   - Claude API
   - Cross-platform Anthropic-compatible skill
3. Key workflow steps the agent should perform
4. Constraints, guardrails, or quality requirements
5. Expected output or deliverable
6. Whether supporting files would materially improve execution

4. Assumptions

If the request is incomplete:
1. Infer the most likely platform from the wording
2. Default to a cross-platform skill if the skill is not clearly tied to Claude Code or the API
3. Keep the skill minimal and reusable
4. State only the most important assumptions in a short section if they affect behavior

5. Steps

1. Identify the skill objective
   - Summarize what the skill should help Claude do
   - Determine whether it is for Claude Code, the API, or both

2. Define the scope
   - Include only the instructions needed to execute the task well
   - Remove anything that is purely explanatory, repetitive, or too generic

3. Create valid YAML frontmatter
   - Include:
     - `name`
     - `description`
   - Ensure `name`:
     - uses only lowercase letters, numbers, and hyphens
     - is specific to the task
     - is not vague or generic
     - does not use reserved terms such as `anthropic` or `claude`
   - Ensure `description`:
     - clearly explains what the skill does
     - states when it should be used
     - is concrete and discoverable

4. Write the body of `SKILL.md`
   - Use a clean numbered structure
   - Include only sections that improve execution, such as:
     1. Purpose
     2. When to Use
     3. Inputs
     4. Steps
     5. Constraints / Guardrails
     6. Output Format
     7. Supporting Files
   - Skip sections that do not add practical value

5. Tailor the skill to the request
   - Reflect the user's context, workflow, and deliverable type
   - Prefer reusable guidance over overly narrow task details
   - Avoid turning the skill into a generic template unless the request itself is broad

6. Add constraints only when useful
   - Include rules that prevent likely failure modes
   - Keep guardrails concrete, brief, and action-oriented

7. Define the output format
   - State exactly what the agent should produce
   - Specify structure, formatting, and completeness expectations only where needed

8. Suggest supporting files only if they add clear value
   - Examples:
     - examples
     - templates
     - schemas
     - checklists
   - Do not suggest extra files for simple skills that work well with `SKILL.md` alone

9. Validate before finalizing
   - Check that the skill:
     - matches the user's intent
     - has valid and specific frontmatter
     - is concise and discoverable
     - avoids vague wording and redundant sections
     - can be used directly by an AI agent without extra explanation

6. Constraints / Guardrails

1. Always center the skill on `SKILL.md`
2. Keep the skill concise and execution-focused
3. Do not include unnecessary background, rationale, or teaching text
4. Do not use placeholder-heavy instructions unless the user asked for a template
5. Do not produce invalid frontmatter
6. Do not use a generic skill name like `assistant-skill`, `general-helper`, or `tool-use`
7. Do not include supporting files unless they materially improve outcomes
8. If assumptions are necessary, keep them short and explicit

7. Output Format

Return:
1. A complete `SKILL.md` in a copy-paste-ready Markdown code block
2. Optionally, a short second section with suggested supporting files or folder structure if those would genuinely help

The `SKILL.md` should:
1. Start with valid YAML frontmatter
2. Use concise numbered sections
3. Be immediately usable by an Anthropic-compatible agent system

8. Quality Standard

A strong result is:
1. Specific enough for Claude to apply reliably
2. General enough to reuse for similar requests
3. Short enough to scan quickly
4. Structured enough to be discoverable and maintainable
5. Free of vague filler, duplicate guidance, or unnecessary sections
