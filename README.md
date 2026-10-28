# 11 West Mead wall dashboard (backup)

Backup of the live Home Assistant dashboard `11-west-mead-wall-beta` (portrait 720x1280 wall panel).
The live dashboard is the master; this repo is a restore point, one commit per version.

- `dashboard/wall/dashboard.json`: full Lovelace config exactly as stored in HA (restore from this)
- `dashboard/wall/templates.json`: button_card_templates only, for easy reading
- `dashboard/wall/views/NN-path.json`: one file per view
- `dashboard/wall/CONFIG_HASH`: HA config_hash of the config at the time of the commit

Commit messages: `wall vNNN: what changed`.
