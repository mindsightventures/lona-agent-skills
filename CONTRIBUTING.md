# Contributing to Lona Agent Skills

Thank you for your interest in contributing to Lona Agent Skills! This guide will help you get started.

## How to Contribute

### Reporting Issues

- Use [GitHub Issues](https://github.com/mindsightventures/lona-agent-skills/issues) to report bugs or suggest improvements.
- Include a clear description of the problem or suggestion.
- For skill-related issues, mention which skill is affected (trading-strategy, market-data, or backtest-analysis).

### Submitting Pull Requests

1. **Fork** the repository.
2. **Create a branch** from `main` for your changes (`git checkout -b feature/my-improvement`).
3. **Make your changes** following the conventions below.
4. **Test** your changes by loading the skills in Claude Code or Claude Cowork.
5. **Submit a pull request** with a clear description of what you changed and why.

### Adding a New Skill

To add a new skill to this repository:

1. Create a new directory at the root level with a descriptive name (e.g., `portfolio-optimization/`).
2. Add a `SKILL.md` file inside the directory with the following structure:
   ```markdown
   ---
   name: lona-your-skill-name
   description: A clear one-sentence description of when this skill should be activated.
   ---

   # Skill Title

   Explanation of the skill's purpose and available tools.

   ## Available Tools
   - List all MCP tools this skill uses

   ## Workflows
   - Describe step-by-step workflows

   ## Examples
   - Include practical examples

   ## Tips
   - Add usage tips and gotchas
   ```
3. Update the skills table in `README.md`.
4. Add an entry to `CHANGELOG.md`.

### Adding a New Command

1. Create a new `.md` file in the `commands/` directory.
2. Use the frontmatter format with `name` and `description` fields.
3. Include clear steps and user prompts.
4. Update the commands table in `README.md`.

## Conventions

- **Skill names** use the `lona-` prefix (e.g., `lona-trading-strategy`).
- **SKILL.md files** must include YAML frontmatter with `name` and `description`.
- **Command files** must include YAML frontmatter with `name` and `description`.
- **Tool references** use backtick-wrapped names (e.g., `lona_list_strategies`).
- **Markdown** should be clean, well-structured, and free of unnecessary formatting.

## Code of Conduct

This project follows the [Contributor Covenant Code of Conduct](./CODE_OF_CONDUCT.md). By participating, you agree to uphold this code.

## Questions?

If you have questions about contributing, open a [Discussion](https://github.com/mindsightventures/lona-agent-skills/discussions) or reach out at [lona.agency](https://www.lona.agency).
