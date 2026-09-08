# Jane App Plugins

A small Claude plugin marketplace with one plugin, **jane-app-exports**, containing two skills used with the Claude in Chrome browser tools against a Jane App admin panel (`*.janeapp.com/admin`):

- **jane-export-patient-list** — export the full Patient List to Excel.
- **jane-export-appointment-history** — export Appointment History over a custom date range to Excel.

Both skills also cover renaming the exported files to a stable `_LATEST.xlsx` name and syncing them to a shared OneDrive folder for a downstream operations dashboard. Those file names and the OneDrive link are specific to ROOTS Physical Therapy & Wellness — edit `plugins/jane-app-exports/skills/*/SKILL.md` before sharing this outside that context.

## Installing (recipient)

In Claude Code / Cowork:

```
/plugin marketplace add <your-github-username>/<this-repo-name>
/plugin install jane-app-exports@jane-app-plugins
```

(In the Cowork desktop app, this may instead be a "Add marketplace by URL" option under plugin/skill settings rather than a slash command — check your version's UI.)

## Requirements

- Claude in Chrome browser tools (for navigating Jane App).
- A Jane App admin login for the relevant clinic.
- For the OneDrive/Excel steps: a linked desktop session (`mcp__remote-devices__*` tools) or manual follow-through by the user — these skills describe but cannot themselves perform file-system/OneDrive/desktop-Excel actions from a browser-only session.
