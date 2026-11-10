# v026: Power PC card on the Office page (10 Nov 2026)

- New templates: wm_pc_card (glass card: status dot, CPU bar, power ring, Desk button), wm_pc_power (round power ring), wm_pc_desk (Desk pill, toggles the Shelly).
- views[25] room-office-one: new "Computer" label + wm_pc_card, placed between Climate and Curtains. Always shown, no fold.
- Variables: on_script script.office_pc_turn_on, off_script script.office_pc_turn_off, desk_switch switch.office_tiago_desk_shelly1pmminig3, entity sensor.tiago_powerpc_cpuload.
- Replaces the phone dashboard's "Remote desktop" button with the Desk (Shelly) button.
- Footer bumped to v026. Live CONFIG_HASH 6cf6d42cf263708f.
