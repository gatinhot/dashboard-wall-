# wall v025 · 4 Nov 2026

## Frigate page (keeps the nav bar)
- New template `wm_ingress_frame`: generic full-screen add-on iframe above the nav bar (same layout as `wm_ma_frame`).
  Variables: `slug` (add-on slug), `view` (view path it lives on), `title`, `zoom`, `unload_ms`.
  Opens its own ingress session (window.__wmIngSess, validated every 60 s), reads the add-on's ingress_url,
  and sets the frame to about:blank `unload_ms` after leaving the view (Frigate: 2 s, streams are heavy).
  Needs the panel user to be admin (Supervisor API), same as Music Assistant.
- New view 26 `frigate` (wm_ingress_frame slug ccab4aaf_frigate-proxy + wm_nav).
- CCTV page: only the "Open Frigate" row's navigation_path changed, /ccab4aaf_frigate-proxy -> /11-west-mead-wall-beta/frigate.
- wm_nav_item: new variable `also` (comma list of extra view paths that light the item). wm_nav CCTV item has also: 'frigate'.

## Automation (not in dashboard.json)
automation.11_westmead_tablet_turn_off actions were:
  light.turn_off light.touchkio_walldashboardmain_display
now:
  if text.touchkio_walldashboardmain_page_url doesn't end with /11-west-mead-wall-beta/idle:
    text.set_value page_url = <same host>/11-west-mead-wall-beta/idle ; delay 5 s
  light.turn_off light.touchkio_walldashboardmain_display
Triggers unchanged (last_active above 1 min, above 5 min).
