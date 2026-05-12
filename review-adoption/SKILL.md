---
name: review-adoption
description: Evaluate a link, library, tool, framework, or technical claim for adoption fit. Cross-checks marketing claims against reality, weighs maintenance/maturity, considers fit for the user's stack, and surfaces alternatives. Outputs Adopt / Watch / Skip verdict and saves an eval when adopt/watch.
---

# Review for Adoption

The user is asking whether something is worth adopting — a library, tool, framework, blog post, technique, or vendor pitch. Your job is to give them a grounded verdict, not a summary.

## Stance

- **Skeptical of hype, but not dismissive.** Marketing claims are a starting point, not evidence. Find independent signals.
- **Avoid FOMO.** Popularity and recency are not reasons to adopt. New ≠ better.
- **Don't miss genuinely valuable ideas.** Conversely, dismissing novel approaches because they're unfamiliar is its own failure mode. If something is genuinely novel and the downside of exploring it is low, say so — even when uncertain.
- **The user is an operator who ships.** They don't need a feature survey; they need to know if this earns a place in their workflow or one of their projects.

## First-run personalization

Before doing any evaluation, check whether `~/.claude/skills/review-adoption/my-stack.md` exists.

- **If it doesn't exist**, pause and onboard the user. Ask these four short questions (one at a time, conversational tone):
  1. What are your active projects right now? (1–3 of them, with a one-line "what it is" each — tech stack, what stage)
  2. What's your primary tooling? (e.g., languages, frameworks, IDE/editor, AI tools you've already invested in)
  3. What's your role and what kinds of decisions does this skill need to inform? (e.g., "founder picking infra", "engineer choosing libraries", "tech lead evaluating vendors")
  4. Any hard constraints? (license restrictions, compliance, vendor lock-in tolerance, budget sensitivity)

  Then write the answers to `~/.claude/skills/review-adoption/my-stack.md` with this structure:
  ```
  # My Stack

  ## Active projects
  - **<Name>** — <one-line description, stack, stage>
  - ...

  ## Tooling & investments
  - ...

  ## Role & decision lens
  - ...

  ## Constraints
  - ...

  _Last updated: <YYYY-MM-DD>_
  ```

  Tell the user: "Saved your stack to `~/.claude/skills/review-adoption/my-stack.md` — edit it any time. Now reviewing X..." and proceed.

- **If it exists**, read it. Use it as ground truth for the fit check.

If the user invokes the skill with no argument and `my-stack.md` already exists, ask what they want reviewed. If both are missing, do onboarding first, then ask.

## What to evaluate

Run through these four dimensions. Don't write headings for every section in the final output — synthesize. But cover all four in your research.

### 1. Claims vs reality
- What does the source/site claim? List the load-bearing claims (perf, DX, cost, novelty).
- Are claims backed by benchmarks, demos, third-party reviews, or just assertions?
- Check GitHub issues, HN/Reddit threads, blog posts from people who actually used it (not the vendor).
- Flag anything that smells like marketing puffery ("10x faster", "the future of X") without substance.

### 2. Fit for the user's stack
Cross-reference against `my-stack.md`. Be concrete — name the project where it would slot in, or explain why none fit. If the thing solves a problem the user has explicitly mentioned, say so. If it's a solution looking for a problem in their world, say so.

### 3. Maintenance & maturity
- Last commit, release cadence, open issue count vs closed, # of contributors
- License (MIT/Apache fine; AGPL/SSPL flag for commercial use — and re-check against user's constraints from `my-stack.md`)
- Funding/backing — VC-funded with runway, solo maintainer, big-co OSS, foundation?
- How old is it? Bus factor?
- Any recent security incidents or supply chain events? (Search for these explicitly.)

### 4. Alternatives & lock-in
- What else solves this problem? How does this compare?
- If they adopt and later want out, what's the switching cost? Proprietary formats? Data export?
- Is there a more boring/proven option that does 80% of the job?

## Process

1. **Fetch the primary source.** If a URL was given, WebFetch it. If a library name was given, WebFetch the GitHub repo and the official docs. For GitHub repos, also use `gh repo view <owner>/<name> --json name,description,stargazerCount,forkCount,licenseInfo,createdAt,pushedAt,issues,latestRelease,primaryLanguage,isArchived` to get clean metadata.
2. **Find independent signals.** WebSearch for: `"<thing>" review`, `"<thing>" vs <known alternative>`, `"<thing>" production`, `"<thing>" issues`, `"<thing>" security`, HN/Reddit discussions. Don't just trust the homepage.
3. **Check fit explicitly** against `my-stack.md`. Be concrete.
4. **Synthesize, then verdict.**

## Output format

Keep it tight. The user doesn't want a white paper.

```
**<Name>** — <one-line what-it-is>

**Claims that hold up:** <2-4 bullets, or "none load-bearing">
**Claims that don't:** <bullets, or "no obvious puffery">
**Maturity:** <one line — age, activity, backing, license, any security flags>
**Fit:** <one line tying to a specific project from my-stack.md, or explaining no fit>
**Alternatives:** <1-3, with the boring/proven option called out>

**Verdict: Adopt | Watch | Skip** — <one-line reason>
```

Verdict definitions:
- **Adopt** — worth investing time to integrate now. Real value, fits the stack, switching cost acceptable.
- **Watch** — interesting but not yet. Note conditions that would flip it to Adopt (e.g., "revisit if we need multi-provider", "wait for v1.0", "revisit after Q3 hiring").
- **Skip** — not worth pursuing. Either the claims don't hold up, no fit, or a boring alternative wins.

## Saving the eval

**Only save if verdict is Adopt or Watch.** Skips don't get saved — they're noise.

When saving:
1. Ensure `~/.claude/skills/review-adoption/evals/` exists.
2. Write `~/.claude/skills/review-adoption/evals/eval_<slug>.md` with frontmatter:
   ```
   ---
   name: <thing> evaluation
   description: <one-line summary including verdict>
   verdict: adopt | watch
   date: <YYYY-MM-DD>
   ---
   ```
   Body: mirror the output format above, plus a `**Why:**` line (why the user surfaced it) and `**How to apply:**` line (what triggers revisiting for Watch, or how to start adopting for Adopt).
3. Append a line to `~/.claude/skills/review-adoption/evals/INDEX.md` (create the file with a `# Evals` header if it doesn't exist): `- [<thing>](eval_<slug>.md) — **<verdict>** (<date>): <one-line hook>`.

If an eval for this thing already exists, update it instead of creating a duplicate. Note the previous verdict and date in a `**Previously:**` line if the verdict is changing.

## When the user wants to update their stack

If the user says things like "update my stack", "my stack changed", "I dropped X", or "I'm now working on Y" — re-read `my-stack.md`, ask what changed, write the update, and confirm. Always bump the `_Last updated:_` date.
