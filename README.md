# Analytics Team Workflows
Contains workflows, prompts, and automations for the Analytics Team to use across projects.  

## Cursor Rules
The `.cursor/` directory contains rules for directing Cursor when using an LLM to generate models or documentation. The current rules are:
- **dbt-documentation-standards**: Contains general standards for documenting a dbt model, including table-level and column-level requirements.
- **dbt-overview-standards**: Contains guidance on maintaining the `__overview__.md` for a dbt project, including keeping the list of quicklinks up to date and adding a set of XML tags for LLM use.
- **general-coding-standards**: Contains general coding standards for dbt models, including naming conventions, documentation requirements, and code structure.
- **review-dbt-documentation**: A process-based rule for use in reviewing and updating out of date model documentation. Specifically geared towards modernizing a project's documentation for the AI platform.

## Claude Subagents
Claude subagents are extremely useful for automating tasks and workflows when the process can be easily defined and described. Read more [here](https://docs.anthropic.com/en/docs/claude-code/sub-agents). The defined subagents, at the moment, are:
- **dbt-job-failure-investigator**: This subagent is designed to identify the cause of and suggest solutions to failed github actions workflows. The `gh` cli tool is required for the agent to properly find the failed workflow and read the logs. The `snow` cli tool allows the agent to access Snowflake to read recent query logs and replicate the issue for triage.
  - Save this file in `~/.claude/agents/` for global access or simply in the `<project>/.claude/agents/` for use in a specific project.
  - Run the agent from the repository root of the target project as that will allow the agent access to read the dbt models to help diagnose the issue.

### Snow CLI Quickstart

**1. Install**
```bash
# macOS (Homebrew)
brew tap snowflakedb/snowflake-cli
brew install snowflake-cli

# Any OS (pipx)
pipx install snowflake-cli
```

**2. Add a Connection**
```bash
snow connection add
# follow prompts: account, user, role, warehouse
```

**3. Test Connection**
```bash
snow connection test --connection <name>
```

**4. Run SQL**
```bash
snow sql -c <name> -q "SELECT CURRENT_USER();"
```

**5. Config Location**  
`~/.snowflake/config.toml`

### GitHub CLI Quickstart

**1. Install**
```bash
# macOS (Homebrew)
brew install gh

# Ubuntu/Debian
sudo apt install gh

# Fedora/RHEL
sudo dnf install gh
```

**2. Authenticate**
```bash
gh auth login
# follow prompts: GitHub.com, HTTPS, browser login or token
```

**3. Test**
```bash
gh repo view owner/repo
```

**4. Common Commands**
```bash
gh repo clone owner/repo
gh pr create
gh issue list
```
