# Claude Code Skills

A collection of reusable [skills](https://code.claude.com/docs/en/skills) for Claude Code.

## Skills

| Skill | Description | Auto-trigger |
|-------|-------------|:------------:|
| `/ship-feature` | Commit changes, mark feature done in VISION.md, push | Manual |
| `/fix-build` | Diagnose and fix build failures | Manual |
| `/fix-issue` | Fix a GitHub issue end-to-end | Manual |
| `/review-code` | Review code for bugs, security, and quality | Manual |
| `/pr-summary` | Summarize a pull request with risks and review notes | Manual |
| `/deploy` | Deploy the application to an environment | Manual |
| `/explain-code` | Explain code with diagrams and analogies | Auto |

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
