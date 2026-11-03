# wall v024 (3 Nov 2026): flat room cards, Lights single tap, self-hosted Inter (pending upload)

Applied live with a python_transform on config_hash 7f7e5ff244addf7f (live hash after: 90ede9d335f39a1d).
Builds on v023-performance.md. dashboard.json in this repo is still the v022 snapshot.

## Room cards (wm_room)
- Removed custom_fields l, m, t, c (four nested custom:button-cards using wm_ctrl_light / _media / _temp / _cover)
  and their styles. Added one custom field `ctl` that renders the four icons as plain HTML.
- Grid areas: last row is now "ctl ctl ctl ctl ctl". The icons keep the old positions (52 x 44, 8 px gap, -12 px left).
- Taps are handled by one set of capture listeners on the card's shadowRoot, wired once per card (this.__wmRoomWired):
  tap on light or cover = <domain>.toggle; tap on media or thermometer = more-info; hold 500 ms on any = more-info.
  Events on an icon are stopped at the shadowRoot so the card's own tap (navigate to the room page) does not fire.
  Moving more than 12 px cancels the tap. Entities that don't exist render at 0.55 opacity with pointer-events none.
- Because the nested cards are gone, each of the 15 wm_room cards on Home now lists media, cover and process in
  triggers_update (added from its variables).
- Colours and opacity rules copied from the old wm_ctrl_* templates. Those templates are still in the config, unused.

## Lights quick button
- Removed double_tap_action (turn off all lights) so a single tap navigates immediately. Turning everything off is
  still on the Lights page ("Turn all lights off") and on More ("All lights off").

## Font
- fonts/inter-wall.woff2: Inter 4 (rsms/inter, SIL OFL 1.1, licence in fonts/Inter-LICENSE.txt), cut to Latin + Latin-1 +
  punctuation, weight axis 200-500, optical size fixed at 14 (same as the Google Fonts version), 33 KB.
- fonts/inter-wall.css: @font-face family 'Inter', weight 200 500, font embedded as base64 (45 KB, no other files needed).
- Pending: upload inter-wall.css to /config/www/fonts/ on HA, then change resource 8f059cc4b68c438ba7562bfbabd11d24
  from the Google Fonts URL to /local/fonts/inter-wall.css?v=1 (type css).

Footer: v024.
