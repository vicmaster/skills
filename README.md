# Claude Code Skills

A collection of reusable [skills](https://code.claude.com/docs/en/skills) for Claude Code.

## Task Skills

Invoke these manually with `/skill-name` to perform specific actions.

| Skill | Description |
|-------|-------------|
| `/ship-feature` | Commit changes, mark feature done in VISION.md, push |
| `/fix-build` | Diagnose and fix build failures |
| `/fix-issue` | Fix a GitHub issue end-to-end |
| `/review-code` | Review code for bugs, security, and quality |
| `/pr-summary` | Summarize a pull request with risks and review notes |
| `/deploy` | Deploy the application to an environment |
| `/test-writer` | Write or update tests for changed code |
| `/explain-code` | Explain code with diagrams and analogies |

## Background Skills

Claude loads these automatically when relevant. They silently improve output quality without you having to prompt for it.

| Skill | Triggers when |
|-------|---------------|
| `self-review` | Claude is about to report a task as complete |
| `react-conventions` | Writing or modifying React components |
| `ts-conventions` | Writing or modifying TypeScript code |
| `git-conventions` | Creating commits or branches |
| `security-check` | Handling user input, auth, or external data |
| `minimal-changes` | Implementing any task (prevents over-engineering) |

## Usage

### As personal skills (all projects)

Copy any skill directory to `~/.claude/skills/`:

```bash
cp -r explain-code ~/.claude/skills/
```

### As project skills

Copy into your project's `.claude/skills/` directory:

```bash
cp -r fix-build my-project/.claude/skills/
```

### Import into coide

Use the **Import** button in coide's Skills tab to import any `SKILL.md` file.

## Structure

Each skill follows the [Agent Skills](https://agentskills.io) open standard:

```
skill-name/
└── SKILL.md    # Frontmatter + instructions
```

Every `SKILL.md` includes YAML frontmatter with `name`, `description`, and optional fields like `disable-model-invocation`, `argument-hint`, `context`, and `allowed-tools`.

## Contributing

1. Create a new directory with the skill name
2. Add a `SKILL.md` with proper frontmatter
3. Test the skill in Claude Code
