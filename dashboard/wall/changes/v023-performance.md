# wall v023 (3 Nov 2026): performance after panel wake

Applied live to 11-west-mead-wall-beta with a python_transform on config_hash ecde4cbe338b0337
(live hash after the change: 7f7e5ff244addf7f). dashboard.json / templates.json / views/ in this
folder are still the v022 snapshot (CONFIG_HASH = ecde4cbe338b0337). This file is the exact diff
to get from v022 to v023. A full v023 snapshot needs a session that can save the dashboard to disk.

## What changed
1. Scroll lock (wm_header.custom_fields.lock and wm_idle.custom_fields.lock, same script in both)
   - Before: non-passive touchmove/wheel/keydown listeners on window, always attached, plus a 1.5 s
     setInterval. A non-passive touchmove listener makes the browser wait for JS before every swipe.
   - After: those listeners are attached only while the path is /home, /idle or the dashboard root,
     and removed everywhere else. Fallback interval is 5 s.
2. Music Assistant iframe (wm_ma_frame.custom_fields.frame)
   - Before: after the first visit to /music the iframe (a whole second web app) kept running hidden.
   - After: 90 s after leaving /music the iframe src is set to about:blank; it reloads the ingress url
     when /music is opened again. Hook installed once via window.__wmMaUnload.
3. Animation and shadows
   - Removed `animation:wm-pulse 2s ease-in-out infinite` from all template custom_fields
     (wm_alarm_pill, wm_room, wm_alarm_hero, wm_climate, wm_vacuum). Dots keep their colour and glow.
   - wm_idle title marquee: `infinite alternate` -> `2 alternate` (scrolls twice, then stops).
   - Removed blurred drop shadows: `, 0 12px 32px rgba(0,0,0,0.45)` (wm_now_playing) and
     `, 0 2px 12px rgba(0,0,0,0.30)` (selected segments in wm_segment, wm_seg_select, wm_alarm_mode).
4. Footer (views[5].cards[11].variables.text): v022 -> v023, date 3 November 2026.

## Not changed (needs a decision)
- Lights quick button has a double_tap_action, so button-card waits about 250 ms before a single tap fires.
- 44 JS modules are registered as global dashboard resources and load on every dashboard, including this one,
  although the wall dashboard uses about 6. They are shared with the phone dashboard.
- Inter is loaded from fonts.googleapis.com on every page load.
