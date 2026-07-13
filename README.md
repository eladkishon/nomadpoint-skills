# NomadPoint skill

An [agent skill](https://skills.sh) that teaches Claude (and other agents) how to use the **NomadPoint** MCP server to read and edit your trips — journeys, stays, flights, accommodations, activities, and visa/country info.

## Install

```bash
npx skills add eladkishon/nomadpoint-skills
```

This installs the skill into `.claude/skills/` (add `--global` for `~/.claude/skills`).

## Connect the MCP

The skill uses the NomadPoint MCP server. In the **NomadPoint app → Settings → Integrations → Claude / MCP**, tap **Copy prompt for Claude** and paste it into Claude — it adds the MCP server (with your personal token) and installs this skill.

The MCP endpoint is an HTTP server authenticated with a per-user `Bearer np_mcp_…` token. No secrets live in this skill.

## What it covers

- Reading trips: `list_journeys`, `get_journey`, `get_country_info`
- Creating: `create_stay`, `create_flight`, `create_accommodation`, `create_activity`
- Editing/removing: `update_*` / `delete_*` for each

See [`SKILL.md`](./SKILL.md) for the full guidance.
