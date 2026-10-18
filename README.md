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

## Travel API (no key)

Plain JSON over HTTPS, CORS open, no account or key.

```
GET https://gxhdcvoveufbkthhendf.supabase.co/functions/v1/travel-api/visa?passport=US&destination=TH
GET https://gxhdcvoveufbkthhendf.supabase.co/functions/v1/travel-api/schengen?stays=2026-01-05..2026-01-20,2026-03-01..2026-03-14&as_of=2026-04-01
```

- `visa`: entry type (visa free, visa on arrival, e-visa, visa required) and the allowed stay in days for a passport and destination, both ISO 3166-1 alpha-2. Covers 39,601 pairs, with source and the date checked. Short tourist stays only.
- `schengen`: days used and left under the 90/180 rule, the date you have to be out by, and the next date a full stay opens again. `stays` is a comma-separated list of `entry..exit` dates. Entry and exit days both count, and the window covers the whole Schengen Area, not each country separately. `as_of` defaults to today.

The same answers are available as a no-auth MCP server, `app.nomadpoint/travel-facts` in the official MCP registry, which can also save a planned route as an itinerary (`create_trip_plan`).
Entry rules change, so confirm with the destination's official source before travelling.
